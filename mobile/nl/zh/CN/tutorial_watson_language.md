---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# 教程 - Watson Language Code Starter
{: #tutorial_watson_language}

{{site.data.keyword.Bluemix}} Mobile Code Starter for Watson Language 显示 Watson 的 Text To Speech 和 Language Translation 服务，并为您提供每个 {{site.data.keyword.Bluemix_notm}} Mobile Services 的集成点。


## 需求
{: #tutorial_requirements}

* [Bluemix ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://bluemix.net "外部链接图标") 帐户
* 从 [Bluemix 目录![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://console.{DomainName}/catalog/ "外部链接图标") 获取的 [Language Translator ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://console.{DomainName}/catalog/services/language-translator/ "外部链接图标") 和 [Text to Speech ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://console.{DomainName}/catalog/services/text-to-speech/ "外部链接图标") 服务实例


## 入门
{: #tutorial_gs}

要快速入门和熟悉运用 Watson Language Code Starter，请遵循以下步骤：

1. 在 {{site.data.keyword.Bluemix_notm}} 中创建 Mobile 仪表板项目。

   1. 从 Mobile 仪表板的**入门**页面中，单击**创建项目**。

      或者，您可以从**项目**页面单击**创建项目**。

   2. 单击**代码入门模板**。

   3. 选择 **Watson Language** 并单击**创建项目**。

   4. 输入项目名称并单击**创建**。

2. 可选：添加 {{site.data.keyword.mobilepushshort}} 功能。

   1. 在**项目概述**页面中，针对 **{{site.data.keyword.mobilepushshort}}** 单击**添加**。

      或者，您可以在 **{{site.data.keyword.mobilepushshort}}** 页面上单击**创建**。

   2. 输入服务名称并单击**创建**。

   3. 对于 iOS，[配置 Apple PushNotification Service ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/services/mobilepush/t_push_provider_ios.html "外部链接图标"){: new_window}。

   4. 对于 Android，[配置 Google 云消息传递 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/services/mobilepush/t_push_provider_android.html "外部链接图标"){: new_window}。
   
3. 可选：添加 Analytics 功能。

   1. 在**项目概述**页面上，针对 **Analytics** 单击**添加**。

      或者，您可以在 **Analytics** 页面上单击**创建**。

   2. 输入服务名称并单击**创建**。
   
   3. 您可以在运行应用程序后关闭**演示模式**，以查看您的分析数据。

   4. 查看 [{{site.data.keyword.mobileanalytics_short}} 入门 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/services/mobileanalytics/index.html "外部链接图标"){: new_window}，以获取配置 Analytics 的更多信息。

4. 可选：添加 Authentication 功能。

   1. 在**项目概述**页面上，针对 **Authentication** 单击**添加**。

      或者，您可以在 **Authentication** 页面上选择**创建**。

   2. 输入服务名称并单击**创建**。
   
   3. 打开 **Authentication**。
   
   4. 选择身份提供者，并输入必需的信息以对其进行配置。只能启用一个身份提供者。

   5. 请参阅 [ Mobile Client Access 入门 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/services/mobileaccess/index.html "外部链接图标"){: new_window}，以获取配置 Authentication 的更多信息。

5. 下载项目。

   1. 单击**代码**并选择首选语言。

   2. 单击**下载代码**。

6. 解压缩归档文件，并在 Markdown 查看器中查看 `README.md` 文件，以完成设置。


## 接下来执行的操作
{: #tutorial_next}

[立即使用！![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://console.{DomainName}/mobile/create-project?starter=512568a1-72db-35c7-b9c4-4f3e3bc89375 "外部链接图标"){: new_window}



### UI 入门模板教程
{: #tutorials_UI}

* [教程 - Store Catalog](tutorial_store_catalog.html)


### 代码入门模板教程
{: #tutorials_Code}

* [教程 - 基本](tutorial.html)
* [教程 - Cloudant Sync](tutorial_cloudant_synd.html)
* [教程 - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [教程 - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [教程 - Weather](tutorial_weather.html)

