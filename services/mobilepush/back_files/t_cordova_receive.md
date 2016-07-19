---

copyright:
 years: 2015, 2016

---

# Receiving push notifications on devices
{: #cordova_receive}

Copy and paste the following code snippets to receive push notifications on devices.

##JavaScript

Add the following JavaScript code snippet to the web part of your Cordova application.


```
var notification = function(notification){
    // notification is a JSON object.
    alert(notification.message);
};
MFPPush.registerNotificationsCallback(notification);
```

##Android notification properties

The following section lists the Android notification properties:

* message - Push notification message
* payload - JSON object containing a notification payload


##iOS notification properties

The following section lists the iOS notification properties:

* message - Push notification message
* payload - JSON object containing a notification payload
action-loc-key - The string is used as a key to get a localized string in the current localization to use for the right button’s title instead of “View".
* badge - The number to display as the badge of the app icon. If this property is absent, the badge is not changed. To remove the badge, set the value of this property to 0.
* sound - The name of a sound file in the app bundle or in the Library/Sounds folder of the app data container.

##Objective-C

Add the following Objective-C code snippets to your application delegate class.

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

Add the following Swift code snippets to your application delegate class.

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
Next Step. [Send basic push notifications](t_send_push_notifications.html).
