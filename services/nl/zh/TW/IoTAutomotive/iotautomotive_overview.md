---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 關於 {{site.data.keyword.iot4auto_short}}（測試版）
{: #iotautomotive_overview}

前次更新：2016 年 7 月 29 日
{: .last-updated}

{{site.data.keyword.iot4auto_full}} 是 {{site.data.keyword.Bluemix_notm}} 上的服務，可用來檢視和分析車輛的海量資料。

使用 {{site.data.keyword.iot4auto_short}} 服務，您可以收集和處理車輛的大量資料。{{site.data.keyword.iot4auto_short}} 分析提供下列項目之效用強大且可採取動作的見解：駕駛人行為、車輛位置，以及其他汽車相關活動和感興趣事件。
{:shortdesc}

## 架構
{: #architecture}
{{site.data.keyword.iot4auto_short}} 是汽車應用程式和已連接車輛裝置的即時基礎架構平台。此服務也設計成支援未來的新興自主駕駛功能。

![{{site.data.keyword.iot4auto_full}} 架構](images/architecture_iotautomotive.png "{{site.data.keyword.iot4auto_full}} 架構")

{{site.data.keyword.iot4auto_short}} 服務包括也可以在 {{site.data.keyword.Bluemix_notm}} 型錄中個別取得的下列 {{site.data.keyword.Bluemix_notm}} 服務：

|服務|說明|
|:---|:---|
|[Driver Behavior](../IotDriverInsights/index.html)| 一種服務，可以從擷取自已連接車輛的汽車探測資料和環境定義資料中分析駕駛人行為以及識別行程的行程型樣。
|[Context Mapping](../IotMapInsights/index.html)| 一種服務，可提供地理空間功能（例如，道路網的地圖比對和最短路徑搜尋）。
*表格 1. {{site.data.keyword.iot4auto_short}} 服務*

## 特性
{: #features}

{{site.data.keyword.iot4auto_short}} 支援解決方案的下列特性和功能，可提供已連接車輛裝置的汽車探測資料：

### 擷取自 {{site.data.keyword.iot4auto_short}} 裝置的資料

- 支援下列通訊協定和資料模型：
   - TPEG
   - ITS
   - ISO 汽車標準
- 支援其他非車輛裝置和感應器

### 資料正規化和儲存

- 識別和過濾異常資料
- 將資料對映、轉換和格式化為標準資料模型，以進行分析
- 根據應用程式或服務的數量、延遲和使用情形，將資料放在下列其中一個資料儲存庫：
   -  進行海量資料分析的 Hadoop 資料儲存庫
   -  進行即時分析的代理程式資料儲存庫

### 地理空間地圖型服務

- 即時地圖比對
- 事件服務
- 來自車輛和外部來源的動態事件注入
- 連接通道或節點型拓蹼察覺搜尋
- 具有整合天氣資料的環境定義地圖支援

### 高度可擴充和低延遲的即時分析平台

- 代理程式型技術
- 個人化分析
- 彈性規則型分析

### 移動物件地圖分析 (MOMA)

- 使用車輛資料進行的批次（海量資料）分析
- 駕駛人行為分析
- 駕駛人側寫
- 行程型樣分析

### 資料提供者服務

- 協力廠商應用程式和服務的 API

### 與資產管理的整合

- 車輛資產管理系統

## REST API
{: #api}

[{{site.data.keyword.iot4auto_short}} API](http://ibm.biz/IoT4Automotive_APIdoc) 提供協助您進一步開發 {{site.data.keyword.iot4auto_short}} 的指令，以符合您的需求。

使用可用的 REST API 指令，即可自訂 {{site.data.keyword.iot4auto_short}} 服務實例：

- 將特定事件注入系統中
- 將車輛的正規化汽車探測資料儲存至偏好的分析資料儲存庫中
- 即時擷取感興趣事件與車輛地理位置

### REST API 指令

|目標 |API 指令 |說明 |
|:---|:---|:---|
|注入事件|`sendEvent`|將交通或其他事件傳送至平台。|
|傳送汽車探測資料|`sendCarProbe`|傳送車輛的位置型感應器資料，以及依即時分析結果來擷取車輛的受影響事件。|
|建立車輛資料|`createVehicle`|將車輛的記錄建立為資產。此資訊用於鑑別、庫存和其他用途。|
|地圖 API|不適用|如需相關資訊，請參閱 [Context Mapping 服務 API](http://ibm.biz/IoTContextMapping_APIdoc)。|
|分析 API|不適用|如需相關資訊，請參閱 [Driver Behavior 服務 API]( http://ibm.biz/IoTDriverBehavior_APIdoc)。|
|取得汽車探測資料|`getCarProbe`|取得 `sendCarProbe` API 指令所傳送之車輛的最新汽車探測資料。|
|取得地圖事件|`getEvent` |取得地圖上 `sendEvent` API 指令所傳送的事件。|
|取得車輛資產資料|`getVehicle`| 從 `createVehicle` API 指令，將車輛資料取得為資產。|
*表格 2. {{site.data.keyword.iot4auto_short}} REST API 指令*
