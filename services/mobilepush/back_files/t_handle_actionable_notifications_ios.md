---

copyright:
 years: 2015, 2016

---

# Handling actionable notifications for iOS
{: #actionable-notifications}


When an actionable notification is received, the control is passed onto the following method based on the identifier chosen.

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
    

