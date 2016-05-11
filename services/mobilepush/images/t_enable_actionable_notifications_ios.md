---

copyright:
 years: 2015, 2016

---

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
