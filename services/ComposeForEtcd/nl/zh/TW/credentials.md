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

若要將應用程式連接至服務，請使用與服務一起建立的認證。[compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) 範例應用程式會示範如何使用 Node.js，利用認證來連接至 {{site.data.keyword.composeForEtcd}} 服務。

欄位名稱|說明
----------|-----------
`ca_certificate_base64`|用來確認應用程式將連接至適當伺服器的自簽憑證。憑證是 base64 編碼。您必須先解碼金鑰，才能使用金鑰（如範例應用程式中所示）。
`deployment_id`|Compose 內所建立之服務的內部 ID。
`db_type`|服務所提供的資料庫類型；在此情況下，為 `etcd`。
`name`|資料庫部署名稱。
`uri`|要在連接至服務時使用的 URI。`uri` 包括綱目 (`amqps:`)、管理使用者名稱和密碼、伺服器的主機名稱、要連接至的埠號，以及 vhost 名稱。

{: caption="表 1. Compose for etcd 認證" caption-side="top"}
