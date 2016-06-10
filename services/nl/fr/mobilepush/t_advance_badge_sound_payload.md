---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}


#Activation des notifications push avancées

Configurez un badge iOS, un son, un contenu JSON supplémentaire, des notifications interactives et la conservation des notifications.

## Configuration d'un son, d'un contenu et d'un badge iOS
{: #badge-sound-payload}

Configurez un badge iOS, un son et un contenu JSON supplémentaire.

1. Dans le tableau de bord Push Notifications, accédez à l'onglet **Notifications**.
2. Accédez à la section des **zones facultatives** pour configurer les fonctions de notification push ci-après. 
	- **Fichier son** - Entrez une chaîne pour pointer vers le fichier son dans votre application mobile. Dans le contenu, spécifiez le nom de
chaîne du fichier son à utiliser.
	- **Badge iOS** - Pour les périphériques iOS, numéro à afficher comme badge de l'icône d'application. Si cette propriété manque, le badge n'est pas changé. Pour supprimer le badge, associez cette propriété à la valeur 0.
	
	


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
**Contenu supplémentaire** - Ce contenu peut être représenté par n'importe quelle paire clé-valeur et doit être un objet JSON que
vous voulez envoyer avec la notification push.

```
{"clé":"valeur", "clé2":"valeur2"}
```


## Conservation des notifications Android 
{: #hold-notifications-android}

Lorsque votre application passe en arrière-plan, il peut être judicieux que Push conserve les notifications qui lui sont envoyées. Pour conserver des notifications, appelez la méthode hold() dans la méthode onPause() de l'activité qui traite les notifications push.

```
@Override
protected void onPause() {
    super.onPause();

    if (push != null) {
        push.hold();
    }
} 
```

## Activations des notifications iOS interactives  
{: #enable-actionable-notifications-ios}

A la différence des notifications push traditionnelles, les notifications
interactives invitent les utilisateurs à effectuer une sélection lorsqu'ils
reçoivent l'alerte de notification sans ouvrir l'application. Utilisez les
instructions ci-après pour activer les notifications push interactives dans
votre application.

1. Créez une réponse utilisateur.

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

2. Créez une catégorie de notification et définissez une action. **UIUserNotificationActionContextDefault** ou
**UIUserNotificationActionContextMinimal** sont des contextes
valides.

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

1. Créez le paramètre de notification et affectez les catégories de l'étape
précédente.

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

1. Créez la notification locale ou éloignée et affectez-lui l'identité de la
catégorie.

	Objective-C

	```
	// Pour Objective-C

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
	
## Traitement des notifications iOS interactives  
{: #actionable-notifications}

Lors de la réception d'une notification interactive, le contrôle est
transmis à la méthode suivante en fonction de l'identificateur choisi.

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
    
