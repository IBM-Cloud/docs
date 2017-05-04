---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 關於 {{site.data.keyword.openwhisk_short}}

{{site.data.keyword.openwhisk}} 是事件驅動運算平台（也稱為「無伺服器運算」或「函數即服務 (FaaS)」），會執行程式碼來回應事件或直接呼叫。下圖顯示高階 {{site.data.keyword.openwhisk}} 架構。
{: shortdesc}

![{{site.data.keyword.openwhisk_short}} 架構](./images/OpenWhisk.png)

事件範例包括資料庫記錄變更、超出特定溫度的 IoT 感應器讀數、GitHub 儲存庫的新程式碼確定，或來自 Web 或行動應用程式的簡單 HTTP 要求。來自外部及內部事件來源的事件是透過觸發程式進行傳送，而規則容許動作反應這些事件。

動作可以是 JavaScript 或 Swift 程式碼的小型 Snippet，或內嵌在 Docker 容器中的自訂二進位程式碼。只要發動觸發程式，就會立即部署及執行 {{site.data.keyword.openwhisk_short}} 中的動作。發動的觸發程式數目越多，呼叫的動作數目就越多。如果未發動任何觸發程式，則不會執行任何動作碼，因此不會有任何成本。

除了關聯動作與觸發程式之外，還可能會使用 {{site.data.keyword.openwhisk_short}} API、CLI 或 iOS SDK 來直接呼叫動作。也可以鏈結一組動作，而不需要撰寫任何程式碼。序列中呼叫鏈結中的每一個動作，其將某個動作的輸出傳遞為序列中下一個動作的輸入。

運用傳統長時間執行的虛擬機器或容器，常見的是部署多個 VM 或容器，讓單一實例的運作中斷更具復原力。不過，{{site.data.keyword.openwhisk_short}} 所提供的替代模型沒有備援相關成本額外負擔。依需求執行動作可提供固有可擴充性及最佳使用率，因為執行中動作數目一律會符合觸發程式比率。此外，開發人員現在只會關注程式碼，而且不需擔心如何監視、修補，以及保護基礎伺服器、儲存空間、網路及作業系統基礎架構。

可以利用套件來新增與其他服務及事件提供者的整合。套件是資訊來源及動作的組合。資訊來源是程式碼片段，可配置外部事件來源來發動觸發程式事件。例如，使用 Cloudant 變更資訊來源所建立的觸發程式，會將服務配置成在每次修改文件或將其新增至 Cloudant 資料庫時發動觸發程式。套件中的動作代表服務提供者可設為可用的可重複使用邏輯，如此，開發人員不僅可以使用服務作為事件來源，還可以呼叫該服務的 API。

現有套件型錄提供快速的方式以使用有用的功能來加強應用程式，以及在生態系統中存取外部服務。已啟用 {{site.data.keyword.openwhisk_short}} 功能的外部服務範例包括 Cloudant、The Weather Company、Slack 及 GitHub。


## {{site.data.keyword.openwhisk_short}} 的運作方式
{: #openwhisk_how}

OpenWhisk 是一個開放程式碼專案，利用各種技術，包括 Nginx、Kafka、Consul、Docker、CouchDB。合併使用這些元件，以構成「無伺服器事件型程式設計服務」。若要更詳細地說明所有元件，請透過系統追蹤所發生的動作呼叫。OpenWhisk 中的呼叫是無伺服器引擎所執行的核心事項：執行使用者已提供給系統的程式碼，並傳回該執行的結果。

### 建立動作

若要提供環境定義的更多說明，請先在系統中建立一個動作。我們稍後將在透過系統追蹤時使用該動作來說明這些概念。下列指令假設[已適當地設定 OpenWhisk CLI](https://github.com/openwhisk/openwhisk/tree/master/docs#setting-up-the-openwhisk-cli)。

首先，我們將建立檔案 *action.js*，其所包含的下列程式碼會將 "Hello World" 列印至 stdout，並傳回在索引鍵 "hello" 下包含 "world" 的 JSON 物件。
```javascript
function main() {
    console.log('Hello World');
    return { hello: 'world' };
}
```
{: codeblock}

我們可以使用下列指令來建立該動作。
```
wsk action create myAction action.js
```
{: pre}

完成。現在，我們想要實際呼叫該動作：
```
wsk action invoke myAction
```
{: pre}

## 內部處理流程
OpenWhisk 中實際發生什麼情況？

![OpenWhisk 處理流程](images/OpenWhisk_flow_of_processing.png)

### 進入系統：nginx

首先：OpenWhisk 的使用者應對 API 完全是以 HTTP 為基礎，並且遵循 RESTful 設計。因此，透過 wsk-CLI 傳送的指令基本上是對 OpenWhisk 系統提出的 HTTP 要求。上面的特定指令大致上會轉換為：
```
POST /api/v1/namespaces/$userNamespace/actions/myAction
Host: $openwhiskEndpoint
```
{: screen}

請記下這裡的 *$userNamespace* 變數。使用者可以存取至少一個名稱空間。為求簡化，假設使用者擁有放入 *myAction* 的名稱空間。

系統的第一個進入點是透過 **nginx**（HTTP 及反向 Proxy 伺服器）。它主要用於 SSL 終止，並且將適當的 HTTP 呼叫轉遞給下一個元件。

### 進入系統：控制器

nginx 不會對我們的 HTTP 要求進行太多處理，而是將它轉遞給**控制器**（透過 OpenWhisk 的流程中的下一個元件）。它是實際 REST API 的 Scala 型實作（根據 **Akka** 及 **Spray**），因此可作為使用者執行一切作業的介面，包括 OpenWhisk 中之實體的 [CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete) 要求，以及動作的呼叫（也就是我們現在正在做的事）。

「控制器」會先釐清使用者嘗試執行的動作。作法是根據您在 HTTP 要求中使用的 HTTP 方法。根據上述轉換，使用者會對現有的動作發出 POST 要求，而「控制器」會將其轉換為**動作的呼叫**。

提供「控制器」的中央角色（因此得名），下列步驟都會將它併入特定範圍。

### 鑑別及授權：CouchDB

現在，「控制器」會驗證您的身分（*鑑別*），並驗證您是否具有專用權可以執行您想要對該實體執行的動作（*授權*）。針對 **CouchDB** 實例中所謂的 **subjects** 資料庫驗證要求中所含的認證。

在此情況下，「控制器」會確認使用者存在於 OpenWhisk 的資料庫中，並且具有專用權可以呼叫動作 myAction（我們假設它是使用者所擁有的名稱空間中的動作）。後者可以有效率地將使用者想要執行的動作呼叫的專用權授與使用者。

一切就緒後，就會開啟下一個處理階段的閘道。

### 重新取得動作：CouchDB…

因為「控制器」現在確定使用者已獲許加入並且具有呼叫其動作的專用權，所以會從 CouchDB 的 **whisks** 資料庫中實際載入此動作（在此情況下為 *myAction*）。

動作的記錄主要包含要執行的程式碼（如上所示），以及您要傳遞給動作並與實際呼叫要求中所含參數合併的預設參數。同時包含執行時強加於它的資源限制（例如允許它使用的記憶體）。

在此特定情況下，我們的動作不會採用任何參數（函數的參數定義是空清單），因此我們假設尚未設定任何預設參數，並且尚未將任何特定參數傳送給動作，從此觀點來看，這是最微不足道的情況。

### 呼叫動作的對象：Consul

「控制器」（或更具體的說是它的負載平衡部分）現在已全部就緒，可實際執行程式碼。它需要知道可以執行此作業的對象。**Consul**（服務探索）用來連續檢查執行程式的性能狀態，以追蹤系統中可用的執行程式。這些執行程式稱為**呼叫程式**。

「控制器」（現在知道哪些「呼叫程式」可供使用）會選擇其中一個來呼叫所要求的動作。

在此情況下，假設系統有 3 個「呼叫程式」可供使用（呼叫程式 0 到 2），而且「控制器」已選擇*呼叫程式 2* 來呼叫現有的動作。

### 請排隊：Kafka

從現在開始，您傳入的呼叫要求主要可能會發生兩件不好的事情：

1. 系統可能損毀，遺失呼叫。
2. 系統可能有這類大量載入，因此呼叫需要先等待其他呼叫完成。

這兩者的解答都是 **Kafka**，它是一種高產量的分散式發佈/訂閱傳訊系統。「控制器」及「呼叫程式」只能透過 Kafka 所緩衝及持續保存的訊息進行通訊。這會增加「控制器」及「呼叫程式」記憶體中的緩衝負擔，導致發生 *OutOfMemoryException* 的風險，同時確保訊息不會在系統損毀時遺失。

若要呼叫動作，「控制器」會將訊息發佈至 Kafka，其包含要呼叫的動作以及要傳遞給該動作的參數（在此情況下沒有參數）。此訊息會定址到「呼叫程式」，其為上述從 Consul 取得的清單中所選擇的「控制器」。

Kafka 確認它取得訊息之後，會使用 **ActivationId** 回應對使用者的 HTTP 要求。使用者稍後會使用該項目，以存取此特定呼叫的結果。請注意，這是非同步呼叫模型，其中，HTTP 要求會在系統接受動作呼叫要求之後終止。可以使用同步模型（稱為區塊處理呼叫），但本文並未涵蓋。

### 已實際呼叫程式碼：呼叫程式

**呼叫程式**是 OpenWhisk 的核心。「呼叫程式」的責任是呼叫動作。它也會在 Scala 中進行實作。但還需要進行許多作業。若要使用隔離及安全的方式執行動作，它會使用 **Docker**。

Docker 用來設定使用快速、隔離及控制方式所呼叫的每一個動作的全新自行封裝環境（稱為*容器*）。在 nutshell 中，針對每一個動作呼叫，會大量產生 Docker 容器、注入動作碼、使用傳遞給它的參數予以執行、取得結果，以及破壞容器。這也是執行許多效能最佳化以減少額外負擔並盡可能設定低回應時間的位置。 

在我們的特定情況下，因為我們已具有 *Node.js* 型動作，所以「呼叫程式」將會啟動 Node.js 容器、從 *myAction* 注入程式碼、在不使用參數的情況下予以執行、擷取結果、儲存日誌，並且再次破壞 Node.js 容器。

### 重新儲存結果：CouchDB

「呼叫程式」取得結果時，會將它儲存至 **whisks** 資料庫，作為上述所提及的 ActivationId 下的啟動。**whisks** 資料庫存在於 **CouchDB** 中。

在我們的特定情況下，「呼叫程式」會取得動作傳回的產生的 JSON 物件、抓取 Docker 所撰寫的日誌、將它們全都放入啟動記錄，並將它儲存至資料庫。它大致上會類似下列內容：

```json
{
   "activationId": "31809ddca6f64cfc9de2937ebd44fbb9",
   "response": {
       "statusCode": 0,
       "result": {
           "hello": "world"
       }
   },
   "end": 1474459415621,
   "logs": [
       "2016-09-21T12:03:35.619234386Z stdout: Hello World"
   ],
   "start": 1474459415595,
}
```
{: codeblock}

請注意記錄如何包含傳回的結果及撰寫的日誌。它也會包含動作呼叫的開始及結束時間。啟動記錄中還有其他欄位，這是精簡版。

現在，您可以重新使用 REST API（從步驟 1 重新開始）以取得您的啟動，因而取得動作的結果。若要這樣做，請使用：

```bash
wsk activation get 31809ddca6f64cfc9de2937ebd44fbb9
```
{: pre} 

### 摘要

我們已瞭解簡單的 **wsk action invoke myAction** 如何通過 {{site.data.keyword.openwhisk_short}} 系統的不同階段。系統本身主要僅包含兩個自訂元件：**控制器**及**呼叫程式**。由開放程式碼社群中的許多人員所開發的其他所有項目也都已就緒。

您可以在下列主題中尋找 {{site.data.keyword.openwhisk_short}} 的其他資訊：

* [實體名稱](./openwhisk_reference.html#openwhisk_entities)
* [動作語意](./openwhisk_reference.html#openwhisk_semantics)
* [限制](./openwhisk_reference.md#openwhisk_syslimits)
* [REST API](./openwhisk_reference.md#openwhisk_ref_restapi)
