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


#{{site.data.keyword.streaminganalyticsshort}} 入门
{: #gettingstarted}

{{site.data.keyword.streaminganalyticsshort}} 由 {{site.data.keyword.streamsshort}} 提供支持，该产品是一款高级分析平台，可用于在信息从不同类型的数据源到达时，实时摄入、分析和关联信息。
当您创建 {{site.data.keyword.streaminganalyticsshort}} 服务的实例时，可以获取在 {{site.data.keyword.Bluemix_short}} 云中运行的自己的 {{site.data.keyword.streamsshort}} 实例，并准备好运行您的 {{site.data.keyword.streamsshort}} 应用程序。
{:shortdesc}

您可以将应用程序部署到在 {{site.data.keyword.Bluemix_short}} 云中运行的 {{site.data.keyword.streaminganalyticsshort}} 实例。

您可以通过运行[入门模板应用程序](/docs/services/StreamingAnalytics/c_starterapps.html){:new_window}，立即开始使用 {{site.data.keyword.streaminganalyticsshort}}。如果您想要进一步使用自己的应用程序，您需要 {{site.data.keyword.streamsshort}} 开发环境，且您必须已经准备好 SPL 云。


要开始使用 {{site.data.keyword.streaminganalyticsshort}}，请使用下列其中一个方法，提交与您 SPL or Java™ 应用程序相关联的应用程序捆绑软件（.sab 文件）：

* 使用 {{site.data.keyword.streaminganalyticsshort}} 控制台。

* 开发 {{site.data.keyword.Bluemix_short}} 应用程序并向其添加 {{site.data.keyword.streamsshort}} 应用程序。
使用 [{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220) 对其进行控制。验证 SPL 或 Java 应用程序在开发环境中运行正常。


您现在可以使用 {{site.data.keyword.streaminganalyticsshort}} 与其他 {{site.data.keyword.Bluemix_short}} 服务，包括 {{site.data.keyword.cloudant}} 和 {{site.data.keyword.messagehub}}。请参阅[与其他 {{site.data.keyword.Bluemix_short}} 服务集成的教程](/docs/services/StreamingAnalytics/r_integrating_cloudant_rest.html){:new_window}，以获取可让您快速入门和熟悉运用的示例。


要开发 {{site.data.keyword.streamsshort}} 应用程序，您必须具有 {{site.data.keyword.streamsshort}} 开发环境。
如果您没有 {{site.data.keyword.streamsshort}} 开发环境，那么您可以免费从 [{{site.data.keyword.streamsshort}}产品页面](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)下载 {{site.data.keyword.streamsshort}} Quick Start Edition。

如果您不熟悉 {{site.data.keyword.streamsshort}} 应用程序开发，那么有很多资源可帮助您学习。有关更多信息，请参阅 [{{site.data.keyword.streamsshort}} Knowledge Center。](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}

如果您已经具有在内部部署中运行的 SPL 应用程序，那么您必须[使应用程序为云做好准备](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud/){:new_window}。

# 相关链接
{: #rellinks}

## 教程与样本
{: #samples}
* [{{site.data.keyword.streaminganalyticsshort}} 简介](https://developer.ibm.com/streamsdev/docs/streaming-analytics-now-available-bluemix){:new_window}
* [适用于 Node.js™ Starter Application 的 {{site.data.keyword.streaminganalyticsshort}} SDK](http://bit.ly/1iR1bzu){:new_window}
* [适用于 Java™ Starter Application 的 {{site.data.keyword.streaminganalyticsshort}} Liberty](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-starter-application/){:new_window}
* [使 SPL 应用程序为云做好准备](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud){:new_window}
* [Bluemix {{site.data.keyword.streaminganalyticsshort}} Development Guide](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-development-guide/){:new_window}
* [更多教程](StreamingAnalytics.html#r_integrating_cloudant_rest){:new_window}


## API 参考
{: #api}
* [{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220){:new_window}
* [使用 {{site.data.keyword.streamsshort}} REST API 的 {{site.data.keyword.streaminganalyticsshort}} 度量](https://developer.ibm.com/bluemix/2016/07/25/streaming-analytics-metrics-using-rest-api/){:new_window}

## 兼容的运行时
{: #buildpacks}
* [Liberty for Java](/docs/runtimes/liberty/index.html#liberty)
* [Node.js](/docs/runtimes/nodejs/index.html#nodejs)

## 相关链接
{: #general}
* [{{site.data.keyword.streamsshort}} 文档](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}
* [{{site.data.keyword.streamsshort}}Quick
Start Edition](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window}
