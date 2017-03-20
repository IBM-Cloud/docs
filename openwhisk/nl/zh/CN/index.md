---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 入门


{{site.data.keyword.openwhisk}} 是一种分布式事件驱动型计算服务，也称为无服务器计算或功能即服务 (FaaS)。{{site.data.keyword.openwhisk_short}} 从 Web 或移动应用程序通过 HTTP 运行应用程序逻辑来响应事件或直接调用。事件可以通过 Bluemix 服务（如 Cloudant）提供，也可以从外部源提供。开发者可以专注于编写应用程序逻辑，以及创建按需执行的操作。这种新规范的优点是无需显式供应服务器，也不必担心自动扩展或担心高可用性、更新、维护以及在服务器运行但不进行请求服务时为处理器时间（小时）付费。
只要存在 HTTP 调用、数据库状态更改或触发代码执行的其他类型的事件，就会执行代码。
您将获得按执行时间（毫秒，向上舍入到最接近的 100 毫秒）计费，而不是按每小时虚拟机使用率计费，与该 VM 是否正在执行有用的工作无关。
{: shortdesc}

此编程模型是微服务、移动、IoT 和其他许多应用程序的完美搭档 - 您能获得开箱即用的固有自动缩放和负载均衡功能，而不必手动配置集群、负载均衡器、HTTP 插件等。如果碰巧在 {{site.data.keyword.openwhisk}} 上运行，那么还将获得零管理的好处 - 这意味着所有的硬件、联网和软件都由 IBM 进行维护。您只需要提供要执行的代码，并将其提供给 {{site.data.keyword.openwhisk}} 即可。剩余工作像“变魔术一样”。[Martin Fowler 的博客](https://martinfowler.com/articles/serverless.html)上提供了对无服务器编程模型的详细介绍.

您也可以获取 [Apache OpenWHisk 源代码](https://github.com/openwhisk/openwhisk)，然后自行运行系统。


有关 {{site.data.keyword.openwhisk_short}} 如何工作的更多详细信息，请参阅[关于 {{site.data.keyword.openwhisk_short}}](./openwhisk_about.html)。

您可以使用浏览器或 CLI 来开发 {{site.data.keyword.openwhisk_short}} 应用程序。
对于开发应用程序来说，这两种方法具有类似的功能，但 CLI 可对部署和操作提供更多的控制。

## 在浏览器中开发
{: #openwhisk_start_editor}

在[浏览器](https://console.{DomainName}/openwhisk/editor){: new_window}中尝试使用 {{site.data.keyword.openwhisk_short}} 来创建操作、使用触发器自动化操作，并探索公共包。
请访问[了解更多信息](https://console.{DomainName}/openwhisk/learn){: new_window}页面，以快速浏览 OpenWhisk 用户界面。

## 使用 CLI 进行开发
{: #openwhisk_start_configure_cli}

可以使用 {{site.data.keyword.openwhisk_short}} 命令行界面 (CLI) 来设置名称空间和授权密钥。转至[配置 CLI](https://new-console.{DomainName}/openwhisk/cli){: new_window}，然后遵循指示信息来进行安装。

## 概述
{: #openwhisk_start_overview}
- [OpenWhisk 工作原理](./openwhisk_about.html)
- [无服务器应用程序的一般用例](./openwhisk_use_cases.html)
- [设置和使用 OpenWhisk CLI](./openwhisk_cli.html)
- [通过 iOS 应用程序使用 OpenWhisk](./openwhisk_mobile_sdk.html)

## 编程模型
{: #openwhisk_start_programming}
- [系统详细信息](./openwhisk_reference.html)
- [OpenWhisk 所提供服务的目录](./openwhisk_catalog.html)
- [操作](./openwhisk_actions.html)
- [触发器和规则](./openwhisk_triggers_rules.html)
- [订阅源](./openwhisk_feeds.html)
- [包](./openwhisk_packages.html)
- [注释](./openwhisk_annotations.html)
- [Web 操作](./openwhisk_webactions.html)
- [API 网关](./openwhisk_apigateway.html)
- [实体名称](./openwhisk_reference.html#openwhisk_entities)
- [操作语义](./openwhisk_reference.html#openwhisk_semantics)
- [限制](./openwhisk_reference.html#openwhisk_syslimits)

## {{site.data.keyword.openwhisk_short}} Hello World 示例
{: #openwhisk_start_hello_world}
要开始使用 {{site.data.keyword.openwhisk_short}}，请尝试以下 JavaScript 代码示例。

```javascript
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

    ```json
    {
        "payload": "Hello, World!"
    }
    ```
    
    ```
wsk action invoke hello --blocking --result --param name Fred
    ```
    {: pre}  

    此命令的输出为：

    ```json
    {
        "payload": "Hello, Fred!"
    }
    ```

您还可以使用 {{site.data.keyword.openwhisk_short}} 中的事件驱动型功能来调用此操作以响应事件。遵循[警报服务示例](./openwhisk_packages.html#openwhisk_packages_trigger)，以将事件源配置为每次生成定期事件时都调用 `hello` 操作。


## API 参考
{: #openwhisk_start_api notoc}
* [REST API 文档](./openwhisk_reference.html#openwhisk_ref_restapi)
* [REST API](https://new-console.{DomainName}/apidocs/98){:new_window}

## 相关链接
{: #general notoc}
* [Discover: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [{{site.data.keyword.openwhisk_short}} on IBM developerWorks](https://developer.ibm.com/openwhisk/){:new_window}
* [Apache {{site.data.keyword.openwhisk_short}} 项目 Web 站点](http://openwhisk.org){:new_window}
