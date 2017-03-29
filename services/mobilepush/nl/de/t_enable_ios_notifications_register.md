# iOS-Anwendungen und -Geräte registrieren
{: #enable-push-ios-notifications-register}


Eine Anwendung (App) muss bei APNs registriert werden, um ferne Benachrichtigungen zu
empfangen. Dieser Schritt erfolgt meistens nach der Installation der App auf einem Gerät. Nachdem
das von APNs generierte Gerätetoken von der App empfangen wurde, muss es zurück an
Push Notifications Service geleitet werden.

Führen Sie zum Registrieren von iOs-Anwendungen und -Geräten die folgenden Schritte aus:

1. Back-End-Anwendung erstellen
2. Token an Push Notifications übergeben


##Back-End-Anwendung erstellen

Erstellen Sie eine Back-End-Anwendung im Abschnitt 'Boilerplates' des Bluemix®-Katalogs, mit der der Push-Service automatisch an diese Anwendung gebunden wird. Wenn Sie bereits eine Back-End-App erstellt haben, stellen Sie sicher, dass Sie die App an Push Notifications Service binden.

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

##Token an Push Notifications übergeben

Nachdem das Token von APNs empfangen worden ist, leiten Sie es als Teil der Methode `registerDevice:withDeviceToken` an Push Notifications weiter.

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

Nachdem das Token von APNS empfangen worden ist, leiten Sie es als Teil der Methode `didRegisterForRemoteNotificationsWithDeviceToken` an Push Notifications weiter.

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
