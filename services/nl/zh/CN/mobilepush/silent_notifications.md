---

copyright:
 years: 2015, 2016

---

# 处理针对 iOS 的静默通知
{: #silent-notifications}

静默通知不会显示在设备屏幕上。这些通知由应用程序在后台进行接收，这会将应用程序唤醒最多 30 秒来执行指定的后台任务。用户可能并不知道有通知到达。要发送针对 iOS 的静默通知，请使用 [REST API](https://mobile.{DomainName}/imfpushrestapidocs/)。   

1. 要发送静默推送通知，请在项目的 `appDelegate.m` 文件中实施以下方法。


```
//For Objective C
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
{
   NSNumber *contentAvailable = userInfo[@"aps"][@"content-available"];   if([contentAvailable intValue]== 1){
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

对于 Swift，服务器针对静默通知发送的 `contentAvailable` 值等于 1。

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

