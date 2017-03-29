---

copyright:
 years: 2015, 2016

---

# Réception de notifications push sur des appareils iOS
{: #enable-push-ios-notifications-receiving}

Recevez des notifications push sur des appareils iOS.

##Objective-C
Pour recevoir des notifications push sur des appareils iOS, ajoutez la méthode Objective-C suivante au délégué d'application de votre application :

```
// For Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
}
```

##Swift
Pour recevoir des notifications push sur des appareils iOS, ajoutez la méthode Swift suivante au délégué d'application de votre application :

```
 // For Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       //UserInfo dictionary will contain data sent from the server
   }
```

