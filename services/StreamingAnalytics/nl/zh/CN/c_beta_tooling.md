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

#开发工具和环境
{: #c_beta_tooling}


以下注意事项适用于您用来为 {{site.data.keyword.streaminganalyticsshort}} 开发应用程序的工具和环境。
{:shortdesc}


* {{site.data.keyword.streaminganalyticsshort}} 未在云中包括 {{site.data.keyword.streamsshort}} 开发环境，也未在云中包括 Streams Studio。请在本地安装的 {{site.data.keyword.streamsshort}} 环境中开发应用程序，并作为应用程序捆绑软件提交它们。
如果您没有开发环境，那么您可以免费从 [{{site.data.keyword.streamsshort}}产品页面](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)下载 {{site.data.keyword.streamsshort}} Quick Start Edition。
* 在 Red Hat Enterprise Linux 6.5 6.5 环境或等同的 CentOS 版本中编译应用程序捆绑软件，以确保兼容性。

* 在 {{site.data.keyword.streamsshort}} 开发环境中，将环境变量 `JAVA_HOME` 设置为 $STREAMS_INSTALL/java。
