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

# 开始使用 Compose for Elasticsearch
{: #getting-started-with-compose-for-elasticsearch}

{{site.data.keyword.composeForElasticsearch_full}} 将全文搜索引擎的强大功能和 JSON 文档数据库的建立索引优势结合在一起。如此一来，创建出强大的工具，可对大量数据执行富数据分析。使用 Elasticsearch，可对您搜索的正确性进行评分，让您深度挖掘您的数据集，以获得那些您可能遗漏的近似匹配项和接近遗漏项。
{:shortdesc}

**注：**在 2016 年 9 月 14 日之前供应的任何仍处于活动状态的 Compose 服务实例仍可通过 [https://www.compose.com/](https://www.compose.com) 使用和直接访问。从此处供应的任何 Compose 服务实例都可在 Bluemix 帐户中直接访问和使用。

完成以下步骤，以开始使用 {{site.data.keyword.composeForElasticsearch}}：

1. [创建 {{site.data.keyword.composeForElasticsearch}} 实例](https://console.ng.bluemix.net/catalog/services/compose-for-elasticsearch/)。

  当您创建服务实例时，请确保选择服务的名称和凭证名称。保持服务处于未绑定状态；您可以稍后使用供应服务时提供的凭证，将应用程序连接到您的服务。*可用凭证*一节列出各种凭证值。

2. 连接到 {{site.data.keyword.composeForElasticsearch}} 服务。

  要将应用程序连接到服务，请使用随服务一起创建的凭证。样本应用程序会示范如何使用 Node.js 连接到 {{site.data.keyword.composeForElasticsearch}} 服务。

  下载 [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) 样本应用程序，并遵循自述文件中的指示信息。然后，在 Bluemix 中的应用程序详细信息页面中，单击**查看应用程序**，以查看*示例*索引的内容。

## 可用凭证

字段名称|描述
----------|-----------
`uri`|连接到服务时要使用的 URI。包括模式 (`https:`)、管理用户名和密码、服务器的主机名和要连接到的端口号。
`uri_direct_1`|连接到服务时可使用的替代 URI。格式与 `uri` 一样。
`uri_health`|`curl` 命令，用于向第一个 haproxy 请求集群运行状况。
`uri_health_1`|`curl` 命令，用于向第二个 haproxy 请求集群运行状况。
`ca_certificate_base64`|自签名证书，用于确认应用程序连接到相应的服务器。这是 Base64 编码。您需要先解码密钥，才能对其进行使用，如样本应用程序中所示。
`deployment_id`|在 Compose 内创建的服务的内部标识。
`db_type`|服务所提供的数据库类型；在本例中为 `elastic_search`。
`name`|数据库部署名称。

{: caption="Table 1. {{site.data.keyword.composeForElasticsearch}} credentials" caption-side="top"}

**注：**两个 `haproxy` 门户网站提供对 Elasticsearch 集群的访问权。`uri` 和 `uri_direct_1` 都可用于连接到集群。在您的应用程序中，在 `uri` 和 `uri_direct_1` 之间进行切换，以管理对连接失败的响应。

# 相关链接
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose 文章](https://www.compose.com/articles/){:new_window}

## 样本和教程
{: #samples}
* [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs){:new_window}

## 相关链接
{: #general}
* [Compose 帮助](https://help.compose.com/docs){:new_window}
