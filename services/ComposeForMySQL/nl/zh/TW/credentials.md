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

# 可用的認證
{: #available-credentials}

若要將應用程式連接至服務，請使用與服務一起建立的認證。[compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) 範例應用程式會示範如何使用 Node.js，利用認證來連接至 {{site.data.keyword.composeForMySQL}} 服務。

欄位名稱|說明
----------|-----------
`db_type`|服務所提供的資料庫類型。在此情況下，為 `mysql`。
`name`|資料庫部署名稱。
`uri_cli`|連接至資料庫實例的 `mysql` Shell 指令行。
`ca_certificate_base64`|用來確認應用程式將連接至適當伺服器的自簽憑證。憑證是以 base64 的方式編碼。
`deployment_id`|Compose 內所建立之服務的內部 ID。
`uri`|連接至服務時使用的 URI，包括綱目 (`mysql:`)、管理使用者名稱和密碼、伺服器的主機名稱、要連接至的埠號，以及 vhost 名稱。
{: caption="表 1. Compose for MySQL 認證" caption-side="top"}
