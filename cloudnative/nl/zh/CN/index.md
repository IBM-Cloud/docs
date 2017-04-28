---

copyright:
  years: 2016, 2017
lastupdated: "2016-04-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# 构建云本机项目
{: #web-mobile}

您可以通过 {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} [项目](projects.html)的概念来管理云本机应用程序。您可以通过使用 [{{site.data.keyword.dev_console}}](devex.html) 或使用适用于 {{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}} CLI 的 [{{site.data.keyword.dev_cli_notm}}](dev_cli.html) 来创建项目。{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} 将云本机应用程序开发者所需的最常用服务集中到单一位置，为开发者提供优化的连接体验。

通过 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}}，云本机应用程序开发者可以利用 SDK，从各种[模式类型](patterns.html)和[入门模板](starters.html)创建项目、创建关键 {{site.data.keyword.Bluemix_notm}} 优化服务并将其连接到项目，以及快速下载工作代码。SDK 完全与功能凭证或依赖关系相集成，使您能够几分钟内就让其运行起来。当应用程序处于运行状态时，如果已经设置并配置了功能，那么您可以返回到项目，监视并管理应用程序用户的参与情况。还可以通过 {{site.data.keyword.dev_console}} 配置和管理服务。

<!--
While the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} provides an integrated development experience, some developers might still want to have finer-grained control and wire services together manually. If this is your preferred approach, you might want to consider using the [{{site.data.keyword.mobilefirstbp}} Starter boilerplate](try_mobile.html).
-->

<!--With {{site.data.keyword.Bluemix}} Mobile services, you can incorporate pre-built, managed, and scalable cloud services into your mobile applications. You can focus on building your mobile apps, instead of the complexities of managing the back-end infrastructure.

The Mobile dashboard provides an integrated experience on {{site.data.keyword.Bluemix_notm}} where you can create mobile projects easily from within the dashboard.
-->


## 项目
{: #projects}

{{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} 将应用程序用户界面、数据和服务结合到完整的*项目*中。通过创建项目，您应用程序所需的所有组件和已添加的功能会保留在 {{site.data.keyword.Bluemix_notm}} 服务器上。如果在项目中配置了这些服务，那么可以下载应用程序代码以及所需凭证和初始化程序。您可以通过选择**项目**来查看所有项目。  

您可以通过在**项目**页面上选择单个项目，查看该项目的其他信息。这将显示**项目概述**页面，其中包含已配置并可用于项目的服务。服务是不同的功能，可通过添加函数来扩展您的应用程序。由于服务是单独添加的，因此您可以添加所需服务，如推送、认证、数据和存储服务以及其他服务。向**项目概述**页面上的项目添加服务并遵循指示信息对其进行配置后，该服务会自动与应用程序相关联。有关“项目概述”页面的更多信息，请参阅[项目概述页面](project_overview_page.html)。

要创建项目，必须选择[模式](patterns.html)，后跟[入门模板](starters.html)。


### 项目概述页面
{: #project_overview}

通过在**项目**页面上选择项目，打开“项目概述”页面，可以查看和使用单个 {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} 项目。
{: shortdesc}

**项目概述**页面显示已使用所选项目配置的或可使用该项目配置的每个功能的磁贴。磁贴显示功能的类型以及有三个垂直对齐点的*操作*按钮。可能可用或已配置的功能示例包括 {{site.data.keyword.mobilepushshort}}、分析或数据和存储。哪些功能可兼容取决于项目的类型以及在该区域可以使用哪些功能，因此并非所有服务都可以与所有项目相关联。 

当某个功能类型尚未与项目相关联时，磁贴上会显示**创建**按钮。操作按钮选项用于创建服务的实例，或者在未关联功能时添加现有服务实例。选择**添加现有项**可提供空间中该类型的服务实例列表。

如果功能已经与此项目相关联，那么相关联的服务实例的名称会显示在该功能类型后面的磁贴上。这样就能在 {{site.data.keyword.dev_console}} 上轻松查找哪个服务实例与此项目相关。当功能已经与项目相关联时，操作按钮上可用的操作是**查看**和**除去**。除去服务实例仅会除去与此项目的关联，而不会从 {{site.data.keyword.dev_console}} 删除该服务实例。要删除服务实例，请单击 **Web 和移动 > 服务**页面，以查看和删除服务实例。

在**代码**磁贴上选择**获取代码**，以下载项目的代码。有关下载代码的更多信息，请参阅[获取代码](get_code.html)。


### 更新项目以使用新的入门模板
{: #update-starter}

1. 从**项目**或**项目概述**页面，单击**溢出菜单**图标并选择**更新入门模板**。

2. 选择新的入门模板并单击**更新**。

3. 单击**项目概述**页面上的**获取代码**，以选择语言。

   或者，您可以在**代码**页面上单击。


### 更新项目以生成新的语言
{: #update-language}

1. 从**项目**或**项目概述**页面，单击**溢出菜单**图标并选择**更新入门模板**。

2. 选择新的语言并单击**更新**。

3. 单击**项目概述**页面上的**获取代码**，以选择语言。


## 模式类型
{: #patterns}

云本机模式的设计经过验证，有助于确保实现具有一致性、可扩展性和可靠性的应用程序拓扑。创建项目时，为您提供了各种模式类型，供您选择。只需选择要合并到项目中的模式类型和功能即可。定义项目首选项后，将为您生成入门模板项目，以编辑、运行或调试以及在本地部署或部署到 {{site.data.keyword.Bluemix}}。


### Web 应用程序
{: #web}

Web 项目添加了新功能，可为 Web 服务器处理诸如 HTML、JavaScript 和样式表等 Web 内容。

提供了以下 Web 入门模板：

* 基本 Web：处理静态 `index.html` 文件、缺省和空样式表以及 JavaScript 文件。
* Webpack：创建项目，在此项目中，ECMAScript 6 (ES6) 源文件位于 `src/client` 中且使用 WebPack 进行编译以实现合并压缩和转换，以便在浏览器中使用。
* Webpack + React：用于构建用户接口的富框架。源文件位于 `src/client/app` 中，且使用 WebPack 进行编译并在公共目录中处理。


### 移动应用程序
{: #mobile}

移动应用程序模式可帮助您构建移动应用程序，这些应用程序直接连接到后端服务，例如 {{site.data.keyword.mobilepushshort}}、{{site.data.keyword.mobileanalytics_short}} 和 {{site.data.keyword.appid_short}} 等。还可以通过 sdkGen（例如 BFF 和微服务）添加项目。

可以从入门模板列表中进行选择（例如，{{site.data.keyword.watson}} Conversation、{{site.data.keyword.visualrecognitionshort}} 和 {{site.data.keyword.openwhisk_short}} 等）。

您可以在 Swift、Android 或 Cordova 中生成移动应用程序。


### 服务于前端的后端 (BFF)
{: #bff}

服务于前端的后端模式通常称为 BFF，让您可以重点关注公开业务数据和服务的方式要能够满足用户的交互需求。要优化云解决方案的用户旅程，可能需要对移动应用程序具有不同的用户旅程，而对 Web 应用程序具有更丰富、更详细的旅程。随着语音控制设备（如 [{{site.data.keyword.conversationfull}} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/conversation.html) 服务）的引入，与用户的交互可以是由语音控制。这个数字通道需要截然不同的 BFF，以管理这些基于语音意图的交互。

有了 {{site.data.keyword.Bluemix_notm}}，可以通过使用混合编程方法来定义 BFF，从而构建 BFF。IBM 建议使用 Node.js、Swift 或 Java，以具有 Cloud Foundry、Container 服务或无服务器的方式，在云本机模式下运行。

BFF 将管理与数据持久性、高速缓存等服务的集成，与高价值服务（如 {{site.data.keyword.ibmwatson}}、{{site.data.keyword.iot_short_notm}}、{{site.data.keyword.weather_short}}）的集成，以及数据分析（如 {{site.data.keyword.sparks}}）。

BFF 将公开最常使用 REST 模式的 API，但是您可以使用 {{site.data.keyword.messagehub}} 来设计 BFF 以通过消息传递体系结构进行工作。

BFF 基本入门模板通过使用 Node.js 或 Swift 提供。


### 微服务
{: #microservice}

微服务项目为构建后端微服务（包括基本运行状况端点这一 REST API）提供基础。生成的项目将包含微服务本身以及所有相关云服务所需的所有依赖关系。

微服务基本入门模板通过使用 Java 提供。

<!--
## Other
{: #other}

The Other pattern represents a project that consists of only the language-specific server-side web framework. It has all the other file assets to work with the project, such as needed libraries and config files.

Content to be provided by Karl Bishop.
-->


### 语言
{: #languages notoc}

以下为受支持的语言：

   * [Java ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](../runtimes/liberty/getting-started.html){: new_window}
   * [Node.js ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](../runtimes/nodejs/getting-started.html){: new_window}
   * [Swift ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](../runtimes/swift/getting-started.html){: new_window}


#### Java
{: #java notoc}

Java 具有强大的功能，用于构建企业级应用程序。同时，Java 8 中提供的新功能以及较轻量级运行时（例如，Liberty）和框架（例如，Spring Boot）使 Java 也非常适合构建微服务。


#### Node.js
{: #node notoc}

Node.js 是使用事件驱动的非阻塞 I/O 模型的 JavaScript 运行时，使其轻量且高效，为 Web 应用程序、服务于前端的后端模式和微服务实现强大吞吐量和可扩展性。Node.js 的软件包生态系统 npm 提供了对大量开放式源代码模块的访问，同时提供很多功能以加速应用程序开发。


#### Swift
{: #swift notoc}

Swift 是 Apple 在 2014 年开发的一种现代编程语言，旨在替换 Objective C，于 2015 年 12 月成为开放式源代码语言。目前，此编程语言用于使用 x86、ARM 或 Z 体系结构在 Linux 和 macOS 操作系统上构建 iOS、macOS、Web Service 和系统软件。此语言编写方式类似脚本语言，但编译后可获得与 C 语言类似的高性能和低开销，适合云运行时。它使用 Java 中所使用的强大和静态类型系统，以及 JavaScript 中所使用的功能样式和异步例程。此语言具有高性能，源代码使用 LLVM 编译器工具链编译为本机代码，且可轻松利用使用 C 语言编写的外部系统库。


## 入门模板
{: #starters}

使用 {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}，可以从多个入门模板中为每种模式类型做出选择。

入门模板已经过优化，是可用于生产的入门模板代码，重点在于演示 {{site.data.keyword.Bluemix_notm}} 与高价值服务的重要集成。每一个入门模板都注重一个服务，并显示服务 SDK 与代码的集成。在某些情况下，入门模板提供简单的用户体验，以突出显示与服务数据或用户交互的集成。每个入门模板都配置为可以通过认证、数据以及其他可能的功能来启用，所以如果您决定为项目配置这些功能，也便于使用。
