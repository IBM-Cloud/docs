---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#使用 {{site.data.keyword.geospatialshort_Geospatial}} 入門範本應用程式
{: #starter_app}


{{site.data.keyword.geospatialshort_Geospatial}} 包含入門範本應用程式，可供您用來作為實驗用的範本，以及進行變更並將變更推送到 {{site.data.keyword.Bluemix_short}} 環境。
{:shortdesc}

入門範本應用程式針對一組在拉斯維加斯附近移動中的模擬裝置，使用來自示範 MQTT 分配管理系統的訊息。應用程式會將關於其作業狀態的相關資訊以及它偵測到的事件，輸出到簡單的網頁。


從該網頁鏈結的視覺化程式，會監視裝置從地圖上的一個位置移動到另一個位置。視覺化程式未鏈結到入門範本應用程式，因此它不會受到您對入門範本應用程式副本所做的變更影響。入門範本應用程式的程式碼是以 Node.js 撰寫，它顯示如何透過其 REST API 來配置及控制 {{site.data.keyword.geospatialshort_Geospatial}} 服務。 


您可以執行入門範本應用程式，而不需要進行修改。如果您要進一步試驗服務，也可以修改程式碼，並將變更推送回 {{site.data.keyword.Bluemix_short}} 環境。
