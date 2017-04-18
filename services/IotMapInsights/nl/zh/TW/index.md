---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 開始使用 {{site.data.keyword.iotmapinsights_short}}
{: #iotdriverinsights_index}
前次更新：2016 年 6 月 22 日
{: .last-updated}

{{site.data.keyword.iotmapinsights_full}} 是 {{site.data.keyword.Bluemix}} 上的服務，可用來啟用您應用程式的地理空間功能（例如，全球道路網的地圖比對和最短路徑搜尋）。  
{:shortdesc}

您可以透過 {{site.data.keyword.iotmapinsights_short}} REST API 使用下列特性：

|特性|用來...|
|:---|:---|
|高度精確的地圖比對|比對 GPS 位置與實際對映的道路網|
|道路幾何佈置資料擷取|擷取對映的道路網，以繪製地圖上的道路形狀|
|動態最短路徑搜尋|搜尋包含即時事件（例如，交通）的最短路徑|
|即時交通事件操作|新增即時與地圖相配的事件（例如，交通狀況），以改善路徑規劃結果|

## 開始之前
{: #byb}

1. 當您從 [{{site.data.keyword.Bluemix_notm}} 型錄](https://console.stage1.ng.bluemix.net/catalog/services/iot-automotive/){: new_window}新增服務實例時，請確定它未連結至應用程式，而且已記下自動產生的承租戶 ID、使用者名稱及密碼值。您稍後需要這些值，才能透過 {{site.data.keyword.iotmapinsights_short}} API 來存取服務。

2. 熟悉 [OpenStreetMap](http://www.openstreetmap.org/){: new_window}。  

 {{site.data.keyword.iotmapinsights_short}} 服務使用以 WGS84 座標擷取自 [OpenStreetMap](http://www.openstreetmap.org/){: new_window} 的道路網資料。只有汽車可以行駛的道路才能用於分析。  

 支援下列地圖地區：

|地區|地圖 ID|
|:---|:---|
|歐洲|map_id=1|
|非洲|map_id=2|
|亞洲|map_id=3|
|澳洲/大洋洲|map_id=4|
|北美洲|map_id=5|
|中美洲|map_id=6|
|南美洲|map_id=7|

## 地圖比對
{: #map_matching}
若要將原始 GPS 座標對映至與地圖相配的座標，請完成下列步驟：

1. 準備一組要分析的原始 GPS 座標。
2. 使用 `mapMatching` API 指令來傳送原始 GPS 座標。選擇性地設定每一個位置的航行角度（以角度為單位），以指定行駛的方向。
 - 要求：原始 GPS 資料
 - 回應：與地圖相配的 GPS 資料、連接通道 ID
3. 選用項目：使用 `getLinkInformation` API 指令來取得道路類型資料。您可以使用 `getLinkInformation` REST API，將相配的道路形狀資料擷取為一系列的座標。
 - 要求：連接通道 ID
 - 回應：道路類型

## 路徑搜尋
{: #route_searching}

使用下列步驟，以尋找所指定原點與目的地座標之間的最短路徑資訊：

1. 判定最短路徑的開始和結束位置。
2. 使用 `routeSearch` REST API 來傳送開始和結束座標。
選擇性地設定每一個位置的航行角度（以角度為單位），以指定行駛的方向。
 - 要求：原點和目的地座標
 - 回應：與地圖相配的最短路徑

使用所傳回的連接通道形狀資料，在地圖上繪製所找到路徑的形狀。

## 新增交通事件
{: #traffic_events}

若要將交通事件資訊新增至 {{site.data.keyword.iotmapinsights_short}} 服務，請完成下列步驟：

1. 選擇您要建立之交通事件的類型和位置。
2. 使用 `createEvent` API 指令來注入事件。
將交通事件資訊傳送至 {{site.data.keyword.iotmapinsights_short}} 服務。
 - 要求：事件資訊
 - 回應：事件 ID
3. 使用 `queryEvent` REST API 指令來尋找事件。
搜尋特定矩形區域內的交通事件，以及選擇性地搜尋特定的交通事件類型。
 - 要求：區域資訊。
 - 回應：事件資訊。  
4. 選用項目：使用 `deleteEvent` API 指令來移除不再有效的交通事件。
5. 選用項目：使用 `getAffectedLinksInformation` API 指令來擷取交通事件所影響道路上的某個區域。

# 相關鏈結
{: #rellinks}

## 指導教學和範例
{: #samples}

* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} 指導教學第 1 部分](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} 指導教學第 2 部分](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}
* [IoT for Automotive Starter 應用程式](https://iot-automotive-starter.mybluemix.net){:new_window}

## API 參考資料
{: #api}

* [API 文件](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}

## 相關鏈結
{: #general}

* [開始使用 {{site.data.keyword.iotdriverinsights_short}}](../IotDriverInsights/index.html){:new_window}
* [開始使用 {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [IBM developerWorks 上的 dW Answers](https://developer.ibm.com/answers/topics/iot-context-mapping){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/iot-context-mapping){:new_window}
* [Bluemix 服務的新增功能](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [OpenStreetMap](http://www.openstreetmap.org/){:new_window}
* [&copy; OpenStreetMap 貢獻者](http://www.openstreetmap.org/copyright){:new_window}
* [Open Data Commons Open Database License (ODbL)](http://opendatacommons.org/licenses/odbl/){:new_window}
