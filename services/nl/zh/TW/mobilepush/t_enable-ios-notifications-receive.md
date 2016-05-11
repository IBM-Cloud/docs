---

copyright:
 years: 2015, 2016

---

# 在 iOS 裝置上接收推送通知
{: #enable-push-ios-notifications-receiving}

在 iOS 裝置上接收推送通知。

##Objective-C
若要在 iOS 裝置上接收推送通知，請將下列 Objective-C 方法新增至應用程式的應用程式委派。

```
// For Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
}
```

##Swift
若要在 iOS 裝置上接收推送通知，請將下列 Swift 方法新增至應用程式的應用程式委派。

```
 // For Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       //UserInfo dictionary will contain data sent from the server
   }
```

