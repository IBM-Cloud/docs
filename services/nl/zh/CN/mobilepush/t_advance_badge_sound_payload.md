---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}


#启用高级推送通知

配置 iOS 角标、声音、其他 JSON 有效内容、可操作通知和暂停通知。

## 配置声音、有效内容和 iOS 角标
{: #badge-sound-payload}

配置 iOS 角标、声音和其他 JSON 有效内容。

1. 在 Push Notifications 仪表板上，转至**通知**选项卡。
2. 转至**可选字段**部分，以配置以下推送通知功能。
 
	- **声音文件** - 输入字符串，以指向移动应用程序中的声音文件。在有效内容中，指定要使用的声音文件的字符串名称。
	- **iOS 角标** - 对于 iOS 设备，要显示为应用程序图标角标的数字。如果缺少此属性，那么角标不会改变。要除去角标，请将此属性的值设置为 0。
	
	


###Android

```
"settings":{
     "gcm":{
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
**其他有效内容** - 此有效内容可以是任何键/值对，但必须为要与推送通知一起发送的 JSON 对象。

```
{"key":"value", "key2":"value2"}
	```


## 暂停 Android 通知 
{: #hold-notifications-android}

应用程序转入后台运行时，您可能希望 Push 暂停发送给应用程序的通知。要暂停通知，请调用处理推送通知的活动的 onPause() 方法中的 hold() 方法。

```
@Override
protected void onPause() {
    super.onPause();


    if (push != null) {
push.hold();
    }
} 
```

## 启用 iOS 可操作通知  
{: #enable-actionable-notifications-ios}

与传统推送通知不同，可操作通知会提示用户在收到通知警报时进行相应的选择，而无需打开应用程序。请使用以下指示信息在应用程序中启用可操作推送通知。

1. 创建用户响应操作。

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

2. 创建通知类别并设置操作。**UIUserNotificationActionContextDefault** 或 **UIUserNotificationActionContextMinimal** 是有效的上下文。

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

1. 创建通知设置并分配前一步中的类别。

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

1. 创建本地或远程通知，并为其分配类别的标识。

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
	
## 处理可操作的 iOS 通知  
{: #actionable-notifications}

收到可操作通知时，会根据所选择的标识将控制权传递到以下方法上。

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
    
