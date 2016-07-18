---

copyright:
 years: 2015, 2016

---

# Hintergrundbenachrichtigungen für iOS verarbeiten
{: #silent-notifications}

Hintergrundbenachrichtigungen werden nicht auf dem Gerät angezeigt. Diese Benachrichtigungen werden von der Anwendung im Hintergrund empfangen; dadurch wird die Anwendung für maximal 30 Sekunden aktiviert, um die angegebene Hintergrundtask auszuführen. Der Eingang der Benachrichtigung wird vom Benutzer möglicherweise nicht bemerkt. Verwenden Sie zum Senden von Hintergrundbenachrichtigungen für iOS die [REST-API](https://mobile.{DomainName}/imfpushrestapidocs/).   

1. Wenn Sie Push-Hintergrundbenachrichtigungen senden möchten, implementieren Sie die folgende Methode in der Datei `appDelegate.m` in Ihrem Projekt.


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

Bei Swift ist der Wert für `contentAvailable`, der vom Server für Hintergrundbenachrichtigungen gesendet wird, gleich 1.

```
// For Swift
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

