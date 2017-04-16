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

# 开始使用 Compose for MongoDB
{: #getting-started-with-compose-for-mongodb}

{{site.data.keyword.composeForMongoDB_full}} 使用强大的建立索引和查询、聚集功能，以及 MongoDB 的广泛驱动程序支持，使其成为许多初创公司和企业的首选 JSON 数据存储库。{{site.data.keyword.composeForMongoDB}} 提供一种简单的自动扩展部署系统。它可在一个简洁明了的用户界面中，提供高可用性和冗余、自动和随需应变不停止备份、监视工具、与警报系统的集成、性能分析视图等一切功能。
{:shortdesc}

**注：**在 2016 年 9 月 14 日之前供应的任何仍处于活动状态的 Compose 服务实例仍可通过 [https://www.compose.com/](https://www.compose.com) 使用和直接访问。从此处供应的任何 Compose 服务实例都可在 Bluemix 帐户中直接访问和使用。

完成以下步骤，以开始使用 {{site.data.keyword.composeForMongoDB}}：

1. [创建 {{site.data.keyword.composeForMongoDB}} 实例](https://console.ng.bluemix.net/catalog/services/compose-for-mongodb/)。

   当您创建服务实例时，请确保选择服务的名称和凭证名称。保持服务处于未绑定状态；您可以稍后使用供应服务时提供的凭证，将应用程序连接到您的服务。*可用凭证*一节列出各种凭证值。

2. 连接到 {{site.data.keyword.composeForMongoDB}} 服务。

   要将应用程序连接到服务，请使用随服务一起创建的凭证。样本应用程序会示范如何使用 Node.js 连接到 {{site.data.keyword.composeForMongoDB}} 服务。

   下载 [compose-mongodb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mongodb-helloworld-nodejs) 样本应用程序，并遵循自述文件中的指示信息。然后，在 Bluemix 中的应用程序详细信息页面中，单击**查看应用程序**。


## 可用凭证

字段名称|描述
----------|-----------
`uri`|连接到服务时要使用的 URI。`uri` 包括模式 (`mongodb:`)、管理用户名和密码、服务器的主机名、要连接到的端口号、数据库名称和用于启用 SSL 连接的 `?ssl=true`。
`uri_cli`|连接到数据库实例的 `mongo` shell 命令行。
`ca_certificate_base64`|自签名证书，用于确认应用程序连接到相应的服务器。证书是 Base64 编码。您必须先解码密钥，才能对其进行使用，如样本应用程序中所示。
`deployment_id`|在 Compose 内创建的服务的内部标识。
`db_type`|服务所提供的数据库类型：在本例中为 `mongodb`。
`name`|数据库部署名称。

{: caption="Table 1. {{site.data.keyword.composeForMongoDB}} credentials" caption-side="top"}

# 相关链接
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose 文章](https://www.compose.com/articles/){:new_window}

## 样本和教程
{: #samples}
* [compose-mongodb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mongodb-helloworld-nodejs){:new_window}

## 相关链接
{: #general}
* [Compose 帮助](https://help.compose.com/docs){:new_window}
