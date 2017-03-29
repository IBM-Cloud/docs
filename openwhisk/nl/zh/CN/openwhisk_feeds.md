---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 实现订阅源
{: #openwhisk_feeds}

{{site.data.keyword.openwhisk_short}} 支持开放 API，通过此 API，任何用户都可以将事件发起者服务公开为**包**中的**订阅源**。此部分描述了用于提供您自己订阅源的体系结构和实现选项。

本资料适用于打算发布自己的订阅源的高级 {{site.data.keyword.openwhisk_short}} 用户。大多数 {{site.data.keyword.openwhisk_short}} 用户可以安全地跳过此部分。

## 订阅源体系结构

至少有 3 种体系结构模式可用于创建订阅源：**Hook**、**轮询**和**连接**。

### Hook
在 *Hook* 模式下，我们使用由其他服务公开的 [Webhook](https://en.wikipedia.org/wiki/Webhook) 工具设置订阅源。在此策略中，我们在外部服务上配置了 Webhook，用于直接向 URL 执行 POST 操作来触发触发器。这是目前为止实现低频率订阅源最简单、最有吸引力的选项。

<!-- The github feed is implemented using webhooks.  Put a link here when we have the open repo ready -->

### 轮询
在“轮询”模式下，我们安排 {{site.data.keyword.openwhisk_short}} *操作*定期轮询端点以访存新数据。此模式构建起来相对容易，但事件频率无疑会受到轮询时间间隔的限制。

### 连接
在“连接”模式下，我们在某个位置坚持使用单独的服务，来保持与源订阅源的持续连接。基于连接的实现可能会通过长时间轮询与服务端点进行交互，或者设置推送通知。

<!-- Our cloudant changes feed is connection based.  Put a link here to
an open repo -->

<!-- What is the foundation for the Message Hub feed? If it is "connections" then lets put a link here as well -->

## 订阅源与触发器的区别

订阅源和触发器是紧密相关的，但在技术上是不同的概念。   

- {{site.data.keyword.openwhisk_short}} 处理流入系统的**事件**。

- **触发器**在技术上是指某类事件的名称。每个事件只属于一个触发器；若用类比说明，触发器类似于基于主题的发布/预订系统中的*主题*。**规则** *T -> A* 表示“每当来自触发器 *T* 的事件到达时，通过触发器有效内容调用操作 *A*。”

- **订阅源**是全部属于某个触发器 *T* 的事件的流。订阅源通过**订阅源操作**进行控制，订阅源操作用于处理包含订阅源的事件的流的创建、删除、暂停和恢复。通常，订阅源操作通过管理通知的 REST API 与生成事件的外部服务进行交互。

##  实现订阅源操作

*订阅源操作*是一种常规 {{site.data.keyword.openwhisk_short}} *操作*，但应该接受以下参数：
* **lifecycleEvent**：“CREATE”、“DELETE”、“PAUSE”或“UNPAUSE”中的一个值。
* **triggerName**：包含从此订阅源所生成事件的触发器的标准名称。
* **authKey**：拥有刚才提及的触发器的 {{site.data.keyword.openwhisk_short}} 用户的基本认证凭证。

订阅源操作还可以接受管理订阅源所需的其他任何参数。例如，cloudant changes 订阅源操作预期会接收多个参数，包括“*dbname*”、“*username*”等。

用户使用 **--feed** 参数通过 CLI 创建触发器时，系统会自动调用具有相应参数的订阅源操作。

例如，假定用户通过将其用户名和密码作为绑定参数，为 `cloudant` 包创建了 `mycloudant` 绑定。用户通过 CLI 发出以下命令时：

`wsk trigger create T --feed mycloudant/changes -p dbName myTable`

然后系统将在后台执行等同于下面的操作：

`wsk action invoke mycloudant/changes -p lifecycleEvent CREATE -p triggerName T -p authKey <userAuthKey> -p password <password value from mycloudant binding> -p username <username value from mycloudant binding> -p dbName mytype`

名为 *changes* 的订阅源操作将采用这些参数，并预计执行设置来自 Cloudant 中的事件流所需的任何操作，并通过相应的配置定向到触发器 *T*。    

对于 Cloudant *changes* 订阅源，该操作恰巧会与已经通过基于连接的体系结构实现的 *cloudant trigger* 服务直接进行对话。下面我们将讨论其他体系结构。

会对 `wsk trigger delete` 执行类似的订阅源操作协议。    

## 通过 Hook 实现订阅源

如果事件发起者支持 Webhook/回调工具，那么通过 Hook 设置订阅源非常简单。

通过此方法，*无需*在 OpenWhisk 外部坚持使用任何持久服务。所有订阅源管理工作均通过无状态的 {{site.data.keyword.openwhisk_short}} *订阅源操作*很自然地执行，这些操作直接与第三方 Webhook API 进行协商。

使用 `CREATE` 进行调用时，订阅源操作只会为其他某个服务安装 Webhook，并请求远程服务执行 POST 操作将通知发布到 OpenWhisk 中的相应 `fireTrigger` URL。

Webhook 应该定向到向 URL 发送通知，例如：

`POST /namespaces/{namespace}/triggers/{triggerName}`

具有 POST 请求的表单将解释为 JSON 文档，用于定义有关触发器事件的参数。{{site.data.keyword.openwhisk_short}} 规则会将这些触发器参数传递到要作为事件结果进行触发的任何操作。

## 通过轮询实现订阅源

可以设置 {{site.data.keyword.openwhisk_short}} *操作*来轮询 OpenWhisk 中的整个源订阅源，而无需坚持使用任何持续连接或外部服务。

对于 Webhook 不可用，但无需大容量或短等待响应时间的订阅源，轮询是很有吸引力的选项。

要设置基于轮询的订阅源，订阅源操作在针对 `CREATE` 进行调用时执行以下步骤：

1.   订阅源操作使用 `whisk.system/alarms` 订阅源将定期触发器 (*T*) 设置为所需频率。
2.   订阅源开发者创建 `pollMyService` 操作，以只轮询远程服务并返回任何新事件。
3.  订阅源操作设置*规则* *T -> pollMyService*。

此过程完全使用 {{site.data.keyword.openwhisk_short}} 操作来实现基于轮询的触发器，而无需任何单独的服务。

## 通过连接实现订阅源

前 2 个体系结构选项实现起来既简单又轻松。但是，如果需要高性能订阅源，那么没有持续连接和长时间轮询的替代方法或类似方法。

由于 {{site.data.keyword.openwhisk_short}} 操作必须是短时间运行的，因此操作不能保持与第三方的持续连接。必须改为坚持使用始终运行的单独服务（在 OpenWhisk 外部）。我们将这些服务称为*提供者服务*。提供者服务可以保持与第三方事件源的连接，这些事件源支持长时间轮询或其他基于连接的通知。

提供者服务应该提供 REST API 以允许 {{site.data.keyword.openwhisk_short}} *订阅源操作*控制订阅源。提供者服务充当事件提供程序和 {{site.data.keyword.openwhisk_short}} 之间的代理；当提供者服务收到来自第三方的事件时，会通过触发触发器来将其发送给 {{site.data.keyword.openwhisk_short}}。

Cloudant *changes* 订阅源是典型示例 - 它坚持运行 `cloudanttrigger` 服务，以调解通过持续连接发送的 Cloudant 通知和 {{site.data.keyword.openwhisk_short}} 触发器。
<!-- TODO: add a reference to the open source implementation -->

*alarm* 订阅源通过类似模式实现。

基于连接的体系结构是性能最高的选项，但相对于轮询和 Hook 体系结构，它在操作方面的开销更大。   
