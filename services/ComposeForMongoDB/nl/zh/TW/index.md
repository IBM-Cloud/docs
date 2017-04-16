---

copyright:
  years: 2016
lastupdated: "2016-12-09"
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

   若要將應用程式連接至服務，請使用與服務一起建立的認證。範例應用程式會示範如何使用 Node.js 來連接至 {{site.data.keyword.composeForMongoDB}} 服務。

   請下載 [compose-mongodb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mongodb-helloworld-nodejs) 範例應用程式，並遵循 Readme 檔中的指示。然後，在 Bluemix 的應用程式詳細資料頁面中，按一下**檢視應用程式**。


## 可用的認證

欄位名稱|說明
----------|-----------
`uri`|要在連接至服務時使用的 URI。`uri` 包括綱目 (`mongodb:`)、管理使用者名稱和密碼、伺服器的主機名稱、要連接至的埠號、資料庫名稱及 `?ssl=true`，以啟用 SSL 連線。
`uri_cli`|連接至資料庫實例的 `mongo` Shell 指令行。
`ca_certificate_base64`|用來確認應用程式將連接至適當伺服器的自簽憑證。憑證是 base64 編碼。您必須先解碼金鑰，才能使用金鑰（如範例應用程式中所示）。
`deployment_id`|Compose 內所建立之服務的內部 ID。
`db_type`|服務所提供的資料庫類型；在此情況下，為 `mongodb`。
`name`|資料庫部署名稱。
{: caption="Table 1. {{site.data.keyword.composeForMongoDB}} credentials" caption-side="top"}

# 相關鏈結
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose 文章](https://www.compose.com/articles/){:new_window}

## 指導教學及範例
{: #samples}
* [compose-mongodb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mongodb-helloworld-nodejs){:new_window}

## 相關鏈結
{: #general}
* [Compose 說明](https://help.compose.com/docs){:new_window}
