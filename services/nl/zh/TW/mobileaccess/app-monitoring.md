---

copyright:
  years: 2015, 2016
  
---

# 監視應用程式
{: #app-monitoring}
*前次更新：2016 年 5 月 6 日*
{: .last-updated}

除了安全特性之外，{{site.data.keyword.amafull}} 還會提供行動應用程式的監視及分析。您可以使用 {{site.data.keyword.amashort}} 用戶端 SDK 來記錄用戶端日誌以及監視資料。開發人員可以控制何時將此資料傳送給「{{site.data.keyword.amashort}} 服務」。將自動記載「{{site.data.keyword.amashort}} 服務」中所發生的所有安全事件（例如鑑別成功或失敗）。

將資料遞送至 {{site.data.keyword.amashort}} 時，您可以使用 {{site.data.keyword.amashort}} 監視儀表板來取得行動應用程式、裝置及用戶端日誌的分析洞察。預設會記錄您的應用程式對 {{site.data.keyword.amashort}} 所保護資源提出之要求的相關資訊。


**附註**：{{site.data.keyword.amashort}} 服務的監視功能，預計會移轉至新的 [{{site.data.keyword.mobileanalytics_short}} 服務](https://console.ng.bluemix.net/catalog/services/mobile-analytics)。新的 Swift SDK 會利用新的 {{site.data.keyword.mobileanalytics_short}} 服務，它服務提供更豐富的分析體驗。{{site.data.keyword.mobileanalytics_short}} 服務目前處於實驗階段，預計在今年稍晚正式上市。由於預計會在 {{site.data.keyword.mobileanalytics_short}} 正式上市時停止使用 {{site.data.keyword.amashort}} 服務的監視功能，因此建議您先研究移轉應用程式以使用新的 {{site.data.keyword.mobileanalytics_short}} 服務及 Swift SDK。


自動記錄的資料包括鑑別次數、新裝置數目和新使用者數目這類的資訊。此外，您還可以配置 {{site.data.keyword.amashort}} 用戶端 SDK 來報告下列資訊：

### 行動應用程式的用量統計資料
{: #usage-stats}

您可以配置行動應用程式，使用一些簡單的 API 呼叫來記錄應用程式生命週期事件，並將記錄的資料傳送給 {{site.data.keyword.amashort}} 服務。您可以記錄應用程式開啟次數、收到的推送通知數等等。

### 用戶端日誌擷取
{: #client-side-logcapture}

現場運作中的應用程式有時會遇到問題，需要開發人員注意並進行修正。通常很難重新產生這些問題。<!--in R&D.--> 從事程式碼開發的開發人員可能缺乏用於測試的環境或確切裝置。在這些狀況下，能夠在環境中發生問題時從用戶端裝置中擷取除錯日誌就會非常有用。

## 保留擷取的資料
{: #preserve-captureddata}

沒有任何方式可保證所有擷取的資料都保留在用戶端上。您的使用者可能離線執行行動應用程式，並且同步累計擷取的分析和日誌資料。因為用戶端處於離線狀態且檔案系統空間有限，所以必須清除較舊的記載事件，以騰出空間來保留更新的記載事件。開發人員可以決定何時使用提供的 API 將擷取的資料傳送給「{{site.data.keyword.amashort}} 服務」。

## 使用 {{site.data.keyword.amashort}} 監視儀表板
{: #monitoring-dashboard}

1. 開啟 {{site.data.keyword.Bluemix}} 儀表板，然後按一下 {{site.data.keyword.Bluemix_notm}} 應用程式。

2. 開啟 {{site.data.keyword.Bluemix_notm}} 應用程式儀表板時，按一下 {{site.data.keyword.amashort}} 磚。

3. 在 {{site.data.keyword.amashort}} 儀表板中，按一下左側功能表中的`監視`鏈結。

## 後續步驟
{: #next-steps}
* [啟用、配置及使用日誌程式](app-monitoring-logger.html)
* [收集用量分析](app-monitoring-gathering-analytics.html)
