---

 

copyright:

  years: 2016
lastupdated: "2016-09-09"
 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 實作資訊來源
{: #openwhisk_feeds}

OpenWhisk 支援開放式 API，任何使用者都可以在其中將事件生產者服務公開為**套件**中的**資訊來源**。本節說明用於提供專屬資訊來源的架構及實作選項。

本資料適用於要發佈其專屬資訊來源的進階 OpenWhisk 使用者。大部分的 OpenWhisk 使用者都可以放心地跳過本節。

## 資訊來源架構

至少有 3 個架構型樣可用於建立資訊來源：**連結鉤**、**輪詢**及**連線**。

### 連結鉤
在*連結鉤* 型樣中，已使用另一個服務所公開的 [Webhook](https://en.wikipedia.org/wiki/Webhook) 機能來設定資訊來源。在此策略中，於外部服務上配置 Webhook，以直接 POST 至 URL 來發動觸發程式。到目前為止，這是用於實作低頻率資訊來源的最簡單且最具吸引力的選項。

### 輪詢
在「輪詢」型樣中，安排 OpenWhisk *動作* 定期輪詢端點，以提取新的資料。
此型樣相當容易建置，但事件頻率當然受限於輪詢間隔。

### 連線
在「連線」型樣中，使用維護持續性資訊來源連線的不同服務。連線型實作可能會透過長期輪詢與服務端點互動，或設定推送通知。


## 資訊來源與觸發程式的差異

資訊來源及觸發程式密切相關，但技術上而言是不同的概念。   

- OpenWhisk 會處理流入系統的**事件**。

- **觸發程式**技術上而言是某個事件類別的名稱。每一個事件只屬於一個觸發程式；觸發程式則類似主題型發佈/訂閱系統中的*主題*。**規則** *T -> A* 表示只要觸發程式 *T* 的事件到達，就會使用觸發程式有效負載來呼叫動作 *A*。

- **資訊來源**是全部屬於某個觸發程式 *T* 的一連串事件。資訊來源是透過**資訊來源動作**所控制，而資訊來源動作會處理建立、刪除、暫停及繼續可構成資訊來源的一連串事件。資訊來源動作一般會透過管理通知的 REST API，以與產生事件的外部服務互動。

##  實作資訊來源動作

*資訊來源動作* 是一般 OpenWhisk *動作*，但應該接受下列參數：
* **lifecycleEvent**：'CREATE'、'DELETE'、'PAUSE' 或 'UNPAUSE' 其中之一
* **triggerName**：包含從此資訊來源產生之事件的觸發程式的完整名稱。
* **authKey**：擁有剛剛提及之觸發程式的 OpenWhisk 使用者的基本鑑別認證

資訊來源動作也可以接受任何管理資訊來源所需的其他參數。例如，Cloudant changes 資訊來源動作預期會接收包括 *'dbname'*、*'username'* 等參數。

使用者從 CLI 使用 **--feed** 參數建立觸發程式時，系統會使用適當的參數自動呼叫資訊來源動作。

例如，假設使用者已使用其使用者名稱及密碼作為已連結參數，來建立 `cloudant` 套件的 `mycloudant` 連結。如果使用者從 CLI 發出下列指令：

`wsk trigger create T --feed mycloudant/changes -p dbName myTable`

系統則會隱含地執行與下列對等的動作：

`wsk action invoke mycloudant/changes -p lifecycleEvent CREATE -p triggerName T -p authKey <userAuthKey> -p password <password value from mycloudant binding> -p username <username value from mycloudant binding> -p dbName mytype`

名為 *changes* 的資訊來源動作會採用這些參數，並且預期將適當的配置導向觸發程式 *T*，以採取從 Cloudant 設定一連串事件所需的動作。    

針對 Cloudant *changes* 資訊來源，動作會直接與使用連線型架構所實作的 *cloudant trigger* 服務交談。我們將在下面討論其他架構。

`wsk trigger delete` 會執行類似的資訊來源動作通訊協定。    

## 使用連結鉤實作資訊來源

如果事件生產者支援 Webhook/回呼機能，則透過連結鉤可以輕鬆地設定資訊來源。

運用此方法，*不需要* 在 OpenWhisk 外部使用任何持續性服務。所有資訊來源管理都會透過 Stateless OpenWhisk *資訊來源動作* 自然進行，而這些資訊來源動作會直接與協力廠商的 Webhook API 進行協議。

使用 `CREATE` 呼叫時，資訊來源動作只會安裝某個其他服務的 Webhook，並要求遠端服務將通知 POST 至 OpenWhisk中的適當 `fireTrigger` URL。

應該指示 Webhook 將通知傳送至 URL，例如：

`POST /namespaces/{namespace}/triggers/{triggerName}`

具有 POST 要求的表單將會解譯為 JSON 文件，該文件會在觸發程式事件上定義參數。
OpenWhisk 規則會將這些觸發程式參數傳遞至因該事件而發動的任何動作。

## 使用輪詢實作資訊來源

可以在 OpenWhisk 內設定 OpenWhisk *動作* 來完整輪詢資訊來源，而不需要使用任何持續性連線或外部服務。

針對無法使用 Webhook 但不需要高容量或低延遲回應時間的資訊來源，輪詢是具吸引力的選項。

為了設定輪詢型資訊來源，資訊來源動作會在呼叫 `CREATE` 時採取下列步驟：

1.   資訊來源動作會使用 `whisk.system/alarms` 資訊來源，以所要的頻率設定定期觸發程式 (*T*)。
2.   資訊來源開發人員會建立 `pollMyService` 動作，此動作只會輪詢遠端服務並傳回任何新事件。
3.  資訊來源動作設定*規則* *T -> pollMyService*。

此程序會使用 OpenWhisk 動作完整實作輪詢型觸發程式，而不需要使用個別服務。

## 透過連線實作資訊來源

前兩個架構選項十分簡單且容易實作。不過，如果您想要有高效能資訊來源，則最好的選擇是持續性連線及長期輪詢或類似技術。

因為 OpenWhisk 動作必須是短時間執行的，所以動作無法維護與協力廠商的持續性連線。相反地，我們必須使用隨時都執行的個別服務（在 OpenWhisk 外部）。我們將這些服務稱為*提供者服務*。提供者服務可以維護支援長期輪詢或其他連線型通知的協力廠商事件來源連線。   
提供者服務應該提供容許 OpenWhisk *資訊來源動作* 控制資訊來源的 REST API。提供者服務會作為事件提供者與 OpenWhisk 之間的 Proxy -- 當它接收到來自協力廠商的事件時，會透過發動觸發程式將它們傳送至 OpenWhisk。

Cloudant *changes* 資訊來源是標準範例 -- 它會使用透過持續性連線在 Cloudant 通知之間調解的 `cloudanttrigger` 服務，並觸發 OpenWhisk。

*警示* 資訊來源是使用類似的型樣所實作。

連線型架構是最高效能選項 -- 但與輪詢及連結鉤架構相較，會增加更多的作業額外負擔。   
