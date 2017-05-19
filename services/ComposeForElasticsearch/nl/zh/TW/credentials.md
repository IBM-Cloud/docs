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

若要將應用程式連接至服務，請使用與服務一起建立的認證。[compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) 範例應用程式會示範如何使用 Node.js，利用認證來連接至 {{site.data.keyword.composeForElasticsearch}} 服務。

欄位名稱|說明
----------|-----------
`uri`|要在連接至服務時使用的 URI。包括綱目 (`https:`)、管理使用者名稱和密碼、伺服器的主機名稱，以及要連接至的埠號。
`uri_direct_1`|可以在連接至服務時使用的替代 URI。針對 `uri` 進行格式化。
`uri_health`|要求第一個 haproxy 之叢集性能的 `curl` 指令。
`uri_health_1`|要求第二個 haproxy 之叢集性能的 `curl` 指令。
`ca_certificate_base64`|用來確認應用程式將連接至適當伺服器的自簽憑證。這是 base64 編碼。您需要先解碼金鑰，才能使用金鑰（如範例應用程式中所示）。
`deployment_id`|Compose 內所建立之服務的內部 ID。
`db_type`|服務所提供的資料庫類型；在此情況下，為 `elastic_search`。
`name`|資料庫部署名稱。
{: caption="表 1. Compose for Elasticsearch 認證" caption-side="top"}

**附註：**兩個 `haproxy` 入口網站都可以存取 Elasticsearch 叢集。`uri` 及 `uri_direct_1` 都可以用來連接至叢集。在應用程式中，切換 `uri` 與 `uri_direct_1`，以管理連線失敗的回應。
