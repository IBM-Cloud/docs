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

# 开始使用 Compose for Redis
{: #getting-started-with-compose-for-redis}

Redis 是一个开放式源代码内存中键值存储库。Redis 中的值可以是简单的字符串、散列、列表和集合或强大的位图、hyperloglogs 和地理空间索引。Redis 非常适合作为应用程序高速缓存或快速响应数据存储库。{{site.data.keyword.composeForRedis_full}} 为您提供预调整的配置，以获得高可用性和磁盘上持久性，所有项目都由额外的安全功能锁定。
{:shortdesc}

**注：**在 2016 年 9 月 14 日之前供应的任何仍处于活动状态的 Compose 服务实例仍可通过 [https://www.compose.com/](https://www.compose.com) 使用和直接访问。从此处供应的任何 Compose 服务实例都可在 Bluemix 帐户中直接访问和使用。

完成以下步骤，以开始使用 {{site.data.keyword.composeForRedis}}。

1. [创建 {{site.data.keyword.composeForRedis}} 实例](https://console.ng.bluemix.net/catalog/services/compose-for-redis/)。

  当您创建服务实例时，请确保选择服务的名称和凭证名称。保持服务处于未绑定状态；您可以稍后使用供应服务时提供的凭证，将应用程序连接到您的服务。*可用凭证*一节列出各种凭证值。

2. 连接到 {{site.data.keyword.composeForRedis}} 服务。

  要将应用程序连接到服务，请使用随服务一起创建的[凭证](./credentials.html)。样本应用程序会示范如何使用 Node.js 连接到 {{site.data.keyword.composeForRedis}} 服务。

  下载 [compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs) 样本应用程序，并遵循自述文件中的指示信息。然后，在 Bluemix 中的应用程序详细信息页面中，单击**查看应用程序**。
