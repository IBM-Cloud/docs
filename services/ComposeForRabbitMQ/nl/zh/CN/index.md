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

# 开始使用 Compose for RabbitMQ
{: #getting-started-with-compose-for-rabbitmq}

RabbitMQ 可在应用程序和数据库之间异步处理消息，从而实现数据和应用层的分离。通过 RabbitMQ，开发者可以利用可定制的持久性级别、交付设置和已确认发布，递送、跟踪消息，并将消息移入队列。使用 {{site.data.keyword.composeForRabbitMQ_full}}，您可以获得易用管理界面的访问权，其中包括一系列管理功能，如部署监视、单击按钮扩展、用户设置和日志文件访问等。
{:shortdesc}

**注：**在 2016 年 9 月 14 日之前供应的任何仍处于活动状态的 Compose 服务实例仍可通过 [https://www.compose.com/](https://www.compose.com) 使用和直接访问。从此处供应的任何 Compose 服务实例都可在 Bluemix 帐户中直接访问和使用。

完成以下步骤，以开始使用 {{site.data.keyword.composeForRabbitMQ}}。

1. [创建 {{site.data.keyword.composeForRabbitMQ}} 实例](https://console.ng.bluemix.net/catalog/services/compose-for-rabbitmq/)。

  当您创建服务实例时，请确保选择服务的名称和凭证名称。保持服务处于未绑定状态；您可以稍后使用供应服务时提供的凭证，将应用程序连接到您的服务。*可用凭证*一节列出各种凭证值。

2. 连接到 {{site.data.keyword.composeForRabbitMQ}} 服务。

  要将应用程序连接到服务，请使用随服务一起创建的[凭证](./credentials.html)。样本应用程序会示范如何使用 Node.js 连接到 {{site.data.keyword.composeForRabbitMQ}} 服务。

  下载 [compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs) 样本应用程序，并遵循自述文件中的指示信息。然后，在 Bluemix 中的应用程序详细信息页面中，单击**查看应用程序**。
