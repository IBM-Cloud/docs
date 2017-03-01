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


#開始使用 {{site.data.keyword.streaminganalyticsshort}}
{: #gettingstarted}

{{site.data.keyword.streaminganalyticsshort}} 採用 {{site.data.keyword.streamsshort}} 技術，這是一種進階分析平台，可用來即時吸收及分析來自不同資料來源類型的資訊，並與之產生關聯。當您建立 {{site.data.keyword.streaminganalyticsshort}} 服務的實例時，即可獲得在 {{site.data.keyword.Bluemix_short}} 雲端中執行的專屬 {{site.data.keyword.streamsshort}} 實例，以執行 {{site.data.keyword.streamsshort}} 應用程式。
{:shortdesc}

您可以將應用程式部署至在 {{site.data.keyword.Bluemix_short}} 雲端中執行的 {{site.data.keyword.streaminganalyticsshort}} 實例。

執行[入門範本應用程式](/docs/services/StreamingAnalytics/c_starterapps.html){:new_window}，即可立即開始使用 {{site.data.keyword.streaminganalyticsshort}}。如果要進一步使用您專屬的應用程式，則需要 {{site.data.keyword.streamsshort}} 開發環境，而且 SPL 必須準備好使用雲端。

若要開始使用 {{site.data.keyword.streaminganalyticsshort}}，請使用下列其中一種方法來提交與您 SPL 或 Java™ 應用程式相關聯的應用程式軟體組（.sab 檔案）：
* 使用 {{site.data.keyword.streaminganalyticsshort}} 主控台。
* 開發 {{site.data.keyword.Bluemix_short}} 應用程式，並在其中新增 {{site.data.keyword.streamsshort}} 應用程式。其控制方式是使用 [{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220)。驗證 SPL 或 Java 應用程式在開發環境中適當地執行。

您現在可以搭配使用 {{site.data.keyword.streaminganalyticsshort}} 與其他 {{site.data.keyword.Bluemix_short}} 服務（包括 {{site.data.keyword.cloudant}} 和 {{site.data.keyword.messagehub}}）。請參閱[與其他 {{site.data.keyword.Bluemix_short}} 服務整合的指導教學](/docs/services/StreamingAnalytics/r_integrating_cloudant_rest.html){:new_window}，來取得開始進行的範例。

若要開發 {{site.data.keyword.streamsshort}} 應用程式，您必須具備 {{site.data.keyword.streamsshort}} 開發環境。如果您沒有 {{site.data.keyword.streamsshort}} 環境，則可以在 [{{site.data.keyword.streamsshort}} 產品頁面](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)上免費下載 {{site.data.keyword.streamsshort}} Quick Start Edition。

如果您不熟悉 {{site.data.keyword.streamsshort}} 應用程式開發，則有資源可協助您瞭解。如需相關資訊，請參閱 [{{site.data.keyword.streamsshort}} Knowledge Center](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}。

如果您已有在內部部署執行的 SPL 應用程式，則必須[準備好用於雲端的應用程式](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud/){:new_window}。

# 相關鏈結
{: #rellinks}

## 指導教學及範例
{: #samples}
* [Introduction to {{site.data.keyword.streaminganalyticsshort}}](https://developer.ibm.com/streamsdev/docs/streaming-analytics-now-available-bluemix){:new_window}
* [{{site.data.keyword.streaminganalyticsshort}} SDK for Node.js™ Starter Application](http://bit.ly/1iR1bzu){:new_window}
* [{{site.data.keyword.streaminganalyticsshort}} Liberty for Java™ Starter Application](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-starter-application/){:new_window}
* [Getting your SPL application ready for the cloud](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud){:new_window}
* [Bluemix {{site.data.keyword.streaminganalyticsshort}} Development Guide](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-development-guide/){:new_window}
* [其他指導教學](StreamingAnalytics.html#r_integrating_cloudant_rest){:new_window}


## API 參考資料
{: #api}
* [{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220){:new_window}
* [{{site.data.keyword.streaminganalyticsshort}} metrics using the {{site.data.keyword.streamsshort}} REST API](https://developer.ibm.com/bluemix/2016/07/25/streaming-analytics-metrics-using-rest-api/){:new_window}

## 相容的運行環境
{: #buildpacks}
* [Liberty for Java](/docs/runtimes/liberty/index.html#liberty)
* [Node.js](/docs/runtimes/nodejs/index.html#nodejs)

## 相關鏈結
{: #general}
* [{{site.data.keyword.streamsshort}} 文件](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}
* [{{site.data.keyword.streamsshort}} Quick Start Edition](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window}
