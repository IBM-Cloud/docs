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

# 開始使用 Compose for ScyllaDB
{: #getting-started-with-compose-for-scylladb}

ScyllaDB 是 Cassandra 寬直欄分散式資料庫的就地取代。ScyllaDB 以 C++ 撰寫，而不是 Cassandra 的 Java，它能夠更充份利用資源，在基準性能測試時可達到 10 倍的效能。除了維持與 Cassandra 工具及資料檔案的相容性以外，ScyllaDB 也新增了自行調整的功能。{{site.data.keyword.composeForScyllaDB_full}} 延伸了 ScyllaDB 的功能，因為它能替您管理、提供容易、自動擴充的部署系統，此系統能提供高可用性與備援，也能提供自動化備份。
{:shortdesc}

**附註：**{{site.data.keyword.composeForScyllaDB_full}} 不會提供 Compose 使用者介面的存取權。如需詳細資料，請參閱 [Compose on Bluemix Support](https://help.compose.com/docs/bluemix-compose-support)。

請完成下列步驟，以開始使用 {{site.data.keyword.composeForScyllaDB}}：

1. [建立 {{site.data.keyword.composeForScyllaDB}} 實例](https://console.ng.bluemix.net/catalog/services/compose-for-scylladb/)。

   當您建立服務的實例時，請選擇服務名稱及認證名稱。請維持服務不連結；稍後使用佈建服務時所提供的認證，即可將應用程式連接至服務。「可用的認證」小節中會列出各種認證值。

2. 連接至 {{site.data.keyword.composeForScyllaDB}} 服務。

   若要將應用程式連接至服務，請使用與服務一起建立的認證。

   請下載 [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) 範例應用程式，並遵循 Readme 檔中的指示。然後，在 Bluemix 主控台的應用程式詳細資料頁面中，按一下**檢視應用程式**。

   範例應用程式會示範如何使用 Node.js 來連接至 {{site.data.keyword.composeForScyllaDB}} 服務。


## 可用的認證

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
{: caption="Table 1. {{site.data.keyword.composeForScyllaDB}} credentials" caption-side="top"}


# 相關鏈結
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose 文章](https://www.compose.com/articles/){:new_window}

## 指導教學及範例
{: #samples}
* [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs){:new_window}

## 相關鏈結
{: #general}
* [Compose 說明](https://help.compose.com/docs){:new_window}
