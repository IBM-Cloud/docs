
---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# 模式类型
{: #patterns}

云本机模式的设计经过验证，有助于确保实现具有一致性、可扩展性和可靠性的应用程序拓扑。创建项目时，为您提供了各种模式类型，供您选择。只需选择要合并到项目中的模式类型和功能即可。定义项目首选项后，将为您生成入门模板项目，以编辑、运行或调试以及在本地部署或部署到 {{site.data.keyword.Bluemix}}。

## Web 应用程序
{: #web}

Web 项目添加了新功能，可为 Web 服务器处理诸如 HTML、JavaScript 和样式表等 Web 内容。

提供了以下 Web 入门模板：

* 基本 Web：处理静态 `index.html` 文件、缺省和空样式表以及 JavaScript 文件。
* Webpack：创建项目，在此项目中，ECMAScript 6 (ES6) 源文件位于 `src/client` 中且使用 WebPack 进行编译以实现合并压缩和转换，以便在浏览器中使用。
* Webpack + React：用于构建用户接口的富框架。源文件位于 `src/client/app` 中，且使用 WebPack 进行编译并在公共目录中处理。


## 移动应用程序
{: #mobile}

移动应用程序模式可帮助您构建移动应用程序，这些应用程序直接连接到后端服务，例如 {{site.data.keyword.mobilepushshort}}、{{site.data.keyword.mobileanalytics_short}} 和 {{site.data.keyword.appid_short}} 等。还可以通过 sdkGen（例如 BFF 和微服务）添加项目。

可以从入门模板列表中进行选择（例如，{{site.data.keyword.watson}} Conversation、{{site.data.keyword.visualrecognitionshort}} 和 {{site.data.keyword.openwhisk_short}} 等）。

您可以在 Swift、Android 或 Cordova 中生成移动应用程序。


## 服务于前端的后端 (BFF)
{: #bff}

服务于前端的后端模式通常称为 BFF，让您可以重点关注公开业务数据和服务的方式要能够满足用户的交互需求。要优化云解决方案的用户旅程，可能需要对移动应用程序具有不同的用户旅程，而对 Web 应用程序具有更丰富、更详细的旅程。随着语音控制设备（如 [{{site.data.keyword.conversationfull}} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/conversation.html) 服务）的引入，与用户的交互可以是由语音控制。这个数字通道需要截然不同的 BFF，以管理这些基于语音意图的交互。

有了 {{site.data.keyword.Bluemix_notm}}，可以通过使用混合编程方法来定义 BFF，从而构建 BFF。IBM 建议使用 Node.js、Swift 或 Java，以具有 Cloud Foundry、Container 服务或无服务器的方式，在云本机模式下运行。

BFF 将管理与数据持久性、高速缓存等服务的集成，与高价值服务（如 {{site.data.keyword.ibmwatson}}、{{site.data.keyword.iot_short_notm}}、{{site.data.keyword.weather_short}}）的集成，以及数据分析（如 {{site.data.keyword.sparks}}）。

BFF 将公开最常使用 REST 模式的 API，但是您可以使用 {{site.data.keyword.messagehub}} 来设计 BFF 以通过消息传递体系结构进行工作。

BFF 基本入门模板通过使用 Node.js 或 Swift 提供。


## 微服务
{: #microservice}

微服务项目为构建后端微服务（包括基本运行状况端点这一 REST API）提供基础。生成的项目将包含微服务本身以及所有相关云服务所需的所有依赖关系。

微服务基本入门模板通过使用 Java 提供。

<!--
## Other
{: #other}

The Other pattern represents a project that consists of only the language-specific server-side web framework. It has all the other file assets to work with the project, such as needed libraries and config files.

Content to be provided by Karl Bishop.
-->


## 语言
{: #languages notoc}

以下为受支持的语言：

   * [Java ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](../runtimes/liberty/getting-started.html){: new_window}
   * [Node.js ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](../runtimes/nodejs/getting-started.html){: new_window}
   * [Swift ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](../runtimes/swift/getting-started.html){: new_window}


### Java
{: #java notoc}

Java 具有强大的功能，用于构建企业级应用程序。同时，Java 8 中提供的新功能以及较轻量级运行时（例如，Liberty）和框架（例如，Spring Boot）使 Java 也非常适合构建微服务。


### Node.js
{: #node notoc}

Node.js 是使用事件驱动的非阻塞 I/O 模型的 JavaScript 运行时，使其轻量且高效，为 Web 应用程序、服务于前端的后端模式和微服务实现强大吞吐量和可扩展性。Node.js 的软件包生态系统 npm 提供了对大量开放式源代码模块的访问，同时提供很多功能以加速应用程序开发。


### Swift
{: #swift notoc}

Swift 是 Apple 在 2014 年开发的一种现代编程语言，旨在替换 Objective C，于 2015 年 12 月成为开放式源代码语言。目前，此编程语言用于使用 x86、ARM 或 Z 体系结构在 Linux 和 macOS 操作系统上构建 iOS、macOS、Web Service 和系统软件。此语言编写方式类似脚本语言，但编译后可获得与 C 语言类似的高性能和低开销，适合云运行时。它使用 Java 中所使用的强大和静态类型系统，以及 JavaScript 中所使用的功能样式和异步例程。此语言具有高性能，源代码使用 LLVM 编译器工具链编译为本机代码，且可轻松利用使用 C 语言编写的外部系统库。
