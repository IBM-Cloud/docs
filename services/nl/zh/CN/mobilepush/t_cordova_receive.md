---

copyright:
 years: 2015, 2016

---

# 在设备上接收推送通知
{: #cordova_receive}

复制并粘贴以下代码片段，以在设备上接收推送通知。

##JavaScript

将以下 JavaScript 代码片段添加到 Cordova 应用程序的 Web 部分中。


```
var notification = function(notification){
    // notification is a JSON object.
    alert(notification.message);
};
MFPPush.registerNotificationsCallback(notification);
```

##Android 通知属性

以下部分列出了 Android 通知属性：

* message - 推送通知消息
* payload - 包含通知有效内容的 JSON 对象


##iOS 通知属性

以下部分列出了 iOS 通知属性：

* message - 推送通知消息
* payload - 包含通知有效内容的 JSON 对象
* action-loc-key - 此字符串用作键以从当前本地化版本中获取本地化字符串，用于正确按钮的标题，而不是“View”。
* badge - 要显示为应用程序图标角标的数字。如果缺少此属性，那么角标不会改变。要除去角标，请将此属性的值设置为 0。
* sound - 应用程序捆绑包中或应用程序数据容器的 Library/Sounds 文件夹中声音文件的名称。

##Objective-C

将以下 Objective-C 代码片段添加到应用程序代表类中。

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

将以下 Swift 代码片段添加到应用程序代表类中。

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
后续步骤：[发送基本推送通知](t_send_push_notifications.html)。
