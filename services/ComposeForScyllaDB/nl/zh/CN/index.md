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

# 开始使用 Compose for ScyllaDB
{: #getting-started-with-compose-for-scylladb}

ScyllaDB 是 Cassandra 宽列分布式数据库的内部替代产品。ScyllaDB 是用 C++ 而不是 Cassandra 的 Java 编写的，目的是更好地利用资源，使基准性能提高到原先的 10 倍。除了保留与 Cassandra 工具和数据文件的兼容性外，ScyllaDB 还添加了自调整功能。通过 {{site.data.keyword.composeForScyllaDB_full}}，ScyllaDB 的功能得到扩展，不仅可以为您管理 ScyllaDB ，还提供了易于使用、自动扩展的部署系统，能交付高可用性、冗余性和自动备份功能。
{:shortdesc}

**注：**{{site.data.keyword.composeForScyllaDB_full}} 不会授予对 Compose UI 的访问权。请参阅[在 Bluemix 上对 Compose 的支持](https://help.compose.com/docs/bluemix-compose-support)，以获取更多详细信息。

完成以下步骤，以开始使用 {{site.data.keyword.composeForScyllaDB}}：

1. [创建 {{site.data.keyword.composeForScyllaDB}} 实例](https://console.ng.bluemix.net/catalog/services/compose-for-scylladb/)。

   当您创建服务实例时，请选择服务的名称和凭证名称。保持服务处于未绑定状态；您可以稍后使用供应服务时提供的凭证，将应用程序连接到您的服务。“可用凭证”一节列出了各种凭证值。

2. 连接到 {{site.data.keyword.composeForScyllaDB}} 服务。

   要将应用程序连接到服务，请使用随服务一起创建的[凭证](./credentials.html)。

   下载 [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) 样本应用程序，并遵循自述文件中的指示信息。然后，在 Bluemix 控制台中的应用程序详细信息页面中，单击**查看应用程序**。

   样本应用程序会示范如何使用 Node.js 连接到 {{site.data.keyword.composeForScyllaDB}} 服务。
