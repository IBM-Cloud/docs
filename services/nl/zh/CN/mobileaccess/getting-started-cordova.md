---

copyright:
  years: 2015, 2016
  
---

# 设置 Cordova 插件
{: #getting-started-cordova}

在 Cordova 应用程序中安装 {{site.data.keyword.amashort}} 客户端 SDK，初始化该 SDK，然后对受保护和不受保护的资源发起请求。

## 开始之前
{: #before-you-begin}

- 必须具有受 {{site.data.keyword.amashort}} 服务保护的移动后端的实例。有关如何创建移动后端的更多信息，请参阅[入门](getting-started.html)。

- 创建 Cordova 应用程序或使用现有项目。有关如何设置 Cordova 应用程序的更多信息，请参阅 [Cordova Web 站点](https://cordova.apache.org/)。

## 安装 {{site.data.keyword.amashort}} Cordova 插件
{: #getting-started-cordova-plugin}

{{site.data.keyword.amashort}} Client SDK for Cordova 是一种 Cordova 插件，用于打包本机 {{site.data.keyword.amashort}} 客户端 SDK。它使用 Cordova 命令行界面 (CLI) 和 `npmjs`（Cordova 项目的插件存储库）进行分发。Cordova CLI 会从存储库自动下载插件，并将其提供给 Cordova 应用程序。

1. 将 Android 和 iOS 平台添加到 Cordova 应用程序。在命令行中运行以下一个或两个命令：

	```Bash
	cordova platform add android
	```

	```Bash
	cordova platform add ios
	```

1. 如果添加的是 Android 平台，那么必须将支持的最低 API 级别添加到 Cordova 应用程序的 `config.xml` 文件。打开 `config.xml` 文件，并将以下行添加到 `<platform name="android">` 元素：

	```XML
	<platform name="android">  
		<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
  	<!-- add minimum and target Android API level declaration -->
	</platform>
	```

	*minSdkVersion* 值必须高于 `15`。*targetSdkVersion* 值必须是 Google 中可用的最新 Android SDK。



1. 如果添加的是 iOS 操作系统，请针对目标声明更新 `<platform name="ios">` 元素：

	```XML
	<platform name="ios">
    <preference name="deployment-target" value="8.0"/>
     <!-- add deployment target declaration -->
	</platform>
	```

1. 安装 {{site.data.keyword.amashort}} Cordova 插件：

 	```Bash
	cordova plugin add ibm-mfp-core
	```

1. 针对 Android 和/或 iOS 配置平台。

	* **Android**

		在 Android Studio 中打开项目之前，为避免发生构建错误，请使用命令行界面 (CLI) 构建 Cordova 应用程序。

		```
		cordova build android
		```

	* **iOS**

		为避免发生构建错误，请按如下所示配置 Xcode 项目。

		1. 使用最新版本 Xcode 打开 &lt;*app_name*&gt;/platforms/ios 目录中的 xcode.proj 文件。

		**重要信息：**如果收到消息，提示您“转换为最新 Swift 语法”，请单击“取消”。

		2. 转至**构建设置 > Swift 编译器 - 代码生成 > Objective-C 桥接头**，然后添加以下路径：

			```
			<your_project_name>/Plugins/ibm-mfp-core/Bridging-Header.h
			```

		3. 转至**构建设置 > 链接 > Runpath 搜索路径**，然后添加以下 Frameworks 参数：

			```
			@executable_path/Frameworks
			```

		4. 使用 Xcode 构建并运行应用程序。

1. 通过运行以下命令，验证该插件是否已成功安装：


	```Bash
	cordova plugin list
	```

## 初始化 {{site.data.keyword.amashort}} 客户端插件
{: #getting-started-cordova-initialize}

要使用 {{site.data.keyword.amashort}} 客户端 SDK，您必须通过传递 *applicationGUID* 和 *applicationRoute* 参数来初始化该 SDK。

1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”的主页上，查找您的路径和应用程序 GUID 值。单击应用程序名称，然后单击**移动选项**以显示用于初始化 SDK 的**应用程序路径**和**应用程序 GUID** 值。

3. 将以下调用添加到 `index.js` 文件以初始化 {{site.data.keyword.amashort}} 客户端 SDK。将 *applicationRoute* 和 *applicationGUID* 替换为 {{site.data.keyword.Bluemix_notm}} 仪表板中**移动选项**中的值。

	```JavaScript
	BMSClient.initialize("applicationRoute", "applicationGUID");
	```

## 对移动后端发起请求
{: #getting-started-request}

初始化 {{site.data.keyword.amashort}} 客户端 SDK 后，可以开始对移动后端发起请求。

1. 尝试对新移动后端的受保护端点发送请求。在浏览器中，打开以下 URL：`{applicationRoute}/protected`。例如：


	```
	http://my-mobile-backend.mybluemix.net/protected
	```

	使用 MobileFirst Services Starter 样板创建的移动后端的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护。浏览器中将返回 `Unauthorized` 消息。由于此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问，因此会返回此消息。



1. 使用 Cordova 应用程序对同一端点发起请求。初始化 `BMSClient` 后，添加以下代码：

	```Javascript
	var success = function(data){
	console.log("success", data);
	}

	var failure = function(error){
		console.log("failure", error);
	}

	var request = new MFPRequest("/protected", MFPRequest.GET);

	request.send(success, failure);
	```

1. 请求成功后，将在 LogCat 或 Xcode 控制台（取决于使用的平台）中看到以下输出：

	![图像](images/getting-started-android-success.png)

	## 后续步骤
	{: #next-steps}

	连接到受保护端点时，无需任何凭证。如果需要用户登录到您的应用程序，那么必须配置 Facebook、Google 或定制认证。
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [定制](custom-auth-cordova.html)
