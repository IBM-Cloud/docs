---

copyright:
 years: 2015, 2016

---

# 注册设备

{: #cordova_register}

要向 Push Notification Service 注册设备，请调用 register 方法。

将以下代码片段复制并粘贴到 Cordova 应用程序中，以注册设备。

```
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	MFPPush.registerDevice({}, success, failure);
```

## Android
{: #cordova_register_android}
Android 不使用 settings 参数。如果要仅构建 Android 应用程序，请传递空对象；例如：

```
	MFPPush.registerDevice({}, success, failure);
	MFPPush.unregisterDevice(success, failure);
```

##	iOS
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



##JavaScript
{: #cordova_register_js}

```
MFPPush.registerDevice({}, success, failure);
```

可使用 JSON.parse 访问 JavaScript 中成功响应参数的内容：**var token = JSON.parse(response).token**


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

## Objective-C
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

##Swift
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

1. 使用以下命令构建项目，然后运行项目：

	* Android - 运行 **cordova build android**，然后运行 **cordova run android**

	* iOS - 运行 **cordova build ios**，然后运行 **cordova run ios**
1. [在设备上接收推送通知](t_cordova_receive.html)。
