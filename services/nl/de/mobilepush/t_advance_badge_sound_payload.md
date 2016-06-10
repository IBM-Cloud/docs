---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}


#Erweiterte Push-Benachrichtigungen aktivieren

Konfigurieren Sie ein iOS Badge, zusätzliche JSON-Nutzdaten, umsetzbare Benachrichtigungen und Blockierungsnachrichten.

## Audio, Nutzdaten und iOS Badge konfigurieren
{: #badge-sound-payload}

Konfigurieren Sie ein iOS Badge, Audio und zusätzliche JSON-Nutzdaten.

1. Navigieren Sie im Dashboard für Push-Benachrichtigungen zur Registerkarte **Benachrichtigungen**.
2. Konfigurieren Sie im Abschnitt **Optionale Felder** die folgenden Komponenten für Push-Benachrichtigungen: 
	- **Sound File**: Geben Sie eine Zeichenfolge ein, die auf die Audiodatei in Ihrer mobilen App verweist. Geben Sie den Zeichenfolgenamen der zu verwendenden Audiodatei in den Nutzdaten an.
	- **iOS Badge**: Für iOS-Geräte die Nummer, die als Badge für das App-Symbol angezeigt werden soll. Wenn diese Eigenschaft fehlt, wird das Badge nicht geändert. Um das Badge zu entfernen, legen Sie für diese Eigenschaft den Wert 0 fest.
	
	


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
**Zusätzliche Nutzdaten** - Diese Nutzdaten können ein beliebiges Schlüssel/Wert-Paar sein; es muss sich jedoch um ein JSON-Objekt handeln, das Sie mit der Push-Benachrichtigung senden möchten.

```
{"key":"value", "key2":"value2"}
```


## Android-Benachrichtigungen blockieren 
{: #hold-notifications-android}

Wenn Ihre Anwendung in den Hintergrund wechselt, möchten Sie möglicherweise, dass Push Benachrichtigungen blockiert, die an Ihre Anwendung gesendet werden. Zum Blockieren von Benachrichtigungen rufen Sie die Methode 'hold()' in der Methode 'onPause()' der Aktivität auf, die Push-Benachrichtigungen verarbeitet.

```
@Override
protected void onPause() {
    super.onPause();

    if (push != null) {
        push.hold();
    }
} 
```

## Umsetzbare iOS-Benachrichtigungen aktivieren  
{: #enable-actionable-notifications-ios}

Im Gegensatz zu konventionellen Push-Benachrichtigungen werden Benutzer bei umsetzbaren Benachrichtigungen dazu aufgefordert, bei Erhalt des Benachrichtigungsalerts eine Auswahl zu treffen, ohne die App zu öffnen. Gehen Sie nach den folgenden Anweisungen vor, um umsetzbare Benachrichtigungen in Ihrer Anwendung zu aktivieren.

1. Erstellen Sie eine Benutzeraktion.

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

2. Erstellen Sie die Benachrichtigungskategorie und legen Sie eine Aktion fest. **UIUserNotificationActionContextDefault** oder **UIUserNotificationActionContextMinimal** sind gültige Kontexte.

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

1. Erstellen Sie die Benachrichtigungseinstellung und weisen Sie die Kategorien aus dem vorherigen Schritt zu.

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

1. Erstellen Sie die lokale oder ferne Benachrichtigung und weisen Sie ihr die Identität der Kategorie zu.

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
	
## Umsetzbare iOS-Benachrichtigungen verarbeiten  
{: #actionable-notifications}

Wenn eine umsetzbare Benachrichtigung empfangen wird, wird die Steuerung basierend auf der ausgewählten Kennung an die folgende Methode weitergeleitet.

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
    
