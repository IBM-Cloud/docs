# iOS アプリケーションとデバイスの登録
{: #enable-push-ios-notifications-register}


アプリケーション (アプリ) でリモート通知を受け取るには、そのアプリケーション (アプリ) を APNs に登録する必要があります。これは、通常アプリをデバイスにインストールした後で行われます。
アプリは、APNs によって生成されたデバイス・トークンを受け取った後、それを Push Notifications Service に送り返す必要があります。


iOS のアプリケーションおよびデバイスを登録するには、以下を行います。

1. バックエンド・アプリケーションの作成
2. プッシュ通知へのトークンの受け渡し


##バックエンド・アプリケーションの作成

Bluemix® カタログの Boilerplates セクションでバックエンド・アプリケーションを作成します。これにより、プッシュ・サービスはこのアプリケーションに自動的にバインドされます。バックエンド・アプリを既に作成済みの場合は、必ずアプリを Push Notification Service にバインドしてください。


###Objective-C

```
	//For Objective-C

	- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	if ([[[UIDevice currentDevice] systemVersion] floatValue] >= 8.0){
[[UIApplication sharedApplication] registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge) categories:categories]];
	    [[UIApplication sharedApplication] registerForRemoteNotifications];
	    }
	    else{
	    [[UIApplication sharedApplication] registerForRemoteNotificationTypes:
	    (UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)];
	    }
	    return YES;
	}
```

###Swift

```
	//For Swift
	func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
let notificationTypes: UIUserNotificationType = UIUserNotificationType.Badge | UIUserNotificationType.Alert | UIUserNotificationType.Sound
		let notificationSettings: UIUserNotificationSettings = UIUserNotificationSettings(forTypes: notificationTypes, categories: categories)
		application.registerUserNotificationSettings(notificationSettings)
		application.registerForRemoteNotifications()
	}
```

##プッシュ通知へのトークンの受け渡し

トークンを APNs から受け取った後で、```registerDevice:withDeviceToken``` メソッドの一部としてそのトークンをプッシュ通知に渡します。

###Objective-C

```
//For Objective-C
-( void) application:( UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:( NSData *)deviceToken{

   IMFClient *client = [IMFClient sharedInstance];


 [client initializeWithBackendRoute: @"your-backend-route-here" backendGUID: @"Your-backend-GUID-here"];


 // get Push instance
IMFPushClient* push = [IMFPushClient sharedInstance];
[push registerDeviceToken:deviceToken completionHandler:^(IMFResponse *response,  NSError *error) {
   if (error){
     [ self  updateMessage:error .description];
  }  else {
    [ self updateMessage:response .responseJson .description];
}
}];
```

###Swift

トークンを APNS から受け取った後で、```didRegisterForRemoteNotificationsWithDeviceToken``` メソッドの一部としてそのトークンをプッシュ通知に渡します。

```
func application (application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   let push =  BMSPushClient.sharedInstance
   push.registerDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
        if error.isEmpty {print( "Response during device registration : \(response)")
            print( "status code during device registration : \(statusCode)")
        }
        else{
            print( "Error during device registration \(error) ")
            Print( "Error during device registration \n  - status code: \(statusCode) \n Error :\(error) \n")
        }
    }

}
```
