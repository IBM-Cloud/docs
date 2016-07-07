---

copyright:
 years: 2015, 2016

---

# iOS의 자동 알림 처리
{: #silent-notifications}

자동 알림은 디바이스 화면에 표시되지 않습니다. 이러한 알림은 애플리케이션에서 백그라운드로 수신되며 애플리케이션이 최대 30초 동안 특정 백그라운드 작업을 수행하도록 지시합니다. 사용자는 알림 도착을 인식하지 못할 수 있습니다. iOS를 위한 자동 알림을 전송하려면 [REST API](https://mobile.{DomainName}/imfpushrestapidocs/)를 사용하십시오.    

1. 자동 푸시 알림을 전송하려면 프로젝트의 `appDelegate.m` 파일에서 다음 메소드를 구현하십시오.


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

Swift의 경우 자동 알림을 위해 서버에서 전송하는 `contentAvailable` 값은 1입니다. 

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

