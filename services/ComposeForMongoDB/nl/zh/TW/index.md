---

copyright:
  years: 2016,2017
lastupdated: "2017-04-27"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 開始使用 Compose for MongoDB
{: #getting-started-with-compose-for-mongodb}

{{site.data.keyword.composeForMongoDB_full}} 使用 MongoDB 的強大編製索引及查詢、聚集及廣泛驅動程式支援，讓 MongoDB 成為許多新創事業和企業的首選 JSON 資料儲存庫。{{site.data.keyword.composeForMongoDB}} 提供簡單的自動調整部署系統。它提供高可用性及備援、自動化及隨需應變持續備份、監視工具、整合至警示系統、效能分析視圖等，全部都是透過全新的簡單使用者介面完成。
{:shortdesc}

**附註：**在 2016 年 9 月 14 日之前佈建且仍然作用中的任何 Compose 服務實例，仍然可以使用，而且可以在 [https://www.compose.com/](https://www.compose.com) 直接存取。在 Bluemix 帳戶內，可以直接存取及使用從此點往前佈建的任何 Compose 服務實例。

請完成下列步驟，以開始使用 {{site.data.keyword.composeForMongoDB}}：

1. [建立 {{site.data.keyword.composeForMongoDB}} 實例](https://console.ng.bluemix.net/catalog/services/compose-for-mongodb/)。

   當您建立服務的實例時，請確保要選擇服務名稱及認證名稱。請維持服務不連結；稍後使用佈建服務時所提供的認證，即可將應用程式連接至服務。*可用的認證* 小節中會列出各種認證值。

2. 連接至 {{site.data.keyword.composeForMongoDB}} 服務。

   若要將應用程式連接至服務，請使用與服務一起建立的[認證](./credentials.html)。範例應用程式會示範如何使用 Node.js 來連接至 {{site.data.keyword.composeForMongoDB}} 服務。

   請下載 [compose-mongodb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mongodb-helloworld-nodejs) 範例應用程式，並遵循 Readme 檔中的指示。然後，在 Bluemix 的應用程式詳細資料頁面中，按一下**檢視應用程式**。
