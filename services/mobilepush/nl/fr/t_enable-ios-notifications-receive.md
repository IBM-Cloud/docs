---

Copyright :
  Années : 2015, 2016

---

# Réception de notifications push sur des périphériques iOS
{: #enable-push-ios-notifications-receiving}

Recevez des notifications push sur des périphériques iOS.

##Objective-C
Pour recevoir des notifications push sur des périphériques iOS, ajoutez la méthode Objective-C suivante au délégué d'application de votre application :

```
// Pour Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
// le dictionnaire userInfo contiendra les données envoyées depuis le serveur
}
```

##Swift
Pour recevoir des notifications push sur des périphériques iOS, ajoutez la méthode Swift suivante au délégué d'application de votre application :

```
 // Pour Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       //Le dictionnaire UserInfo contiendra les données envoyées depuis le serveur
   }
```

