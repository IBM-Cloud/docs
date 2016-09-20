---

copyright:
 years: 2015, 2016

---

# Ricezione di notifiche di push su dispositivi iOS
{: #enable-push-ios-notifications-receiving}

Ricezione di notifiche di push su dispositivi iOS.

##Objective-C
Per ricevere notifiche di push sui dispositivi ioS, aggiungi il seguente metodo Objective-C al delegato applicazione della tua applicazione.

```
// Per Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//il dizionario userInfo conterrà i dati inviati dal server.
}
```

##Swift
Per ricevere notifiche di push sui dispositivi ioS, aggiungi il seguente metodo Swift al delegato applicazione della tua applicazione.

```
 // Per Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       //Il dizionario UserInfo conterrà i dati inviati dal server
   }
```

