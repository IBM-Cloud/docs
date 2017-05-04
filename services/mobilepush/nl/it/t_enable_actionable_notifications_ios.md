---

copyright:
 years: 2015, 2016

---

# Abilitazione di notifiche operative per iOS
{: #enable-actionable-notifications-ios}

A differenza delle notifiche di push tradizionali, le notifiche operative
richiedono agli utenti di effettuare una selezione al momento della ricezione dell'avviso di notifica
senza aprire l'applicazione. Utilizza le seguenti istruzioni
per abilitare le notifiche di push operative nella tua applicazione.

1. Crea un'azione di risposta utente.

	Objective-C

	```
	// Per Objective-C
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

2. Crea la categoria di notifica e imposta un'azione. **UIUserNotificationActionContextDefault** o
                **UIUserNotificationActionContextMinimal** sono
contesti validi.

	Objective-C

	```
	// Per Objective-C
	UIMutableUserNotificationCategory *callCat = [[UIMutableUserNotificationCategory alloc] init];
	    callCat.identifier = @"POLL_CATEGORY";
	    [callCat setActions:@[acceptAction, declineAction] forContext:UIUserNotificationActionContextDefault];
	```    

	Swift

	```
	// Per Swift
	let pushCategory = UIMutableUserNotificationCategory()
	pushCategory.identifier = "TODO_CATEGORY"
	pushCategory.setActions([acceptAction, declineAction], forContext: UIUserNotificationActionContext.Default)
	```

1. Crea l'impostazione di notifica e assegna le categorie
dal passo precedente.

	Objective-C

	```
	// Per Objective-C
	NSSet *categories = [NSSet setWithObjects:callCat, nil];
	```

	Swift

	```
	// Per Swift
	let categories = NSSet(array:[pushCategory]);
	```

1. Crea la notifica locale o remota e assegnale
l'identità della categoria.

	Objective-C

	```
	//Per Objective-C

	[[UIApplication sharedApplication] registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge) categories:categories]];

	[[UIApplication sharedApplication] registerForRemoteNotifications];
	```

	Swift

	```
	//Per Swift
	let notificationTypes: UIUserNotificationType = UIUserNotificationType.Badge | UIUserNotificationType.Alert | UIUserNotificationType.Sound
	let notificationSettings: UIUserNotificationSettings = UIUserNotificationSettings(forTypes: notificationTypes, categories: categories)

	application.registerUserNotificationSettings(notificationSettings)
	application.registerForRemoteNotifications()
	```
