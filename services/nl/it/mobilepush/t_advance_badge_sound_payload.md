---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}


#Abilitazione delle notifiche di push avanzate

Configura un badge iOS, audio, payload JSON aggiuntivo, notifiche operative e notifiche messe in pausa.

## Configurazione di audio e payload e badge iOS
{: #badge-sound-payload}

Configura un badge, l'audio e del payload JSON aggiuntivo iOS.

1. Nel dashboard Push Notifications, vai alla scheda **Notifications**.
2. Vai alla sezione **Optional Fields** per configurare le seguenti funzioni di notifica di
                    push. 
	- **Sound File** - immetti una stringa per puntare al file audio nella tua applicazione mobile. Nel payload, specifica
                            il nome stringa del file audio da utilizzare.
	- **iOS Badge** - per i dispositivi iOS, il numero da visualizzare come badge dell'icona
                            applicazione. Se questa proprietà
                            non è presente, il badge non viene modificato. Per rimuovere il badge, imposta
                            il valore di questa proprietà su 0.
	
	


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
**Payload aggiuntivo** - questo payload può essere qualsiasi coppia chiave-valore e deve essere un
                            oggetto JSON che vuoi inviare con la notifica di push.

```
{"chiave":"valore", "chiave2":"valore2"}
```


## Messa in pausa delle notifiche Android  
{: #hold-notifications-android}

Quando la tua applicazione va in background, probabilmente vuoi che Push metta in pausa le notifiche inviate alla
                            tua applicazione. Per mettere in pausa le notifiche, richiama il metodo hold() nel metodo onPause() dell'attività che sta gestendo le notifiche di push.

```
@Override
protected void onPause() {
    super.onPause();

    if (push != null) {
        push.hold();
    }
} 
```

## Abilitazione di notifiche operative iOS  
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
	//Per Swift
	let acceptAction = UIMutableUserNotificationAction()
	acceptAction.identifier = "ACCEPT_ACTION"
	acceptAction.title = "Accept"
	acceptAction.destructive = false
	acceptAction.authenticationRequired = false
	acceptAction.activationMode = UIUserNotificationActivationMode.Foreground*/
	```
	
	```
	//Per Swift
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
	
## Gestione di notifiche iOS operative  
{: #actionable-notifications}

Quando viene ricevuta una notifica operativa, il controllo
viene spostato sul seguente metodo in base all'identificativo
scelto.

###Objective-C

```
(void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forRemoteNotification:
(UILocalNotification *)notification completionHandler:(void (^)())completionHandler
{
  NSLog(@"actionable notification received.");
  //è necessario richiamare il gestore del completamente quando finito
  completionHandler();
}
```

###Swift
 
```
func application(application: UIApplication, handleActionWithIdentifier identifier: String?, forRemoteNotification userInfo: [NSObject : AnyObject], completionHandler: () -> Void) {
      //è necessario richiamare il gestore del completamente quando finito
      completionHandler()
  }
```    
    
