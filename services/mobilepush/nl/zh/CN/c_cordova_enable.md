---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 使 Cordova 应用程序能够接收推送通知
{: #cordova_enable}
上次更新时间：2017 年 1 月 18 日
{: .last-updated}

Cordova 是一种平台，用于通过 JavaScript、CSS 和 HTML 构建混合应用程序。{{site.data.keyword.mobilepushshort}} 服务支持开发基于 Cordova 的 iOS 和 Android 应用程序。

您可以让 Cordova 应用程序具有向您的设备接收推送通知的能力。

## 安装 Cordova 推送插件
{: #cordova_install}

安装并使用客户机推送插件来进一步开发 Cordova 应用程序。这还会安装 Cordova 核心插件，该插件会初始化与 Bluemix 的连接。

### 开始之前

1. 下载最新版本的 Android Studio SDK 和 Xcode。
1. 设置仿真器。对于 Android Studio，请使用支持 Google Play API 的仿真器。
1. 安装 Git 命令行工具。对于 Windows，请确保选择**从 Windows 命令提示符运行 Git** 选项。有关如何下载和安装此工具的更多信息，请参阅 [Git ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://git-scm.com/downloads "外部链接图标"){: new_window}。
1. 安装 Node.js 和 Node 软件包管理器 (NPM) 工具。NPM 命令行工具与 Node.js 捆绑在一起。有关如何下载和安装 Node.js 的更多信息，请参阅 [Node.js ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://nodejs.org/en/download/ "外部链接图标"){: new_window}。
1. 在命令行中，使用 **npm install -g cordova** 命令来安装 Cordova 命令行工具。必须有该工具才能使用 Cordova 推送插件。有关如何安装 Cordova 并设置 Cordova 应用程序的更多信息，请参阅 [Cordova Apache ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cordova.apache.org/#getstarted "外部链接图标"){: new_window}。有关的更多信息，请参阅 Cordova 推送插件[自述文件 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push "外部链接图标"){: new_window}。
1. 切换到要在其中创建 Cordova 应用程序的文件夹，然后运行以下命令来创建 Cordova 应用程序。如果已有 Cordova 应用程序，请转至步骤 3。
```cordova create your_app_name
	cd your_app_name
	```
	{: codeblock}
- 可选：您可以编辑 **config.xml** 文件，然后将 <name> 元素中的应用程序名称更改为所选名称，而不使用缺省 HelloCordova 名称。

确保指定正确的捆绑软件标识。如果指定不正确的捆绑软件标识，那么以下错误消息可能会导致 Xcode。

* 对可执行文件进行签名的权利无效。
* 应用程序的“代码签名权利”文件中指定的权利与供应概要文件中指定的权利不同。要解决此问题，请在 Xcode 或 Cordova 应用程序 **config.xml** 文件中指定正确的捆绑软件标识。

1. 将支持的最低版本 API 或部署目标声明添加到 Cordova 应用程序的 config.xml 文件中。minSdkVersion 值必须高于 15。targetSdkVersion 值必须始终反映出 Google 上可用的最新版本 Android SDK。
	
	* Android - 使用编辑器，打开 **config.xml** 文件并使用最低 SDK 版本和目标 SDK 版本更新 `<platform name="android">` 元素：

	```
	<platform name="android">
    	<preference name="android-minSdkVersion" value="15" />
    	<preference name="android-targetSdkVersion" value="23" />
    	<!-- add minimum and target Android API level declaration -->
	</platform> 
	```
    	{: codeblock}

   * iOS - 使用部署目标声明更新 <platform name="ios"> 元素：

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- add deployment target declaration -->
	</platform>
	```
		{: codeblock}

1. 在 Cordova 命令行界面 (CLI) 中，使用以下命令添加 iOS 和/或 Android 平台：
```
cordova platform add ios
	cordova platform add android
	```
	{: codeblock}

1. 在 Cordova 应用程序根目录中，输入以下命令来安装 Cordova 推送插件：**cordova plugin add bms-push**。根据您所添加的平台，您可能会看到：
```
Installing "bms-push" for android
Installing "bms-push" for ios
```
	{: codeblock}

1. 在 your-app-root-folder 中，使用以下命令来验证 Cordova 核心和推送插件是否成功安装：**cordova plugin list**。根据您所添加的平台，您可能会看到：
```
bms-core <version> "BMSCore"
bms-push <version> "BMSPush" 
```
	{: codeblock}

1. 配置 iOS 开发环境。
2. 使用 Xcode 构建并运行应用程序。
1. 下载 Android 的 Firebase `google-services.json`，并将它们放在 Cordova 项目的根文件夹的 `[your-app-name]/platforms/android 中。
	1. 转至 `[your-app-name]/platforms/android`。
	2. 打开文件 `build.gradle`（路径：平台 > android > build.gradle）。
	3. 在 `build.gradle` 文件中查找 `buildscript` 文本。
	4. 在 classpath 行之后，添加一行 classpath 'com.google.gms:google-services:3.0.0'
	5. 然后查找“dependencies”。选择具有文本 `compile` 且依赖关系结束处的依赖关系，在那之后，添加此行：apply plugin: 'com.google.gms.google-services'。
	6. 准备并构建 Cordova Android 项目。
		```
		cordova prepare android
		cordova build android
		```
			{: codeblock}
	**注**：在 Android Studio 中打开项目之前，先通过 Cordova CLI 构建 Cordova 应用程序。这将帮助您避免构建错误。
## 初始化 Cordova 插件
{: #cordova_initialize}

开始使用 {{site.data.keyword.mobilepushshort}} 服务 Cordova 插件之前，需要通过传递应用程序路径和应用程序 GUID 对其进行初始化。初始化该插件后，可以连接到在 Bluemix“仪表板”中创建的服务器应用程序。 Cordova 插件是 Android 和 iOS 客户机 SDK 的包装程序，可以使 Cordova 应用程序能够与 Bluemix 服务进行通信。

1. 通过将以下代码片段复制并粘贴到主 JavaScript 文件（通常位于 **www/js** 目录下）中来初始化 BMSClient。

```
onDeviceReady: function() {
	    app.receivedEvent('deviceready');
	BMSClient.initialize("YOUR APP REGION");
	var category =  {};
	BMSPush.initialize(appGUID,clientSecret,category);
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	BMSPush.registerDevice({}, success, failure);
	var showNotification = function(notif)
	{
	alert(JSON.stringify(notif));
	};
	BMSPush.registerNotificationsCallback(showNotification);
    } 
```
	{: codeblock}

为应用程序传入区域。提供以下常量：

```
REGION_US_SOUTH // ".ng.bluemix.net";
REGION_UK //".eu-gb.bluemix.net";
REGION_SYDNEY // ".au-syd.bluemix.net";
```

例如：

```
BMSClient.initialize(BMSClient.REGION_US_SOUTH);
```

**注**：如果是使用 Cordova CLI（例如，Cordova create app-name 命令）创建的 Cordova 应用程序，请将此 JavaScript 代码放入 index.js 文件内 onDeviceReady: function() 函数中的 app.receivedEvent 函数之后，以初始化 `BMSClient`。 


## 注册设备
{: #cordova_register}


要向 {{site.data.keyword.mobilepushshort}} 服务注册设备，请调用 register 方法。将以下代码片段复制到 Cordova 应用程序中，以注册设备。

```
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure);
```
	{: codeblock}

以下 JavaScript 代码片段显示如何初始化 Bluemix Mobile Services 客户机 SDK，向 {{site.data.keyword.mobilepushshort}} 服务注册设备以及侦听推送通知。将此代码放入 JavaScript 文件中。

在 **onDeviceReady: function()** 中。

```
onDeviceReady: function() {
     app.receivedEvent('deviceready');
BMSClient.initialize("YOUR APP REGION");
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure); 
 var showNotification = function(notif)
 {
 alert(JSON.stringify(notif));
 };
BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

将以下 Swift 代码片段添加到应用程序代表类中。

```
// Register the device token with Bluemix Push Notification Service
func application(application: UIApplication,
  didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData) {
   CDVBMSPush.sharedInstance().didRegisterForRemoteNotificationsWithDeviceToken(deviceToken)
} 
// Handle error when failed to register device token with APNs
func application(application: UIApplication,
    didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer) {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(error)
} 
```
	{: codeblock}

##后续步骤

{: #cordova_register_next}

使用以下命令构建项目，然后运行项目：

####Android
{: android-next-steps}

```
cordova build android
```
	{: codeblock}

```
cordova run android
```
	{: codeblock}

####iOS
{: ios-next-steps}

```
cordova build ios
```
	{: codeblock}

```
cordova run ios
```
	{: codeblock}

## 在设备上接收推送通知
{: #cordova_receive}

复制以下代码片段，以在设备上接收推送通知。

###JavaScript

将以下 JavaScript 代码片段添加到 Cordova 应用程序的 Web 部分中。
```
var showNotification = function(notif) {
  alert(JSON.stringify(notif));
        };
        BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

###Android 通知属性

以下部分列出了 Android 通知属性：

* **message** - 推送通知消息
* **payload** - 包含通知有效内容的 JSON 对象


###iOS 通知属性

以下部分列出了 iOS 通知属性：

* **message** - 推送通知消息
* **payload** - 包含通知有效内容的 JSON 对象 action-loc-key - 此字符串用作键以从当前本地化版本中获取本地化字符串，用于适当按钮标题，而不是 `View`。
* **badge** - 要显示为应用程序图标角标的数字。如果缺少此属性，那么角标不会改变。要除去角标，请将此属性的值设置为 0。
* **sound** - 应用程序捆绑包中或应用程序数据容器的 Library/Sounds 文件夹中声音文件的名称。


将以下 Swift 代码片段添加到应用程序代表类中。
```
// Handle receiving a remote notification
func application(application: UIApplication,
   didReceiveRemoteNotification userInfo: [NSObject : AnyObject],  fetchCompletionHandler completionHandler: ) {
   CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(userInfo)
}
```
	{: codeblock}

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

    let remoteNotif = launchOptions?[UIApplicationLaunchOptionsKey.remoteNotification] as? NSDictionary
  if remoteNotif != nil {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationOnLaunchWithLaunchOptions(launchOptions)
  }
} 
```
	{: codeblock}

## 发送基本推送通知
{: #push-send-notifications}

开发应用程序后，可以发送基本推送通知。

要发送基本推送通知，请完成以下步骤：

1. 选择**发送通知**，并通过选择**发送至**选项编辑消息。支持的选项有**按标记列出设备**、**设备标识**、**用户标识**、**Android 设备**、**iOS 设备**、**Web 通知**和**所有设备**。
**注**：选择**所有设备**选项时，预订了 {{site.data.keyword.mobilepushshort}} 的所有设备都会收到通知。![“通知”屏幕](images/tag_notification.jpg)

2. 在**消息**字段中，编辑您的消息。根据需要，选择配置可选设置。
3. 单击**发送**。
3. 验证设备是否收到通知。

以下屏幕快照显示了在 Android 和 iOS 设备上前台处理 {{site.data.keyword.mobilepushshort}} 的警报框。


![Android 上的前台推送通知](images/Android_Screenshot.jpg)

![iOS 上的前台推送通知](images/iOS_Screenshot.jpg)

   下图显示 Android 上的后台 {{site.data.keyword.mobilepushshort}}。
 ![Android 上的后台推送通知](images/background.jpg)

## 后续步骤
{: #next_steps_tags}

成功设置基本通知后，可以配置基于标记的通知和高级选项。

将 {{site.data.keyword.mobilepushshort}} 服务功能添加到应用程序中。要使用基于标记的通知，请参阅[基于标记的通知](c_tag_basednotifications.html)。要使用高级通知选项，请参阅[启用高级推送通知](t_advance_badge_sound_payload.html)。
