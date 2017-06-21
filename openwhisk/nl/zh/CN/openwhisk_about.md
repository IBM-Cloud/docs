---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 关于 {{site.data.keyword.openwhisk_short}}

{{site.data.keyword.openwhisk}} 是一种事件驱动型计算平台，也称为无服务器计算或功能即服务 (FaaS)，用于运行代码以响应事件或直接调用。下图显示了高层次的 {{site.data.keyword.openwhisk}} 体系结构。
{: shortdesc}

![{{site.data.keyword.openwhisk_short}} 体系结构](./images/OpenWhisk.png)

事件的示例包括对数据库记录进行更改、IoT 传感器读数超过特定温度、新代码落实到 GitHub 存储库，或者从 Web 或移动应用程序发起简单 HTTP 请求。来自外部和内部事件源的事件将通过触发器进行传递，并且规则允许操作对这些事件做出反应。

操作可以是 JavaScript 或 Swift 代码的小片段，也可以是嵌入在 Docker 容器中的定制二进制代码。只要有触发器触发，就会立即部署并执行 {{site.data.keyword.openwhisk_short}} 中的操作。触发的触发器越多，调用的操作也越多。如果没有触发器触发，那么不会运行任何操作码，所以也不会产生任何开销。

除了将操作与触发器关联外，还可以使用 {{site.data.keyword.openwhisk_short}} API、CLI 或 iOS SDK 来直接调用操作。此外，也可以将一组操作链接在一起，而不必编写任何代码。链中的各个操作会按顺序进行调用，其中一个操作的输出将作为输入传递给序列中下一个操作。

对于长时间运行的传统虚拟机或容器，常用做法是部署多个 VM 或容器，以便具备弹性来应对单个实例中断情况。不过，{{site.data.keyword.openwhisk_short}} 提供了替代模型，无需与弹性相关的成本开销。通过按需执行操作，可提供固有的可扩展性和最佳利用率，因为运行中操作的数量始终与触发率相匹配。此外，开发者现在只需专注于代码，而不必担心关于对底层服务器、存储器、网络和操作系统基础架构进行监视、打补丁和安全保护的问题。

可以随包集成其他服务和事件提供程序。一个包是捆绑在一起的一组订阅源和操作。订阅源是一段代码，用于配置外部事件源以触发触发器事件。例如，使用 Cloudant 更改订阅源创建的触发器会将一个服务配置为每次修改文档或将文档添加到 Cloudant 数据库时都触发该触发器。包中的操作表示可复用逻辑，服务提供者可提供此逻辑，以便开发者不仅能够将服务用作事件源，还能调用该服务的 API。

通过包的现有目录，能够迅速借助多个有用的功能来增强应用程序，也能访问生态系统中的外部服务。启用了 {{site.data.keyword.openwhisk_short}} 的外部服务的示例包括 Cloudant、The Weather Company、Slack 和 GitHub。


## {{site.data.keyword.openwhisk_short}} 的工作方式
{: #openwhisk_how}

作为开放式源代码项目，OpenWhisk 可以说是站在巨人的肩膀上，包括 Nginx、Kafka、Consul、Docker 和 CouchDB。所有这些组件集合在一起，构成了“基于事件的无服务器编程服务”。为了更详细地说明所有组件，我们会跟踪在整个系统中调用一个操作的全过程。OpenWhisk 中的调用是无服务器引擎执行的核心工作：执行用户馈入系统中的代码，并返回这一执行操作的结果。

### 创建操作

为了让我们的说明有一点背景，我们先在系统中创建一个操作。后续在整个系统中跟踪时，我们将使用该操作来说明相关概念。以下命令假定 [OpenWhisk CLI 已正确设置](https://github.com/openwhisk/openwhisk/tree/master/docs#setting-up-the-openwhisk-cli)。

首先，我们将创建包含以下代码的 *action.js* 文件，该代码会将“Hello World”显示到 stdout，并返回在键“hello”下包含“world”的 JSON 对象。
```javascript
function main() {
    console.log('Hello World');
    return { hello: 'world' };
}
```
{: codeblock}

使用以下命令创建该操作：
```
wsk action create myAction action.js
```
{: pre}

创建完毕。现在，我们实际来调用该操作：
```
wsk action invoke myAction
```
{: pre}

## 内部处理流程
在 OpenWhisk 中的后台实际发生了什么？

![OpenWhisk 处理流程](images/OpenWhisk_flow_of_processing.png)

### 进入系统：nginx

首先：OpenWhisk 面向用户的 API 是完全基于 HTTP 的，遵循的是 RESTful 设计。因此，通过 wsk-CLI 发送的命令本质上是针对 OpenWhisk 系统的 HTTP 请求。上述特定命令大致会转换为：
```
POST /api/v1/namespaces/$userNamespace/actions/myAction
Host: $openwhiskEndpoint
```
{: screen}

请注意此处的 *$userNamespace* 变量。用户有权访问至少一个名称空间。为了简化起见，我们假定用户拥有的是放入了 *myAction* 的名称空间。

系统的第一个入口点是 **nginx**，这是一个“HTTP 和逆向代理服务器”。它主要用于 SSL 终止以及将相应的 HTTP 调用转发到下一个组件。

### 进入系统：控制器

nginx 对 HTTP 请求没有进行多少处理，就会将其转发到**控制器**，这是 OpenWhisk 流程中的下一个组件。这是对实际 REST API（基于 **Akka** 和 **Spray**）的基于 Scala 的实现，因此会用作用户可执行的所有操作的接口，包括在 OpenWhisk 中对您实体的 [CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete) 请求以及操作调用（这正是我们目前要做的事情）。

控制器首先会明确用户要尝试执行的操作。这基于您在 HTTP 请求中使用的 HTTP 方法。根据上面的转换，用户是要对现有操作发出 POST 请求，而控制器会将其转换为**操作调用**。

鉴于控制器的核心角色（顾名思义），以下步骤在某种程度上都将涉及到控制器。

### 认证和授权：CouchDB

现在，控制器将验证您的身份（*认证*），并验证您是否有权执行要对该实体执行的操作（*授权*）。请求中包含的凭证将根据 **CouchDB** 实例中的所谓 **subjects** 数据库进行验证。

在本例中，将检查用户在 OpenWhisk 的数据库中是否存在，以及该用户是否有权调用操作 myAction（我们假定这是用户拥有的名称空间中的操作）。如果真是用户拥有的名称空间中的操作，用户就确实有权调用该操作，如其所愿。

一切就绪后，即可顺理成章进入下一个处理阶段。

### 获取操作：还是 CouchDB…

由于控制器现在确定用户已获准进入并有权调用其操作，因此会实际从 CouchDB 中的 **whisks** 数据库装入此操作（在本例中为 *myAction*）。

操作记录主要包含要执行的代码（如上所示）和要传递到操作的缺省参数，并与实际调用请求中包含的参数合并。此外，还包含在执行中对其施加的资源限制，例如允许其使用的内存。

在此特定例子中，我们的操作并不会采用任何参数（函数的参数定义为空列表），因此我们假定没有设置任何缺省参数，并且未向操作发送任何特定参数，从这个角度来说是最轻巧的情况。

### 操作调用者：Consul

控制器（更具体而言，是其负载均衡部分）现在已经一切就绪，可实际开始运行您的代码。但控制器还需要知道谁可以执行此操作。为此，将使用 **Consul**（一种服务发现组件）通过持续检查系统中可用执行者的运行状态来跟踪这些执行者。这些执行者称为**调用者**。

现在，控制器已经知道有哪些调用者可用，接着会选择其中一个来调用请求的操作。

对于本例，我们假定系统中有 3 个调用者可用（调用者 0 到 2），并且控制器选择了*调用者 2* 来调用这一操作。

### 请排好队：Kafka

从现在开始，对于您发来的调用请求，可能发生的糟糕情况主要有两种：

1. 系统可能崩溃，导致丢失调用。
2. 系统可能负载过重，该调用需要等待其他调用先完成。

解决这两种情况的办法都是使用 **Kafka**，这是“一种高吞吐量、分布式的发布/预订消息传递系统”。控制器和调用者只通过由 Kafka 缓存和持久存储的消息进行通信。这会为控制器和调用者减轻在内存中进行缓存的负担并降低伴随的 *OutOfMemoryException* 风险，同时还可确保消息不会在系统崩溃时丢失。

为了使操作得到调用，控制器会向 Kafka 发布消息，其中包含要调用的操作以及要传递给该操作的参数（在本例中没有参数）。此消息会发给控制器在从 Consul 获取的上述列表中选择的调用者。

一旦 Kafka 确认自己获得了该消息，即会使用 **ActivationId** 响应对用户的 HTTP 请求。用户后续将其用于访问对此特定调用的结果。请注意，这是异步调用模型，其中一旦系统接受调用操作的 HTTP 请求后，该请求即会终止。异步模型（称为阻塞性调用）是可用的，但不在本文讨论范围之内。

### 已经开始实际调用代码：调用者

**调用者**是 OpenWhisk 的核心。调用者的职责是调用操作。在 Scala 中也实施了调用者。但远远不止于此。为了以隔离、安全的方式执行操作，它会使用 **Docker**。

Docker 用于以快速、隔离且受控的方式为我们调用的每个操作设置新的自封装环境（称为*容器*）。简言之，就是对于每个操作调用，都会衍生一个 Docker 容器，将操作码注入其中，使用传递给它的参数予以执行，获取结果，然后销毁该容器。还会在此执行大量性能优化，以降低开销，并且可以缩短响应时间。 

在我们的特定例子中，由于我们手头是基于 *Node.js* 的操作，因此调用者将启动 Node.js 容器，注入 *myAction* 中的代码，在不带参数的情况下运行该代码，抽取结果，保存日志，然后再次销毁 Node.js 容器。

### 存储结果：又是 CouchDB

调用者获取结果后，该结果会存储在 **whisks** 数据库中作为上文提到的 ActivationId 下的激活。**whisks** 数据库位于 **CouchDB** 中。

在我们的特定例子中，调用者获得从操作生成的 JSON 对象，抓取 Docker 编写的日志，将这些全部放入激活记录中，然后将其存储到数据库中。这大致类似下面的示例：

```json
{
   "activationId": "31809ddca6f64cfc9de2937ebd44fbb9",
   "response": {
       "statusCode": 0,
       "result": {
           "hello": "world"
       }
   },
   "end": 1474459415621,
   "logs": [
       "2016-09-21T12:03:35.619234386Z stdout: Hello World"
   ],
   "start": 1474459415595,
}
```
{: codeblock}

请注意该记录是如何同时包含返回的结果和编写的日志的。它还包含操作调用的开始时间和结束时间。在激活记录中还有更多字段，此处为了简单起见只提供了精练版。

现在，可以再次使用 REST API（重新从步骤 1 开始）来获取您的激活，进而获得操作的结果。为此，您将使用：

```bash
wsk activation get 31809ddca6f64cfc9de2937ebd44fbb9
```
{: pre} 

### 总结

我们已经了解了简单的 **wsk 操作调用 myAction** 是如何经历 {{site.data.keyword.openwhisk_short}} 系统的不同阶段的。该系统本身主要只包含两个定制组件：**控制器**和**调用者**。其他一切都是现成的，是开放式源代码社团中的许多人员开发的。

可以在以下主题中找到有关 {{site.data.keyword.openwhisk_short}} 的更多信息：

* [实体名称](./openwhisk_reference.html#openwhisk_entities)
* [操作语义](./openwhisk_reference.html#openwhisk_semantics)
* [限制](./openwhisk_reference.md#openwhisk_syslimits)
* [REST API](./openwhisk_reference.md#openwhisk_ref_restapi)
