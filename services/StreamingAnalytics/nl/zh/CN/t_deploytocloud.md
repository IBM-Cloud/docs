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

#将 {{site.data.keyword.streamsshort}} 应用程序部署到云
{: #t_deploytocloud}

您可以将 {{site.data.keyword.streamsshort}} 应用程序部署到在 {{site.data.keyword.Bluemix_short}} 云中运行的 {{site.data.keyword.streaminganalyticsshort}} 实例。
{:shortdesc}

{{site.data.keyword.streamsshort}} 应用程序在 {{site.data.keyword.streamsshort}} 环境中以 {{site.data.keyword.streamsshort}} Processing Language (SPL) 编写。{{site.data.keyword.streamsshort}} 还支持若干 Java™ Development Kit，您可用于开发应用程序。
有关 {{site.data.keyword.streamsshort}} 中 Java 支持的更多信息，请参阅[应用程序开发支持的 Java Development Kit](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-prerequisites-java-supported-sdks.html){:new_window}。
{{site.data.keyword.streaminganalyticsshort}} 未在云中包括 {{site.data.keyword.streamsshort}} 开发环境，但是您可以将本地开发的应用程序部署到云。


开始之前，先禁用浏览器的弹出窗口阻止程序，以显示 Streaming Analytics 控制台。

要将 {{site.data.keyword.streamsshort}} 应用程序部署到云：


1. 设置 {{site.data.keyword.streamsshort}} 环境，以开发并测试应用程序。
 

	如果您没有 {{site.data.keyword.streamsshort}} 环境，那么您可以免费下载 {{site.data.keyword.streamsshort}} Quick Start Edition。
转至 [IBM Streams 产品页面](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window}并单击**下载本机软件安装**。

2. 使用 Streams Studio 或命令行工具，在 {{site.data.keyword.streamsshort}} 环境中，开发 SPL 或 Java 应用程序。
3. 验证 SPL 或 Java 应用程序在开发环境中运行正常。

4. 使用下列其中一个方法，将与您 SPL 或 Java 应用程序相关联的应用程序捆绑软件（.sab 文件）提交到云中的服务实例：

	* 使用 {{site.data.keyword.streaminganalyticsshort}} 控制台，来提交应用程序捆绑软件。

    * 开发 {{site.data.keyword.Bluemix_short}} 应用程序并向其添加 {{site.data.keyword.streamsshort}} 应用程序。
使用 {{site.data.keyword.streaminganalyticsshort}} REST API 对其进行控制。

现在，您的应用程序已在云中部署。您可以使用 {{site.data.keyword.streaminganalyticsshort}} 服务，来监视应用程序。您还可以将多个 SPL 或 Java 应用程序（.sab 文件）提交到服务实例。多少个都可以。

