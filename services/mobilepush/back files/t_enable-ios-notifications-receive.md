---

copyright:
 years: 2015, 2016

---

# Receiving push notifications on iOS devices
{: #enable-push-ios-notifications-receiving}

Receive push notifications on iOS devices.

##Objective-C
To receive push notifications on iOS devices, add the following Objective-C method to the application delegate of your application.

```
// For Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
}
```

##Swift
To receive push notifications on iOS devices, add the following Swift method to the application delegate of your application.

```
 // For Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       //UserInfo dictionary will contain data sent from the server
   }
```

