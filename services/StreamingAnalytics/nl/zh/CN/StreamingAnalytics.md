---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 关于
{: #about}

作为您 {{site.data.keyword.Bluemix_short}} 应用程序的一部分，您可以使用 {{site.data.keyword.streaminganalyticsfull}}，对动态数据执行实时分析。
{:shortdesc}

{{site.data.keyword.streaminganalyticsshort}} 由 {{site.data.keyword.streamsshort}} 提供支持，该产品是一款高级分析平台，可用于在信息从不同类型的数据源到达时，实时摄入、分析和关联信息。
当您创建 {{site.data.keyword.streaminganalyticsshort}} 服务的实例时，可以获取在 {{site.data.keyword.Bluemix_short}} 云中运行的自己的 {{site.data.keyword.streamsshort}} 实例，并准备好运行您的 {{site.data.keyword.streamsshort}} 应用程序。

第一次使用 {{site.data.keyword.streaminganalyticsshort}}？获取[服务的快速简介](https://developer.ibm.com/streamsdev/docs/streaming-analytics-now-available-bluemix-2/){:new_window}。如果您想要进一步使用自己的应用程序，您需要 {{site.data.keyword.streamsshort}} 开发环境，且您必须已经准备好 SPL 云。


{{site.data.keyword.streaminganalyticsshort}} 服务提供下列功能，通过这些功能，可在云中部署、分析和监视数据：


**服务的交互和编程使用：**

您可以通过[{{site.data.keyword.streaminganalyticsshort}} 控制台](/docs/services/StreamingAnalytics/c_streams_console.html)交互使用服务，或者通过 [{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220){:new_window}，以编程方式加以使用。

**SPL 和 Java 应用程序的部署和监视：**

{{site.data.keyword.streamsfull}} Processing Language (SPL) 是编程语言，可用于创建流式处理应用程序。可以使用 SPL 或 Java 编写 {{site.data.keyword.streamsshort}} 应用程序。使用 {{site.data.keyword.streaminganalyticsshort}}，[部署和监视这些应用程序](/docs/services/StreamingAnalytics/t_deploytocloud.html)。 

**与 {{site.data.keyword.streamsshort}} 操作程序的兼容性：**

[{{site.data.keyword.streamsshort}} Processing Language (SPL) 标准工具箱](/docs/services/StreamingAnalytics/c_beta_adapters.html)中的 {{site.data.keyword.streamsshort}} 操作程序应该全部与 {{site.data.keyword.streaminganalyticsshort}} 兼容。

## {{site.data.keyword.streaminganalyticsfull}} 职责

### 客户职责

客户负责：

* 遵循 IBM 最初的 {{site.data.keyword.streamsshort}} 配置，监视、配置和管理在其实例上运行的 {{site.data.keyword.streamsshort}} 作业。
客户可灵活地启动和停止实例，以及启动和停止在实例上的 jobskeywordnning。

* 必要的话，在服务上开发程序和应用程序，以分析数据并从中获得见解。
客户还负责所开发此类程序或应用程序的质量和性能。
程序可能通过 {{site.data.keyword.streamsshort}} Topology 功能，使用 SPL、Java 或其他受支持的语言开发。
它们必须使用 {{site.data.keyword.streamsshort}} Developer Edition 或 {{site.data.keyword.streamsshort}} Quick Start Edition 搭配与用于 {{site.data.keyword.streaminganalyticsshort}} 相同的操作系统。 
* 定期检查以下链接，以随时了解已安排的非中断性或中断性停机 - [https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window}  
* 根据业务需要，备份所有数据、元数据、配置文件和环境参数，以确保连续性。

* 在可能发生的任何类型的故障中（包括但不限于数据中心或 pod 故障、服务器故障或硬盘故障或软件故障），从任何备份复原数据、元数据、配置文件和环境参数，以确保连续性。


### IBM 职责

作为 {{site.data.keyword.streaminganalyticsfull}} 的一部分，IBM 将：

* 为客户实例提供和管理服务器、存储器和网络基础架构。 
* 在所选的节点数上，提供 {{site.data.keyword.streamsshort}} 的初始配置。
* 为面向因特网的内部防火墙提供和管理基础架构，用于保护和隔离。
 
* 在 {{site.data.keyword.streaminganalyticsfull}} 上监视和管理以下组件：
	* 网络组件
	* 服务器及其本地存储器
	* 基础架构操作系统
	* {{site.data.keyword.streamsshort}} 管理服务
	* {{site.data.keyword.streamsshort}} 实例 
* 为基础架构操作系统和 {{site.data.keyword.streamsshort}} 提供维护补丁，包括适当的安全补丁。
* 执行应该不需要任何系统停机（“非中断性”维护）的定期维护，和可能需要一些系统停机和重新启动（“中断性”维护）的维护，这些维护将在 [https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window} 中发布的所安排时间执行 
* 对所安排维护时间的任何更改都以适当的通知形式发布。 
