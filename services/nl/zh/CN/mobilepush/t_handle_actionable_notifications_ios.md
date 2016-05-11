---

copyright:
 years: 2015, 2016

---

# 处理针对 iOS 的可操作通知
{: #actionable-notifications}


收到可操作通知时，会根据所选择的标识将控制权传递到以下方法上。

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
    

