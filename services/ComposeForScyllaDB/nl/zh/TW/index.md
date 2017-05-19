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

# 開始使用 Compose for ScyllaDB
{: #getting-started-with-compose-for-scylladb}

ScyllaDB 是 Cassandra 寬直欄分散式資料庫的就地取代。ScyllaDB 以 C++ 撰寫，而不是 Cassandra 的 Java，它能夠更充份利用資源，在基準性能測試時可達到 10 倍的效能。除了維持與 Cassandra 工具及資料檔案的相容性以外，ScyllaDB 也新增了自行調整的功能。{{site.data.keyword.composeForScyllaDB_full}} 延伸了 ScyllaDB 的功能，因為它能替您管理、提供容易、自動擴充的部署系統，此系統能提供高可用性與備援，也能提供自動化備份。
{:shortdesc}

**附註：**{{site.data.keyword.composeForScyllaDB_full}} 不會提供 Compose 使用者介面的存取權。如需詳細資料，請參閱 [Compose on Bluemix Support](https://help.compose.com/docs/bluemix-compose-support)。

請完成下列步驟，以開始使用 {{site.data.keyword.composeForScyllaDB}}：

1. [建立 {{site.data.keyword.composeForScyllaDB}} 實例](https://console.ng.bluemix.net/catalog/services/compose-for-scylladb/)。

   當您建立服務的實例時，請選擇服務名稱及認證名稱。請維持服務不連結；稍後使用佈建服務時所提供的認證，即可將應用程式連接至服務。「可用的認證」小節中會列出各種認證值。

2. 連接至 {{site.data.keyword.composeForScyllaDB}} 服務。

   若要將應用程式連接至服務，請使用與服務一起建立的[認證](./credentials.html)。

   請下載 [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) 範例應用程式，並遵循 Readme 檔中的指示。然後，在 Bluemix 主控台的應用程式詳細資料頁面中，按一下**檢視應用程式**。

   範例應用程式會示範如何使用 Node.js 來連接至 {{site.data.keyword.composeForScyllaDB}} 服務。
