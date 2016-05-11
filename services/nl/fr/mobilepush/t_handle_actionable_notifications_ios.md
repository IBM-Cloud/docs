---

Copyright :
  Années : 2015, 2016

---

# Traitement des notifications interactives pour iOS
{: #actionable-notifications}


Lors de la réception d'une notification interactive, le contrôle est
transmis à la méthode suivante en fonction de l'identificateur choisi.

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
    

