---

copyright:
 years: 2015, 2016

---

# Gestione di notifiche operative per iOS
{: #actionable-notifications}


Quando viene ricevuta una notifica operativa, il controllo
viene spostato sul seguente metodo in base all'identificativo
scelto.

###Objective-C

```
(void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forRemoteNotification:
(UILocalNotification *)notification completionHandler:(void (^)())completionHandler
{
  NSLog(@"actionable notification received.");
  //è necessario richiamare il gestore del completamente quando finito
  completionHandler();
}
```

###Swift
 
```
func application(application: UIApplication, handleActionWithIdentifier identifier: String?, forRemoteNotification userInfo: [NSObject : AnyObject], completionHandler: () -> Void) {
      //è necessario richiamare il gestore del completamente quando finito
      completionHandler()
  }
```    
    

