---

copyright:
 years: 2015, 2016

---

# 在裝置上接收推送通知
{: #cordova_receive}

複製並貼上下列程式碼 Snippet，以在裝置上接收推送通知。

##JavaScript

將下列 JavaScript 程式碼 Snippet 新增至 Cordova 應用程式的 Web 組件。


```
var notification = function(notification){
    // notification is a JSON object.
    alert(notification.message);
};
MFPPush.registerNotificationsCallback(notification);
```

##Android 通知內容

下節列出 Android 通知內容：

* message - 推送通知訊息
* payload - 包含通知有效負載的 JSON 物件


##iOS 通知內容

下節列出 iOS 通知內容：

* message - 推送通知訊息
* payload - 包含通知有效負載的 JSON 物件
* action-loc-key - 此字串用來作為索引鍵，在現行本地化中取得一個本地化字串，以用於右按鈕的標題，取代「檢視」。
* badge - 顯示為應用程式圖示徽章的號碼。如果沒有此內容，則不會變更徽章。若要移除徽章，請將此內容的值設為 0。
* sound - 應用程式組合或者應用程式資料儲存器之 Library/Sounds 資料夾中的音效檔名稱。

##Objective-C

將下列 Objective-C 程式碼 Snippet 新增至應用程式委派類別。

```
// Handle receiving a remote notification
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler {

 [[CDVMFPPush sharedInstance] didReceiveRemoteNotification:userInfo];
}
```

```
// Handle receiving a remote notification on launch
- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

    [[CDVMFPPush sharedInstance] didReceiveRemoteNotificationOnLaunch:launchOptions];
}
```

##Swift

將下列 Swift 程式碼 Snippet 新增至應用程式委派類別。

```
// Handle receiving a remote notification
funcapplication(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: ){

    CDVMFPPush.sharedInstance().didReceiveRemoteNotification(userInfo)
}
```

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {


    CDVMFPPush.sharedInstance().didReceiveRemoteNotificationOnLaunch(launchOptions)
}

```
後續步驟。[傳送基本推送通知](t_send_push_notifications.html)。
