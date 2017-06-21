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

# 开始使用 Compose for Elasticsearch
{: #getting-started-with-compose-for-elasticsearch}

{{site.data.keyword.composeForElasticsearch_full}} 将全文搜索引擎的强大功能和 JSON 文档数据库的建立索引优势结合在一起。如此一来，创建出强大的工具，可对大量数据执行富数据分析。使用 Elasticsearch，可对您搜索的正确性进行评分，让您深度挖掘您的数据集，以获得那些您可能遗漏的近似匹配项和接近遗漏项。
{:shortdesc}

**注：**在 2016 年 9 月 14 日之前供应的任何仍处于活动状态的 Compose 服务实例仍可通过 [https://www.compose.com/](https://www.compose.com) 使用和直接访问。从此处供应的任何 Compose 服务实例都可在 Bluemix 帐户中直接访问和使用。

完成以下步骤，以开始使用 {{site.data.keyword.composeForElasticsearch}}：

1. [创建 {{site.data.keyword.composeForElasticsearch}} 实例](https://console.ng.bluemix.net/catalog/services/compose-for-elasticsearch/)。

  当您创建服务实例时，请确保选择服务的名称和凭证名称。保持服务处于未绑定状态；您可以稍后使用供应服务时提供的凭证，将应用程序连接到您的服务。*可用凭证*一节列出各种凭证值。

2. 连接到 {{site.data.keyword.composeForElasticsearch}} 服务。

  要将应用程序连接到服务，请使用随服务一起创建的[凭证](./credentials.html)。样本应用程序会示范如何使用 Node.js 连接到 {{site.data.keyword.composeForElasticsearch}} 服务。

  下载 [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) 样本应用程序，并遵循自述文件中的指示信息。然后，在 Bluemix 中的应用程序详细信息页面中，单击**查看应用程序**，以查看*示例*索引的内容。
