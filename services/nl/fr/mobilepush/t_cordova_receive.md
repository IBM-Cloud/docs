---

Copyright :
  Années : 2015, 2016

---

# Réception de notifications push sur les périphériques
{: #cordova_receive}

Copiez et collez les fragments de code ci-après pour recevoir des notifications push sur les périphériques.

##JavaScript

Ajoutez le fragment de code JavaScript suivant à la partie Web de votre application Cordova :


```
var notification = function(notification){
    // notification est un objet JSON.
    alert(notification.message);
};
MFPPush.registerNotificationsCallback(notification);
```

##Propriétés de notification Android

La section suivante répertorie les propriétés de notification Android :

* message - Message de notification push
* payload - Objet JSON comportant un contenu de notification


##Propriétés de notification iOS

La section suivante répertorie les propriétés de notification iOS :

* message - Message de notification push
* payload - Objet JSON comportant un contenu de notification
action-loc-key - Chaîne utilisée comme clé pour obtenir une chaîne localisée à l'emplacement en cours, à utiliser comme titre de bouton approprié à la place de "View".
* badge - Numéro à afficher comme badge de l'icône d'application. Si cette propriété manque, le badge n'est pas changé. Pour supprimer le badge, associez cette propriété à la valeur 0.
* sound - Nom d'un fichier son dans le regroupement d'applications ou dans le dossier Library/Sounds du conteneur des données d'application.

##Objective-C

Ajoutez les fragments de code Objective-C suivants à la classe de votre délégué d'application :

```
// Traitez la réception d'une notification distante
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler {

 [[CDVMFPPush sharedInstance] didReceiveRemoteNotification:userInfo];
}
```

```
// Traitez la réception d'une notification distante lors du lancement
- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

    [[CDVMFPPush sharedInstance] didReceiveRemoteNotificationOnLaunch:launchOptions];
}
```

##Swift

Ajoutez les fragments de code Swift suivants à la classe de votre délégué d'application :

```
// Traitez la réception d'une notification distante
funcapplication(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: ){

    CDVMFPPush.sharedInstance().didReceiveRemoteNotification(userInfo)
}
```

```
// Traitez la réception d'une notification distante lors du lancement
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

    CDVMFPPush.sharedInstance().didReceiveRemoteNotificationOnLaunch(launchOptions)
}

```
Etape suivante. [Envoyez des notifications push de base](t_send_push_notifications.html).
