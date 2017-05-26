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

# 開始使用 Compose for PostgreSQL
{: #getting-started-with-compose-for-postgreSQL}

{{site.data.keyword.composeForPostgreSQL}} 提供可高度自訂的強大開放程式碼物件導向資料庫。使用 Postgres，開發十分快速，而且可以輕鬆地擴充。您可以使用想要的語言（例如 C/C++、Perl、Python、TCL/TK、Delphi/Kylix、VB、PHP、ASP 及 Java）進行開發。您可以取得具有 JSON 支援之特性豐富的企業資料庫，提供最佳的 SQL 及 NoSQL 世界。
{:shortdesc}

**附註：**在 2016 年 9 月 14 日之前佈建且仍然作用中的任何 Compose 服務實例，仍然可以使用，而且可以在 [https://www.compose.com/](https://www.compose.com) 直接存取。在 Bluemix 帳戶內，可以直接存取及使用從此點往前佈建的任何 Compose 服務實例。

請完成下列步驟，以開始使用 Compose for PostgreSQL：

1. [建立 {{site.data.keyword.composeForPostgreSQL}} 實例](https://console.ng.bluemix.net/catalog/services/compose-for-postgresql/)。

  當您建立服務的實例時，請確保要選擇服務名稱及認證名稱。請維持服務不連結；稍後使用佈建服務時所提供的認證，即可將應用程式連接至服務。*可用的認證* 小節中會列出各種認證值。

2. 連接至 {{site.data.keyword.composeForPostgreSQL}} 服務。

  若要將應用程式連接至服務，請使用與服務一起建立的[認證](./credentials.html)。範例應用程式會示範如何使用 Node.js 來連接至 {{site.data.keyword.composeForPostgreSQL}} 服務。

  請下載 [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs) 範例應用程式，並遵循 Readme 檔中的指示。然後，在 Bluemix 的應用程式詳細資料頁面中，按一下**檢視應用程式**來檢視 *examples* 表格的內容。
