# Enregistrements d'applications et de périphériques iOS
{: #enable-push-ios-notifications-register}


Une application doit être enregistrée auprès d'APNs pour pouvoir recevoir des notifications distantes. Cet
enregistrement s'effectue généralement après l'installation de l'application sur un périphérique. Une fois que le jeton de périphérique généré par APNs a
été reçu par l'application, il doit être transmis au service Push Notifications.

Pour enregistrer les applications et les périphériques iOs :

1. Créez une application de back end
2. Transmettez le jeton au service Notification push


##Créez une application de back end

Créez une application de back end dans la section Conteneurs boilerplate du catalogue Bluemix, qui lie automatiquement le service Push à cette application. Si vous avez déjà créé une application de
back end, veillez à lier l'application au service Notification push.

###Objective-C

```
	// Pour Objective-C
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
	//Pour Swift
	func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
		let notificationTypes: UIUserNotificationType = UIUserNotificationType.Badge | UIUserNotificationType.Alert | UIUserNotificationType.Sound
		let notificationSettings: UIUserNotificationSettings = UIUserNotificationSettings(forTypes: notificationTypes, categories: categories)
		application.registerUserNotificationSettings(notificationSettings)
		application.registerForRemoteNotifications()
	}
```

##Transmettez le jeton au service Notification push

Une fois que le jeton envoyé par APNs a été reçu, transmettez-le au service Notification push dans le cadre de la méthode ```registerDevice:withDeviceToken```.

###Objective-C

```
//Pour Objective-C
-( void) application:( UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:( NSData *)deviceToken{

   IMFClient *client = [IMFClient sharedInstance];

 [client initializeWithBackendRoute: @"your-backend-route-here" backendGUID: @"Your-backend-GUID-here"];


 // obtenir une instance Push
IMFPushClient* push = [IMFPushClient sharedInstance];
[push registerDeviceToken:deviceToken completionHandler:^(IMFResponse *response,  NSError *error) {
   if(error) {
     [ self  updateMessage:error .description];
  }  else {
    [ self updateMessage:response .responseJson .description];
}
}];
```

###Swift

Une fois que le jeton envoyé par APNS a été reçu, transmettez-le au service Notification push dans le cadre de la méthode ```didRegisterForRemoteNotificationsWithDeviceToken```.

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
