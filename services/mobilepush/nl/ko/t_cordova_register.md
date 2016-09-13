---

copyright:
 years: 2015, 2016

---

# 디바이스 등록

{: #cordova_register}

디바이스를 푸시 알림 서비스에 등록하려면 등록 메소드를 호출하십시오.

디바이스를 등록하려면 다음 코드 스니펫을 복사하여 Cordova 애플리케이션에 붙여넣으십시오. 

```
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	MFPPush.registerDevice({}, success, failure);
```

## Android
{: #cordova_register_android}
Android에서는 이 설정 매개변수를 사용하지 않습니다. Android 앱만 빌드할 경우에는 공백 오브젝트를 전달하십시오. 예를 들어 다음과 같습니다. 

```
	MFPPush.registerDevice({}, success, failure);
	MFPPush.unregisterDevice(success, failure);
```

##	iOS
{: #cordova_register_ios}
경보, 배지 및 사운드 특성을 사용자 정의하려면 다음의 JavaScript 코드 스니펫을 Cordova 애플리케이션의 웹 파트에 추가하십시오. 

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

JSON.parse를 사용하여 Javascript에서 성공 응답 매개변수의 컨텐츠에 액세스할 수 있습니다.
**var token = JSON.parse(response).token**


사용 가능한 키는 다음과 같습니다. ```token```, ```userId``, ```deviceId``.

다음 JavaScript 코드 스니펫은 Bluemix Mobile Services 클라이언트 SDK를 초기화하고, 푸시 알림 서비스를 사용하여 디바이스를 등록하고, 푸시 알림을 청취하는 방법을 보여줍니다. 이 코드를 Javascript 파일에 넣으십시오. 



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

**onDeviceReady: function()**에서 다음을 수행하십시오. 

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
다음의 Objective-C 코드 스니펫을 애플리케이션 위임 클래스에 추가하십시오. 

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
다음의 Swift 코드 스니펫을 애플리케이션 위임 클래스에 추가하십시오. 

```     
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
// Handle error when failed to register device token with APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
   CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```

##다음 단계
{: #cordova_register_next}

1. 프로젝트를 빌드하고 다음 명령을 사용하여 프로젝트를 실행하십시오. 

	* Android - **cordova build android** 실행 후 **cordova run android** 실행

	* iOS - **cordova build ios** 실행 후 **cordova run ios** 실행
1. [디바이스에서 푸시 알림 수신](t_cordova_receive.html).
