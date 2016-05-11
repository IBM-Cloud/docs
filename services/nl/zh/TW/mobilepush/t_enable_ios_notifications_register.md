# 登錄 iOS 應用程式及裝置
{: #enable-push-ios-notifications-register}


應用程式必須向 APNs 登錄才能接收遠端通知，這通常發生在應用程式安裝到裝置上之後。在應用程式接收到 APNs 所產生的裝置記號之後，必須將裝置記號傳回給 Push Notifications Service。

若要登錄 iOS 應用程式及裝置，請執行下列動作：

1. 建立後端應用程式
2. 將記號傳遞至 Push Notifications


##建立後端應用程式

在 Bluemix® 型錄的「樣板」區段中建立後端應用程式，以自動將 Push 服務連結至此應用程式。如果您已建立後端應用程式，請確定將應用程式連結至 Push Notification Service。

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

##將記號傳遞至 Push Notifications

從 APNs 接收到記號之後，將記號傳遞至 Push Notifications，這是 ```registerDevice:withDeviceToken``` 方法的一部分。

###Objective-C

```
//For Objective-C
-( void) application:( UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:( NSData *)deviceToken{

   IMFClient *client = [IMFClient sharedInstance];


 [client initializeWithBackendRoute:@"your-backend-route-here" backendGUID:@"Your-backend-GUID-here"];



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

從 APNs 接收到記號之後，將記號傳遞至 Push Notifications，這是 ```didRegisterForRemoteNotificationsWithDeviceToken``` 方法的一部分。

```
func application (application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   let push =  BMSPushClient.sharedInstance
   push.registerDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
        if error.isEmpty {
            print( "Response during device registration : \(response)")
            print( "status code during device registration : \(statusCode)")
        }
        else{
            print( "Error during device registration \(error) ")
            Print( "Error during device registration \n  - status code: \(statusCode) \n Error :\(error) \n")
        }
    }

}
```
