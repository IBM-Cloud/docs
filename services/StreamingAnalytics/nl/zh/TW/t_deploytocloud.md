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

# 將 {{site.data.keyword.streamsshort}} 應用程式部署至雲端
{: #t_deploytocloud}

您可以將 {{site.data.keyword.streamsshort}} 應用程式部署至在 {{site.data.keyword.Bluemix_short}} 雲端中執行的 {{site.data.keyword.streaminganalyticsshort}} 實例。
{:shortdesc}

{{site.data.keyword.streamsshort}} 應用程式是以 {{site.data.keyword.streamsshort}} 環境中的 {{site.data.keyword.streamsshort}} Processing Language (SPL)、SPL、Java、Scala 或 Python 所撰寫。您現在可以開發 Streams Python 應用程式而不使用 {{site.data.keyword.streamsshort}} 環境。請參閱[將 {{site.data.keyword.streamsshort}} Python 應用程式部署至雲端](docs/services/StreamingAnalytics/t_deploytocloud.html#t_deploypython)


{{site.data.keyword.streaminganalyticsshort}} 未包括雲端中的 {{site.data.keyword.streamsshort}} 開發環境，但可以將在本端開發的應用程式部署至雲端。

開始之前，請先停用瀏覽器的蹦現畫面封鎖程式，以便顯示 {{site.data.keyword.streaminganalyticsshort}} 主控台。

若要將 {{site.data.keyword.streamsshort}} 應用程式部署至雲端，請執行下列動作：

1. 設定開發環境來開發及測試應用程式。

	如果您沒有 {{site.data.keyword.streamsshort}} 環境，則可以免費下載 {{site.data.keyword.streamsshort}} Quick Start Edition。移至 [IBM Streams 產品頁面](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window}，然後按一下 **Download the native software installation**。

2. 在您的開發環境中開發串流應用程式。在 {{site.data.keyword.streamsshort}} 開發環境中，您可以使用 Streams Studio 或指令行工具來開發應用程式。

3. 驗證串流應用程式在開發環境中適當地執行。
**附註：**您必須在 Red Hat Enterprise Linux (RHEL) 6.5 作業系統或相等的 CentOS 版本中，編譯應用程式，並且使用 Intel 處理器。

4. 使用下列其中一種方法，將與 SPL、Java、Scala 或 Python 應用程式相關聯的應用程式軟體組（.sab 檔案）提交至雲端中的服務實例：
	* 使用 {{site.data.keyword.streaminganalyticsshort}} 主控台來提交應用程式軟體組。
  * 建立 {{site.data.keyword.Bluemix_short}} 應用程式，並在其中新增 {{site.data.keyword.streamsshort}} 應用程式。其控制方式是使用 {{site.data.keyword.streaminganalyticsshort}} REST API。

您的應用程式現在已部署在雲端中。您可以使用 {{site.data.keyword.streaminganalyticsshort}} 服務來監視應用程式。您也可以將多個應用程式（.sab 檔案）提交至服務實例。數目由您決定。

{{site.data.keyword.streamsshort}} 也支援數個可用來開發應用程式的 Java™ 開發套件。如需 {{site.data.keyword.streamsshort}} 中 Java 支援的相關資訊，請參閱[支援進行應用程式開發的 Java 開發套件](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-prerequisites-java-supported-sdks.html){:new_window}。


## 將 {{site.data.keyword.streamsshort}} Python 應用程式部署至雲端
{: #t_deploypython}

將 {{site.data.keyword.streamsshort}} Python 應用程式部署至在 {{site.data.keyword.Bluemix_short}} 雲端中執行的 {{site.data.keyword.streaminganalyticsshort}} 服務。您不需要有 {{site.data.keyword.streamsshort}} 安裝。
{:shortdesc}

[{{site.data.keyword.streamsshort}} Python Application API](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features)（它包含在 streamsx 套件中），能讓您將 Python 應用程式部署到 {{site.data.keyword.streaminganalyticsshort}} 服務。請參閱 [Developing for the {{site.data.keyword.streaminganalyticsshort}} service](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html) 指導教學，以取得如何針對 {{site.data.keyword.streaminganalyticsshort}} 服務建立和部署簡單 Python 應用程式的範例。

IBM Data Science Experience (DSX) 也支援在 Jupyter 互動式記事本中提交 Python 應用程式。如需相關資訊，請參閱[針對 {{site.data.keyword.streaminganalyticsshort}} 開發 Python 應用程式](/docs/services/StreamingAnalytics/t_develop_apps_python.html)。
