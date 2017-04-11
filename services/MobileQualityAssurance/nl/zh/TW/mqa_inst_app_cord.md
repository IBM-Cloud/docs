---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 对 MQA 安装 Cordova 应用程序（已弃用）
{: #instrumentcord}

要搭配使用 {{site.data.keyword.mqafull}} 和 Cordova 应用程序，必须下载 SDK，并使用命令行界面，进行一些更改，以对其执行安装操作。
{: shortdesc}

您必须具有 {{site.data.keyword.Bluemix}} 帐户并为执行安装操作的应用程序平台正确安装了开发环境版本，才能对应用程序安装 {{site.data.keyword.mqa}}。

要对 {{site.data.keyword.mqa}} 执行安装操作以使用 Cordova 应用程序，请完成以下任务：

1. 将所需许可权和已下载的 SDK 添加到 Cordova 项目。

	1. 打开命令提示符并导航到包含项目文件的目录。

	2. 通过完成以下步骤（根据环境），将 {{site.data.keyword.mqa}} 插件添加到 Cordova 项目：

		**重要信息**：如果您在 iOS 9 上使用 Xcode 7.x，那么您必须在“Xcode 构建”设置中，将“启用位码”设置设为“否”。您可以使用位于 platform\iPhone 文件夹中的 Cordova 项目文件 .xcodeproj 打开 Xcode，以更改此设置。

		* IBM MobileFirst™ Platform Foundation V7.1：

			1. 输入以下命令，以安装 {{site.data.keyword.mqa}} 插件：

				```
				mfp cordova plugin add plugin_location
				```
				{: codeblock}

			其中，*plugin_location* 是解压缩所下载 {{site.data.keyword.mqa}} 插件的目录路径。

			2. 如果您的应用程序在 Android 上运行，请将 `project_name/app_name/platforms/android/custom_rules.xml` 文件重命名为 `custom_rules.xml.bak`。

		* V4.0 之前的 Apache Cordova：
			1. 输入以下命令，以安装 {{site.data.keyword.mqa}} 插件：

				```
				cordova plugin add plugin_location
				```
				{: codeblock}

			其中，*plugin_location* 是解压缩所下载 {{site.data.keyword.mqa}} 插件的目录路径。

			2. 输入以下命令，以添加其他所需插件：

				```
				cordova plugin add cordova-plugin-device
				```
				{: codeblock}

			3. 如果您的应用程序在 Android 上运行，请将 `project_name/app_name/platforms/android/custom_rules.xml` 文件重命名为 `custom_rules_bak.xml`。

		* Apache Cordova V4.0 或更新版本：

			1. 输入以下命令：

				```
				cordova plugin add plugin_location
				```
				{: codeblock}

			其中，*plugin_location* 是解压缩所下载 {{site.data.keyword.mqa}} Cordova 插件的目录路径。

			2. 输入以下命令，以添加其他所需插件：

				```
				cordova plugin add cordova-plugin-device
				```
				{: codeblock}

2. 每次登录都启动新的 {{site.data.keyword.mqa}} 会话。

	1. 打开以下目录中的 `index.js` 文件：`your_project_name\www\js`。

	2. 在 `index.js` 文件的 `onDeviceReady()` 函数中，添加以下函数和参数。将函数置于函数右花括号之前。

	限制：对于已经使用较旧版本的 Cordova 插件，为 Mobile Quality Assurance 执行安装操作的应用程序来说，要使用 Cordova V3.0.18 的 Mobile Quality Assurance 插件中所随附的功能，您必须重新生成并替换应用程序密钥。有关如何重新生成应用程序密钥的更多信息，请参阅“管理应用程序设置”。在 2016 年 2 月之前生成的应用程序密钥可继续在较旧的插件中使用，但是在您将插件升级到 V3.0.18 或更新版本之后即无效。

		```
		MQA.startNewSession(
			{
				mode: "QA",
				// or mode: "MARKET" for production mode.
			android: {
				appKey: "your_MQA_Android_appKey" ,
				notificationsEnabled: true},
			ios: {
				appKey: "your_MQA_iOS_appKey" ,
				screenShotsFromGallery: true,}
			},
			{
			success: function () {console.log("Session
			   Started successfully");},
			error: function (string) { console.log("Session
			   error" + string);}
			}
			);
		```
		{: codeblock}

	3. 继续 [{{site.data.keyword.mqa}} 入门](index.html)中的步骤。



# 相关链接
{: #rellinks notoc}

## 相关链接
{: #general notoc}
* [{{site.data.keyword.mqa}} 入门](index.html){:new_window}
