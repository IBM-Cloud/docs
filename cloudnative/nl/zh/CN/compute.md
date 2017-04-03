---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 计算
{: #compute}

当您为 Web 和移动构建云本机数字通道应用程序时，最好的做法是采用服务于前端的后端 (BFF)，将其专门用于数字通道，或者为 Web 和移动客户端应用程序提供相同的数据和逻辑集成支持。有关此体系结构的更多信息，请参阅 [Web 和移动的微服务 ![外部链接图标](../icons/launch-glyph.svg)](https://www.ibm.com/devops/method/content/architecture/omnichannelArchitecture)。

下图显示 BFF 体系结构的概述。

![BFF 体系结构](images/bff-arch.png)

图 1：BFF 体系结构

BFF 的概念是从微服务或高价值的 {{site.data.keyword.Bluemix}} 云服务中抽象出常用的业务逻辑和集成逻辑。

有了此体系结构，可以使用持续 Delivery Pipeline 搭配开发运营服务，来部署并发布移动或 Web 应用程序的更新，以及部署 BFF 的新版本。

如果您对 iOS 使用一个 BFF，而对 Android 使用另一个 BFF，则为这些应用程序提供功能的工程团队不会局限于通过集中 API 发布安排来发布功能。这是微服务和数字通道体系结构的常见目标 - 让团队能够自由地经常发布功能和特性，而无需与另一个团队的发布计划紧密结合。

<!--
## Backend for Frontends (BFF)
{: #bff}

Backend for Frontend patterns, commonly known as BFFs, really help you to focus on exposing business data and services in a form that matches the user interaction requirements. To optimize a user journey to your cloud solution, it may require a different user journey for the mobile application and a richer, more detailed journey for the Web application. With the introduction of voice-controlled devices like the [{{site.data.keyword.conversationfull}} ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/conversation.html) service, the interaction with a user could be controlled by voice. This digital channel will require a very different BFF for managing these voice intent-based interactions.

With {{site.data.keyword.Bluemix_notm}}, you can build a BFF by using polyglot programming approach to define the BFF. IBM recommends using Node, Swift, or Java and running them in a cloud native pattern with either Cloud Foundry, Container services, or serverless.

The BFF will manage the integration with services for data persistence, caching, and integration with high-value services like {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}}, and data analytics like {{site.data.keyword.sparks}}.

The BFF will expose an API most commonly using a REST pattern, but you can design your BFF to work from a messaging architecture using {{site.data.keyword.messagehub}}.
-->


## 将移动客户端与服务于前端的后端集成
{: #integration}

为了在移动客户端与 BFF 之间实现轻松集成，{{site.data.keyword.Bluemix_notm}} 支持分别以 Swift 和 Java 语言，为 iOS 和 Android 生成移动客户端 SDK。要启用此功能，您必须使用开放 API 规范 (Swagger) 文档，公开 BFF 集成。此文档可以是 JSON 或 YAML 形式。

客户端 SDK 生成器使用开放 API 定义文件，来定义可轻松在本机移动应用程序中使用的客户端优化开发者 SDK。这会加快将 BFF 与移动应用程序的集成的速度。


## 定义 API
{: #definition}

BFF 需要公开 API 定义文件，该文件符合在活动服务器端点上运行的开放 API 规范。要启用 {{site.data.keyword.Bluemix_notm}} Developer Experience 和 {{site.data.keyword.Bluemix_notm}} SDK CLI（命令行界面）以探索此端点，您必须向名为 `OPENAPI_SPEC` 的 Cloud Foundry 应用程序中添加环境变量。此环境变量必须使用相对路径参考规范。

要在 {{site.data.keyword.Bluemix_notm}} 中添加 `OPENAPI_SPEC` 环境变量，请遵循以下步骤：

1. 登录到 [{{site.data.keyword.Bluemix_notm}} ![外部链接图标](../icons/launch-glyph.svg)](http://bluemix.net)。
2. 选择 Cloud Foundry 应用程序。
3. 选择**运行时**。
4. 选择**环境变量**。
5. 在**用户定义**部分中单击**添加**。
6. 为 **NAME** 指定 `OPENAPI_SPEC`，并指定开放 API 定义文件的相对 URL 路径。
7. 单击**保存**。

<!--
To add the `OPENAPI_SPEC` environment variable locally and push your changes to {{site.data.keyword.Bluemix_notm}} with the [Cloud Foundry CLI ![External link icon](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli#getting-started), follow these steps:

1. Open Terminal and navigate to your project directory.
2. Add the following code to the `manifest.yml` file.

   ```
   env:
       "OPENAPI_SPEC": "<relative URL path to your Open API definition file>"
   ```
   {: codeblock}
3. Save your changes to the `manifest.yml` file.
4. Run `cf push` to deploy the changes to {{site.data.keyword.Bluemix_notm}}.
-->

例如：

```
OPENAPI_SPEC='/explorer/swagger.json'
```
{: codeblock}

使用此方法，{{site.data.keyword.apiconnect_long}} 和 Loopback 应用程序运作得非常好。您可以使用 Loopback 和 {{site.data.keyword.apiconnect_short}} 来定义持久性模型，并使用开放 API 定义文件公开 CRUD（创建、读取、更新和删除）操作。

您还可以定义业务逻辑操作。


### 开放 API 规范的支持元素
{: #supported-elements notoc}

开放 API 规范中唯一不受完全支持的部分是文件结构。规范允许定义部分分成几个不同的文件，并使用 `$ref` 字段进行参考。整个定义必须包含在一个文件中。


## 使用 Bluegen 的前端服务于后端示例
{: #bff-bluegen}

{{site.data.keyword.Bluemix_notm}} 使用 {{site.data.keyword.apiconnect_short}} 和 Strongloop 创建了参考 BFF，其将产品模型与 {{site.data.keyword.cloudant}} 和图像 API 相映射，以参考 {{site.data.keyword.objectstorageshort}} 中的图形。

您可以使用此 BFF 模式快速熟悉将完整工作 BFF 供应到 {{site.data.keyword.Bluemix_notm}}，并使用它来帮助理解将 BFF 集成到移动项目，并分别以 Swift 和 Java 为 iOS 和 Android 生成本机 SDK 是多么轻松的一件事。

遵循[自述文件 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/backend-for-frontend-node) 指示信息，以创建项目并对其进行安装。


## 使用前端服务于后端与 Developer Experience 项目
{: #bff-devex}

{{site.data.keyword.Bluemix_notm}} Mobile Developer Experience 设计用来以一种更简单的方法，来定义与若干云服务相关联的移动项目。您可以轻松地添加 [{{site.data.keyword.mobilepushshort}} ![外部链接图标](../icons/launch-glyph.svg)](/docs/services/mobilepush/index.html)、[Analytics ![外部链接图标](../icons/launch-glyph.svg)](/docs/services/mobileanalytics/index.html) 和 Data 或 Storage 服务。

{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} 在**计算**页面中引入了将 BFF 与移动项目集成的功能。您可以将现有的计算服务实例添加到移动项目。添加之后，您可以为您的语言选择生成本地 SDK，或者您可以生成完整的项目，SDK 将集成到**代码**页面中项目的源程序包中。当您与已很好定义的 BFF 相集成时，这非常有用。

在您下载项目之后，可以使用 Xcode 或 Android Studio 打开该项目，并使用客户端 SDK 对项目进行编译。


## 使用 CLI
{: #cli}

当您开发 BFF 时，API 规范可能会更改。要支持这些更改，您必须具有以下两个选项：

* 在全新 GitHub 分支中重新生成整个项目并将更改合并至开发分支。
* 直接使用命令行 (CLI) 工具重新生成 SDK，并仅更新移动项目的 SDK 部分。

要使用 CLI，您必须对其进行[安装](sdk_cli.html#installation)。

使用以下命令列出您可以执行的操作。

```
bluemix sdk
```
{: codeblock}

使用以下命令，列出当前 {{site.data.keyword.Bluemix_notm}} 空间中正在运行的 Cloud Foundry 实例。

```
bluemix sdk list
```
{: codeblock}

如果已设置 `OPENAPI_SPEC` 环境变量，则会列出每一个应用程序并验证 API。在 `VALID` 列中，您将看到绿色的勾号或红色的 `X`。应用程序中 `VALID` 列的勾号表示存在有效的开放 API 定义。应用程序的 `VALID` 列中的 `X` 表示以下其中一项：

* 未对应用程序定义 `OPENAPI_SPEC` 环境变量，或者
* 对于开放 API 规范，API 定义无效

使用以下命令来查看 API 的完整 URL。列出 API 规范的完整路径和 URI。您可以在浏览器中查看原始规范，直接在 CLI 中使用，或者验证 BFF `OPENAPI_SPEC` 环境变量是否设置正确。

```
bluemix sdk list --url
```
{: codeblock}

使用以下命令来验证 `<AppName>` 的开放 API 定义文件，以确定其是否可用于生成 SDK。该命令会在当前空间中查找 `<AppName>`，并在 `OPENAPI_SPEC` 环境变量中使用相对路径，查找要验证的规范。

```
bluemix sdk validate <AppName>
```
{: codeblock}

使用以下命令，为您所选择的本机 `<Platform>` 生成 SDK，并将压缩文件置于当前工作目录中。

```
bluemix sdk generate <AppName> <SDKName> --<Platform>
```
{: codeblock}

使用 `--unzip` 选项会自动将 SDK 解压缩至当前工作目录。您可以使用 `--output` 选项，选择性地指定要将 SDK 解压缩的位置。您可以使用 GitHub 管理源代码，并创建新分支，专门用于更新 SDK。使用此方法，可更加轻松地查看更改，并将更新的 SDK 合并到开发分支。


## 使用 SDK 生成的模型和 API
{: #models-apis}

既然您的 BFF 已使用生成的 SDK 集成到移动应用程序中，那么您可以开始使用它。

SDK 在 `docs` 目录和 `source` 目录中随附有完整生成的文档。您可以打开 `README.html` 文件以启动文档的 Web 视图，或者打开 `README.md` 文件以启动文档的 Markdown 视图。当您将 SDK 发布到 Cocoapods 或 Maven Central 时，Markdown 文档非常有用。

在文档中，可以查看所生成的 API 列表。您可以单击 API，以查看您可以直接粘贴到移动应用程序中的代码片段。
