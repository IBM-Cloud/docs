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

# 開始使用 Compose for RethinkDB
{: #getting-started-with-compose-for-rethinkdb}

{{site.data.keyword.composeForRethinkDB}} 使用整合式管理及探索主控台來提供 JSON 文件型分散式資料庫。RethinkDB 所使用的 ReQL 查詢語言是根據功能鏈結所建置，且位於 Java、JavaScript、Python 及 Ruby 的用戶端程式庫中。使用 ReQL，可以跨叢集節點使用 RethinkDB 伺服器端特性（例如分散式結合及子查詢）。RethinkDB 也支援次要索引，以獲得較佳的讀取查詢效能。RethinkDB 的最強大特性 (changefeeds) 容許將許多 ReQL 查詢轉換為即時資訊來源。
{:shortdesc}

**附註：**在 2016 年 9 月 14 日之前佈建且仍然作用中的任何 Compose 服務實例，仍然可以使用，而且可以在 [https://www.compose.com/](https://www.compose.com) 直接存取。在 Bluemix 帳戶內，可以直接存取及使用從此點往前佈建的任何 Compose 服務實例。

請完成下列步驟，以開始使用 {{site.data.keyword.composeForRethinkDB}}。

1. [建立 {{site.data.keyword.composeForRethinkDB}} 實例](https://console.ng.bluemix.net/catalog/services/compose-for-rethinkdb/)。

  當您建立服務的實例時，請確保要選擇服務名稱及認證名稱。請維持服務不連結；稍後使用佈建服務時所提供的認證，即可將應用程式連接至服務。*可用的認證* 小節中會列出各種認證值。

2. 連接至 {{site.data.keyword.composeForRethinkDB}} 服務。

   若要將應用程式連接至服務，請使用與服務一起建立的[認證](./credentials.html)。範例應用程式會示範如何使用 Node.js 來連接至 {{site.data.keyword.composeForRethinkDB}} 服務。

   請下載 [compose-rethinkdb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rethinkdb-helloworld-nodejs) 範例應用程式，並遵循 Readme 檔中的指示。然後，在 Bluemix 的應用程式詳細資料頁面中，按一下**檢視應用程式**。
