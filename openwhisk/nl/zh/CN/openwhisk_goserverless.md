---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# OpenWhisk 与无服务器框架的集成
{: #openwhisk_goserverless}

[无服务器框架](https://serverless.com/)是一种开放式源代码框架，用于构建无服务器应用程序。使用简单的清单文件，开发者可以定义无服务器功能，将其连接到事件源，并声明其应用程序需要的云服务。框架会处理将这些无服务器应用程序部署到云提供程序的过程。此外，还允许开发者监视生产中的服务、推广更新和协助调试问题。它还有充满活力的第三方插件生态系统，可扩展框架的功能。这正是 OpenWhisk 派上用场之处。
{:shortdesc}

OpenWhisk 具有[自己的面向无服务器框架的提供程序插件](https://github.com/serverless/serverless-openwhisk)。使用无服务器框架的开发者可以选择将自己的应用程序部署到任何 OpenWhisk 平台实例（在 Bluemix 或其他云上托管，或以专用方式托管）。多提供程序支持还意味着在平台之间移动应用程序要容易得多，并且开发者可以开发多云无服务器应用程序。

## 入门
{: #openwhisk_goserverless_starting}

下面是正式的无服务器框架 [OpenWhisk 入门指南](https://serverless.com/framework/docs/providers/openwhisk/guide/intro/) - 此指南涵盖安装、开发工作流程、最佳实践和分步指南，用于说明构建和部署有效 OpenWhisk 应用程序等操作。

[此视频](https://youtu.be/GJY10W98Itc)说明了如何将无服务器框架与 OpenWhisk 提供程序插件配合使用。
## 文档
{: #openwhisk_goserverless_docs}

有关如何将 OpenWhisk 与无服务器框架配合使用的最新文档，请访问[此处](https://serverless.com/framework/docs/providers/openwhisk/)。
## 样本
{: #openwhisk_goserverless_samples}
[无服务器框架示例 GitHub 存储库](https://github.com/serverless/examples)现在具有 OpenWhisk，显示了如何构建 HTTP API、基于 cron 的计划程序、链接函数，等等。
