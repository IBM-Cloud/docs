---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 開始使用 {{site.data.keyword.iot4auto_short}}（測試版）
{: #getting_started_iotautomotive}

前次更新：2016 年 7 月 29 日
{: .last-updated}

{{site.data.keyword.iot4auto_full}} 是 {{site.data.keyword.Bluemix_notm}} 服務，可用來擷取、管理和分析已連接車輛的海量資料。{{site.data.keyword.iot4auto_short}} 分析提供下列項目之效用強大且可採取動作的見解：駕駛行為、車輛位置，以及其他汽車相關活動和感興趣事件。

{:shortdesc}

使用 {{site.data.keyword.iot4auto_short}}，即可執行下列作業：

- 將汽車探測資料和正規化資料傳送至資料儲存庫，以進行分析
- 將事件注入環境定義地圖，以及擷取影響特定車輛的事件
- 識別汽車探測資料中的新事件
- 擷取已連接車輛的相關資訊
- 管理駕駛人、車輛、事件規則、事件類型和供應商的資產資料


{{site.data.keyword.iot4auto_short}} 服務包括也可以在 {{site.data.keyword.Bluemix_notm}} 型錄中個別取得的下列 {{site.data.keyword.Bluemix_notm}} 服務：

|服務|說明|
|:---|:---|
|[Driver Behavior](../IotDriverInsights/index.html){:new_window}| 一種服務，可以從擷取自已連接車輛的汽車探測資料和環境定義資料中，分析駕駛人行為以及識別行程的行程型樣。
|[Context Mapping](../IotMapInsights/index.html){:new_window}| 一種服務，可提供地理空間功能（例如，道路網的地圖比對和最短路徑搜尋）。
*表格 1. {{site.data.keyword.iot4auto_short}}* 的服務

開始整合汽車裝置和應用程式與服務之前，請確定已完成下列步驟：

1. 檢閱[關於 {{site.data.keyword.iot4auto_short}}](iotautomotive_overview.html) 主題，以熟悉服務可用和支援的特性和分析。
2. 從 [{{site.data.keyword.Bluemix_notm}} 型錄](https://console.ng.bluemix.net/catalog/labs/){:new_window}新增服務實例時，請確定它未連結至應用程式，而且已記下自動產生的承租戶 ID、使用者名稱及密碼值。您稍後需要這些值，才能透過 {{site.data.keyword.iot4auto_short}} API 來存取服務。
3. 使用儀表板上的主控台，配置 {{site.data.keyword.iot4auto_short}} 的埠、目標主機名稱和其他設定。如需相關資訊，請參閱[管理](iotautomotive_admin.html)。

您可以使用 {{site.data.keyword.iot4auto_short}} REST API 指令，來整合汽車裝置和應用程式與此服務。

若要快速開始進行，請完成下列步驟：

1. 使用 `sendEvent` API 要求指令來傳送要分析的事件，以注入事件。
  - 要求：含有位置的事件資料
2. 使用 `getEvent` API 要求指令來擷取事件，以確認事件資料是與「地圖比對」一起儲存。
  - 要求：區域資料（開始點或結束點的經緯度）
  - 回應：含有連接通道 ID 的事件資料
3.  使用 `sendCarProbe` API 要求指令，來傳送要分析的汽車探測資料。
  - 要求：含有位置的汽車探測資料
4. 使用 `getCarProbe` API 要求指令來擷取資料，以確認汽車探測資料是與「地圖比對」一起儲存。
  - 要求：區域資料（開始點或結束點的經緯度）
  - 回應：含有連接通道 ID 的汽車探測資料
5. 分析駕駛人資料。如需相關資訊，請參閱 [Driver Behavior](../IotDriverInsights/index.html){:new_window}。

# 相關鏈結
{: #rellinks}

## API 參考資料
{: #api}
* [{{site.data.keyword.iot4auto_short}} API 文件](http://ibm.biz/IoT4Automotive_APIdoc){:new_window}
* [Context Mapping 服務 API](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}
* [Driver Behavior 服務 API]( http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}


## 相關鏈結
{: #general}
* [開始使用 {{site.data.keyword.iotdriverinsights_short}}](../IotDriverInsights/index.html){:new_window}
* [開始使用 {{site.data.keyword.iotmapinsights_short}}](../IotMapInsights/index.html){:new_window}
* [開始使用 {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [Bluemix 服務的新增功能](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [IBM developerWorks 上的 dW Answers](https://developer.ibm.com/answers/topics/iot-for-automotive){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/iot-for-automotive){:new_window}
