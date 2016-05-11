---

copyright:
 years: 2015, 2016

---

# iOS의 조치 가능 알림 처리
{: #actionable-notifications}


조치 가능 알림이 수신되면 선택한 ID를 기반으로 다음 메소드에 제어가 전달됩니다. 

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
    

