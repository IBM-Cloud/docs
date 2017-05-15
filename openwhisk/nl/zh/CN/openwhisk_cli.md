---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-25"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} CLI

{{site.data.keyword.openwhisk_short}} 提供了功能强大的命令行界面，支持对系统的所有方面进行全面管理。

## 设置 {{site.data.keyword.openwhisk_short}} CLI 

可以使用 {{site.data.keyword.openwhisk_short}} 命令行界面 (CLI) 来设置名称空间和授权密钥。转至[配置 CLI](https://console.{DomainName}/openwhisk/cli)，然后遵循指示信息来进行安装。

要使用 CLI，应配置两个必需属性：

1. 要使用的 {{site.data.keyword.openwhisk_short}} 部署的 **API 主机**（名称或 IP 地址）。
2. **授权密钥**（用户名和密码），用于授予您对 {{site.data.keyword.openwhisk_short}} API 的访问权。

运行以下命令来设置 API 主机：

```
wsk property set --apihost openwhisk.ng.bluemix.net
```
{: pre} 

如果您知道您的授权密钥，那么可以配置 CLI 来予以使用。 

运行以下命令来设置授权密钥：

```
wsk property set --auth <authorization_key>
```
{: pre}

**提示：**缺省情况下，OpenWhisk CLI 将属性集存储在 `~/.wskprops` 中。此文件的位置可以通过设置 `WSK_CONFIG_FILE` 环境变量进行变更。 

要验证 CLI 设置，请尝试[创建并运行操作](./index.html#openwhisk_start_hello_world)。

## 使用 {{site.data.keyword.openwhisk_short}} CLI

配置好环境后，就可以开始使用 {{site.data.keyword.openwhisk_short}} CLI 来执行以下操作：

* 在 {{site.data.keyword.openwhisk_short}} 上运行代码片段或操作。请参阅[创建和调用操作](./openwhisk_actions.html)。
* 使用触发器和规则以支持操作对事件进行响应。请参阅[创建触发器和规则](./openwhisk_triggers_rules.html)。
* 了解包如何捆绑操作以及配置外部事件源。请参阅[使用和创建包](./openwhisk_packages.html)。
* 浏览包的目录，并通过外部服务（例如，[Cloudant 事件源](./openwhisk_cloudant.html)）来增强应用程序的功能。请参阅[使用启用了 OpenWhisk 的服务](./openwhisk_catalog.html)。

## 配置 CLI 以使用 HTTPS 代理

CLI 可以设置为使用 HTTPS 代理。要设置 HTTPS 代理，必须创建名为 `HTTPS_PROXY` 的环境变量。该变量必须设置为 HTTPS 代理的地址，并且其端口使用以下格式：`{PROXY IP}:{PROXY PORT}`。
