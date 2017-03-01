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

#開發工具和環境
{: #c_beta_tooling}


這些考量適用於用來開發 {{site.data.keyword.streaminganalyticsshort}} 之應用程式的工具和環境。
{:shortdesc}


* {{site.data.keyword.streaminganalyticsshort}} 未包括雲端中的 {{site.data.keyword.streamsshort}} 開發環境，或雲端中的 Streams Studio。請在本端安裝的 {{site.data.keyword.streamsshort}} 環境中開發應用程式，並將它們提交為應用程式軟體組。如果您沒有開發環境，則可以在 [{{site.data.keyword.streamsshort}} 產品頁面](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)上免費下載 {{site.data.keyword.streamsshort}} Quick Start Edition。
* 在 Red Hat Enterprise Linux 6.5 環境（或對等的 CentOS 版本）中編譯應用程式軟體組，以確保相容性。
* 在 {{site.data.keyword.streamsshort}} 開發環境中，將環境變數 `JAVA_HOME` 設為 $STREAMS_INSTALL/java。
