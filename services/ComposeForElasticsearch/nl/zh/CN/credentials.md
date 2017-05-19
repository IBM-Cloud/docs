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

要将应用程序连接到服务，请使用随服务一起创建的凭证。[compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) 样本应用程序会示范如何使用 Node.js 连接到使用凭证的 {{site.data.keyword.composeForElasticsearch}} 服务。

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

{: caption="表 1. Compose for Elasticsearch 凭证" caption-side="top"}

**注：**两个 `haproxy` 门户网站提供对 Elasticsearch 集群的访问权。`uri` 和 `uri_direct_1` 都可用于连接到集群。在您的应用程序中，在 `uri` 和 `uri_direct_1` 之间进行切换，以管理对连接失败的响应。
