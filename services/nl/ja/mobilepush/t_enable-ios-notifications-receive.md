---

copyright:
 years: 2015, 2016

---

# iOS デバイスでのプッシュ通知の受け取り
{: #enable-push-ios-notifications-receiving}

iOS デバイスでプッシュ通知を受け取ります。

##Objective-C
iOS デバイスでプッシュ通知を受け取るには、アプリケーションのアプリケーション代行に以下の Objective-C メソッドを追加します。

```
// For Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
}
```

##Swift
iOS デバイスでプッシュ通知を受け取るには、アプリケーションのアプリケーション代行に以下の Swift メソッドを追加します。

```
 // For Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       //UserInfo dictionary will contain data sent from the server
   }
```

