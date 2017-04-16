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

# 开始使用 Compose for ScyllaDB
{: #getting-started-with-compose-for-scylladb}

ScyllaDB 是 Cassandra 宽列分布式数据库的内部替代产品。ScyllaDB 是用 C++ 而不是 Cassandra 的 Java 编写的，目的是更好地利用资源，使基准性能提高到原先的 10 倍。除了保留与 Cassandra 工具和数据文件的兼容性外，ScyllaDB 还添加了自调整功能。通过 {{site.data.keyword.composeForScyllaDB_full}}，ScyllaDB 的功能得到扩展，不仅可以为您管理 ScyllaDB ，还提供了易于使用、自动扩展的部署系统，能交付高可用性、冗余性和自动备份功能。
{:shortdesc}

**注：**{{site.data.keyword.composeForScyllaDB_full}} 不会授予对 Compose UI 的访问权。请参阅[在 Bluemix 上对 Compose 的支持](https://help.compose.com/docs/bluemix-compose-support)，以获取更多详细信息。

完成以下步骤，以开始使用 {{site.data.keyword.composeForScyllaDB}}：

1. [创建 {{site.data.keyword.composeForScyllaDB}} 实例](https://console.ng.bluemix.net/catalog/services/compose-for-scylladb/)。

   当您创建服务实例时，请选择服务的名称和凭证名称。保持服务处于未绑定状态；您可以稍后使用供应服务时提供的凭证，将应用程序连接到您的服务。“可用凭证”一节列出了各种凭证值。

2. 连接到 {{site.data.keyword.composeForScyllaDB}} 服务。

   要将应用程序连接到服务，请使用随服务一起创建的凭证。

   下载 [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) 样本应用程序，并遵循自述文件中的指示信息。然后，在 Bluemix 控制台中的应用程序详细信息页面中，单击**查看应用程序**。

   样本应用程序会示范如何使用 Node.js 连接到 {{site.data.keyword.composeForScyllaDB}} 服务。


## 可用凭证

字段名称|描述
----------|-----------
`db_type`|服务所提供的数据库类型；在本例中为 `scylla`。
`uri_cli_1`|连接到数据库实例的替代 `cqlsh` shell 命令行。
`maps`|ScyllaDB 连接映射，提供各种驱动程序将内部 IP 地址与 ScyllaDB 数据库的外部 DNS 名称相关联所需的信息。
`name`|数据库部署名称。

`uri_cli`|连接到数据库实例的 `cqlsh` shell 命令行。
`uri_direct_2`|可用于连接到服务的替代 URI。格式与 `uri` 一样。
`uri_direct_1`|可用于连接到服务的替代 URI。格式与 `uri` 一样。
`ca_certificate_base64`|自签名证书，用于确认应用程序连接到相应的服务器。此证书是 Base64 编码。
`deployment_id`|在 Compose 内创建的服务的内部标识。
`uri_cli_2`|连接到数据库实例的替代 `cqlsh` shell 命令行。
`uri`|连接到服务时使用的 URI，包括模式 (`scylla:`)、密码、服务器的主机名、要连接到的端口号和数据库名称。
{: caption="Table 1. {{site.data.keyword.composeForScyllaDB}} credentials" caption-side="top"}


# 相关链接
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose 文章](https://www.compose.com/articles/){:new_window}

## 样本和教程
{: #samples}
* [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs){:new_window}

## 相关链接
{: #general}
* [Compose 帮助](https://help.compose.com/docs){:new_window}
