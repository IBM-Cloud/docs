---

copyright:
 years: 2015, 2016

---

# Push-Benachrichtigungen in iOS-Geräten empfangen
{: #enable-push-ios-notifications-receiving}

Empfangen Sie Push-Benachrichtigungen in iOS-Geräten.

## Objective-C
Um Push-Benachrichtigungen in iOS-Geräten zu empfangen, fügen Sie die folgende Objective-C-Methode zum Anwendungs-Delegat Ihrer Anwendung hinzu.

```
// Für Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
}
```

## Swift
Um Push-Benachrichtigungen in iOS-Geräten zu empfangen, fügen Sie die folgende Swift-Methode zum Anwendungs-Delegat Ihrer Anwendung hinzu.

```
 // Für Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       //UserInfo dictionary will contain data sent from the server
   }
```

