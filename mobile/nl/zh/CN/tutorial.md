---

copyright:
  years: 2016
lastupdated: "2016-10-21"

---
{:new_window: target="_blank"}

# {{site.data.keyword.visualrecognitionshort}} 代码入门模板端到端教程
{: #tutorial}

以下端到端教程将引导您完成通过 {{site.data.keyword.visualrecognitionshort}}“代码入门模板”创建项目的步骤（包括必须安装的工具）以及在 Xcode 和 Android Studio 中运行入门模板的步骤。


### 安装开发者工具
{: #dev_tools}

确保您已安装[必备开发者工具](get_code.html#prereq-dev-tools){: new_window}。


### 通过 {{site.data.keyword.visualrecognitionshort}}“代码入门模板”创建项目
{: #create_project}

1. 在 {{site.data.keyword.Bluemix}} 中创建 Mobile 仪表板项目。

   1. 从 Mobile 仪表板的**入门**页面中，单击**创建项目**。

      或者，您可以从**项目**页面单击**创建项目**。

   2. 单击**代码入门模板**。

   3. 选择 **Visual Recognition** 并单击**创建项目**。

   4. 输入项目名称。对于本教程，请使用 `VisualRecognitionProject`。
   
   5. 单击**创建**。

2. 可选：添加 Push Notifications 功能。

   1. 在**项目概述**页面上，针对 **Push Notifications** 单击**添加**。

      或者，您可以在 **Push Notifications** 页面上单击**创建**。

   2. 输入服务名称并单击**创建**。

   3. 对于 iOS，[配置 Apple Push Notification 服务](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}。

   4. 对于 Android，[配置 Firebase Cloud Messaging](/docs/services/mobilepush/t_push_provider_android.html){: new_window}。
   
3. 可选：添加 Analytics 功能。

   1. 在**项目概述**页面上，针对 **Analytics** 单击**添加**。

      或者，您可以在 **Analytics** 页面上单击**创建**。

   2. 输入服务名称并单击**创建**。
   
   3. 您可以在运行应用程序后关闭**演示模式**，以查看您的分析数据。
   
   4. 请参阅 [{{site.data.keyword.mobileanalytics_short}} 入门](/docs/services/mobileanalytics/index.html){: new_window}，以获取有关配置 Analytics 的更多信息。
  
4. 可选：添加 Authentication 功能。

   1. 在**项目概述**页面上，针对 **Authentication** 单击**添加**。

      或者，您可以在 **Authentication** 页面上选择**创建**。

   2. 输入服务名称并单击**创建**。
   
   3. 打开 **Authentication**。
   
   4. 选择身份提供者，并输入必需的信息以对其进行配置。只能启用一个身份提供者。

   5. 请参阅 [{{site.data.keyword.amashort}} 入门](/docs/services/mobileaccess/index.html){: new_window}，以获取有关配置 Authentication 的更多信息。

5. 生成项目代码。

   1. 单击**项目概述**页面上的**获取代码**，以选择平台和语言。
   
      或者，您可以在**代码**页面上单击。
      
   2. 对于 iOS，单击 **iOS Swift**。
   
   3. 对于 Android，单击 **Android**。
   
   4. 项目代码完成生成后，单击**下载代码**以下载项目归档。


### 在 Xcode 中运行项目
{: #run_xcode}

1. 解压缩 `VisualRecognitionProject-Swift.zip` 文件。

2. 在 Markdown 查看器中打开 `README.md` 文件，以查看配置项目的步骤。

   1. 创建 [{{site.data.keyword.visualrecognitionshort}}](https://console.{DomainName}/catalog/services/visual-recognition/){: new_window} 服务实例。
   
   2. 打开“终端”并浏览到项目文件夹。
   
      1. 如果需要设置 CocoaPods 存储库，请运行 `pod setup`。
      
      2. 如果需要更新现有 Pods，请运行 `pod update`。
      
      3. 运行 `pod install` 以安装项目所需的 Pods。
      
      4. 运行 `carthage update --platform iOS` 构建依赖关系和框架，以使用 {{site.data.keyword.ibmwatson}} Developer Cloud iOS SDK。
      
   3. 打开 `VisualRecognitionProject.xcworkspace` Xcode 工作空间。
   
   4. 添加 {{site.data.keyword.visualrecognitionshort}} 服务凭证。
   
      1. 从 {{site.data.keyword.visualrecognition}} 服务凭证中复制 `api_key`。
      
      2. 将 `api_key` 粘贴到 `WatsonCredentials.plist` 文件中的 `VisualRecognitionAPIKey` 密钥中。
      
3. 运行应用程序。


### 在 Android Studio 中运行项目
{: #run_studio}

1. 解压缩 `VisualRecognitionProject-Android.zip` 文件。

2. 在 Markdown 查看器中打开 `README.md` 文件，以配置项目。

   1. 创建 [{{site.data.keyword.visualrecognitionshort}}](https://console.{DomainName}/catalog/services/visual-recognition/){: new_window} 服务实例。
   
      如果已经有 {{site.data.keyword.visualrecognitionshort}} 服务实例，请跳过此步骤。
   
   2. 在 Android Studio 中打开 `VisualRecognitionProject-Android` 项目。
   
   4. 添加 {{site.data.keyword.visualrecognitionshort}} 服务凭证。
   
      1. 从 {{site.data.keyword.visualrecognition}} 服务凭证中复制 `api_key`。
      
      2. 将 `api_key` 粘贴到 `res/values/watson_credentials.xml` 文件中的 `watson_visual_recognition_api_key` 密钥中。
      
3. 运行应用程序。


## 接下来执行的操作
{: #what_next}

查看其他教程。


### UI 入门模板教程
{: #tutorials_UI}

* [教程 - Store Catalog](tutorial_store_catalog.html)


### 代码入门模板教程
{: #tutorials_Code}

* [教程 - Watson Language](tutorial_watson_language.html)
* [教程 - Weather](tutorial_weather.html)
