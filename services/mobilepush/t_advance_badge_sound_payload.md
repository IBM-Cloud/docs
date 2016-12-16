---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

#Enabling advanced push notifications
Last updated: 15 December 2016
{: .last-updated}

Configure an iOS badge, sound, additional JSON payload, actionable notifications, and holding notifications.

## Configure sound, and payload and iOS badge
{: #badge-sound-payload}

Configure an iOS badge, sound, and additional JSON payload.

1. On the {{site.data.keyword.mobilepushshort}} dashboard, go to the **Notifications** tab.
2. Go to the **Optional Fields** section to configure the {{site.data.keyword.mobilepushshort}} features. 
	- **Sound File** - Enter a string to point to the sound file in your mobile app. In the payload, specify the string name of the sound file to use.
	- **iOS Badge** - For iOS devices, the number to display as the badge of the app icon. If this property is absent, the badge is not changed. To remove the badge, set the value of this property to 0.
	
###Android

Add your sound file in `res/raw` directory of your android application. While sending notification, add the sound file name in the sound field of {{site.data.keyword.mobilepushshort}}.

```
"settings":{
     "gcm":{
     "sound":"tt.wav",
  }
 }  
```
    {: codeblock}	
	
###iOS

```
"settings": {
     "apns" : {
      "badge": 10,
      "sound": "tt.wav",
  }
}
``` 
	{: codeblock}
		
**Additional Payload** - This payload can be any key-value pair and must be a JSON object that you want to send with the {{site.data.keyword.mobilepushshort}}.

```
{"key":"value", "key2":"value2"}
```
	{: codeblock}

## Holding Android notifications 
{: #hold-notifications-android}

When your application goes into background, you might want {{site.data.keyword.mobilepushshort}} to hold back notifications sent to your application. To hold notifications, call the hold() method in the onPause() method of the activity that is handling {{site.data.keyword.mobilepushshort}}.

```
@Override
protected void onPause() {
    super.onPause();
    if (push != null) {
        push.hold();
    }
} 
```
	{: codeblock}
## Enabling iOS actionable notifications  
{: #enable-actionable-notifications-ios}

Unlike traditional {{site.data.keyword.mobilepushshort}}, actionable notifications prompt users to make a selection upon receipt of the notification alert without opening the app. 

Complete the steps to enable actionable {{site.data.keyword.mobilepushshort}} in your application.

1. Create a user response action.
```
//For Swift
let acceptAction = UIMutableUserNotificationAction()
acceptAction.identifier = "ACCEPT_ACTION"
acceptAction.title = "Accept"
acceptAction.destructive = false
acceptAction.authenticationRequired = false
acceptAction.activationMode = UIUserNotificationActivationMode.Foreground
```
	{: codeblock}
```
//For Swift
let declineAction = UIMutableUserNotificationAction()
declineAction.identifier = "DECLINE_ACTION"
declineAction.title = "Decline"
declineAction.destructive = true
declineAction.authenticationRequired = false
declineAction.activationMode = UIUserNotificationActivationMode.Background
```
	{: codeblock}

2. Create the notification category and set an action. **UIUserNotificationActionContextDefault** or **UIUserNotificationActionContextMinimal** are valid contexts.
```
// For Swift
let pushCategory = UIMutableUserNotificationCategory()
pushCategory.identifier = "TODO_CATEGORY"
pushCategory.setActions([acceptAction, declineAction], forContext: UIUserNotificationActionContext.Default)
```
	{: codeblock}

1. Create the notification setting and assign the categories from the earlier step.
```
// For Swift
let categories = NSSet(array:[pushCategory]);
```
	{: codeblock}

1. Create the local or remote notification and assign it the identity of the category.
```
//For Swift
let settings = UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound], categories: categories as? Set<UIUserNotificationCategory>)
  UIApplication.sharedApplication().registerUserNotificationSettings(settings)
  UIApplication.sharedApplication().registerForRemoteNotifications() 
```
	{: codeblock}
	
## Handling actionable iOS notifications  
{: #actionable-notifications}

When an actionable notification is received, the control is passed onto the following method based on the chosen identifier.

 
```
func application(application: UIApplication, handleActionWithIdentifier identifier: String?, forRemoteNotification userInfo: [NSObject : AnyObject], completionHandler: () -> Void) {
      //must call completion handler when finished
      completionHandler()
  }
```    
	{: codeblock}
    
