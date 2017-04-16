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

# 開始使用 {{site.data.keyword.composeForRedis}}
{: #getting-started-with-compose-for-redis}

Redis 是開放程式碼記憶體內鍵值儲存庫。Redis 中的值可以是簡式字串、雜湊、清單，以及集合或強大的點陣圖、hyperloglogs 和地理空間索引。Redis 最適合用作應用程式快取或快速回應資料儲存庫。{{site.data.keyword.composeForRedis_full}} 提供已預先針對高可用性及磁碟內存持續性進行調整的配置，全部都透過額外安全特性鎖定。
{:shortdesc}

**附註：**在 2016 年 9 月 14 日之前佈建且仍然作用中的任何 Compose 服務實例，仍然可以使用，而且可以在 [https://www.compose.com/](https://www.compose.com) 直接存取。在 Bluemix 帳戶內，可以直接存取及使用從此點往前佈建的任何 Compose 服務實例。

請完成下列步驟，以開始使用 {{site.data.keyword.composeForRedis}}。

1. [建立 {{site.data.keyword.composeForRedis}} 實例](https://console.ng.bluemix.net/catalog/services/compose-for-redis/)。

  當您建立服務的實例時，請確保要選擇服務名稱及認證名稱。請維持服務不連結；稍後使用佈建服務時所提供的認證，即可將應用程式連接至服務。*可用的認證* 小節中會列出各種認證值。

2. 連接至 {{site.data.keyword.composeForRedis}} 服務。

  若要將應用程式連接至服務，請使用與服務一起建立的認證。範例應用程式會示範如何使用 Node.js 來連接至 {{site.data.keyword.composeForRedis}} 服務。

  請下載 [compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs) 範例應用程式，並遵循 Readme 檔中的指示。然後，在 Bluemix 的應用程式詳細資料頁面中，按一下**檢視應用程式**。

## 可用的認證

欄位名稱|說明
----------|-----------
`uri`|要在連接至服務時使用的 URI，包括綱目 (redis:)、管理使用者名稱和密碼、伺服器的主機名稱，以及要連接至的埠號。
`uri_cli`|連接至資料庫實例的 `redis-cli` 指令行。
`deployment_id`|Compose 內所建立之服務的內部 ID。
`db_type`|服務所提供的資料庫類型；在此情況下，為 `redis`。
`name`|資料庫部署名稱。
{: caption="Table 1. {{site.data.keyword.composeForRedis}} credentials" caption-side="top"}

# 相關鏈結
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose 文章](https://www.compose.com/articles/){:new_window}

## 指導教學及範例
{: #samples}
* [compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs){:new_window}

## 相關鏈結
{: #general}
* [Compose 說明](https://help.compose.com/docs){:new_window}
