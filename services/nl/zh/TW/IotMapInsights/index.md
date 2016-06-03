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
{: #gettingstartedtemplate}
*前次更新：2016 年 5 月 13 日*

{{site.data.keyword.iotmapinsights_full}} 可讓開發人員輕鬆啟用其應用程式來使用地理空間功能，例如根據全球道路網的地圖比對及最短路徑搜尋。
{:shortdesc}

您可以透過 {{site.data.keyword.iotmapinsights_short}} REST API 使用下列功能：

- 使用道路網幾何佈置的高度精準地圖比對。
- 運用地圖上的即時事件（例如，交通）。
- 考量即時事件（例如，交通）的動態最短路徑搜尋（路徑搜尋）。
- 擷取可用來在地圖上繪製道路形狀的道路幾何佈置資料。

{{site.data.keyword.iotmapinsights_short}} 服務使用以 WGS84 座標擷取自 OpenStreetMap 的道路網資料。只有車輛可以行駛的道路才能用於分析。

支援的地圖區域如下：

- 歐洲 (map_id=1)
- 非洲 (map_id=2)
- 亞洲 (map_id=3)
- 澳洲/大洋洲 (map_id=4)
- 北美洲 (map_id=5)
- 中美洲 (map_id=6)
- 南美洲 (map_id=7)


請遵循下列步驟，以使用 {{site.data.keyword.iotmapinsights_short}} 服務的分析功能。

## 使用 {{site.data.keyword.iotmapinsights_short}} 以進行地圖比對

1. 準備一組要分析的原始 GPS 座標資料。
2. 使用 `mapMatching` REST API，將原始 GPS 座標資料按時間序列順序傳送至 {{site.data.keyword.iotmapinsights_short}} 服務。選擇性地設定每一個位置的航行角度（以角度為單位；北方為 0，順時針旋轉角度），以指定行駛的方向。
3. 在 `mapMatching` REST API 呼叫的回應中，收到與地圖相配的座標。
4. 選擇性地使用 `getLinkInformation` REST API，以擷取與地圖相配的連接通道的道路形狀資料。以連接通道 ID 呼叫 `getLinkInformation` REST API，即可取得組成道路形狀的一系列座標。

## 使用 {{site.data.keyword.iotmapinsights_short}} 以進行路徑搜尋

1. 判定您要取得最短路徑的起始及結束位置。
2. 使用 `routeSearch` REST API，將開始和結束座標傳送至 {{site.data.keyword.iotmapinsights_short}} 服務。選擇性地設定每一個位置的航行角度（以角度為單位；北方為 0，順時針旋轉角度），以指定行駛的方向。
3. 在 `routeSearch` REST API 呼叫的回應中，收到連接通道的清單。您可以使用結果資料中所包含的形狀資料，在地圖上繪製所找到路徑的形狀。

## 使用 {{site.data.keyword.iotmapinsights_short}} 以運用交通事件

1. 判定您要建立之交通事件的類型及位置。
2. 使用 `createEvent` REST API，將交通事件資訊傳送至 {{site.data.keyword.iotmapinsights_short}} 服務。
3. 在 `createEvent` REST API 呼叫的回應中，收到所建立之交通事件的事件 ID。
4. 使用 `queryEvent` REST API，選擇性地利用特定的交通事件類型，搜尋特定矩形區域內的交通事件。

- 選擇性地使用 `deleteEvent` REST API，移除不再有效的交通事件。
- 選擇性地使用 `getAffectedLinksInformation` REST API，擷取交通事件所影響道路上的某個區域。


# 相關鏈結
{: #rellinks}
## 指導教學和範例
{: #samples}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} 指導教學第 1 部分](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} 指導教學第 2 部分](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}

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

