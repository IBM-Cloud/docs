---

copyright:
  years: 2016, 2017
lastupdated: "2016-09-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 入门


{{site.data.keyword.openwhisk}} 是一种分布式事件驱动型计算服务，也称为无服务器计算或功能即服务 (FaaS)。{{site.data.keyword.openwhisk_short}} 从 Web 或移动应用程序通过 HTTP 运行应用程序逻辑来响应事件或直接调用。事件可以通过 Bluemix 服务（如 Cloudant）提供，也可以从外部源提供。开发者可以专注于编写应用程序逻辑，以及创建按需执行的操作。执行操作的速率始终与事件速率相匹配，从而产生固有的扩展和弹性以及最佳利用率。您只需为您使用的内容付费，而且不必管理服务器。您也可以获取[源代码](https://github.com/openwhisk/openwhisk)，然后自行运行系统。
{: shortdesc}

有关 {{site.data.keyword.openwhisk_short}} 如何工作的更多详细信息，请参阅[关于 {{site.data.keyword.openwhisk_short}}](./openwhisk_about.html)。

您可以使用浏览器或 CLI 来开发 {{site.data.keyword.openwhisk_short}} 应用程序。
对于开发应用程序来说，这两种方法具有类似的功能，但 CLI 可对部署和操作提供更多的控制。


## 在浏览器中开发
{: #openwhisk_start_editor}

在[浏览器](https://console.{DomainName}/openwhisk/editor){: new_window}中尝试使用 {{site.data.keyword.openwhisk_short}} 来创建操作、使用触发器自动化操作，并探索公共包。
请访问[了解更多信息](https://console.{DomainName}/openwhisk/learn){: new_window}页面，以快速浏览 OpenWhisk 用户界面。

## 设置 {{site.data.keyword.openwhisk_short}} CLI
{: #openwhisk_start_configure_cli}

可以使用 {{site.data.keyword.openwhisk_short}} 命令行界面 (CLI) 来设置名称空间和授权密钥。转至[配置 CLI](https://new-console.{DomainName}/openwhisk/cli){: new_window}，然后遵循指示信息来进行安装。

### 配置 CLI 以使用 HTTPS 代理
{: #openwhisk_configure_https_proxy_cli}

CLI 可以设置为使用 HTTPS 代理。要设置 HTTPS 代理，必须创建名为 `HTTPS_PROXY` 的环境变量。该变量必须设置为 HTTPS 代理的地址，并且其端口使用以下格式：`{PROXY IP}:{PROXY PORT}`。

使用 CLI 设置 {{site.data.keyword.openwhisk_short}} 后，可以通过命令行对其开始使用。

## 使用 {{site.data.keyword.openwhisk_short}} CLI
{: #openwhisk_start_using_cli}

[配置环境](https://new-console.{DomainName}/openwhisk/cli){: new_window}后，可以开始使用 {{site.data.keyword.openwhisk_short}} CLI 来执行以下操作：

* 在 {{site.data.keyword.openwhisk_short}} 上运行代码片段或操作。请参阅[创建和调用操作](./openwhisk_actions.html)。
* 使用触发器和规则以支持操作对事件进行响应。请参阅[创建触发器和规则](./openwhisk_triggers_rules.html)。
* 了解包如何捆绑操作以及配置外部事件源。请参阅[使用和创建包](./openwhisk_packages.html)。
* 浏览包的目录，并通过外部服务（例如，[Cloudant 事件源](./openwhisk_catalog.html#openwhisk_catalog_cloudant)）来增强应用程序的功能。请参阅[使用启用了 {{site.data.keyword.openwhisk_short}} 的服务](./openwhisk_catalog.html)。


## 通过 iOS 应用程序使用 {{site.data.keyword.openwhisk_short}}
{: #openwhisk_start_using_ios}

可以使用 {{site.data.keyword.openwhisk_short}} iOS SDK 通过 iOS 移动应用程序或 Apple Watch 来使用 {{site.data.keyword.openwhisk_short}}。有关更多详细信息，请参阅 [iOS 文档](./openwhisk_mobile_sdk.html)。

## 将 REST API 用于 {{site.data.keyword.openwhisk_short}}
{: #openwhisk_start_using_restapi}

启用了 {{site.data.keyword.openwhisk_short}} 环境后，可以通过 REST API 调用将 {{site.data.keyword.openwhisk_short}} 与 Web 应用程序或移动应用程序配合使用。有关用于操作、激活、包、规则和触发器的 API 的更多详细信息，请参阅 [{{site.data.keyword.openwhisk_short}} API 文档](https://new-console.{DomainName}/apidocs/98)。

## {{site.data.keyword.openwhisk_short}} Hello World 示例
{: #openwhisk_start_hello_world}
要开始使用 {{site.data.keyword.openwhisk_short}}，请尝试以下 JavaScript 代码示例。

```
/**
 * Hello world as an OpenWhisk action.
 */
function main(params) {
    var name = params.name || 'World';
    return {payload:  'Hello, ' + name + '!'};
}
```
{: codeblock}

要使用此示例，请执行以下步骤：

1. 将代码保存到文件。例如，*hello.js*。

2. 在 {{site.data.keyword.openwhisk_short}} CLI 命令行中，通过输入以下命令来创建操作：

    ```
wsk action create hello hello.js
    ```
    {: pre}

3. 然后，通过输入以下命令来调用操作。

    ```
wsk action invoke hello --blocking --result
    ```
    {: pre}  

    此命令的输出为：

    ```
    {
        "payload": "Hello, World!"
    }
    ```
    {: screen}

    ```
wsk action invoke hello --blocking --result --param name Fred
    ```
    {: pre}  

    此命令的输出为：

    ```
    {
        "payload": "Hello, Fred!"
    }
    ```
    {: screen}

您还可以使用 {{site.data.keyword.openwhisk_short}} 中的事件驱动型功能来调用此操作以响应事件。遵循[警报服务示例](./openwhisk_packages.html#openwhisk_packages_trigger)，以将事件源配置为每次生成定期事件时都调用 `hello` 操作。


## 系统详细信息
{: #openwhisk_system_details}

可以在以下主题中找到有关 {{site.data.keyword.openwhisk_short}} 的更多信息：

* [实体名称](./openwhisk_reference.html#openwhisk_entities)
* [操作语义](./openwhisk_reference.html#openwhisk_semantics)
* [限制](./openwhisk_reference.html#openwhisk_syslimits)
* [REST API](https://new-console.{DomainName}/apidocs/98)

# 相关链接
{: #rellinks notoc}

## API 参考
{: #api}
* [REST API 文档](./openwhisk_reference.html#openwhisk_ref_restapi)
* [REST API](https://new-console.{DomainName}/apidocs/98){:new_window}

## 相关链接
{: #general}
* [Discover: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [{{site.data.keyword.openwhisk_short}} on IBM developerWorks](https://developer.ibm.com/openwhisk/){:new_window}
