---

copyright:
 years: 2015, 2016

---

# Umsetzbare Benachrichtigungen für iOS verarbeiten
{: #actionable-notifications}


Wenn eine umsetzbare Benachrichtigung empfangen wird, wird die Steuerung basierend auf der ausgewählten Kennung an die folgende Methode weitergeleitet.

###Objective-C

```
(void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forRemoteNotification:
(UILocalNotification *)notification completionHandler:(void (^)())completionHandler
{
  NSLog(@"actionable notification received.");
  //must call completion handler when finished
  completionHandler();
}
```

###Swift
 
```
func application(application: UIApplication, handleActionWithIdentifier identifier: String?, forRemoteNotification userInfo: [NSObject : AnyObject], completionHandler: () -> Void) {
      //must call completion handler when finished
      completionHandler()
  }
```    
    

