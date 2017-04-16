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

# 開始使用 {{site.data.keyword.composeForEtcd}}
{: #getting-started-with-compose-for-etcd}

etcd 是鍵值儲存庫，保留協調及管理伺服器叢集進行分散式伺服器配置管理所需的一律正確資料。etcd 使用 RAFT 共識演算法，來確保叢集中的資料一致性。它會強制執行對資料執行作業的順序，讓叢集中的每個節點以相同的方式達到相同的結果。{{site.data.keyword.composeForEtcd_full}} 會新增 etcd 中所儲存配置資料的自動備份。直覺式管理介面可讓您輕鬆地監視、調整及管理部署。
{:shortdesc}

**附註：**在 2016 年 9 月 14 日之前佈建且仍然作用中的任何 Compose 服務實例，仍然可以使用，而且可以在 [https://www.compose.com/](https://www.compose.com) 直接存取。在 Bluemix 帳戶內，可以直接存取及使用從此點往前佈建的任何 Compose 服務實例。

請完成下列步驟，以開始使用 {{site.data.keyword.composeForEtcd}}。

1. [建立 {{site.data.keyword.composeForEtcd}} 實例](https://console.ng.bluemix.net/catalog/services/compose-for-etcd/)。

  當您建立服務的實例時，請確保要選擇服務名稱及認證名稱。請維持服務不連結；稍後使用佈建服務時所提供的認證，即可將應用程式連接至服務。*可用的認證* 小節中會列出各種認證值。

2. 連接至 {{site.data.keyword.composeForEtcd}} 服務。

若要將應用程式連接至服務，您可以使用與服務一起建立的認證。範例應用程式會示範如何使用 Node.js 來連接至 {{site.data.keyword.composeForEtcd}} 服務。

請下載 [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) 範例應用程式，並遵循 Readme 檔中的指示。然後，在 Bluemix 的應用程式詳細資料頁面中，按一下**檢視應用程式**來檢視 *examples* 的內容。

## 可用的認證

欄位名稱|說明
----------|-----------
`ca_certificate_base64`|用來確認應用程式將連接至適當伺服器的自簽憑證。憑證是 base64 編碼。您必須先解碼金鑰，才能使用金鑰（如範例應用程式中所示）。
`deployment_id`|Compose 內所建立之服務的內部 ID。
`db_type`|服務所提供的資料庫類型；在此情況下，為 `etcd`。
`name`|資料庫部署名稱。
`uri`|要在連接至服務時使用的 URI。`uri` 包括綱目 (`amqps:`)、管理使用者名稱和密碼、伺服器的主機名稱、要連接至的埠號，以及 vhost 名稱。

{: caption="Table 1. {{site.data.keyword.composeForEtcd}} credentials" caption-side="top"}

# 相關鏈結
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose 文章](https://www.compose.com/articles/){:new_window}

## 指導教學及範例
{: #samples}
* [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs){:new_window}

## 相關鏈結
{: #general}
* [Compose 說明](https://help.compose.com/docs){:new_window}
