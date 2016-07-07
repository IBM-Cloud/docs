---

copyright:
 years: 2015, 2016

---

# Manejo de notificaciones silenciosas para iOS
{: #silent-notifications}

Las notificaciones silenciosas no aparecen en la pantalla del dispositivo. Estas notificaciones se reciben mediante la aplicación en segundo plano, que activa la aplicación durante 30 segundos para realizar la tarea en segundo plano. Puede que el usuario no tenga en cuenta la llegada de la notificación. Para enviar notificaciones silenciosas para iOS, utilice la [API REST](https://mobile.{DomainName}/imfpushrestapidocs/).   

1. Para envair notificaciones push silenciosas, implemente el siguiente método en el archivo `appDelegate.m` del proyecto.


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

Para Swift, el valor `contentAvailable` que envía el servidor
                        para las instalaciones silenciosas es igual a 1.

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

