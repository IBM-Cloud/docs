---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# Configure sound, and payload and iOS badge

{: #badge-sound-payload}

Configure an iOS badge, sound and additional JSON payload.

1. On the Push Notifications dashboard, go to the **Notifications** tab.
2. Go to the **Optional Fields** section to configure the following push notification features. 
	a. **iOS Badge** - For iOS devices, the number to display as the badge of the app icon. If this property is absent, the badge is not changed. To remove the badge, set the value of this property to 0.

	b. **Sound File** - Enter a string to point to the sound file in your mobile app. In the payload, specify the string name of the sound file to use.


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
**Additional Payload** - This payload can be any key-value pair and must be a JSON object that you want to send with the push notification.

```
{"key":"value", "key2":"value2"}
```


# Holding notifications for Android
{: #hold-notifications-android}

When your application goes into background, you probably want Push to hold back notifications that are sent to your application. To hold notifications, call the hold() method in the onPause() method of the activity that is handling push notifications.

```
@Override
protected void onPause() {
    super.onPause();

    if (push != null) {
        push.hold();
    }
} 
```

# Enabling actionable notifications for iOS
{: #enable-actionable-notifications-ios}

Unlike traditional push notifications, actionable notifications prompt users to make a selection upon receipt of the notification alert without opening the app. Use the following instructions to enable actionable push notifications in your application.

1. Create a user response action.

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
	let acceptAction = UIMutableUserNotificationAction()
	acceptAction.identifier = "ACCEPT_ACTION"
	acceptAction.title = "Accept"
	acceptAction.destructive = false
	acceptAction.authenticationRequired = false
	acceptAction.activationMode = UIUserNotificationActivationMode.Foreground*/
	```
	```
	let declineAction = UIMutableUserNotificationAction()
	declineAction.identifier = "DECLINE_ACTION"
	declineAction.title = "Decline"
	declineAction.destructive = true
	declineAction.authenticationRequired = false
	declineAction.activationMode = UIUserNotificationActivationMode.Background
	```

2. Create the notification category and set an action. **UIUserNotificationActionContextDefault** or **UIUserNotificationActionContextMinimal** are valid contexts.

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

1. Create the notification setting and assign the categories from the previous step.

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

1. Create the local or remote notification and assign it the identity of the category.

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

# Handling actionable notifications for iOS
{: #actionable-notifications}


When an actionable notification is received, the control is passed onto the following method based on the identifier chosen.

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
    
