---

copyright:
 years: 2015, 2016

---

# デバイスの登録

{: #cordova_register}

デバイスを Push Notification Service に登録するには、登録メソッドを呼び出します。

デバイスを登録するには、次のコード・スニペットを Cordova アプリケーションにコピーして貼り付けます。


```
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	MFPPush.registerDevice({}, success, failure);
```

## Android
{: #cordova_register_android}
Android では、settings パラメーターを使用しません。Android アプリのみをビルドする場合は、空のオブジェクトを受け渡します。例えば、次のようにします。

```
	MFPPush.registerDevice({}, success, failure);
	MFPPush.unregisterDevice(success, failure);
```

##	iOS
{: #cordova_register_ios}
アラート、バッジ、および音声のプロパティーをカスタマイズする場合は、次の JavaScript コード・スニペットを Cordova アプリケーションの Web パーツに追加します。

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

次のように JSON.parse を使用して、Javascript 内の成功した応答パラメーターの内容にアクセスできます。
**var token = JSON.parse(response).token**


使用可能なキーは、`token`、`userId`、および `deviceId` です。

以下の JavaScript コード・スニペットは、Bluemix Mobile Services クライアント SDK を初期化し、デバイスを Push Notification Service に登録し、プッシュ通知を listen する方法を示しています。このコードを Javascript ファイルに置きます。



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

コードは **onDeviceReady: function()** 内に置きます。

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
アプリケーション代行クラスに次の Objective-C コード・スニペットを追加します。

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
アプリケーション代行クラスに次の Swift コード・スニペットを追加します。

```     
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
// Handle error when failed to register device token with APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
   CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```

##次のステップ
{: #cordova_register_next}

1. プロジェクトをビルドし、以下のコマンドを使用してプロジェクトを実行します。

	* Android - **cordova build android** および **cordova run android**

	* iOS - **cordova build ios** および **cordova run ios**
1. [デバイスでのプッシュ通知の受け取り](t_cordova_receive.html)を行います。
