---

copyright:
  years: 2015, 2016
  
---

# 應用程式監視
{: #app-monitoring}

除了安全特性之外，{{site.data.keyword.amafull}} 還會提供行動式應用程式的監視及分析。您可以使用 {{site.data.keyword.amashort}} Client SDK 來記錄用戶端日誌以及監視資料。開發人員可以控制何時將此資料傳送給「{{site.data.keyword.amashort}} 服務」。將自動記載「{{site.data.keyword.amashort}} 服務」中所發生的所有安全事件（例如鑑別成功或失敗）。

將資料遞送至 {{site.data.keyword.amashort}} 時，您可以使用「{{site.data.keyword.amashort}} 監視儀表板」來取得行動式應用程式、裝置及用戶端日誌的分析見解。預設會記錄您的應用程式對 {{site.data.keyword.amashort}} 所保護資源提出之要求的相關資訊。

自動記錄的資料包括鑑別、新裝置和新使用者數目這類的資訊。此外，您還可以配置 {{site.data.keyword.amashort}} Client SDK 來報告下列資訊：

### 行動式應用程式的使用情形統計資料
{: #usage-stats}

您可以使用一些簡單的 API 呼叫來配置行動式應用程式，以記錄應用程式生命週期事件，並將記錄的資料傳送至 {{site.data.keyword.amashort}} 服務。您可以記錄應用程式開啟次數、收到的推送通知數等等。

### 用戶端日誌擷取
{: #client-side-logcapture}

欄位中的應用程式有時會遇到問題，需要開發人員注意並進行修正。通常很難重新產生這些問題。<!--in R&D.--> 從事程式碼開發的開發人員可能缺乏用於測試的環境或確切裝置。在這些狀況下，能夠在環境中發生問題時從用戶端裝置中擷取除錯日誌就會非常有用。

## 保留擷取的資料
{: #preserve-captureddata}

沒有任何方式可保證在用戶端上保留所有擷取的資料。您的使用者可能離線執行行動式應用程式，並且同步累計擷取的分析和日誌資料。因為用戶端處於離線狀態且檔案系統空間有限，所以必須清除較舊的記載事件，以騰出空間來保留更新的記載事件。開發人員可以使用提供的 API 來決定何時將擷取的資料傳送至「{{site.data.keyword.amashort}} 服務」。

## 使用 {{site.data.keyword.amashort}} 監視儀表板
{: #monitoring-dashboard}

1. 開啟 {{site.data.keyword.Bluemix}}「儀表板」，然後按一下 {{site.data.keyword.Bluemix_notm}} 應用程式

2. 開啟 {{site.data.keyword.Bluemix_notm}} 應用程式儀表板時，請按一下 {{site.data.keyword.amashort}} 磚

3. 在 {{site.data.keyword.amashort}}「儀表板」中，按一下左側功能表中的`監視`鏈結

## 後續步驟
{: #next-steps}
* [啟用、配置及使用日誌程式](app-monitoring-logger.html)
* [收集使用情形分析](app-monitoring-gathering-analytics.html)
