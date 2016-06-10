---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}


#고급 푸시 알림 사용

iOS 배지(badge), 사운드, 추가 JSON 페이로드, 조치 가능 알림, 보류 알림을 구성합니다. 

## 사운드, 페이로드 및 iOS 배지 구성
{: #badge-sound-payload}

iOS 배치, 사운드와 추가 JSON 페이로드를 구성하십시오. 

1. 푸시 알림 대시보드에서 **알림** 탭으로 이동하십시오. 
2. **선택적 필드** 섹션으로 이동하여 다음과 같은 푸시 알림 기능을 구성하십시오.  
	- **사운드 파일** - 모바일 앱의 사운드 파일을 가리키는 문자열을 입력하십시오. 페이로드에서 사용할 사운드 파일의 문자열 이름을 지정하십시오. 
	- **iOS 배지** - iOS 디바이스의 경우 앱 아이콘의 배지로 표시할 숫자입니다.
이 특성을 비워두면 배지가 변경되지 않습니다.
배지를 제거하려면 이 특성의 값을 0으로 설정하십시오. 
	
	


###Android

```
"settings": {

     "gcm" : { 
"sound":"tt.wav",
	  }
	 }  
```
	
	
###iOS

```
"settings": {

     "apns" : { 
"badge": 10,
	      "sound": "tt.wav",
	  }
	}
``` 		
**추가 페이로드** - 이 페이로드는 키-값 쌍일 수 있고 푸시 알림을 사용하여 전송할 JSON 오브젝트여야 합니다. 

```
{"key":"value", "key2":"value2"}
```


## Android 알림 보류 
{: #hold-notifications-android}

애플리케이션이 백그라운드로 전환될 경우 애플리케이션에 전송되는 푸시 알림을 보류하고자 할 수 있습니다. 알림을 보류하려면 푸시 알림을 처리하는 활동의 onPause() 메소드에서 hold() 메소드를 호출하십시오. 

```
@Override
protected void onPause() {
    super.onPause();


    if (push != null) {
push.hold();
    }
} 
```

## iOS 조치 가능 알림 사용  
{: #enable-actionable-notifications-ios}

일반적인 조치 알림과 달리, 조치 가능 알림은 알림 경고 수신 시 앱을 열지 않고 수행할 동작을 선택할 수 있는 프롬프트를 사용자에게 표시합니다. 애플리케이션에서 조치 가능 푸시 알림을 사용하려면 다음 지시사항을 따르십시오. 

1. 사용자 응답 조치를 작성하십시오. 

   Objective-C

	```
	// For Objective-C
	UIMutableUserNotificationAction *acceptAction = [[UIMutableUserNotificationAction alloc] init];
	    acceptAction.identifier = @"ACCEPT_ACTION";
	    acceptAction.title = @"Accept";
	     /* Optional properties
	     acceptAction.destructive = NO;
	  acceptAction.authenticationRequired = NO; */
	  
	  
	 ```
   Swift

	```
	//For Swift
	let acceptAction = UIMutableUserNotificationAction()
	acceptAction.identifier = "ACCEPT_ACTION"
	acceptAction.title = "Accept"
	acceptAction.destructive = false
	acceptAction.authenticationRequired = false
	acceptAction.activationMode = UIUserNotificationActivationMode.Foreground*/
	```
	
	```
	//For Swift
	let declineAction = UIMutableUserNotificationAction()
	declineAction.identifier = "DECLINE_ACTION"
	declineAction.title = "Decline"
	declineAction.destructive = true
	declineAction.authenticationRequired = false
	declineAction.activationMode = UIUserNotificationActivationMode.Background
	```

2. 알림 카테고리를 작성하고 조치를 설정하십시오. 올바른 컨텍스트는 **UIUserNotificationActionContextDefault** 또는 **UIUserNotificationActionContextMinimal**입니다.

	Objective-C

	```
	// For Objective-C
	UIMutableUserNotificationCategory *callCat = [[UIMutableUserNotificationCategory alloc] init];
	    callCat.identifier = @"POLL_CATEGORY";
	    [callCat setActions:@[acceptAction, declineAction] forContext:UIUserNotificationActionContextDefault];
	```    

	Swift

	```
	// For Swift
	let pushCategory = UIMutableUserNotificationCategory()
	pushCategory.identifier = "TODO_CATEGORY"
	pushCategory.setActions([acceptAction, declineAction], forContext: UIUserNotificationActionContext.Default)
	```

1. 알림 설정을 작성하고 이전 단계의 범주를 지정하십시오. 

	Objective-C

	```
	// For Objective-C
	NSSet *categories = [NSSet setWithObjects:callCat, nil];
	```

	Swift

	```
	// For Swift
	let categories = NSSet(array:[pushCategory]);
	```

1. 로컬 또는 원격 알림을 작성하고 카테고리 ID를 지정하십시오. 

	Objective-C

	```
	//For Objective-C


	[[UIApplication sharedApplication] registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge) categories:categories]];


	[[UIApplication sharedApplication] registerForRemoteNotifications];
	```

	Swift

	```
	//For Swift
	let notificationTypes: UIUserNotificationType = UIUserNotificationType.Badge | UIUserNotificationType.Alert | UIUserNotificationType.Sound
	let notificationSettings: UIUserNotificationSettings = UIUserNotificationSettings(forTypes: notificationTypes, categories: categories)

	application.registerUserNotificationSettings(notificationSettings)
	application.registerForRemoteNotifications()
	```
	
## 조치 가능 iOS 알림 처리  
{: #actionable-notifications}

조치 가능 알림이 수신되면 선택한 ID를 기반으로 다음 메소드에 제어가 전달됩니다. 

###Objective-C

```
(void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forRemoteNotification:
(UILocalNotification *)notification completionHandler:(void (^)())completionHandler
{
  NSLog(@"actionable notification received.");
  //must call completion handler when finished
  completionHandler();
}
```

###Swift
 
```
func application(application: UIApplication, handleActionWithIdentifier identifier: String?, forRemoteNotification userInfo: [NSObject : AnyObject], completionHandler: () -> Void) {
      //must call completion handler when finished
      completionHandler()
  }
```    
    
