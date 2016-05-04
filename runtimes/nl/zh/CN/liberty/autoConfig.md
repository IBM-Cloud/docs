---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 自动配置绑定服务
{: #auto_config}

*上次更新时间：2016 年 3 月 31 日*

您可以将各种服务绑定到 Liberty 应用程序。可以是容器管理服务和/或应用程序管理服务，具体取决于开发者的需要。

应用程序管理的服务是完全由应用程序管理而无需 Liberty 任何协助的服务。应用程序通常会读取 VCAP_SERVICES 来获取有关绑定服务的信息，并会直接访问服务。应用程序提供所有必要的客户机访问代码。完全不依赖于 Liberty 功能或 server.xml 文件配置。Liberty buildpack 自动配置不会应用于此类型的服务。

容器管理的服务是由 Liberty 运行时管理的服务。在一些情况下，应用程序可能会在 JNDI 中查找绑定服务，而在另一些情况下，服务由 Liberty 本身直接使用。Liberty buildpack 会读取 VCAP_SERVICES 来获取有关绑定服务的信息。对于每个容器管理的服务，该 buildpack 会执行三个功能。

* 为绑定服务生成[云变量](optionsForPushing.html#accessing_info_of_bound_services)。
* 安装 Liberty 功能和访问绑定服务所需的客户机访问代码。
* 生成或更新服务所需的 server.xml 文件节。

此过程称为自动配置。Liberty buildpack 提供以下服务类型的自动配置：

* [SQL Database](../../services/SQLDB/index.html#SQLDB)
* ClearDB MySQL Database
* [MySQL](../../services/MySQL/index.html#MySQL)
* ElephantSQL
* [PostgreSQL](../../services/PostgreSQL/index.html#PostgreSQL)
* [Cloudant NoSQL Database](../../services/Cloudant/index.html#Cloudant)
* MongoLab
* [dashDB](../../services/dashDB/index.html#dashDB)
* [Data Cache](../../services/DataCache/index.html#data_cache)
* [Session Cache](../../services/SessionCache/index.html#session_cache)
* [MQ Light](../../services/MQLight/index.html#mqlight010)
* [Monitoring and Analytics](../..//services/monana/index.html#gettingstartedtemplate)
* [Auto-Scaling](../../services/Auto-Scaling/index.html#autoscaling)
* [Single Sign On](../../services/SingleSignOn/index.html#sso_gettingstarted)
* [New Relic](newRelic.html)
* [Dynatrace](dynatrace.html)

如上所述，某些服务既可以是应用程序管理的服务，也可以是容器管理的服务。例如，Mongo 和 SQLDB 就是此类服务。缺省情况下，Liberty buildpack 假定这些服务是容器管理的服务，并自动对其进行配置。如果希望应用程序来管理服务，那么可以通过设置 services_autoconfig_excludes 环境变量选择退出服务自动配置。有关更多信息，请参阅[选择退出服务自动配置](autoConfig.html#opting_out)。

## 安装 Liberty 功能和客户机访问代码
{: #installation_of_liberty_features}

绑定到容器管理的服务时，服务可能需要在 server.xml 文件的 featureManager 节中配置 Liberty 功能。Liberty buildpack 会更新 featureManager 节，并安装所需的支持二进制文件。如果服务需要客户机驱动程序 jar，那么会将 jar 下载到 Liberty 安装中熟知的位置。

请参阅绑定服务类型的文档，以获取更多详细信息。

## 生成或更新 server.xml 配置节
{: #generating_or_updating_serverxml}

向 Bluemix 推送独立应用程序时，Liberty buildpack 会生成 server.xml 节，如[用于推送 Liberty 应用程序的选项](optionsForPushing.html#options_for_pushing)中所述。推送独立应用程序并绑定到容器管理的服务时，Liberty buildpack 会为绑定服务生成必要的 server.xml 节。

提供 server.xml 文件并绑定到容器管理的服务时，Liberty buildpack 将执行以下操作：

* 如果提供的 server.xml 文件不包含针对绑定服务的配置节，那么将为绑定服务生成配置。
* 如果提供的 server.xml 文件包含针对绑定服务的配置节，那么将更新绑定服务的配置。

请参阅绑定服务类型的文档，以获取更多详细信息。

## 选择退出服务自动配置
{: #opting_out}

在某些情况下，您可能不希望 Liberty buildpack 自动配置已绑定的服务。请考虑以下场景。

* 应用程序使用的是 MongoDB，但希望应用程序直接管理数据库的连接。应用程序中包含必要的客户机驱动程序 jar。我不希望 Liberty buildpack 自动配置 Mongo 服务。
* 我将提供 server.xml 文件，我已为 SQLDB 实例提供配置节，因为我需要非标准数据源配置。我不希望 Liberty buildpack 更新 server.xml 文件，但仍需要 Liberty buildpack 确保安装相应的支持软件。

要选择退出自动服务配置，请使用 services_autoconfig_excludes 环境变量。可以将此环境变量包含在 manifest.yml 中，或者使用 cf 客户机对其进行设置。

可以按每种服务类型来选择退出自动配置服务。您可以选择完全退出（如在 Mongo 场景中），也可以仅选择退出 server.xml 文件配置更新（如在 SQLDB 场景中）。为 services_autoconfig_excludes 环境变量指定的值是字符串，如下所示。

* 字符串可以包含一个或多个服务的选择退出规范。
* 特定服务的选择退出规范是 service_type=option，其中：
  * service_type 是服务的标签，如 VCAP_SERVICES 中显示。
  * option 是 all 或 config。
* 如果字符串包含多个服务的选择退出规范，那么必须使用单个空格字符分隔各个选择退出规范。

更正式地说，字符串的语法如下所示。

```
    Opt_out_string :: <service_type_specification[<delimiter>service_type_specification]*
    <service_type_specification> :: <service_type>=<option>
    <service_type> :: service type (service label as it appears in VCAP_SERVICES)
    <option> :: all | config
    <delimiter> :: one white space character
```
{: #codeblock}

**重要信息**：您指定的服务类型必须与 VCAP_SERVICES 环境变量中所示的服务标签相匹配。不允许使用空格。**重要信息**：&lt;service_type_specification> 中不允许使用空格。空格只允许用于分隔多个 &lt;service_type_specification> 实例。

使用“all”选项可选择退出服务的所有自动配置操作，如上面的 Mongo 场景。使用“config”选项可仅选择退出配置更新操作，如上面的 SQLDB 场景。

下面是 manifest.yml 文件中针对 Mongo 和 SQLDB 场景的样本选择退出规范。

```
    env:
      services_autoconfig_excludes: mongodb-2.2=all

    env:
      services_autoconfig_excludes: sqldb=config

    env:
      services_autoconfig_excludes: sqldb=config mongodb-2.2=all
```
{: #codeblock}

下面是如何使用命令行界面为应用程序 myapp 设置 services_autoconfig_excludes 环境变量的示例。

```
    $ cf set-env myapp services_autoconfig_excludes sqldb=config
    $ cf set-env myapp services_autoconfig_excludes "sqldb=config mongodb-2.2=all"
```
{: #codeblock}

# 相关链接
## 常规
* [Liberty 运行时](index.html)
* [Liberty 概要文件概述](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
