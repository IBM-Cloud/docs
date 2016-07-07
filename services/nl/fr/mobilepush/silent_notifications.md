---

copyright:
 years: 2015, 2016

---

# Traitement des notifications silencieuses pour iOS
{: #silent-notifications}

Les notifications silencieuses n'apparaissent pas sur l'écran du
périphérique. Elles sont
reçues par l'application en arrière-plan, qui sort alors de veille pendant une durée maximale de 30 secondes
pour effectuer la tâche d'arrière-plan spécifiée. Un utilisateur peut ne pas
être conscient de l'arrivée de la notification. Pour envoyer des notifications en mode silencieux pour iOS, utilisez l'[API REST](https://mobile.{DomainName}/imfpushrestapidocs/).   

1. Pour envoyer des notifications push en mode silencieux, implémentez la méthode suivante dans le fichier `appDelegate.m` dans votre projet. 


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

Pour Swift, la valeur de `contentAvailable` envoyée par le serveur pour les notifications silencieuses est égale à 1.

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

