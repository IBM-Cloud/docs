---

copyright:
  years: 2016
lastupdated: "2016-12-09"
---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be --- surrounded by 3 dashes ---
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 开始使用 {{site.data.keyword.composeForPostgreSQL}}
{: #getting-started-with-compose-for-postgreSQL}

{{site.data.keyword.composeForPostgreSQL}} 提供高度可定制的强大开放式源代码对象关系数据库。使用 Postgres，开发快速且易于扩展。您可以使用您熟悉的语言进行开发，如 C/C++、Perl、Python、TCL/TK、Delphi/Kylix、VB、PHP、ASP 和 Java。您将获得功能丰富的企业数据库，其支持 JSON，为您提供最佳的 SQL 和 NoSQL 世界。
{:shortdesc}

**注：**在 2016 年 9 月 14 日之前供应的任何仍处于活动状态的 Compose 服务实例仍可通过 [https://www.compose.com/](https://www.compose.com) 使用和直接访问。从此处供应的任何 Compose 服务实例都可在 Bluemix 帐户中直接访问和使用。

完成以下步骤，以开始使用 Compose for PostgreSQL：

1. [创建 {{site.data.keyword.composeForPostgreSQL}} 实例](https://console.ng.bluemix.net/catalog/services/compose-for-postgresql/)。

  当您创建服务实例时，请确保选择服务的名称和凭证名称。保持服务处于未绑定状态；您可以稍后使用供应服务时提供的凭证，将应用程序连接到您的服务。*可用凭证*一节列出各种凭证值。

2. 连接到 {{site.data.keyword.composeForPostgreSQL}} 服务。

  要将应用程序连接到服务，请使用随服务一起创建的凭证。样本应用程序会示范如何使用 Node.js 连接到 {{site.data.keyword.composeForPostgreSQL}} 服务。

  下载 [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs) 样本应用程序，并遵循自述文件中的指示信息。然后，在 Bluemix 中的应用程序详细信息页面中，单击**查看应用程序**，以查看*示例*表的内容。

## 可用凭证

字段名称|描述
----------|-----------
`uri`|连接到服务时要使用的 URI。包括模式 (`postgres:`)、管理用户名和密码、服务器的主机名、要连接到的端口号、数据库名称和用于启用 SSL 连接的“?ssl=true”。
`uri_cli`|连接到数据库实例的 `psql` shell 命令行。
`ca_certificate_base64`|自签名证书，用于确认应用程序连接到相应的服务器。这是 Base64 编码。您需要先解码密钥，才能对其进行使用，如样本应用程序中所示。
`deployment_id`|在 Compose 内创建的服务的内部标识。
`db_type`|服务所提供的数据库类型；在本例中为 `postgresql`。
`name`|数据库部署名称。

{: caption="Table 1. {{site.data.keyword.composeForPostgreSQL}} credentials" caption-side="top"}

# 相关链接
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose 文章](https://www.compose.com/articles/){:new_window}

## 样本和教程
{: #samples}
* [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs){:new_window}

## 相关链接
{: #general}
* [Compose 帮助](https://help.compose.com/docs){:new_window}
