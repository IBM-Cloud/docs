---

copyright:
 years: 2015, 2016

---

# iOS のアクション可能通知の処理
{: #actionable-notifications}


アクション可能通知を受け取ると、選択した ID に基づいて制御が以下のメソッドに渡されます。

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
    

