---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 入门
*上次更新时间：2016 年 2 月 17 日*

{{site.data.keyword.openwhisk}} 是一种分布式事件驱动型计算服务。{{site.data.keyword.openwhisk_short}} 执行应用程序逻辑以响应通过 HTTP 从 Web 或移动应用程序发出的事件或直接调用。事件可以通过 Bluemix 服务（如 Cloudant）提供，也可以从外部源提供。开发者可以专注于编写应用程序逻辑，以及创建按需执行的操作。执行操作的速率始终与事件速率相匹配，从而产生固有的扩展和弹性以及最佳利用率。您只需为您使用的内容付费，而且不必管理服务器。您也可以获取[源代码](https://github.com/openwhisk/openwhisk)，然后自行运行系统。
{: shortdesc}

有关 {{site.data.keyword.openwhisk_short}} 如何工作的更多详细信息，请参阅[关于 {{site.data.keyword.openwhisk_short}}](./openwhisk_about.html)。

## 设置 {{site.data.keyword.openwhisk_short}}
可以使用 {{site.data.keyword.openwhisk_short}} 命令行界面 (CLI) 来设置名称空间和授权密钥。转至[配置 CLI](https://console.{DomainName}/openwhisk/cli){: new_window}，然后遵循指导经验来进行安装。请注意，必须在系统上安装 Python 2.7，才能使用该 CLI。

使用 CLI 设置 {{site.data.keyword.openwhisk_short}} 后，可以通过命令行或 REST API 开始使用 OpenWhisk。

## 使用 {{site.data.keyword.openwhisk_short}} CLI
配置您的环境后，可以开始使用 {{site.data.keyword.openwhisk_short}} CLI 来执行以下操作：

* 在 {{site.data.keyword.openwhisk_short}} 上运行代码片段或操作。请参阅[创建和调用操作](./openwhisk_actions.html)。
* 使用触发器和规则以支持操作对事件进行响应。请参阅[创建触发器和规则](./openwhisk_triggers_rules.html)。
* 了解包如何捆绑操作以及配置外部事件源。请参阅[使用和创建包](./openwhisk_packages.html)。
* 浏览包的目录，并通过外部服务（例如，[Cloudant 事件源](./openwhisk_catalog.html#openwhisk_catalog_cloudant)）来增强应用程序的功能。请参阅[使用启用了 {{site.data.keyword.openwhisk_short}} 的服务](./openwhisk_catalog.html)。


## 通过 iOS 应用程序使用 {{site.data.keyword.openwhisk_short}}
可以使用 {{site.data.keyword.openwhisk_short}} iOS SDK 通过 iOS 移动应用程序或 Apple Watch 来使用 {{site.data.keyword.openwhisk_short}}。有关更多详细信息，请参阅 [iOS 文档](./openwhisk_mobile_sdk.html)。

## 将 REST API 用于 {{site.data.keyword.openwhisk_short}}
启用了 {{site.data.keyword.openwhisk_short}} 环境后，可以通过 REST API 调用将 {{site.data.keyword.openwhisk_short}} 与 Web 应用程序或移动应用程序配合使用。有关用于操作、激活、包、规则和触发器的 API 的更多详细信息，请参阅 [{{site.data.keyword.openwhisk_short}} API 文档](https://new-console.{DomainName}/apidocs/98)。

## {{site.data.keyword.openwhisk_short}} Hello World 示例
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

可以在以下主题中找到有关 {{site.data.keyword.openwhisk_short}} 的更多信息：

* [实体名称](./openwhisk_reference.html#openwhisk_entities)
* [操作语义](./openwhisk_reference.html#openwhisk_semantics)
* [限制](./openwhisk_reference.html#openwhisk_syslimits)
* [REST API](https://new-console.{DomainName}/apidocs/98)

# 相关链接
## api
* [REST API 文档](https://new-console.{DomainName}/apidocs/98){:new_window}

## 常规
* [Discover: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [{{site.data.keyword.openwhisk_short}} on IBM developerWorks](https://developer.ibm.com/openwhisk/){:new_window}
