# iOS 애플리케이션 및 디바이스 등록
{: #enable-push-ios-notifications-register}


일반적으로 앱이 디바이스에 설치된 후에 발생하는 원격 알림을 수신하려면 APNs에 애플리케이션(앱)을 등록해야 합니다. APNs에 의해 생성된 디바이스 토큰을 애플리케이션에서 수신한 후에는 푸시 알림 서비스에 이를 되돌려 보내야 합니다. 

iOs 애플리케이션 및 디바이스를 등록하려면 다음을 수행하십시오. 

1. 백엔드 애플리케이션 작성
2. 토큰을 푸시 알림에 전달


##백엔드 애플리케이션 작성

Boilerplates 섹션 Bluemix® 카탈로그에서 푸시 서비스를 이 애플리케이션에 자동으로 바인드하는 백엔드 애플리케이션을 작성하십시오. 백엔드 앱을 이미 작성한 경우 앱을 푸시 알림 서비스에 바인드해야 합니다. 

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

##토큰을 푸시 알림에 전달

APNs로부터 토큰이 수신되면 ```registerDevice:withDeviceToken``` 메소드의 일부로 푸시 알림에 토큰을 전달하십시오. 

###Objective-C

```
//For Objective-C
-( void) application:( UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:( NSData *)deviceToken{

   IMFClient *client = [IMFClient sharedInstance];


 [client initializeWithBackendRoute:@"your-backend-route-here" backendGUID:@"Your-backend-GUID-here"];



 // get Push instance
IMFPushClient* push = [IMFPushClient sharedInstance];
[push registerDeviceToken:deviceToken completionHandler:^(IMFResponse *response,  NSError *error) {
   if(error){             

     [ self  updateMessage:error .description];
  }  else {
    [ self updateMessage:response .responseJson .description];
}
}];
```

###Swift

APNS로부터 토큰이 수신되면 ```didRegisterForRemoteNotificationsWithDeviceToken``` 메소드의 일부로 푸시 알림에 토큰을 전달하십시오. 

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
