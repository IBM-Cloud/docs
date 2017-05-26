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

若要將應用程式連接至服務，請使用與服務一起建立的認證。[compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) 範例應用程式會示範如何使用 Node.js，利用認證來連接至 {{site.data.keyword.composeForScyllaDB}} 服務。

欄位名稱|說明
----------|-----------
`db_type`|服務所提供的資料庫類型。在此情況下，為 `scylla`。
`uri_cli_1`|連接至資料庫實例的替代性 `cqlsh` Shell 指令行。
`maps`|ScyllaDB 連線圖，提供各種驅動程式所需的資訊，以便將 ScyllaDB 資料庫的內部 IP 位址與外部 DNS 名稱相關聯。
`name`|資料庫部署名稱。
`uri_cli`|連接至資料庫實例的 `cqlsh` Shell 指令行。
`uri_direct_2`|可用來連接至服務的替代 URI。針對 `uri` 進行格式化。
`uri_direct_1`|可用來連接至服務的替代 URI。針對 `uri` 進行格式化。
`ca_certificate_base64`|用來確認應用程式將連接至適當伺服器的自簽憑證。憑證是以 base64 的方式編碼。
`deployment_id`|Compose 內所建立之服務的內部 ID。
`uri_cli_2`|連接至資料庫實例的替代性 `cqlsh` Shell 指令行。
`uri`|連接至服務時使用的 URI，包括綱目 (`scylla:`)、密碼、伺服器的主機名稱、要連接至的埠號，以及資料庫名稱。
{: caption="表 1. Compose for ScyllaDB 認證" caption-side="top"}
