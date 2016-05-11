---

copyright:
  years: 2015, 2016

---
<!-- Attribute definitions -->
{:codeblock: .codeblock}

# HelloWorld 样本入门
{: #gettingstarted-cordova}
*上次更新时间：2016 年 3 月 17 日*

如果想要从新的 Cordova 应用程序开始操作，可以使用 HelloWorld 应用程序。此应用程序演示了如何在不认证的情况下，从移动应用程序连接到 {{site.data.keyword.Bluemix}} 上的移动后端。该应用程序已经安装有 SDK。准备就绪后，可以获取要在应用程序中使用的特定库。

1. 在 {{site.data.keyword.Bluemix_notm}} 中创建移动后端。

	1. 在 {{site.data.keyword.Bluemix_notm}}“目录”的“样板”部分中，单击 MobileFirst Services Starter。
	1. 输入应用程序的名称和主机，并单击**创建**。
	1. 单击**完成**。

2. 从 GitHub 获取项目。您可以使用 git clone 命令获取项目。从您的计算机打开终端，然后输入以下命令：

	```Bash
	git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld
	```

3. 从项目目录运行以下命令，以添加 Android 和 iOS 平台环境：

	### Android

	```Bash
	cordova platform add android
	```

	### iOS

	```Bash
	cordova platform add ios
	```

4. 使用以下命令添加 Cordova 插件：

	```Bash
	cordova plugin add ibm-mfp-core
	```

5. 配置 HelloWorld 样本。

	* 切换到克隆该项目的目录。
	* 打开 *&lt;your_app_dir&gt;*/www/js/index.js 文件，将 *&lt;APPLICATION_ROUTE&gt;* 和 *&lt;APPLICATION_ID&gt;* 替换为您的 Bluemix 应用程序标识和路径值。

		**注：**确保您的路径安全使用 https 协议。

		```Javascript
		// Bluemix credentials
		route: "<APPLICATION_ROUTE>",
		GUID: "<APPLICATION_GUID>",
		```

6. 为 iOS 配置 Cordova 应用程序。Android 平台不需要额外的配置。

	### iOS
  为避免发生构建错误，请按如下所示配置 Xcode 项目。

	1. 使用最新版本 Xcode 打开 *&lt;app_name&gt;*/platforms/ios 目录中的 `xcode.proj` 文件。

		**重要信息：**如果收到消息，提示您“转换为最新 Swift 语法”，请单击**取消**。

	2. 转至**构建设置 > Swift 编译器 - 代码生成 > Objective-C 桥接头**，然后添加以下路径：

		```
		<your_project_name>/Plugins/ibm-mfp-core/Bridging-Header.h
		```

	3. 转至**构建设置 > 链接 > Runpath 搜索路径**，然后添加以下 Frameworks 参数：

		```
		@executable_path/Frameworks
		```

7. 构建样本并在移动仿真器或设备上运行该样本。

  ### Android
	1. 使用以下命令构建 Cordova 应用程序：

    **重要信息：**在 Android Studio 中打开项目之前，您必须先通过 Cordova 命令行界面 (CLI) 构建 Cordova 应用程序。否则，您将遇到构建错误。

	```Bash
	cordova build android
	```

	2. 在 Android Studio 中运行样本应用程序。

  ### iOS
  1. 在 Xcode 中构建 Cordova 应用程序。

    **提示：**在 Xcode 中构建会为您提供更多选项，如调试和项目配置。

  2. 在 Xcode 中运行样本应用程序。

此时将显示一个视图应用程序，其中含有 **PING BLUEMIX** 按钮。点击该按钮，应用程序将测试客户机到后端 {{site.data.keyword.Bluemix_notm}} 应用程序的连接。应用程序使用您在 `index.js` 文件中指定的应用程序路径测试此连接。


![Hello World 应用程序已成功连接到 Bluemix](images/yayconnected.jpg "图 1. Hello World 应用程序已成功连接到 Bluemix")


从移动应用程序成功连接到 {{site.data.keyword.Bluemix_notm}} 后，将显示消息“恭喜！您已建立连接”。


<!--![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")-->

如果连接失败，将显示错误消息。该消息包含有关错误的更多信息。您可以检查以下各项，对错误进行故障诊断：

- 验证是否正确地粘贴了路径和 GUID 值。
- 查看 Xcode 或 Android 调试日志。
- 在 {{site.data.keyword.Bluemix_notm}} 中检查应用程序的状态。

## 后续步骤：
{: #next}
有关如何获取 SDK 并将其集成到移动应用程序中的信息，请参阅：
* [Mobile Client Access：设置 Cordova 插件](../../services/mobileaccess/getting-started-cordova.html)
* [Push Notifications：设置 Cordova 插件](../../services/mobilepush/enablepush_cordova.html#setup_sdk_cordova)

# 相关链接

## 样本
   * [HelloWorld (Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld)

## sdk
   * [bms-clientsdk-cordova-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

<!--## api
   * [Core API](https://classicdocs.{DomainName}/docs/api/content/api/mobilefirst/cordova/core-api-doc/overview-summary.html)
-->
