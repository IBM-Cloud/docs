---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}


#拡張プッシュ通知の使用可能化

iOS バッジ、音声、追加の JSON ペイロード、アクション可能通知、および保留通知を構成します。

## 音声、ペイロード、および iOS バッジの構成
{: #badge-sound-payload}

iOS のバッジ、音声および追加の JSON ペイロードを構成します。

1. プッシュ通知ダッシュボードで、**「通知」**タブに移動します。
2. **「オプション・フィールド (Optional Fields)」**セクションに移動して、以下のプッシュ通知機能を構成します。
 
	- **音声ファイル (Sound File)** - モバイル・アプリの音声ファイルを指定するストリングを入力します。ペイロードで、使用する音声ファイルのストリング名を指定します。
	- **iOS バッジ (iOS Badge)** - iOS デバイスにアプリ・アイコンのバッジとして表示する数。
このプロパティーがないと、バッジは変更されません。
バッジを削除するには、このプロパティーの値を 0 に設定します。

	
	


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
**追加ペイロード** - このペイロードは、任意のキーと値のペアにすることができますが、プッシュ通知で送信する JSON オブジェクトでなければなりません。

```
{"key":"value", "key2":"value2"}```


## Android 通知の保留  
{: #hold-notifications-android}

アプリケーションがバックグラウンドになる場合、恐らく、アプリケーションに送信された通知を Push が保留するようにする必要があります。通知を保留するには、プッシュ通知を処理しているアクティビティーの onPause() メソッドで hold() メソッドを呼び出します。

```
@Override
protected void onPause() {
    super.onPause();


    if (push != null) {
push.hold();
    }
} 
```

## iOS アクション可能通知の使用可能化  
{: #enable-actionable-notifications-ios}

従来のプッシュ通知とは異なり、アクション可能通知は、通知アラートを受け取る際にアプリを開くことなく選択を行うようにユーザーにプロンプトを出します。アクション可能プッシュ通知をアプリケーションで使用可能にするには、以下の指示に従います。

1. ユーザー応答アクションを作成します。

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

2. 通知カテゴリーを作成し、アクションを設定します。**UIUserNotificationActionContextDefault** または **UIUserNotificationActionContextMinimal** が有効なコンテキストです。

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

1. 通知設定を作成し、前のステップで作成したカテゴリーを割り当てます。

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

1. ローカル通知またはリモート通知を作成し、その通知にカテゴリーの ID を割り当てます。

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
	
## アクション可能 iOS 通知の処理  
{: #actionable-notifications}

アクション可能通知を受け取ると、選択した ID に基づいて制御が以下のメソッドに渡されます。

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
    
