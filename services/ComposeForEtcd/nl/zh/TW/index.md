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

# 開始使用 Compose for etcd
{: #getting-started-with-compose-for-etcd}

etcd 是鍵值儲存庫，保留協調及管理伺服器叢集進行分散式伺服器配置管理所需的一律正確資料。etcd 使用 RAFT 共識演算法，來確保叢集中的資料一致性。它會強制執行對資料執行作業的順序，讓叢集中的每個節點以相同的方式達到相同的結果。{{site.data.keyword.composeForEtcd_full}} 會新增 etcd 中所儲存配置資料的自動備份。直覺式管理介面可讓您輕鬆地監視、調整及管理部署。
{:shortdesc}

**附註：**在 2016 年 9 月 14 日之前佈建且仍然作用中的任何 Compose 服務實例，仍然可以使用，而且可以在 [https://www.compose.com/](https://www.compose.com) 直接存取。在 Bluemix 帳戶內，可以直接存取及使用從此點往前佈建的任何 Compose 服務實例。

請完成下列步驟，以開始使用 {{site.data.keyword.composeForEtcd}}。

1. [建立 {{site.data.keyword.composeForEtcd}} 實例](https://console.ng.bluemix.net/catalog/services/compose-for-etcd/)。

  當您建立服務的實例時，請確保要選擇服務名稱及認證名稱。請維持服務不連結；稍後使用佈建服務時所提供的認證，即可將應用程式連接至服務。*可用的認證* 小節中會列出各種認證值。

2. 連接至 {{site.data.keyword.composeForEtcd}} 服務。

若要將應用程式連接至服務，請使用與服務一起建立的[認證](./credentials.html)。範例應用程式會示範如何使用 Node.js 來連接至 {{site.data.keyword.composeForEtcd}} 服務。

請下載 [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) 範例應用程式，並遵循 Readme 檔中的指示。然後，在 Bluemix 的應用程式詳細資料頁面中，按一下**檢視應用程式**來檢視 *examples* 的內容。
