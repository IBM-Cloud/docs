---

copyright:
  years: 2016,2017
lastupdated: "2017-04-027"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 開始使用 Compose for RabbitMQ
{: #getting-started-with-compose-for-rabbitmq}

RabbitMQ 會非同步處理應用程式與資料庫之間的訊息，以分隔資料及應用程式層。RabbitMQ 可讓開發人員遞送及追蹤具有可自訂持續性層次、遞送設定及已確認發佈的訊息，並且將其置入佇列。透過使用 {{site.data.keyword.composeForRabbitMQ_full}}，您可以存取具有一組管理特性（例如部署監視、按一下按鈕擴充、使用者設定及日誌檔存取）的簡易管理介面。
{:shortdesc}

**附註：**在 2016 年 9 月 14 日之前佈建且仍然作用中的任何 Compose 服務實例，仍然可以使用，而且可以在 [https://www.compose.com/](https://www.compose.com) 直接存取。在 Bluemix 帳戶內，可以直接存取及使用從此點往前佈建的任何 Compose 服務實例。

請完成下列步驟，以開始使用 {{site.data.keyword.composeForRabbitMQ}}。

1. [建立 {{site.data.keyword.composeForRabbitMQ}} 實例](https://console.ng.bluemix.net/catalog/services/compose-for-rabbitmq/)。

  當您建立服務的實例時，請確保要選擇服務名稱及認證名稱。請維持服務不連結；稍後使用佈建服務時所提供的認證，即可將應用程式連接至服務。*可用的認證* 小節中會列出各種認證值。

2. 連接至 {{site.data.keyword.composeForRabbitMQ}} 服務。

  若要將應用程式連接至服務，請使用與服務一起建立的[認證](./credentials.html)。範例應用程式會示範如何使用 Node.js 來連接至 {{site.data.keyword.composeForRabbitMQ}} 服務。

  請下載 [compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs) 範例應用程式，並遵循 Readme 檔中的指示。然後，在 Bluemix 的應用程式詳細資料頁面中，按一下**檢視應用程式**。
