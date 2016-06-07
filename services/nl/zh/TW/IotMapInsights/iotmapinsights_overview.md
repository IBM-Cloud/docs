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

{{site.data.keyword.iotmapinsights_short}} 服務是根據記憶體快取中所儲存的道路網資料。此服務可高速存取靜態道路網資料、動態事件資料及以道路網為基礎的地理空間工具，這可讓您的應用程式整合地理空間功能。
{:shortdesc}

## 靜態地圖資料查詢
{: #static_map_data_query}

為了存取連接通道屬性資料，{{site.data.keyword.iotmapinsights_short}} 服務提供了「連接通道查詢 REST API」介面。此介面會接收地圖比對功能可識別的連接通道 ID 作為參數，並傳回所要求連接通道的詳細資訊，例如道路類型、長度、詳細的形狀點陣列、鄰近的交叉點，以及鄰近的連接通道。透過使用已查詢的詳細連接通道資訊，您的應用程式可以觀察鄰近的連接通道資訊，以遍訪連接通道網路。

## 動態事件資料
{: #dynamic_event_data}

{{site.data.keyword.iotmapinsights_short}} 服務中的事件是交通事件的物件模型，它會動態地放置在特定的連接通道上。此事件含有交通事件的基本屬性，例如 GPS 座標、時間、類型、事件持續時間及受影響的長度。您可以動態地注入及刪除事件。

## 事件注入及刪除
{: #inject_event}

利用事件注入 REST API 介面，您可以在地圖上儲存某個事件。若要注入事件，您可以使用定義的事件類型將事件資訊張貼到此介面，以根據應用程式的預定用途來分類事件及其屬性。利用事件刪除 REST API 介面，您可以移除地圖中的事件，以便能夠管理過期的事件。

## 事件查詢
{: #query_event}

利用事件查詢 REST API 介面，您可以使用已設為要求參數的指定條件來查詢事件。對於查詢條件，您可以設定含有經緯度範圍的區域以及事件屬性，來減少作為要求回應傳回的目標事件。

## 地理空間工具
{: #geospatial_tools}

對於地理空間工具，{{site.data.keyword.iotmapinsights_short}} 服務提供一個用於地圖比對及路徑搜尋功能的 REST API 介面。

## 地圖比對
{: #map_matching}

如果來自裝置的 GPS 資料不夠精確而無法使用分析或視覺化，或者您的應用程式需要連接通道網路的屬性，您可以使用地圖比對 REST API 介面。地圖比對 REST API 可讓您的應用程式將原始 GPS 資料點與連接通道的相符點相配。地圖比對 REST API 介面會收到一個包含 GPS 經緯度座標的點，並傳回與地圖相配的點。這個點會透過考量特定時段內每部車輛的歷程資料來進行分析，以即時找出最可能的點。對於沒有歷程位置資料的點，地圖比對介面會傳回連接通道上離所要求的 GPS 點最接近的點。

## 路徑搜尋
{: #route_search}

如果您必須實作含有地理空間功能的應用程式，則需要搜尋兩個點之間的最短路徑。{{site.data.keyword.iotmapinsights_short}} 服務的路徑搜尋 REST API 介面會計算開始點與結束點 GPS 座標之間的最短路徑。接收的座標會透過使用地圖比對功能與地圖的最接近連接通道相符，而且會計算這些與地圖相配的點之間的最短路徑。

## 受影響連接通道搜尋
{: #link_search}

當道路上發生事件時，它可能會影響各個連接通道。您可以使用 REST API 來搜尋受影響的連接通道，以及尋找車輛可能會接觸到事件的連接通道。此搜尋會將連接通道網路的拓蹼納入考量，而不只是車輛離事件的距離。

