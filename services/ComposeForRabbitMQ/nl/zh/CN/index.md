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

# 开始使用 {{site.data.keyword.composeForRabbitMQ}}
{: #getting-started-with-compose-for-rabbitmq}

RabbitMQ 可在应用程序和数据库之间异步处理消息，从而实现数据和应用层的分离。通过 RabbitMQ，开发者可以利用可定制的持久性级别、交付设置和已确认发布，递送、跟踪消息，并将消息移入队列。使用 {{site.data.keyword.composeForRabbitMQ_full}}，您可以获得易用管理界面的访问权，其中包括一系列管理功能，如部署监视、单击按钮扩展、用户设置和日志文件访问等。
{:shortdesc}

**注：**在 2016 年 9 月 14 日之前供应的任何仍处于活动状态的 Compose 服务实例仍可通过 [https://www.compose.com/](https://www.compose.com) 使用和直接访问。从此处供应的任何 Compose 服务实例都可在 Bluemix 帐户中直接访问和使用。

完成以下步骤，以开始使用 {{site.data.keyword.composeForRabbitMQ}}。

1. [创建 {{site.data.keyword.composeForRabbitMQ}} 实例](https://console.ng.bluemix.net/catalog/services/compose-for-rabbitmq/)。

  当您创建服务实例时，请确保选择服务的名称和凭证名称。保持服务处于未绑定状态；您可以稍后使用供应服务时提供的凭证，将应用程序连接到您的服务。*可用凭证*一节列出各种凭证值。

2. 连接到 {{site.data.keyword.composeForRabbitMQ}} 服务。

  要将应用程序连接到服务，请使用随服务一起创建的凭证。样本应用程序会示范如何使用 Node.js 连接到 {{site.data.keyword.composeForRabbitMQ}} 服务。

  下载 [compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs) 样本应用程序，并遵循自述文件中的指示信息。然后，在 Bluemix 中的应用程序详细信息页面中，单击**查看应用程序**。

## 可用凭证

字段名称|描述
----------|-----------
``uri``|连接到服务时要使用的 URI。包括模式 (`amqps:)、管理用户名和密码、服务器的主机名、要连接到的端口号和 vhost 名称。
`uri_direct_1`|连接到服务时可使用的替代 URI。格式与 `uri` 一样。
`uri_admin`|应该在浏览器中访问的 URI，用于访问数据库的管理界面。访问需要来自 `uri` 字段的管理用户名和密码。
`uri_admin_1`|替代管理 URI - 请参阅 `uri_admin`。
`uri_admin_2`|替代管理 URI - 请参阅 `uri_admin`。
`uri_admin_3`|替代管理 URI - 请参阅 `uri_admin`。
`uri_admin_4`|替代管理 URI - 请参阅 `uri_admin`。
`ca_certificate_base64`|自签名证书，用于确认应用程序连接到相应的服务器。这是 Base64 编码。您需要先解码密钥，才能对其进行使用，如样本应用程序中所示。
`deployment_id`|在 Compose 内创建的服务的内部标识。
`db_type`|服务所提供的数据库类型；在本例中为 `rabbitmq`。
`name`|数据库部署名称。

{: caption="Table 1. {{site.data.keyword.composeForRabbitMQ}} credentials" caption-side="top"}

# 相关链接
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose 文章](https://www.compose.com/articles/){:new_window}

## 样本和教程
{: #samples}
[compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs){:new_window}

## 相关链接
{: #general}
* [Compose 帮助](https://help.compose.com/docs){:new_window}
