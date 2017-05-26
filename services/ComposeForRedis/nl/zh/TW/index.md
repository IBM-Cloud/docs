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

# 開始使用 Compose for Redis
{: #getting-started-with-compose-for-redis}

Redis 是開放程式碼記憶體內鍵值儲存庫。Redis 中的值可以是簡式字串、雜湊、清單，以及集合或強大的點陣圖、hyperloglogs 和地理空間索引。Redis 最適合用作應用程式快取或快速回應資料儲存庫。{{site.data.keyword.composeForRedis_full}} 提供已預先針對高可用性及磁碟內存持續性進行調整的配置，全部都透過額外安全特性鎖定。
{:shortdesc}

**附註：**在 2016 年 9 月 14 日之前佈建且仍然作用中的任何 Compose 服務實例，仍然可以使用，而且可以在 [https://www.compose.com/](https://www.compose.com) 直接存取。在 Bluemix 帳戶內，可以直接存取及使用從此點往前佈建的任何 Compose 服務實例。

請完成下列步驟，以開始使用 {{site.data.keyword.composeForRedis}}。

1. [建立 {{site.data.keyword.composeForRedis}} 實例](https://console.ng.bluemix.net/catalog/services/compose-for-redis/)。

  當您建立服務的實例時，請確保要選擇服務名稱及認證名稱。請維持服務不連結；稍後使用佈建服務時所提供的認證，即可將應用程式連接至服務。*可用的認證* 小節中會列出各種認證值。

2. 連接至 {{site.data.keyword.composeForRedis}} 服務。

  若要將應用程式連接至服務，請使用與服務一起建立的[認證](./credentials.html)。範例應用程式會示範如何使用 Node.js 來連接至 {{site.data.keyword.composeForRedis}} 服務。

  請下載 [compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs) 範例應用程式，並遵循 Readme 檔中的指示。然後，在 Bluemix 的應用程式詳細資料頁面中，按一下**檢視應用程式**。
