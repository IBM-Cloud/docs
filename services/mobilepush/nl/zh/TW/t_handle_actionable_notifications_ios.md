---

copyright:
 years: 2015, 2016

---

# 處理 iOS 可採取動作的通知
{: #actionable-notifications}


接收到可採取動作的通知時，會根據選擇的 ID，將控制權傳遞給下列方法。

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
    

