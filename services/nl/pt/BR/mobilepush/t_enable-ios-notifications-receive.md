---

copyright:
 years: 2015, 2016

---

# Recebendo notificações push em dispositivos iOS
{: #enable-push-ios-notifications-receiving}

Receba notificações push em dispositivos iOS

##Objective-C
Para receber notificações push em dispositivos iOS, inclua o método
Objective-C a seguir na delegação de seu aplicativo.

```
// For Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//O dicionário userInfo conterá dados enviados do servidor.
}
```

##Swift
Para receber notificações push em dispositivos iOS, inclua o método Swift a seguir
na delegação de seu aplicativo.

```
 // For Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       //UserInfo dictionary will contain data sent from the
server
   }
```

