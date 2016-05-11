---

copyright:
 años: 2015, 2016

---

# Recepción de notificaciones push en dispositivos iOS
{: #enable-push-ios-notifications-receiving}

Recibir notificaciones push en dispositivos iOS.

##Objective-C
Para recibir notificaciones push en dispositivos iOS, añada el método Objective-C siguiente en la aplicación delegada de la aplicación.

```
// For Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
}
```

##Swift
Para recibir notificaciones push en dispositivos iOS, añada el método Swift siguiente a la aplicación delegada de la aplicación.

```
 // For Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       //UserInfo dictionary will contain data sent from the server
   }
```

