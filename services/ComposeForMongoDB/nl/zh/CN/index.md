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

# 开始使用 Compose for MongoDB
{: #getting-started-with-compose-for-mongodb}

{{site.data.keyword.composeForMongoDB_full}} 使用强大的建立索引和查询、聚集功能，以及 MongoDB 的广泛驱动程序支持，使其成为许多初创公司和企业的首选 JSON 数据存储库。{{site.data.keyword.composeForMongoDB}} 提供一种简单的自动扩展部署系统。它可在一个简洁明了的用户界面中，提供高可用性和冗余、自动和随需应变不停止备份、监视工具、与警报系统的集成、性能分析视图等一切功能。
{:shortdesc}

**注：**在 2016 年 9 月 14 日之前供应的任何仍处于活动状态的 Compose 服务实例仍可通过 [https://www.compose.com/](https://www.compose.com) 使用和直接访问。从此处供应的任何 Compose 服务实例都可在 Bluemix 帐户中直接访问和使用。

完成以下步骤，以开始使用 {{site.data.keyword.composeForMongoDB}}：

1. [创建 {{site.data.keyword.composeForMongoDB}} 实例](https://console.ng.bluemix.net/catalog/services/compose-for-mongodb/)。

   当您创建服务实例时，请确保选择服务的名称和凭证名称。保持服务处于未绑定状态；您可以稍后使用供应服务时提供的凭证，将应用程序连接到您的服务。*可用凭证*一节列出各种凭证值。

2. 连接到 {{site.data.keyword.composeForMongoDB}} 服务。

   要将应用程序连接到服务，请使用随服务一起创建的[凭证](./credentials.html)。样本应用程序会示范如何使用 Node.js 连接到 {{site.data.keyword.composeForMongoDB}} 服务。

   下载 [compose-mongodb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mongodb-helloworld-nodejs) 样本应用程序，并遵循自述文件中的指示信息。然后，在 Bluemix 中的应用程序详细信息页面中，单击**查看应用程序**。
