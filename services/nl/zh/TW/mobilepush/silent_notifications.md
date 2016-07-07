---

copyright:
 years: 2015, 2016

---

# 處理 iOS 的無聲自動通知
{: #silent-notifications}

無聲自動通知不會出現在裝置畫面上。這些通知由應用程式在背景接收，此情況會喚醒應用程式最多達 30 秒，以執行指定的背景作業。使用者可能不知道有通知送達。若要傳送 iOS 的無聲自動通知，請使用 [REST API](https://mobile.{DomainName}/imfpushrestapidocs/)。   

1. 在專案中，若要傳送無聲自動推送通知，請在 `appDelegate.m` 檔案中實作下列方法。


```
//For Objective C
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
{
   NSNumber *contentAvailable = userInfo[@"aps"][@"content-available"];
   if([contentAvailable intValue]== 1){
       [[IMFPushClient sharedInstance] application:application didReceiveRemoteNotification:userInfo];
       
       //Perform background task
       NSLog(@"Received a silent push..");
       NSLog(@"userInfo: %@", userInfo.description);
       _appDelegateVC.result.text = userInfo.description;
       handler(UIBackgroundFetchResultNewData);
   }
   else{
       //Normal Notification
       [[IMFPushAppManager get] notificationReceived:userInfo];
       
       NSLog(@"Received a normal notification.");
       NSLog(@"userInfo: %@", userInfo.description);
       _appDelegateVC.result.text = userInfo.description;
       handler(UIBackgroundFetchResultNoData);
       
   }
   //Success
}
```

若為 Swift，伺服器傳送以進行無聲自動通知的 `contentAvailable` 值，等於 1。

```
//For Swift

func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
let contentAPS = userInfo["aps"] as [NSObject : AnyObject]
       if let contentAvailable = contentAPS["content-available"] as? Int {
           //silent or mixed push
           if contentAvailable == 1 {
               completionHandler(UIBackgroundFetchResult.NewData)
           } else {
               completionHandler(UIBackgroundFetchResult.NoData)
           }
       } else {
//Default notification 
           completionHandler(UIBackgroundFetchResult.NoData)
       }
    }
```

