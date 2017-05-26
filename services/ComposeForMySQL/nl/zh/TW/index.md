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

# 開始使用 Compose for MySQL
{: #getting-started-with-compose-for-mysql}

MySQL 具有廣泛的 ANSI SQL 99 子集和其自己的延伸集，包括 JSON 文件、全文檢索和可更新的視圖，並且提供豐富的選用區讓開發人員能在應用程式裡利用。管理者也可以找到廣泛的資料庫管理工具，可以搭配 MySQL 使用。{{site.data.keyword.composeForMySQL_full}} 讓 MySQL 延伸 MySQL 的功能，因為它能替您管理、提供容易、自動擴充的部署系統，此系統能提供高可用性與備援，也能提供自動化備份。
{:shortdesc}

**附註：**{{site.data.keyword.composeForMySQL_full}} 不會提供 Compose 使用者介面的存取權。如需詳細資料，請參閱 [Compose on Bluemix Support](https://help.compose.com/docs/bluemix-compose-support)。

請完成下列步驟，以開始使用 {{site.data.keyword.composeForMySQL}}：

1. [建立 {{site.data.keyword.composeForMySQL}} 實例](https://console.ng.bluemix.net/catalog/services/compose-for-mysql/)。

   當您建立服務的實例時，請選擇服務名稱及認證名稱。請維持服務不連結；稍後使用佈建服務時所提供的認證，即可將應用程式連接至服務。「可用的認證」小節中會列出各種認證值。

2. 連接至 {{site.data.keyword.composeForMySQL}} 服務。

  若要將應用程式連接至服務，請使用與服務一起建立的[認證](./credentials.html)。

  請下載 [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) 範例應用程式，並遵循 Readme 檔中的指示。然後，在 Bluemix 主控台的應用程式詳細資料頁面中，按一下**檢視應用程式**。

  範例應用程式會示範如何使用 Node.js 來連接至 {{site.data.keyword.composeForMySQL}} 服務。
