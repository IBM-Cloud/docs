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

# 可用凭证
{: #available-credentials}

要将应用程序连接到服务，请使用随服务一起创建的凭证。[compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) 样本应用程序会示范如何使用 Node.js 连接到使用凭证的 {{site.data.keyword.composeForScyllaDB}} 服务。

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
{: caption="表 1. Compose for ScyllaDB 凭证" caption-side="top"}
