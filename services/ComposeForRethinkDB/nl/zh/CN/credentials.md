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

要将应用程序连接到服务，请使用随服务一起创建的凭证。[compose-rethinkdb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rethinkdb-helloworld-nodejs) 样本应用程序会示范如何使用 Node.js 连接到使用凭证的 {{site.data.keyword.composeForRethinkDB}} 服务。

字段名称|描述
----------|-----------
`uri`|连接到服务时要使用的 URI。包括模式 (rethinkdb:)、管理用户名和密码、服务器的主机名和要连接到的端口号。
`uri_admin`|应该在浏览器中访问的 URI，用于访问数据库的管理界面。访问需要来自 `uri` 字段的管理用户名和密码。
`ca_certificate_base64`|自签名证书，用于确认应用程序连接到相应的服务器。这是 Base64 编码。您需要先解码密钥，才能对其进行使用，如样本应用程序中所示。
`deployment_id`|在 Compose 内创建的服务的内部标识。
`db_type`|服务所提供的数据库类型；在本例中为 `rethink`。
`name`|数据库部署名称。

{: caption="表 1. Compose for RethinkDB 凭证" caption-side="top"}
