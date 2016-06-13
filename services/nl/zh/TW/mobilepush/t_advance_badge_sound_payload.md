---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}


#啟用進階推送通知

配置 iOS 徽章、音效、其他 JSON 有效負載、可採取動作的通知，以及保存通知。

## 配置音效、有效負載以及 iOS 徽章
{: #badge-sound-payload}

配置 iOS 徽章、音效及其他 JSON 有效負載。

1. 在 Push Notifications 儀表板上，移至**通知**標籤。
2. 移至**選用欄位**區段，以配置下列推送通知特性。 
	- **音效檔** - 輸入指向行動式應用程式中音效檔的字串。在有效負載中，指定要使用之音效檔的字串名稱。
	- **iOS 徽章** - 對於 iOS 裝置，這是要顯示為應用程式圖示徽章的號碼。如果沒有此內容，則不會變更徽章。若要移除徽章，請將此內容的值設為 0。
	
	


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
**其他有效負載** - 此有效負載可以是任意鍵值組，而且必須是您要與推送通知一起傳送的 JSON 物件。

```
{"key":"value", "key2":"value2"}
```


## 保存 Android 通知 
{: #hold-notifications-android}

在應用程式進入背景時，您可能會想要 Push 先保留傳送給應用程式的通知。若要保留通知，請在處理推送通知之活動的 onPause() 方法中呼叫 hold() 方法。

```
@Override
protected void onPause() {
    super.onPause();

    if (push != null) {
        push.hold();
    }
} 
```

## 啟用可採取動作的 iOS 通知  
{: #enable-actionable-notifications-ios}

和傳統推送通知不同，可採取動作的通知會提示使用者在接收通知警示時做選擇，而不必開啟應用程式。請使用下列指示，在應用程式中啟用可採取動作的推送通知。

1. 建立使用者回應動作。

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

2. 建立通知種類並設定動作。**UIUserNotificationActionContextDefault** 或 **UIUserNotificationActionContextMinimal** 是有效的環境定義。

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

1. 建立通知設定，並指派前一個步驟的種類。

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

1. 建立本端或遠端通知，並為其指派種類身分。

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
	
## 處理可採取動作的 iOS 通知  
{: #actionable-notifications}

接收到可採取動作的通知時，會根據選擇的 ID，將控制權傳遞給下列方法。

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
    
