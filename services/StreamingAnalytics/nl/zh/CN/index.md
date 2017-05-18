---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# {{site.data.keyword.streaminganalyticsshort}} 入门
{: #gettingstarted}

{{site.data.keyword.streaminganalyticsshort}} 由 {{site.data.keyword.streamsshort}} 提供支持，该产品是一款高级分析平台，可用于在信息从不同类型的数据源到达时，实时摄入、分析和关联信息。
当您创建 {{site.data.keyword.streaminganalyticsshort}} 服务的实例时，可以获取在 {{site.data.keyword.Bluemix_short}} 云中运行的自己的 {{site.data.keyword.streamsshort}} 实例，并准备好运行您的 {{site.data.keyword.streamsshort}} 应用程序。
{:shortdesc}

通过运行[入门模板应用程序](/docs/services/StreamingAnalytics/c_starterapps.html){:new_window}，立即开始使用 {{site.data.keyword.streaminganalyticsshort}}。

要开始使用 {{site.data.keyword.streaminganalyticsshort}}，请使用下列某种方法，提交与 SPL、Java™、Python 或 Scala Streams 应用程序相关联的应用程序捆绑软件（.sab 文件）：

* 使用 {{site.data.keyword.streaminganalyticsshort}} 控制台中的**提交作业**按钮。
* 开发 {{site.data.keyword.Bluemix_short}} 应用程序并向其添加 {{site.data.keyword.streamsshort}} 应用程序。
使用 [{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220) 对其进行控制。


使用 {{site.data.keyword.streaminganalyticsshort}} 与其他 {{site.data.keyword.Bluemix_short}} 服务，包括 {{site.data.keyword.cloudant}} 和 {{site.data.keyword.messagehub}}。请参阅[与其他 {{site.data.keyword.Bluemix_short}} 服务集成的教程](/docs/services/StreamingAnalytics/r_integrating_cloudant_rest.html){:new_window}，以获取可让您快速入门和熟悉运用的示例。


如果您想要进一步使用自己的应用程序，可以获取 {{site.data.keyword.streamsshort}} 开发环境，而且必须使应用程序处于云就绪状态。如果您没有 {{site.data.keyword.streamsshort}} 开发环境，那么您可以免费从 [{{site.data.keyword.streamsshort}}产品页面](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)下载 {{site.data.keyword.streamsshort}} Quick Start Edition。

如果您不熟悉 {{site.data.keyword.streamsshort}} 应用程序开发，那么有很多资源可帮助您学习。有关更多信息，请参阅 [{{site.data.keyword.streamsshort}} Knowledge Center。](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}

如果您已经具有在内部部署中运行的 SPL 应用程序，那么您必须[使应用程序为云做好准备](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud/){:new_window}。

**注：**必须使用 Red Hat Enterprise Linux (RHEL) 6.5 或等同的 CentOS 版本，使用 Intel 处理器，来编译应用程序。

## 针对 {{site.data.keyword.streaminganalyticsshort}} 的 {{site.data.keyword.streamsshort}} Python 应用程序
{: #gettingstarted_py notoc}

现在您可以在 Python 环境中创建 Streams 应用程序，如 IBM Data Science Experience (DSX)，然后将这些应用程序提交给 {{site.data.keyword.streaminganalyticsshort}} 实例以便将其部署在 Bluemix 云中。您不再需要本地安装 {{site.data.keyword.streamsshort}}，就可以编译和部署 Streams Python 应用程序。

开始时，通过在 DSX 中使用 Jupyter 配置页来创建样本 Streams Python 应用程序，然后直接从 DSX 将这些应用程序提交给服务实例。有关更多信息，请参阅[在 DSX 中开发 Streams Python 应用程序](/docs/services/StreamingAnalytics/t_develop_apps_python.html#t_develop_python_dsx)。

{{site.data.keyword.streaminganalyticsshort}} 还支持从本地 Python 环境部署 Streams 应用程序。必须使用 streamsx 程序包中随附的 [{{site.data.keyword.streamsshort}} Python 应用程序 API](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features) 在本地开发 Streams Python 应用程序，然后将其提交给服务实例。开始时，请按照[针对 {{site.data.keyword.streaminganalyticsshort}} 服务进行开发](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html)教程中的步骤进行操作。
