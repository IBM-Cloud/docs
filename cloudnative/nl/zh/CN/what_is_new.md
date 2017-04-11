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

# {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} 中的新增功能
{: #what-is-new}


## 最新更新时间：2017 年 3 月
{: #mar-2017}

{{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} 2017 年 3 月的更新引入了以下更改：

   * {{site.data.keyword.Bluemix_notm}} 移动仪表板现在为 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}}。
   * 已重新设计项目创建，以便包含支持 Node.js、Java 和 Swift 的 Web 应用程序、BFF 和微服务服务器模式类型。
   * 与新的和改进的 {{site.data.keyword.appid_full}} 服务集成，为移动和 Web 项目提供认证。
   * 目前，还可以使用 [SDK Generator 插件](sdk_cli.html)生成项目的 SDK。仅可针对移动项目在 {{site.data.keyword.dev_console}} 中生成 SDK。
   * 现在，还可以使用 [{{site.data.keyword.dev_cli_short}}](dev_cli.html) 创建项目。


## 最新更新时间：2017 年 1 月
{: #jan-2017}

{{site.data.keyword.Bluemix_notm}} Mobile 仪表板 2017 年 1 月的更新引进以下更改：

   * 从 1 月 31 开始，已废弃使用 UI 入门模板。通过 UI 入门模板创建的现有项目可以使用到 2017 年 4 月 30 日。有关迁移步骤和删除日期的更多信息，请参阅[废弃声明博客帖子 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/blogs/bluemix/2017/01/bluemix-mobile-dashboard-update/)。
{: deprecated}
   * 现在，可以更新项目入门模板类型而不是删除项目并创建新项目。
   * 现在，可以使用 [Watson Conversation](tutorial_conversation.html) 代码入门模板创建项目。
   * 支持时，现在可以为项目生成 SDK。
   * 现在，可以添加现有的[计算](sdk_compute.html)实例并生成客户端 SDK，以添加到您的项目。


## 最新更新时间：2016 年 12 月
{: #dec-2016}

{{site.data.keyword.Bluemix_notm}} Mobile 仪表板 2016 年 12 月的更新引进以下更改：

   * 现在，可以从项目除去已连接的服务，以便其可删除或在其他项目中复用。 
   * 现在，可以将现有服务添加到项目。
   * 现在，可以在使用代码入门模板时，作为数据源来创建或连接现有 CloudantNoSQL 服务。
   * 支持时，现在可以作为项目的数据源来创建或连接现有 Object Storage 服务。
   * 现在，可以定制您要使用 UI 入门模板创建的应用程序的导航设计。 
   

## 最新更新时间：2016 年 11 月
{: #nov-2016}

{{site.data.keyword.Bluemix_notm}} Mobile 仪表板 2016 年 11 月的更新引进以下更改：

   * 现在，您可以从**代码**页面生成项目的 SDK 工件。
   * Cordova 现在支持“基本代码入门模板”。
   * 现在，您可以在 {{site.data.keyword.mobileanalytics_short}} 的**网络请求**页面中，[报告网络事件 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/services/mobileanalytics/sdk.html#network-requests){: new_window} 并[监视网络请求 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/services/mobileanalytics/app-monitoring.html#monitor-network-requests){: new_window}。
   * 现在，您可以在 {{site.data.keyword.mobileanalytics_short}} 控制台中，[将数据导出到 dashDB ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/services/mobileanalytics/app-monitoring.html#dashdb){: new_window}。


## 最新更新时间：2016 年 10 月
{: #oct-2016}

{{site.data.keyword.Bluemix_notm}} Mobile 仪表板 2016 年 10 月的更新引进以下更改：

   * 现在，您可以直接从仪表板，向项目添加 {{site.data.keyword.mobilepushshort}} 和 Analytics 功能。
   * [代码入门模板](starters.html#Code_Starter)现在可用。
   * 可以向通过“代码入门模板”创建的项目添加 Authentication。
   * 现在支持 Swift。


### Analytics
{: #analytics notoc}

   * 当您添加 Analytics 功能时，默认情况下会启用演示模式。您可以在运行应用程序后关闭演示模式，以查看您的分析。


### UI 构建器
{: #ui_builder notoc}

   * 现在，从项目可以访问 **{{site.data.keyword.mobilepushshort}}** 功能。
   * **项目设置**选项卡已重命名为**设置**选项卡。
   * **认证**选项卡已重命名为**用户访问权**选项卡。


### 代码
{: #code notoc}

   * 生成的适用于 iOS 的 Objective-C 和 Swift 代码现在使用 CocoaPods 来管理依赖关系。这表示您需要安装 CocoaPods。要安装它，请运行 `sudo gem install cocoapods`。安装 CocoaPods 之后，请运行 `pod setup` 以对其进行配置（如果尚未配置的话）。最后，运行 `pod install` 以下载并安装所需的项目依赖关系，然后在 Xcode 中打开 `.xcworkspace` 文件。在已下载代码归档的 `README.md` 文件中，可以找到其他详细信息。有关更多信息，请阅读[必备开发者工具](get_code.html#prereq-dev-tools)。

经常回顾以及时了解新更新。
