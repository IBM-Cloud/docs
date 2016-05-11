---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 關於 {{site.data.keyword.openwhisk}}

*前次更新：2016 年 2 月 22 日*

下列各節提供有關 {{site.data.keyword.openwhisk}} 的詳細資料。
{: shortdesc}

## {{site.data.keyword.openwhisk_short}} 的運作方式
{: #openwhisk_how}

{{site.data.keyword.openwhisk_short}} 是一個事件驅動運算平台，可執行程式碼來回應事件或直接呼叫。

下圖顯示高階 {{site.data.keyword.openwhisk_short}} 架構。

![{{site.data.keyword.openwhisk_short}} 架構](OpenWhisk.png)

事件範例包括資料庫記錄變更、超出特定溫度的 IoT 感應器讀數、GitHub 儲存庫的新程式碼確定，或來自 Web 或行動式應用程式的簡單 HTTP 要求。來自外部及內部事件來源的事件是透過觸發程式進行傳送，而規則容許動作反應這些事件。

動作可以是 Javascript 或 Swift 程式碼的小型 Snippet，或內嵌在 Docker 儲存器中的自訂二進位檔。只要發動觸發程式，就會立即部署及執行 {{site.data.keyword.openwhisk_short}} 中的動作。發動的觸發程式數目越多，呼叫的動作數目就越多。如果未發動任何觸發程式，則不會執行任何動作碼，因此不會有任何成本。

除了關聯動作與觸發程式之外，還可能會使用 {{site.data.keyword.openwhisk_short}} API、CLI 或 iOS SDK 來直接呼叫動作。也可以鏈結一組動作，而不需要撰寫任何程式碼。序列中呼叫鏈結中的每一個動作，其將某個動作的輸出傳遞為序列中下一個動作的輸入。

運用傳統長時間執行的虛擬機器或儲存器，常見的是部署多個 VM 或儲存器，讓單一實例的運作中斷更具復原力。不過，{{site.data.keyword.openwhisk_short}} 所提供的替代模型沒有復原力相關成本額外負擔。依需求執行動作可提供固有可擴充性及最佳使用率，因為執行中動作數目一律會符合觸發程式比率。此外，開發人員現在只會關注其程式碼，而且不需擔心如何監視、修補，以及保護基礎伺服器、儲存體、網路及作業系統基礎架構。

可以利用套件來新增與其他服務及事件提供者的整合。套件是資訊來源及動作的組合。資訊來源是程式碼片段，可配置外部事件來源來發動觸發程式事件。例如，使用 Cloudant 變更資訊來源所建立的觸發程式，會將服務配置成在每次修改文件或將其新增至 Cloudant 資料庫時發動觸發程式。套件中的動作代表服務提供者可設為可用的可重複使用邏輯，如此，開發人員不僅可以使用服務作為事件來源，還可以呼叫該服務的 API。

現有套件型錄提供快速的方式以使用有用的功能來加強應用程式，以及在生態系統中存取外部服務。已啟用 {{site.data.keyword.openwhisk_short}} 功能的外部服務範例包括 Cloudant、The Weather Company、Slack 及 GitHub。



## 常見使用案例
{: #openwhisk_use_cases}

{{site.data.keyword.openwhisk_short}} 所提供的執行模型支援各種使用案例。下列各節包括一般範例。

### 將應用程式分解成微服務
{{site.data.keyword.openwhisk_short}} 的模組及固有可擴充本質，讓它適合實作運作中邏輯的精細部分。例如，{{site.data.keyword.openwhisk_short}} 可能適用於透過前端程式碼移除載入密集、潛在 spiky（背景）作業，以及將這些作業實作為動作。

### 行動式後端
許多行動式應用程式都需要伺服器端邏輯。有鑒於行動式開發人員通常沒有管理伺服器端邏輯的經驗，而且不是關注裝置上執行的應用程式，所以使用 {{site.data.keyword.openwhisk_short}} 作為伺服器端後端是很好的解決方案。此外，Swift 的內建支援容許開發人員重複使用其現有 iOS 程式設計技術。

### 資料處理
運用現在可用的資料量，應用程式開發需要處理新資料的能力，而且可能會對它做出反應。此需求包括處理結構化資料庫記錄以及非結構化文件、映像檔或視訊。

### IoT
Internet of Things 情境本質上經常是由感應器所驅動。例如，如果需要針對感應器超過特定溫度做出反應，可能會觸發 {{site.data.keyword.openwhisk_short}} 中的動作。



