------

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Gestione di notifiche automatiche per iOS
{: #silent-notifications}
Ultimo aggiornamento: 06 dicembre 2016
{: .last-updated}

Le notifiche automatiche non vengono visualizzate sulla schermata del dispositivo. Queste notifiche vengono ricevute dall'applicazione in background, che la attivano per 30 secondi in modo che esegua l'attività in background specificata. Un utente non viene avvisato dell'arrivo della notifica. Per inviare notifiche automatiche per iOS, utilizza l'[API REST](https://mobile.{DomainName}/imfpush/).   

1. Per inviare notifiche automatiche, implementa il seguente metodo nel file `appDelegate.m` nel tuo progetto.

```
//Per Objective C
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
    else
	{
    //Notifica normale
    [[IMFPushAppManager get] notificationReceived:userInfo];
    NSLog(@"Received a normal notification.");
    NSLog(@"userInfo: %@", userInfo.description);
     _appDelegateVC.result.text = userInfo.description;
    handler(UIBackgroundFetchResultNoData);
    }
    //Riuscito
}
```
    {: codeblock}

Per Swift, il valore `contentAvailable` inviato dal server per le notifiche automatiche è uguale a 1.
```
// Per Swift
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
    //Notifica predefinita
           completionHandler(UIBackgroundFetchResult.NoData)
       }
    }
```
	{: codeblock}

