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

# 開始使用 Compose for Elasticsearch
{: #getting-started-with-compose-for-elasticsearch}

{{site.data.keyword.composeForElasticsearch_full}} 合併全文檢索引擎的功能與 JSON 文件資料庫的編製索引強度。它們也會建立強大的工具，以對大量資料進行豐富資料分析。使用 Elasticsearch，可以針對確切程度評分搜尋，讓您可以探索資料集以尋找最相符的項目以及可能遺漏的接近遺漏項目。
{:shortdesc}

**附註：**在 2016 年 9 月 14 日之前佈建且仍然作用中的任何 Compose 服務實例，仍然可以使用，而且可以在 [https://www.compose.com/](https://www.compose.com) 直接存取。在 Bluemix 帳戶內，可以直接存取及使用從此點往前佈建的任何 Compose 服務實例。

請完成下列步驟，以開始使用 {{site.data.keyword.composeForElasticsearch}}：

1. [建立 {{site.data.keyword.composeForElasticsearch}} 實例](https://console.ng.bluemix.net/catalog/services/compose-for-elasticsearch/)。

  當您建立服務的實例時，請確保要選擇服務名稱及認證名稱。請維持服務不連結；稍後使用佈建服務時所提供的認證，即可將應用程式連接至服務。*可用的認證* 小節中會列出各種認證值。

2. 連接至 {{site.data.keyword.composeForElasticsearch}} 服務。

  若要將應用程式連接至服務，請使用與服務一起建立的認證。範例應用程式會示範如何使用 Node.js 來連接至 {{site.data.keyword.composeForElasticsearch}} 服務。

  請下載 [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) 範例應用程式，並遵循 Readme 檔中的指示。然後，在 Bluemix 的應用程式詳細資料頁面中，按一下**檢視應用程式**來檢視 *examples* 索引的內容。

## 可用的認證

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
{: caption="Table 1. {{site.data.keyword.composeForElasticsearch}} credentials" caption-side="top"}

**附註：**兩個 `haproxy` 入口網站都可以存取 Elasticsearch 叢集。`uri` 及 `uri_direct_1` 都可以用來連接至叢集。在應用程式中，切換 `uri` 與 `uri_direct_1`，以管理連線失敗的回應。

# 相關鏈結
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose 文章](https://www.compose.com/articles/){:new_window}

## 指導教學及範例
{: #samples}
* [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs){:new_window}

## 相關鏈結
{: #general}
* [Compose 說明](https://help.compose.com/docs){:new_window}
