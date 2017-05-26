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


# 開始使用 {{site.data.keyword.streaminganalyticsshort}}
{: #gettingstarted}

{{site.data.keyword.streaminganalyticsshort}} 採用 {{site.data.keyword.streamsshort}} 技術，這是一種進階分析平台，可用來即時吸收及分析來自不同資料來源類型的資訊，並與之產生關聯。當您建立 {{site.data.keyword.streaminganalyticsshort}} 服務的實例時，即可獲得在 {{site.data.keyword.Bluemix_short}} 雲端中執行的專屬 {{site.data.keyword.streamsshort}} 實例，以執行 {{site.data.keyword.streamsshort}} 應用程式。
{:shortdesc}

執行[入門範本應用程式](/docs/services/StreamingAnalytics/c_starterapps.html){:new_window}，立即開始使用 {{site.data.keyword.streaminganalyticsshort}}。

若要開始使用 {{site.data.keyword.streaminganalyticsshort}}，請使用下列其中一種方法來提交與您 SPL、Java™、Python 或 Scala Streams 應用程式相關聯的應用程式軟體組（.sab 檔案）：
* 使用 {{site.data.keyword.streaminganalyticsshort}} 主控台中的**提交工作**按鈕。
* 開發 {{site.data.keyword.Bluemix_short}} 應用程式，並在其中新增 {{site.data.keyword.streamsshort}} 應用程式。其控制方式是使用 [{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220)。


搭配使用 {{site.data.keyword.streaminganalyticsshort}} 與其他 {{site.data.keyword.Bluemix_short}} 服務（包括 {{site.data.keyword.cloudant}} 和 {{site.data.keyword.messagehub}}）。請參閱[與其他 {{site.data.keyword.Bluemix_short}} 服務整合的指導教學](/docs/services/StreamingAnalytics/r_integrating_cloudant_rest.html){:new_window}，來取得開始進行的範例。

如果要進一步使用您自己的應用程式，可以取得 {{site.data.keyword.streamsshort}} 開發環境，而且應用程式必須準備好使用雲端。如果您沒有 {{site.data.keyword.streamsshort}} 環境，則可以在 [{{site.data.keyword.streamsshort}} 產品頁面](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)上免費下載 {{site.data.keyword.streamsshort}} Quick Start Edition。

如果您不熟悉 {{site.data.keyword.streamsshort}} 應用程式開發，則有資源可協助您瞭解。如需相關資訊，請參閱 [{{site.data.keyword.streamsshort}} Knowledge Center](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}。

如果您已有在內部部署執行的 SPL 應用程式，則必須[準備好用於雲端的應用程式](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud/){:new_window}。

**附註：**您必須在 Red Hat Enterprise Linux (RHEL) 6.5 或相等的 CentOS 版本中，編譯應用程式，並且使用 Intel 處理器。

## {{site.data.keyword.streaminganalyticsshort}} 的 {{site.data.keyword.streamsshort}} Python 應用程式
{: #gettingstarted_py notoc}

您現在可以在 Python 環境（例如 IBM Data Science Experience (DSX)）建立 Streams 應用程式，然後將這些應用程式提交到 {{site.data.keyword.streaminganalyticsshort}} 實例，以便部署在 Bluemix 雲端。您不再需要在本端安裝 {{site.data.keyword.streamsshort}}，即可編譯和部署 Streams Python 應用程式。

在 DSX 中使用 Jupyter 記事本建立範例 Streams Python 應用程式以便開始，並從 DSX 直接將這些應用程式提交到服務實例。如需相關資訊，請參閱[在 DSX 中開發 Streams Python 應用程式](/docs/services/StreamingAnalytics/t_develop_apps_python.html#t_develop_python_dsx)。

{{site.data.keyword.streaminganalyticsshort}} 也支援從您的本端 Python 環境部署 Streams 應用程式。您必須使用 [{{site.data.keyword.streamsshort}} Python Application API](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features) （它包含在 streamsx 套件中），在本端開發 Streams Python 應用程式然後將它們提交到服務實例。若要開始，請遵循 [Developing for the {{site.data.keyword.streaminganalyticsshort}} service](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html) 指導教學中的步驟。
