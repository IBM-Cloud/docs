---

copyright:
 years: 2015, 2016

---

# 使 Cordova 应用程序能够接收推送通知
{: #cordova_enable}

Cordova 是一种平台，用于通过 JavaScript、CSS 和 HTML 构建混合应用程序。{{site.data.keyword.mobilepushshort}} 支持开发基于 Cordova 的 iOS 和 Android 应用程序。

使 Cordova 应用程序能够接收推送通知，并向您的设备发送推送通知。




## 安装 Cordova 推送插件
{: #cordova_install}

安装和使用客户机推送插件来进一步开发 Cordova 应用程序。这还会安装 Cordova 核心插件，该插件会初始化与 Bluemix 的连接。

### 开始之前

1. 下载最新版本的 Android Studio SDK 和 Xcode。
1. 设置仿真器。对于 Android Studio，请使用支持 Google Play API 的仿真器。
1. 安装 Git 命令行工具。对于 Windows，请确保选择**从 Windows 命令提示符运行 Git** 选项。有关如何下载并安装此工具的信息，请参阅 [Git](https://git-scm.com/downloads)。

1. 安装 Node.js 和 Node 软件包管理器 (NPM) 工具。NPM 命令行工具与 Node.js 捆绑在一起。有关如何下载并安装 Node.js 的信息，请参阅 [Node.js](https://nodejs.org/en/download/)。
1. 在命令行中，使用 **npm install -g cordova** 命令来安装 Cordova 命令行工具。必须有该工具才能使用 Cordova 推送插件。有关如何安装 Cordova 和设置 Cordova 应用程序的信息，请参阅 [Cordova Apache](https://cordova.apache.org/#getstarted)。

 **注**：要查看 Cordova 推送插件自述文件，请转至 [https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push)。

1. 切换到要在其中创建 Cordova 应用程序的文件夹，然后运行以下命令来创建 Cordova 应用程序。如果已有 Cordova 应用程序，请转至步骤 3。

 ```
cordova create your_app_name
	cd your_app_name
	```
1. 可选：编辑 **config.xml** 文件，然后将 <name> 元素中的应用程序名称更改为所选名称，而不使用缺省 HelloCordova 名称。

	**注**：确保指定正确的捆绑软件标识。否则，将在 Xcode 中显示以下错误消息：
	* 对可执行文件进行签名的权利无效。
	* 应用程序的“代码签名权利”文件中指定的权利与供应概要文件中指定的权利不同。

	要解决此问题，请在 Xcode 或 Cordova 应用程序 **config.xml** 文件中指定正确的捆绑软件标识。

1. 将支持的最低版本 API 或部署目标声明添加到 Cordova 应用程序的 config.xml 文件中。minSdkVersion 值必须高于 15。targetSdkVersion 值必须始终反映出 Google 上可用的最新版本 Android SDK。
	* **Android** - 使用编辑器打开 config.xml 文件，然后使用最低的目标 SDK 版本更新
```<platform name="android">``` 元素：

	```
	<!-- add deployment target declaration -->
	<platform name="android">  
			  <preference name="android-minSdkVersion" value="15" />
			  <preference name="android-targetSdkVersion" value="23" />
			</platform>
	```
   * **iOS** - 使用部署目标声明更新 <platform name="ios"> 元素：

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- other properties -->
	</ platform>
	```

1. 在 Cordova 命令行界面 (CLI) 中，使用以下命令添加平台：iOS 和/或 Android。

	```
	cordova platform add ios@3.9.0
	cordova platform add android
	```
1. 在 Cordova 应用程序根目录中，输入以下命令来安装 Cordova 推送插件：**cordova plugin add ibm-mfp-push**。

	您会看到类似于以下内容的信息，具体取决于您添加的平台：

	```
	Installing "ibm-mfp-push" for android
	Installing "ibm-mfp-push" for ios
	```
1. 在 *your-app-root-folder* 中，使用以下命令来验证 Cordova 核心和推送插件是否成功安装：**cordova plugin list**。

	您会看到类似于以下内容的信息，具体取决于您添加的平台：

	```
	ibm-mfp-core 1.0.0 "MFPCore"
	ibm-mfp-push 1.0.0 “MFPPush"
	```
1. （仅限 iOS）- 配置 iOS 开发环境。
	a. 使用 Xcode 打开 *your-app-name***/platforms/ios** 目录中的 your-app-name.xcodeproj 文件。

	b. 添加桥接头。转至**构建设置 > Swift 编译器 - 代码生成 > Objective-C 桥接头**，然后添加以下路径：*your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	c. 添加 Frameworks 参数。转至**构建设置 > 链接 > Runpath 搜索路径**，然后添加以下参数：
	```
	@executable_path/Frameworks
	```
	d. 取消注释桥接头中的以下推送导入语句。转至 *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	```
	//#import <IMFPush/IMFPush.h>
	//#import <IMFPush/IMFPushClient.h>
	//#import <IMFPush/IMFResponse+IMFPushCategory.h>
	```
	e. 使用 Xcode 构建并运行应用程序。
1. （仅限 Android）- 使用以下命令来构建 Android 项目：
**cordova build android**。

	**注**：在 Android Studio 中打开项目之前，必须先通过 Cordova CLI 构建 Cordova 应用程序。否则，将遇到构建错误。


## 初始化 Cordova 插件
{: #cordova_initialize}

开始使用 Push Notification Service Cordova 插件之前，需要通过传递应用程序路径和应用程序 GUID 对其进行初始化。 初始化该插件后，可以连接到在 Bluemix“仪表板”中创建的服务器应用程序。 Cordova 插件是 Android 和 iOS 客户机 SDK 的包装程序，可以使 Cordova 应用程序能够与 Bluemix 服务进行通信。

1. 通过将以下代码片段复制并粘贴到主 JavaScript 文件（通常位于 **www/js** 目录下）中来初始化 BMSClient。

	```
	BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	```
1. 修改代码片段以使用 Bluemix 的 Route 和 appGUID 参数。 单击 Bluemix 的“应用程序仪表板”中的**移动选项**链接，以获取应用程序的“路径”和“应用程序 GUID”。 在 ```BMSClient.initialize``` 代码片段中将“路径”和“应用程序 GUID”值作为您的参数。

	**注**：如果是使用 Cordova CLI（例如，Cordova create app-name 命令）创建的 Cordova 应用程序，请将此 JavaScript 代码放入 **index.js** 文件内 ```nDeviceReady: function()``` 函数中的 ```app.receivedEvent`` 函数之后，以初始化 BMS 客户机。

```
onDeviceReady: function() {
    app.receivedEvent('deviceready');
	    BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	    },
	```

## 注册设备
{: #cordova_register}

要向 Push Notification Service 注册设备，请调用 register 方法。

将以下代码片段复制并粘贴到 Cordova 应用程序中，以注册设备。

```
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	MFPPush.registerDevice({}, success, failure);
```

### Android
{: #cordova_register_android}
Android 不使用 settings 参数。如果要仅构建 Android 应用程序，请传递空对象；例如：

```
	MFPPush.registerDevice({}, success, failure);
	MFPPush.unregisterDevice(success, failure);
```

### iOS
{: #cordova_register_ios}
如果想要定制警报、角标和声音属性，请将以下 JavaScript 代码片段添加到 Cordova 应用程序的 Web 部分中。

```
	var settings = {
	   ios: {
	       alert: true,
	       badge: true,
	       sound: true
	   }
	}
	MFPPush.registerDevice(settings, success, failure);
```



### JavaScript
{: #cordova_register_js}

```
MFPPush.registerDevice({}, success, failure);
```

可使用 JSON.parse 访问 JavaScript 中成功响应参数的内容：
**var token = JSON.parse(response).token**


可用键如下所示：```token```、```userId`` 和 ```deviceId``。

以下 JavaScript 代码片段显示如何初始化 Bluemix Mobile Services 推送客户机 SDK，向 Push Notification Service 注册设备以及侦听推送通知。将此代码放入 JavaScript 文件中。



```
//Register device token with Bluemix Push Notification Service
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
  CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
```

```
//Handle error when failed to register device token with APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```

在 **onDeviceReady: function()** 中。

```
onDeviceReady: function() {
     app.receivedEvent('deviceready');
     BMSClient.initialize("https://http://myroute_mybluemix.net","my_appGuid");
     var success = function(message) { console.log("Success: " + message); };
     var failure = function(message) { console.log("Error: " + message); };
     var settings = {
         ios: {
alert: true,
             badge: true,
             sound: true
         }   
     };
     MFPPush.registerDevice(settings, success, failure);
     var notification = function(notif){
         alert (notif.message);
     };
     MFPPush.registerNotificationsCallback(notification);

 }
```

### Objective-C
{: #cordova_register_objective}
将以下 Objective-C 代码片段添加到应用程序代表类中

```
	// Register the device token with Bluemix Push Notification Service
	- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
	  [[CDVMFPPush sharedInstance] didRegisterForRemoteNotifications:deviceToken];
	}
	// Handle error when failed to register device token with APNs
	- (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error {
	   [[CDVMFPPush sharedInstance] didFailToRegisterForRemoteNotificationsWithError:error];
	}
```

###Swift
{: #cordova_register_swift}
将以下 Swift 代码片段添加到应用程序代表类中。

```     
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
// Handle error when failed to register device token with APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
   CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```

##后续步骤

{: #cordova_register_next}

使用以下命令构建项目，然后运行项目：

	* Android - 运行 **cordova build android**，然后运行 **cordova run android**

	* iOS - 运行 **cordova build ios**，然后运行 **cordova run ios**



## 在设备上接收推送通知
{: #cordova_receive}

复制并粘贴以下代码片段，以在设备上接收推送通知。

###JavaScript

将以下 JavaScript 代码片段添加到 Cordova 应用程序的 Web 部分中。


```
var notification = function(notification){
    // notification is a JSON object.
    alert(notification.message);
};
MFPPush.registerNotificationsCallback(notification);
```

###Android 通知属性

以下部分列出了 Android 通知属性：

* message - 推送通知消息
* payload - 包含通知有效内容的 JSON 对象


###iOS 通知属性

以下部分列出了 iOS 通知属性：

* message - 推送通知消息
* payload - 包含通知有效内容的 JSON 对象
* action-loc-key - 此字符串用作键以从当前本地化版本中获取本地化字符串，用于正确按钮的标题，而不是“View”。
* badge - 要显示为应用程序图标角标的数字。如果缺少此属性，那么角标不会改变。要除去角标，请将此属性的值设置为 0。
* sound - 应用程序捆绑包中或应用程序数据容器的 Library/Sounds 文件夹中声音文件的名称。

###Objective-C

将以下 Objective-C 代码片段添加到应用程序代表类中。

```
// Handle receiving a remote notification
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler {

 [[CDVMFPPush sharedInstance] didReceiveRemoteNotification:userInfo];
}
```

```
// Handle receiving a remote notification on launch
- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

    [[CDVMFPPush sharedInstance] didReceiveRemoteNotificationOnLaunch:launchOptions];
}
```

###Swift

将以下 Swift 代码片段添加到应用程序代表类中。

```
// Handle receiving a remote notification
funcapplication(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: ){

    CDVMFPPush.sharedInstance().didReceiveRemoteNotification(userInfo)
}
```

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

    CDVMFPPush.sharedInstance().didReceiveRemoteNotificationOnLaunch(launchOptions)
}

```


{: #push-send-notifications}
## 发送基本推送通知


开发应用程序后，可以发送基本推送通知（不使用标记、角标、其他有效内容或声音文件）。


发送基本推送通知。

1. 在**选择受众**中，选择以下某个受众：**所有设备**，或者按平台选择：**仅限 iOS 设备**或**仅限 Android 设备**。

	**注**：选择**所有设备**选项时，预订了推送通知的所有设备都会收到您的通知。

	![“通知”屏幕](images/tag_notification.jpg)

2. 在**创建通知**中，输入消息，然后单击**发送**。
3. 验证设备是否收到通知。

	以下屏幕快照显示了在 Android 和 iOS 设备上前台处理推送通知的警报框。

	![Android 上的前台推送通知](images/Android_Screenshot.jpg)

	![iOS 上的前台推送通知](images/iOS_Screenshot.jpg)

	以下屏幕快照显示了 Android 后台的推送通知。
 ![Android 上的后台推送通知](images/background.jpg)



## 后续步骤
{: #next_steps_tags}

成功设置基本通知后，可以配置基于标记的通知和高级选项。

将这些 Push Notifications Service 功能添加到应用程序中。要使用基于标记的通知，请参阅[基于标记的通知](c_tag_basednotifications.html)。要使用高级通知选项，请参阅[高级推送通知](t_advance_notifications.html)。
