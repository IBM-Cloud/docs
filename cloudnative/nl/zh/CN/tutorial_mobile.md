---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 移动基本入门模板端到端教程
{: #tutorial}

以下端到端教程将引导您完成通过“移动基本入门模板”创建项目的步骤。这包括安装必备工具以及在 Xcode 和 Android Studio 中运行项目的步骤。

您可以使用基于 Web 的 [{{site.data.keyword.dev_console}}](#create-devex) 或通过命令驱动的 [{{site.data.keyword.dev_cli_notm}}](#create-cli) 来创建项目。

## 安装开发者工具
{: #dev_tools}

确保安装[必备开发者工具 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](get_code.html#prereq-dev-tools){: new_window}。


## 使用 {{site.data.keyword.dev_console}} 创建项目
{: #create-devex}

1. 在 {{site.data.keyword.Bluemix}} 中创建 {{site.data.keyword.dev_console}} 项目。

   1. 在 {{site.data.keyword.dev_console}} 中的[**入门** ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/developer/getting-started/) 页面中，单击**创建项目**。

      或者，您可以从**项目**页面单击**创建项目**。

   2. 选择**移动应用程序**并单击**下一步**。

   3. 选择**基本**并单击**下一步**。

   4. 输入项目名称。对于本教程，请使用 `MobileBasicProject`。

   5. 选择平台。对于本教程，请使用 `Swift`。
   
   6. 单击**创建**。

2. 可选：添加 Authentication 功能。

   1. 在**项目概述**页面上，针对 **Authentication** 单击**添加**。

      或者，可在**功能 > 认证**页面上选择**创建**或**添加现有项**。

   2. 输入服务名称并单击**创建**。
   
   3. 打开 **Authentication**。
   
   4. 选择身份提供者，并输入信息以对其进行配置。只能启用一个身份提供者。
   
   5. 请参阅[配置身份提供者} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/services/appid/identity-providers.html){: new_window}，以获取有关配置认证的更多信息。

3. 可选：添加 Analytics 功能。

   1. 在**项目概述**页面上，针对 **Analytics** 单击**添加**。

      或者，您可以从**功能 > 分析**页面单击**创建**或**添加现有项**。

   2. 输入服务名称并单击**创建**。
   
   3. 您可以在运行应用程序后关闭**演示模式**，以查看您的分析数据。
   
   4. 查看 [{{site.data.keyword.mobileanalytics_short}} 入门 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/services/mobileanalytics/index.html){: new_window}，以获取配置 Analytics 的更多信息。

4. 可选：添加 {{site.data.keyword.mobilepushshort}} 功能。

   1. 在**项目概述**页面中，针对 **{{site.data.keyword.mobilepushshort}}** 单击**添加**。

      或者，您可以从**功能 > {{site.data.keyword.mobilepushshort}}** 页面单击**创建**或**添加现有项**。

   2. 输入服务名称并单击**创建**。

   3. 对于 iOS，[配置 Apple PushNotification Service ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}。

   4. 对于 Android，[配置 Firebase 云消息传递 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/services/mobilepush/t_push_provider_android.html){: new_window}。

5. 可选：添加数据功能。

   1. 在**项目概述**页面上，针对**数据**单击**查看**。

      或者，可以在**数据**页面上选择**创建**。
      
   2. 选择 **{{site.data.keyword.cloudant_short_notm}}** 或 **{{site.data.keyword.objectstorageshort}}**。

   3. 输入服务名称并单击**创建**。

   4. 请参阅 [{{site.data.keyword.cloudant_short_notm}} 入门 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/services/Cloudant/index.html){: new_window}，以获取配置 {{site.data.keyword.cloudant_short_notm}} 的更多信息。

   5. 请参阅 [{{site.data.keyword.objectstorageshort}} 入门 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/services/ObjectStorage/index.html){: new_window}，以获取有关配置 {{site.data.keyword.objectstorageshort}} 的更多信息。

6. 生成项目代码：

   1. 单击**项目概述**页面上的**获取代码**，以选择语言。
   
      或者，您可以在**代码**页面上单击。
      
   2. 单击**生成 Swift**。
   
   3. 生成项目代码完成后，单击**下载 Swift** 以下载项目归档。

7. 开始使用下载的项目：

	1. 解压缩归档文件。
	
	2. 浏览到新项目目录。
	
	3. 使用 {{site.data.keyword.dev_cli_notm}} 以继续。

8. 可选：[更新项目](project_overview_page.html#update_language)以生成新语言。


## 使用 {{site.data.keyword.dev_cli_notm}} 创建项目
{: #create-cli}

1. 确保安装 [{{site.data.keyword.dev_cli_short}}](dev_cli.html)。

2. 在“终端”提示符处，浏览到所选的本地目录并运行以下命令。

	```
	bx dev create
	```
	{: codeblock}
	
3. 在系统提示时提供以下值：

	* 选择模式：2（“移动”）
	* 选择入门模板：1（“基本”）
	* 选择平台：3 (iOS Swift)
	* 输入项目的名称：`MobileBasicProjectCLI`

4. 如果要向项目添加服务，请在问题提示处输入 `y` 并回答其余问题。

5. 成功保存 `MobileBasicProjectCLI` 后，浏览到 `MobileBasicProjectCLI/MobileBasicProjectCLI-Swift` 文件夹。


## 在 Xcode 中运行 Swift 项目
{: #run_swift}

1. 解压缩 `MobileBasicProject-Swift.zip` 文件。

2. 在 Markdown 查看器中打开 `README.md` 文件，以查看配置项目的步骤。

   1. 打开“终端”并浏览到项目文件夹。
   
      1. 如果需要设置 CocoaPods 存储库，请运行 `pod setup`。
      
      2. 如果需要更新现有 Pods，请运行 `pod update`。
      
      3. 运行 `pod install` 以安装项目所需的 Pods。
      
   3. 打开 `BasicProject.xcworkspace` Xcode 工作空间。
      
3. 运行应用程序。


## 在 Xcode 中运行 Cordova 项目
{: #run_cordova_xcode}

1. 解压缩 `MobileBasicProject-Cordova.zip` 文件。

2. 在 Markdown 查看器中打开 `README.md` 文件，以配置项目。

   1. 在 Xcode 中打开 `platforms/ios` 项目。
      
3. 运行应用程序。


## 在 Android Studio 中运行 Cordova 项目
{: #run_cordova_studio}

1. 解压缩 `BasicProject-Cordova.zip` 文件。

2. 在 Markdown 查看器中打开 `README.md` 文件，以配置项目。

   1. 在 Android Studio 中打开 `platforms/android` 项目。
      
3. 运行应用程序。


## 在 Android Studio 中运行 Android 项目
{: #run_android}

1. 解压缩 `MobileBasicProject-Android.zip` 文件。

2. 在 Markdown 查看器中打开 `README.md` 文件，以配置项目。

   1. 在 Android Studio 中打开 `BasicProject-Android` 项目。
      
3. 运行应用程序。
