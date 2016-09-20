---

copyright:
 years: 2015, 2016

---

# 登錄裝置

{: #cordova_register}

若要向 Push Notification Service 登錄裝置，請呼叫 register 方法。

複製下列程式碼 Snippet，並將其貼入 Cordova 應用程式，以登錄裝置。

```
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	MFPPush.registerDevice({}, success, failure);
```

## Android
{: #cordova_register_android}
Android 不使用 settings 參數。如果您只是建置 Android 應用程式，請傳遞空物件；例如：

```
	MFPPush.registerDevice({}, success, failure);
	MFPPush.unregisterDevice(success, failure);
```

##	iOS
{: #cordova_register_ios}
如果您要自訂警示、徽章及音效內容，請將下列 JavaScript 程式碼 Snippet 新增至 Cordova 應用程式的 Web 組件。



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
MFPPush.registerDevice({}, success, failure);```

您可以使用 JSON.parse 存取 JavaScript 中成功回應參數的內容：**var token = JSON.parse(response).token**


可用的索引鍵如下：```token```、```userId`` 及 ```deviceId``。

下列 JavaScript 程式碼 Snippet 顯示如何起始設定 Bluemix Mobile Services Push Client SDK、向 Push Notification Service 登錄裝置，以及接聽推送通知。將此程式碼放入 JavaScript 檔案中。



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

在 **onDeviceReady: function()** 內。

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
將下列 Objective-C 程式碼 Snippet 新增至應用程式委派類別

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
將下列 Swift 程式碼 Snippet 新增至應用程式委派類別。

```     
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
// Handle error when failed to register device token with APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
   CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```

##後續步驟
{: #cordova_register_next}

1. 使用下列指令建置專案，然後執行專案：

	* Android - 依序執行 **cordova build android** 及 **cordova run android**

	* iOS - 依序執行 **cordova build ios** 及 **cordova run ios**
1. [在裝置上接收推送通知](t_cordova_receive.html)。
