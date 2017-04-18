---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 關於 {{site.data.keyword.iotmapinsights_short}}
{: #iotmapinsights_overview}
前次更新：2016 年 7 月 20 日
{: .last-updated}

{{site.data.keyword.iotmapinsights_full}} 是 {{site.data.keyword.Bluemix_notm}} 上的服務，可用來快速存取靜態道路網資料和動態事件資料。{{site.data.keyword.iotmapinsights_short}} 也提供道路網的地理空間工具，可用來整合地理空間功能與您的應用程式。
{:shortdesc}

{{site.data.keyword.iotmapinsights_short}} 服務提供下列特性：

- 靜態地圖資料
- 動態事件資料
- 地理空間工具

{{site.data.keyword.iotmapinsights_short}} 服務會收集和使用服務記憶體快取中所儲存的 [OpenStreetMap](http://www.openstreetmap.org/){: new_window} 道路網資料來進行處理。

依 OpenStreetMap Foundation (OSMF) 的 Open Data Common Open Database License (ODbL) 之規定，可使用 OpenStreetMap 中的資料。如需相關資訊，請參閱 [OpenStreetMap 版權與授權條款](http://www.openstreetmap.org/copyright){: new_window}。

## 靜態地圖資料
{: #static_map_data_query}

產品的其中一個主要特性是可擷取詳細道路資訊，以與您的應用程式搭配使用。使用「連接通道查詢 REST API」介面，可依連接通道 ID 來查詢靜態地圖道路屬性資料。使用 {{site.data.keyword.iotmapinsights_short}} 的[地圖比對](#map_matching)功能，可識別必要連接通道 ID 參數。

所傳回的資料包括所要求連接通道 ID 的下列資訊：

- 道路類型
- 道路長度
- 詳細形狀點的陣列
- 相鄰節點和相鄰連接通道的相關資訊

透過查詢詳細連接通道資訊，您的應用程式可以智慧地使用所傳回的相鄰連接通道資訊，來遍訪連接通道網路。

## 動態事件資料
{: #dynamic_event_data}

除了靜態地圖資料之外，真實道路狀況還必須包括動態事件（例如，交通壅塞和道路工程）。請使用 {{site.data.keyword.iotmapinsights_short}}，基於路徑規劃目的，利用[受影響連接通道搜尋](#link_search)來建立、管理和包含交通事件。

### 注入和刪除事件
{: #inject_event}

使用 {{site.data.keyword.iotmapinsights_short}} 服務事件注入 REST API，以放在特定連接通道的地圖物件模型形式來動態注入和移除交通事件。每個事件都會包括基本屬性（例如，GPS 座標、開始時間、事件類型、事件持續時間，以及受影響的道路長度）。

使用事件刪除 REST API 介面，以在地圖中的事件作廢時將其移除。

### 事件查詢
{: #query_event}

使用事件查詢 REST API，來取得特定地理區域中所有動態事件的詳細資訊。您可以依含有經緯度範圍的區域進行查詢，而且可以包括事件屬性來減少所傳回的目標事件數目。

## 地理空間工具
{: #geospatial_tools}

使用 {{site.data.keyword.iotmapinsights_short}} 地理空間工具所提供的地圖比對和路徑搜尋功能，來加強您的應用程式。

### 地圖比對
{: #map_matching}

搭配使用地圖比對 REST API 介面與您的應用程式，將實際裝置 GPS 座標對映至 [OpenStreetMap](http://www.openstreetmap.org/){: new_window} 道路網資料，以提高不準確 GPS 資料的位置精確度。您也可以根據位置來接收道路屬性的相關資訊。地圖比對 REST API 可讓您的應用程式將原始 GPS 資料點與連接通道上的相符點相配。

地圖比對 REST API 介面會收到一個包含 GPS 經緯度座標的點，並傳回與地圖相配的點。與地圖相配的點會透過考量特定時段內每部汽車的歷程資料來進行分析，以即時找出最可能的點。對於沒有歷程位置資料的點，地圖比對介面會傳回連接通道上離所要求的 GPS 點最接近的點。

### 路徑搜尋
{: #route_search}

含有地理空間功能的應用程式的其中一個基本特性，是可尋找兩個點之間的最短路徑。  

{{site.data.keyword.iotmapinsights_short}} 服務的路徑搜尋 REST API 介面會計算開始點與結束點 GPS 座標之間的最短路徑。接收的座標會透過使用地圖比對功能與地圖的最接近連接通道相符，而且會計算這些與地圖相配的點之間的最短路徑。

### 受影響連接通道搜尋
{: #link_search}

當道路上發生事件時，它可能會影響各個連接通道。您可以使用 REST API 來搜尋受影響的連接通道，以及尋找汽車可能會接觸到事件的連接通道。此搜尋會考慮使用連接通道網路的拓蹼，而不只是汽車離事件的距離。
