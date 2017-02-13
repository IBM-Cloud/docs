---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 设置 Cordova 插件
{: #getting-started-cordova}

使用 {{site.data.keyword.amafull}} 客户端 SDK 安装 Cordova 客户端应用程序。在 Android (Java) 或 iOS 代码（使用 Swift SDK 和相关头文件的 ObjectiveC）中初始化授权管理器。初始化该客户端，然后从 WebView 对受保护和不受保护的资源发起请求。


{:shortdesc}

## 开始之前
{: #before-you-begin}
您必须具有：

* {{site.data.keyword.Bluemix_notm}} 应用程序的实例。有关如何创建 {{site.data.keyword.Bluemix_notm}} 后端应用程序的更多信息，请参阅[入门](index.html)。
* {{site.data.keyword.amafull}} 服务的实例。
* 后端应用程序的 URL（**应用程序路径**）。您将需要此值来向后端应用程序的受保护端点发送请求。
* **TenantID** 值。在 {{site.data.keyword.amashort}}“仪表板”中打开服务。单击**移动选项**按钮。`tenantId`（也称为 `appGUID`）值会显示在**应用程序 GUID/TenantId** 字段中。您将需要此值来初始化授权管理器。
* {{site.data.keyword.Bluemix_notm}} **区域**。您可以在**头像**图标 ![“头像”图标](images/face.jpg "“头像”图标") 旁边的头中找到当前 {{site.data.keyword.Bluemix_notm}} 区域。显示的区域值应为以下某个值：`US South`、`United Kingdom` 或 `Sydney`，并对应于 WebView Javascript 代码中需要的 SDK 值：`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_UK` 或 `BMSClient.REGION_SYDNEY`。您将需要此值来初始化 {{site.data.keyword.amashort}} 客户端。
* Cordova 应用程序或现有项目。有关如何设置 Cordova 应用程序的更多信息，请参阅 [Cordova Web 站点![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cordova.apache.org/ " 外部链接图标"){: new_window}。

## 安装 {{site.data.keyword.amashort}} Cordova 插件
{: #getting-started-cordova-plugin}

针对 Cordova 的 {{site.data.keyword.amashort}} 客户端 SDK 是一种 Cordova 插件，用于打包本机 {{site.data.keyword.amashort}} 客户端 SDK。它使用 Cordova 命令行界面 (CLI) 和 `npmjs`（Cordova 项目的插件存储库）进行分发。Cordova CLI 会从存储库自动下载插件，并将其提供给 Cordova 应用程序。

1. 将 Android 和/或 iOS 平台添加到 Cordova 应用程序。在命令行中运行以下一个或两个命令：

	###Android
	{: #install-cordova-android}

	```
	cordova platform add android
	```
	{: codeblock}

	###iOS
	{: #install-cordova-ios}

	```Bash
	cordova platform add ios
	```
	{: codeblock}

2. 如果添加的是 Android 平台，那么必须将支持的最低 API 级别添加到 Cordova 应用程序的 `config.xml` 文件。打开 `config.xml` 文件，并将以下行添加到 `<platform name="android">` 元素：

	```XML
	<platform name="android">  
		<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
  	<!-- add minimum and target Android API level declaration -->
	</platform>
	```
	{: codeblock}

	*minSdkVersion* 值必须不低于 `15`。请参阅 [Android 平台指南 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cordova.apache.org/docs/en/latest/guide/platforms/android/ "外部链接图标"){: new_window} 以及时了解 Android SDK 受支援的 *targetSdkVersion*。

3. 如果添加的是 iOS 操作系统，请针对目标声明更新 `<platform name="ios">` 元素：

	```XML
	<platform name="ios">
		<preference name="deployment-target" value="8.0"/>
		<!-- add deployment target declaration -->
	 </platform>
	```
	{: codeblock}

4. 安装 {{site.data.keyword.amashort}} Cordova 插件：

 	```Bash
	cordova plugin add bms-core
	```
	{: codeblock}

5. 针对 Android 和/或 iOS 配置平台。

	####Android
	{: #cordova-android}

	在 Android Studio 中打开项目之前，为避免发生构建错误，请使用命令行界面 (CLI) 构建 Cordova 应用程序。

	```Bash
	cordova build android
	```
	{: codeblock}

	####iOS
	{: #cordova-ios}

	按如下所示配置 Xcode 项目。

	1. 使用最新版本 Xcode 打开 `<app_name>/platforms/ios` 目录中的 `xcode.proj` 文件。

		**重要信息：**如果您收到消息，提示您转换到最新 Swift 语法，请单击**取消**。

	2. 使用 Xcode 构建并运行应用程序。

	**注**：运行 `cordova build ios` 时您可能会收到以下错误。导致此问题的原因是依赖关系插件中存在错误，此问题在[问题 12 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/blakgeek/cordova-plugin-cocoapods-support/issues/12 "外部链接图标"){: new_window} 中进行跟踪。您仍可以通过模拟器或设备在 Xcode 中运行 iOS 项目。

	```
	xcodebuild: error: Unable to find a destination matching the provided destination specifier:
			{ platform:iOS Simulator }

		Missing required device specifier option.
		The device type “iOS Simulator” requires that either “name” or “id” be specified.
		Please supply either “name” or “id”.
	```

6. 通过运行以下命令，验证该插件是否已成功安装：


	```Bash
	cordova plugin list
	```
	{: codeblock}

7. 通过在**功能**选项卡中将**密钥链共享**切换为`开启`来启用 iOS 的密钥链共享。

8. 通过在**构建设置** > **打包**选项卡中将**定义模块**切换为`是`来启用 iOS 的**定义模块**。


## 在 Cordova WebView 中初始化 {{site.data.keyword.amashort}} 客户端 (Javascript)
{: #getting-started-cordova-initialize}

要使用 {{site.data.keyword.amashort}} 客户端 SDK，必须通过传递 `applicationBluemixRegion` 来初始化该 SDK。

将以下调用添加到 `index.js` 文件以初始化 {{site.data.keyword.amashort}} 客户端 SDK。

```JavaScript
BMSClient.initialize(<applicationBluemixRegion>);
```
{: codeblock}

**注：**将 `<applicationBluemixRegion>` 替换为托管 {{site.data.keyword.Bluemix_notm}} 服务的区域；请参阅[开始之前](#before-you-begin)。

##通过本机代码初始化 {{site.data.keyword.amashort}} 授权管理器
{: #initializing-auth-manager}

为了使用 `BMSAuthorizationManager`，您将需要添加以下代码片段。以下本机代码使用 {{site.data.keyword.amashort}} 服务 `tenantId` 初始化 `BMSAuthorizationManager`（请参阅[开始之前](#before-you-begin)）。

### Android (Java)

在 `MainActivity.java` 文件的 `OnCreate` 方法中，将该代码添加到 `loadUrl` 前面。
```Java
MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),"<tenantId>");
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
```
{: codeblock}
### iOS (Objective C)
根据 Xcode 的版本，在 `AppDelegate.m` 中添加授权管理器初始化。

```Objective-C
  #import "<your_module_name>-Swift.h"
  [CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];
```
{: codeblock}

**注：**导入的头文件名由合并到字符串 `-Swift.h` 的模块名称构成，例如，如果模块名称为 `Cordova`，那么 import 行应该为 `#import "Cordova-Swift.h"` 。要查找模块名称，请转至 `构建设置` > `打包` > `产品模块名称`。将 `<tenantId>` 替换为租户标识（请参阅[开始之前](#before-you-begin)）。


## 对移动后端服务发起请求
{: #getting-started-request}

初始化 {{site.data.keyword.amashort}} 客户端 SDK 后，可以开始对移动后端服务发起请求。

1. 尝试对移动后端应用程序的受保护端点发送请求。在浏览器中，打开以下 URL：`{applicationRoute}/protected`（例如：`http://my-mobile-backend.mybluemix.net/protected`）。

	使用 MobileFirst Services Starter 样板创建的移动后端应用程序的 `/protected` 端点通过 {{site.data.keyword.amashort}} 进行保护。浏览器中将返回 `Unauthorized` 消息。由于此端点只能由安装了 {{site.data.keyword.amashort}} 客户端 SDK 的移动应用程序进行访问，因此会返回此消息。



2. 使用 Cordova 应用程序对同一端点发起请求。初始化 `BMSClient` 后，添加以下代码：

	```Javascript
	var success = function(data){
	 console.log("success", data);
	 }

	 var failure = function(error){
	 console.log("failure", error);
	 }

	 var request = new BMSRequest("<your route>/protected", BMSRequest.GET);

	 request.send(success, failure);
	```
	{: codeblock}

3. 请求成功后，将在 LogCat 或 Xcode 控制台（取决于使用的平台）中看到以下输出：

	![成功消息](images/getting-started-android-success.png)

	## 后续步骤
	{: #next-steps}

	连接到受保护端点时，无需任何凭证。如果需要用户登录到您的应用程序，那么必须配置 Facebook、Google 或定制认证。
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [定制](custom-auth-cordova.html)
