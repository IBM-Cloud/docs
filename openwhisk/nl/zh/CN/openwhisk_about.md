---

 

copyright:

  years: 2016, 2017
lastupdated: "2016-08-02"
 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 关于 {{site.data.keyword.openwhisk_short}}

以下各部分提供了有关 {{site.data.keyword.openwhisk}} 的详细信息。
{: shortdesc}

## {{site.data.keyword.openwhisk_short}} 的工作方式
{: #openwhisk_how}

{{site.data.keyword.openwhisk_short}} 是一种事件驱动型计算平台，也称为无服务器计算或功能即服务 (FaaS)，用于运行代码以响应事件或直接调用。

下图显示了高层次的 {{site.data.keyword.openwhisk_short}} 体系结构。

![{{site.data.keyword.openwhisk_short}} 体系结构](OpenWhisk.png)

事件的示例包括对数据库记录进行更改、IoT 传感器读数超过特定温度、新代码落实到 GitHub 存储库，或者从 Web 或移动应用程序发起简单 HTTP 请求。来自外部和内部事件源的事件将通过触发器进行传递，并且规则允许操作对这些事件做出反应。

操作可以是 JavaScript 或 Swift 代码的小片段，也可以是嵌入在 Docker 容器中的定制二进制代码。只要有触发器触发，就会立即部署并执行 {{site.data.keyword.openwhisk_short}} 中的操作。触发的触发器越多，调用的操作也越多。如果没有触发器触发，那么不会运行任何操作码，所以也不会产生任何开销。

除了将操作与触发器关联外，还可以使用 {{site.data.keyword.openwhisk_short}} API、CLI 或 iOS SDK 来直接调用操作。此外，也可以将一组操作链接在一起，而不必编写任何代码。链中的各个操作会按顺序进行调用，其中一个操作的输出将作为输入传递给序列中下一个操作。

对于长时间运行的传统虚拟机或容器，常用做法是部署多个 VM 或容器，以便具备弹性来应对单个实例中断情况。不过，{{site.data.keyword.openwhisk_short}} 提供了替代模型，无需与弹性相关的成本开销。通过按需执行操作，可提供固有的可扩展性和最佳利用率，因为运行中操作的数量始终与触发率相匹配。此外，开发者现在只需专注于代码，而不必担心关于对底层服务器、存储器、网络和操作系统基础架构进行监视、打补丁和安全保护的问题。

可以随包集成其他服务和事件提供程序。一个包是捆绑在一起的一组订阅源和操作。订阅源是一段代码，用于配置外部事件源以触发触发器事件。例如，使用 Cloudant 更改订阅源创建的触发器会将一个服务配置为每次修改文档或将文档添加到 Cloudant 数据库时都触发该触发器。包中的操作表示可复用逻辑，服务提供者可提供此逻辑，以便开发者不仅能够将服务用作事件源，还能调用该服务的 API。

通过包的现有目录，能够迅速借助多个有用的功能来增强应用程序，也能访问生态系统中的外部服务。启用了 {{site.data.keyword.openwhisk_short}} 的外部服务的示例包括 Cloudant、The Weather Company、Slack 和 GitHub。


## 一般用例
{: #openwhisk_use_cases}

{{site.data.keyword.openwhisk_short}} 提供的执行模型支持各种用例。以下各部分包含典型的示例。

### 将应用程序分解成微服务
{: #openwhisk_use_cases_decomp}

{{site.data.keyword.openwhisk_short}} 具有模块化和固有的可扩展性质，因此适用于在操作中实现细颗粒度的逻辑片段。例如，{{site.data.keyword.openwhisk_short}} 很适合用于从前端代码中除去装入密集型、潜在高峰（后台）任务并将这些任务作为操作实现。

### 移动后端
{: #openwhisk_use_cases_mobile_backend}

许多移动应用程序需要服务器端逻辑。考虑到移动开发者通常在管理服务器端逻辑方面没有什么经验，而更倾向于关注设备上运行的应用程序，所以比较好的解决方案是将 {{site.data.keyword.openwhisk_short}} 用作服务器端后端。此外，内置 Swift 支持也允许开发者复用自己现有的 iOS 编程技能。

### 数据处理
{: #openwhisk_use_cases_data_proc}

针对现在可用的数据量，应用程序开发需要处理新数据并可能对其做出响应的能力。此需求包括处理结构化数据库记录以及非结构化的文档、图像或视频。

### IoT
{: #openwhisk_use_cases_iot}

Internet of Things 场景通常具备由传感器驱动的固有性质。例如，如果需要对超过特定温度的传感器做出反应，那么可能会触发 {{site.data.keyword.openwhisk_short}} 中的操作。
