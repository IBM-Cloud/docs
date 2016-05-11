---

copyright:
 years: 2015, 2016

---

# 在 iOS 设备上接收推送通知
{: #enable-push-ios-notifications-receiving}

在 iOS 设备上接收推送通知

##Objective-C
要在 iOS 设备上接收推送通知，请将以下 Objective-C 方法添加到应用程序的应用程序代表中。

```
// For Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
}
```

##Swift
要在 iOS 设备上接收推送通知，请将以下 Swift 方法添加到应用程序的应用程序代表中。

```
 // For Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       //UserInfo dictionary will contain data sent from the server
   }
```

