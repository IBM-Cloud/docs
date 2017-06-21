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

# 开始使用 Compose for MySQL
{: #getting-started-with-compose-for-mysql}

借助大量 ANSI SQL 99 子集及其自己的广泛扩展集，包括 JSON 文档、全文搜索和可更新视图，MySQL 为开发者提供了内容丰富的选用板，供其在自己的应用程序中使用。此外，还为管理员提供了诸多数据库管理工具，可选择用于处理 MySQL。通过 {{site.data.keyword.composeForMySQL_full}}，MySQL 的功能得到扩展，不仅可以为您管理 MySQL，还提供了易于使用、自动扩展的部署系统，能交付高可用性、冗余性和自动备份功能。
{:shortdesc}

**注：**{{site.data.keyword.composeForMySQL_full}} 不会授予对 Compose UI 的访问权。请参阅[在 Bluemix 上对 Compose 的支持](https://help.compose.com/docs/bluemix-compose-support)，以获取更多详细信息。

完成以下步骤，以开始使用 {{site.data.keyword.composeForMySQL}}：

1. [创建 {{site.data.keyword.composeForMySQL}} 实例](https://console.ng.bluemix.net/catalog/services/compose-for-mysql/)。

   当您创建服务实例时，请选择服务的名称和凭证名称。保持服务处于未绑定状态；您可以稍后使用供应服务时提供的凭证，将应用程序连接到您的服务。“可用凭证”一节列出了各种凭证值。

2. 连接到 {{site.data.keyword.composeForMySQL}} 服务。

  要将应用程序连接到服务，请使用随服务一起创建的[凭证](./credentials.html)。

  下载 [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) 样本应用程序，并遵循自述文件中的指示信息。然后，在 Bluemix 控制台中的应用程序详细信息页面中，单击**查看应用程序**。

  样本应用程序会示范如何使用 Node.js 连接到 {{site.data.keyword.composeForMySQL}} 服务。
