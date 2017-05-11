---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-4"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 关于 Continuous Delivery  
{: #cd_about}  

通过 {{site.data.keyword.contdelivery_full}}，您可以使用 DevOps 实践和业界领先的工具来构建、测试和交付应用程序。
{:shortdesc}

{{site.data.keyword.contdelivery_short}} 服务支持 DevOps 工作流程：

 * 可以创建集成 DevOps 开放式[工具链](/docs/services/ContinuousDelivery/toolchains_about.html){: new_window}，以启用支持开发、部署和操作任务的工具集成。

  工具链是一组集成工具，可用于以协作方式开发、构建、部署、测试和管理应用程序。可以创建包含 {{site.data.keyword.Bluemix_notm}} 服务、开放式源代码工具和第三方工具（例如，GitHub、PagerDuty 和 Slack）的工具链，使开发和操作可重复，也更容易对开发和操作进行管理。

 * 使用自动化[管道](/docs/services/ContinuousDelivery/pipeline_about.html){: new_window}持续交付。

  自动执行构建、单元测试、部署等操作。以可重复的方式进行构建、测试和部署，需要的人为干预最少。可随时发布到生产环境。

 * 使用[基于 Web 的 IDE](/docs/services/ContinuousDelivery/web_ide.html){: new_window} 从任意位置编辑并推送代码。

  在 GitHub 中创建、编辑、运行、调试和完成源代码控制任务。从编辑代码到将代码部署到生产环境，实现无缝衔接。

 * 通过 [{{site.data.keyword.DRA_short}}](/docs/services/ContinuousDelivery/di_working.html){: new_window} 提高质量。

  了解团队开发和交付代码的动态情况。了解用户与应用程序的交互方式。复查数据以帮助您管理应用程序的操作。


## Bluemix Public 与 Bluemix Dedicated 比较的工具链可用性
{: #public_and_dedicated}

{{site.data.keyword.Bluemix_notm}} Public 是一种以云为基础的开放式标准平台，您可以在其中构建、运行和管理通过 [http://bluemix.net ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://bluemix.net){:new_window} 访问的应用程序。{{site.data.keyword.Bluemix_notm}} Dedicated 在安全连接到 {{site.data.keyword.Bluemix_notm}} Public 环境和您网络的专用 SoftLayer 环境中提供 {{site.data.keyword.Bluemix_notm}} 的功能。您公司的 {{site.data.keyword.Bluemix_notm}} Dedicated 环境可能未包含与 {{site.data.keyword.Bluemix_notm}} Public 站点相同的工具集成。

对于源代码管理和问题跟踪，{{site.data.keyword.Bluemix_notm}} Public 一般使用 github.com。{{site.data.keyword.Bluemix_notm}} Dedicated 也可以使用 github.com，但是它通常使用由您公司安装或由 IBM 管理的 {{site.data.keyword.ghe_short}}。

{{site.data.keyword.contdelivery_short}} 在 {{site.data.keyword.Bluemix_notm}} Public 和 {{site.data.keyword.Bluemix_notm}} Dedicated 上提供。根据是在 {{site.data.keyword.Bluemix_notm}} Public 上还是在 {{site.data.keyword.Bluemix_notm}} Dedicated 上使用 {{site.data.keyword.contdelivery_short}}，工具链有所不同。

|工具链 |{{site.data.keyword.Bluemix_notm}} Public	|{{site.data.keyword.Bluemix_notm}} Dedicated |
|:----------|:------------------------------|:------------------|
|工具集成 		|有关受支持工具集成的列表，请参阅[配置工具集成](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}。 		|可用的工具集成取决于 {{site.data.keyword.contdelivery_short}} 在您环境中的设置方式。			|
|通过模板创建工具链		|登录到 [{{site.data.keyword.Bluemix_notm}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://console.ng.bluemix.net/devops){:new_window}		|登录到 {{site.data.keyword.Bluemix_notm}} 上的 Dedicated 环境。			|
|通过应用程序创建工具链		|此时，将会对应用程序进行配置，以便可通过填充应用程序入门模板代码的新 GitHub 存储库，进行持续交付。		|此时，将会对应用程序进行配置，以便可通过填充应用程序入门模板代码的新 GitHub 或 GitHub Enterprise 存储库，进行持续交付。		|  
|Delivery Pipeline 部署区域		|所有 {{site.data.keyword.Bluemix_notm}} Public 区域都可用于 Cloud Foundry 部署作业。 		|{{site.data.keyword.Bluemix_notm}} Dedicated 区域可用。根据 {{site.data.keyword.contdelivery_short}} 在特定环境中的设置方式，相同客户帐户中的其他 Dedicated 或 Local 区域也可能可用。		|
|Delivery Pipeline 部署作业		|所有[作业类型](/docs/services/ContinuousDelivery/pipeline_about.html#deliverypipeline_jobs)都可用。		|取决于未安装在 Dedicated 环境中的 {{site.data.keyword.Bluemix_notm}} 服务的作业类型可能不可用。例如，容器构建和部署作业类型在没有 {{site.data.keyword.Bluemix_notm}} Container 服务的环境中可能不可用。	|
{: caption="Table 1. Differences between toolchains on {{site.data.keyword.Bluemix_notm}} Dedicated 和 {{site.data.keyword.Bluemix_notm}} Public" caption-side="top"}


## 工具链模板
{: #templates}

您可以使用模板作为起始点来[创建工具链 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/devops/create){: new_window}。工具链模板包括支持开发、部署和操作任务的一组特定工具集成。

**提示**：您公司的 {{site.data.keyword.Bluemix_notm}} Dedicated 环境可能未包含与 {{site.data.keyword.Bluemix_notm}} Public 站点相同的工具链模板。在 {{site.data.keyword.Bluemix_notm}} Public 和 {{site.data.keyword.Bluemix_notm}} Dedicated 上都可用的工具链模板可能在 {{site.data.keyword.Bluemix_notm}} Dedicated 上包含一组不同的工具集成。

一些工具链模板包含属于 {{site.data.keyword.contdelivery_short}} 服务的工具集成。如果该服务的实例不在组织中，那么当您单击**创建**以创建工具链时，系统会自动免费添加该服务。有关更多信息和条款，请参阅 [Bluemix 目录 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/catalog/services/continuous-delivery/){:new_window}。

微型服务工具链模板使用 Cloudant 存储库所支持的目录和订单 API 来部署应用程序。在部署应用程序的过程中，会创建免费的 Cloudant 服务实例。有关更多信息和条款，请参阅 [Bluemix 目录 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/catalog/services/cloudant-nosql-db/){:new_window}。

|模板 |描述	|
|:----------|:------------------------------|
|[Garage Method 云本机教程工具链 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fcloud-native-toolchain-tutorial){:new_window} 		|此工具链示范 Garage Method 中配备的 DevOps 实践。该工具链已针对持续交付、源代码控制、测试自动化和自动化监视和操作进行了预配置。它随附以 Node.js Express 4 编写的样本应用程序，您可以进行进一步扩展。 		|
|[具有 {{site.data.keyword.DRA_short}} 的微型服务工具链 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Ftoolchain-demo){:new_window} 		|有了此云本机工具链，您可以使用样本来创建包含三个微型服务的网上商店：目录 API、订单 API 和调用这两个 API 的 UI。此工具链已针对持续交付、源代码控制、功能测试、问题跟踪、联机编辑和警报通知进行了预配置。 		|
|[具有 {{site.data.keyword.DRA_short}} 的微型服务工具链 (v2) ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fmicroservices-toolchain-hosted){:new_window} 		|有了此云本机工具链，您可以使用样本来创建包含三个微型服务的网上商店：目录 API、订单 API 和调用这两个 API 的 UI。此工具链已针对持续交付、源代码控制、功能测试、问题跟踪、联机编辑和警报通知进行了预配置。 		|
|[安全容器工具链 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsecure-container-toolchain){:new_window} 		|有了此工具链，您可以开发和部署安全的 Docker 容器应用程序。缺省情况下，该工具链使用样本 Node.js“Hello World”应用程序，但是您可以改为链接到自己的 GitHub 存储库。该工具链已针对具有漏洞顾问程序的持续交付、源代码控制、问题跟踪和联机编辑进行了预配置。 		|
|[简单 Cloud Foundry 工具链 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain){:new_window}		|有了此工具链，您可以开发和部署 Cloud Foundry 应用程序。缺省情况下，此工具链使用样本 Node.js“Hello world”应用程序，但是您可以改为链接到自己的 GitHub 存储库。该工具链已针对持续交付、源代码控制、问题跟踪和联机编辑进行了预配置。 		|
|[简单 Cloud Foundry 工具链	(v2) ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain-hosted){:new_window}	|有了此工具链，您可以开发和部署 Cloud Foundry 应用程序。缺省情况下，此工具链将样本 Node.js“Hello world”应用程序克隆到 IBM 托管的 Git 存储库，然后您可以对其进行修改。该工具链已针对持续交付、源代码控制、问题跟踪和联机编辑进行了预配置。 		|
|[具有 {{site.data.keyword.DRA_short}} 的简单 Cloud Foundry 工具链 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdra-toolchain-demo){:new_window}		|有了此云本机工具链，您可以使用 {{site.data.keyword.DRA_short}} 来设置简单 Cloud Foundry 应用程序部署的检测点。缺省情况下，此工具链使用样本 Node.js Weather 应用程序，或者您可以链接到自己的 GitHub 存储库。 		|
|[简单 Container 工具链 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-container-toolchain){:new_window}		|有了此工具链，您可以开发和部署 Docker 容器应用程序。缺省情况下，该工具链使用样本 Node.js“Hello World”应用程序，但是您可以改为链接到自己的 GitHub 存储库。该工具链已针对持续交付、源代码控制、问题跟踪和联机编辑进行了预配置。 		|
|[具有 IBM UrbanCode Deploy 的 Delivery Insights ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdeliveryinsights-toolchain){:new_window}		|有了此工具链，您可以从 IBM UrbanCode Deploy 查看部署度量值。通过从 {{site.data.keyword.DRA_short}} 的“设置”页面下载并配置 DevOps Connect，启用此工具链以与 IBM UrbanCode Deploy 进行通信。 		|
|[具有 GitHub 和 Jenkins 的部署风险分析 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevopsinsights-toolchain){:new_window}		|有了此工具链，您可以深入了解 Jenkins 流程，以实现持续集成和交付。您可以配置 Jenkins 服务器，以在 Jenkins 运行作业时，将数据发送到 {{site.data.keyword.DRA_short}}。您还可以实施质量检测点，以根据策略阻止部署。您可以在 {{site.data.keyword.DRA_short}} 的“部署风险”仪表板上查看结果。如果您配置 GitHub 存储库以指示 Jenkins 所使用的源存储库，那么可以使用更改可跟踪性。  		|
|[具有 GitHub 和 JIRA 的 Developer Insights 和 Team Dynamic ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevteaminsights-toolchain){:new_window}		|有了此工具链，您可以浏览项目的开发风险并使用社交编码分析，来了解开发人员之间的交互模式。您可以与 GitHub Issues 和（或）JIRA Issues 一起分析 GitHub 源代码。使用 Developer Insights 以识别很容易出错的文件，并查看项目如何符合 DevOps 实践。Team Dynamics 中的社交编码分析可识别团队成员之间的交互级别，以便团队可以修订没有效果的实践。 		|
|[构建自己的工具链 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fempty-toolchain){:new_window}		|此工具链没有预配置的工具。如果您已经熟悉工具链，那么您可以设置自己的工具链。 		|
{: caption="Table 2. Toolchain templates" caption-side="top"}
