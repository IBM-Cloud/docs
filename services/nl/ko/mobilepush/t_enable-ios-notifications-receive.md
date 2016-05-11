---

copyright:
 years: 2015, 2016

---

# iOS 디바이스에서 푸시 알림 수신
{: #enable-push-ios-notifications-receiving}

iOS 디바이스에서 푸시 알림을 수신합니다. 

##Objective-C
iOS 디바이스에서 푸시 알림을 수신하려면 애플리케이션의 위임자에 다음 Objective-C 메소드를 추가하십시오.

```
// For Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
}
```

##Swift
iOS 디바이스에서 푸시 알림을 수신하려면 애플리케이션의 위임자에 다음 Swift 메소드를 추가하십시오.

```
 // For Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       //UserInfo dictionary will contain data sent from the server
   }
```

