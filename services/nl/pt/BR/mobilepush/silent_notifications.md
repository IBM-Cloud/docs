---

copyright:
 years: 2015, 2016

---

# Manipulando notificações silenciosas para iOS
{: #silent-notifications}

As notificações silenciosas não aparecem na tela do dispositivo. Essas notificações são recebidas pelo aplicativo no segundo plano, que acorda o aplicativo por até 30 segundos para executar a tarefa em segundo plano especificada. É possível que um usuário não perceba a chegada da notificação. Para enviar notificações silenciosas para iOS, use a [API REST](https://mobile.{DomainName}/imfpushrestapidocs/).   

1. Para enviar notificações push silenciosas, implemente o método a seguir no arquivo `appDelegate.m` em seu projeto.


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

Para Swift, o valor `contentAvailable` que é enviado pelo servidor para notificações silenciosas é igual a 1.

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

