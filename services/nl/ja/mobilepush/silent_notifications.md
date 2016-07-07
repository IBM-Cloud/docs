---

copyright:
 years: 2015, 2016

---

# iOS のサイレント通知の処理
{: #silent-notifications}

サイレント通知は、デバイスの画面に表示されません。これらの通知は、アプリケーションがバックグラウンドで受け取ります。その結果、アプリケーションは最大で 30 秒までウェイク状態になり、指定されたバックグラウンド・タスクを実行します。ユーザーは、この通知の着信に気付かない可能性があります。iOS のサイレント通知の送信には、[REST API](https://mobile.{DomainName}/imfpushrestapidocs/) を使用します。   

1. サイレント・プッシュ通知を送信するには、プロジェクトの `appDelegate.m` ファイルで以下のメソッドを実装します。


```
//For Objective C
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
{
   NSNumber *contentAvailable = userInfo[@"aps"][@];
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

Swift では、サイレント通知でサーバーから送信される `contentAvailable` の値は 1 です。


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

