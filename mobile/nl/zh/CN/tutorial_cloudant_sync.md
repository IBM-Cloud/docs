---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Cloudant 同步代码入门模板端到端教程
{: #tutorial}

以下端到端教程将引导您完成通过“Cloudant 同步代码入门模板”创建项目的步骤（包括必须安装的工具）以及在 Android Studio 中运行入门模板的步骤。


### 安装开发者工具
{: #dev_tools}

请确保您已安装[必备开发者工具![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](get_code.html#prereq-dev-tools "外部链接图标"){: new_window}。


### 通过“Cloudant 同步代码入门模板”创建项目
{: #create_project}

1. 在 {{site.data.keyword.Bluemix}} 中创建 Mobile 仪表板项目。

   1. 从 Mobile 仪表板的**入门**页面中，单击**创建项目**。

      或者，您可以从**项目**页面单击**创建项目**。

   2. 单击**代码入门模板**。

   3. 选择 **Cloudant 同步**并单击**创建项目**。

   4. 输入项目名称。对于本教程，请使用 `CloudantSyncProject`。
   
   5. 单击**创建**。

2. 添加数据功能。您可以创建新的 {{site.data.keyword.cloudant}} 服务实例或添加现有服务实例。

   1. 在**项目概述**页面的**数据**磁贴上，单击**查看**。

      或者，您可以在**数据**页面上，单击**创建**或**添加现有项**，然后单击 **Cloudant NoSQL DB**。
      
   2. 可选：如果选择创建新的服务实例，请输入服务名称，并单击**创建**。

   3. 可选：如果选择添加现有服务实例，请从列表中选择服务实例，并单击**添加现有项**。

   4. 单击服务磁贴中的**菜单**图标，并选择**启动...** 以启动服务实例。

      1. 单击**启动**以启动 {{site.data.keyword.cloudant}} 控制台。

      2. 单击**创建数据库**，输入数据库名称，并单击**创建**。

      3. 单击**所有文档**旁边的 **+** 图标以添加文档。

3. 可选：添加 {{site.data.keyword.mobilepushshort}} 功能。

   1. 在**项目概述**页面中，针对 **{{site.data.keyword.mobilepushshort}}** 单击**添加**。

      或者，您可以在 **{{site.data.keyword.mobilepushshort}}** 页面上单击**创建**。

   2. 输入服务名称并单击**创建**。

   3. 对于 Android，[配置 Firebase 云消息传递 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/services/mobilepush/t_push_provider_android.html "外部链接图标"){: new_window}。
   
4. 可选：添加 Analytics 功能。

   1. 在**项目概述**页面上，针对 **Analytics** 单击**添加**。

      或者，您可以在 **Analytics** 页面上单击**创建**。

   2. 输入服务名称并单击**创建**。
   
   3. 您可以在运行应用程序后关闭**演示模式**，以查看您的分析数据。
   
   4. 查看 [{{site.data.keyword.mobileanalytics_short}} 入门 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/services/mobileanalytics/index.html "外部链接图标"){: new_window}，以获取配置 Analytics 的更多信息。
  
5. 可选：添加 Authentication 功能。

   1. 在**项目概述**页面上，针对 **Authentication** 单击**添加**。

      或者，您可以在 **Authentication** 页面上选择**创建**。

   2. 输入服务名称并单击**创建**。
   
   3. 打开 **Authentication**。
   
   4. 选择身份提供者，并输入必需的信息以对其进行配置。只能启用一个身份提供者。

   5. 请参阅 [{{site.data.keyword.amashort}} 入门 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/services/mobileaccess/index.html "外部链接图标"){: new_window}，以获取配置 Authentication 的更多信息。

6. 生成项目代码。

   1. 单击**项目概述**页面上的**获取代码**，以选择平台和语言。
   
      或者，您可以在**代码**页面上单击。
      
   2. 对于 Android，单击 **Android**。
   
   3. 项目代码完成生成后，单击**下载代码**以下载项目归档。


### 在 Android Studio 中运行 Android 项目
{: #run_android}

1. 解压缩 `CloudantSyncProject-Android.zip` 文件。

2. 在 Markdown 查看器中打开 `README.md` 文件，以配置项目。

   1. 在 Android Studio 中打开 `CloudantSyncProject-Android` 项目。

   2. 添加 Cloudant 凭证。

      1. 从**数据**页面，单击服务磁贴中的**菜单**图标，并选择**启动...** 以启动服务实例。

         1. 单击**启动**以启动 {{site.data.keyword.cloudant}} 控制台。

         2. 单击数据库名称，并单击**许可权**。

         3. 在 `res/values/cloudant_credentials.xml` 文件的 `cloudant_dbname` 字符串中输入数据库名称。

         4. 单击**生成 API 密钥**。

             1. 复制**密钥**值，并将该值粘贴到 `res/values/cloudant_credentials.xml` 文件的 `cloudant_api_key` 字符串中。

             2. 复制**密码**值，并将该值粘贴到 `res/values/cloudant_credentials.xml` 文件的 `cloudant_api_password` 字符串中。

             3. 选择 **_admin** 许可权。
      
3. 运行应用程序。


## 接下来执行的操作
{: #what_next}

查看其他教程。


### UI 入门模板教程
{: #tutorials_UI}

* [教程 - Store Catalog](tutorial_store_catalog.html)


### 代码入门模板教程
{: #tutorials_Code}

* [教程 - 基本](tutorial.html)
* [教程 - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [教程 - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [教程 - Watson Language](tutorial_watson_language.html)
* [教程 - Weather](tutorial_weather.html)
