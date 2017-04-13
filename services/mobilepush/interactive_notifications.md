---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Interactive and silent notifications  
{: #interactive-notifications}
Last updated: 03 March 2017
{: .last-updated}

Interactive notifications enable users to respond to a notification without opening the application. When an interactive notification arrives, the device shows the action buttons along with the notification message. Interactive notifications are supported on iOS devices with version 8 or later. For interactive notifications sent to iOS devices that are earlier than version 8, the notification actions are not displayed.

## Sending interactive notifications
{: #send_interactive_notifications}

Interactive notification can be sent by using the Push dashboard or by using the [REST API documentation](t_restapi.html).

From the {{site.data.keyword.mobilepushshort}} console: 

1. On the notification tab in Push dashboard, click **Send Notification**. 
2. Choose your notification recipients and click **Next**. 
3. In the compose notification page, interactive push can be sent by setting the Type to either Default or Mixed and specifying the Category value under Advanced Options tab. To configure the category value on the client, check **Handling interactive {{site.data.keyword.mobilepushshort}}** in native iOS application section.

## Handling interactive notifications on an iOS application
{: #send_interactive_notifications_ios}

### Swift
{: #send_interactive_notifications_ios_swift}

Complete the following steps to receive interactive notifications:

1. Enable the application capability to perform background tasks on receiving the remote notifications. 
1. Initialize the `BMSPush` SDK with your action category.
	```
	let myBMSClient = BMSClient.sharedInstance
	myBMSClient.initialize(bluemixRegion: BMSClient.Region.usSouth)
	let push =  BMSPushClient.sharedInstance
    let actionOne = BMSPushNotificationAction(identifierName: "FIRST", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
   	let actionTwo = BMSPushNotificationAction(identifierName: "SECOND", buttonTitle: "Reject", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
   	let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
   	let notifOptions = BMSPushClientOptions(categoryName: [category])
	push.initializeWithAppGUID(appGUID: "YOUR_APP_GUID", clientSecret:"YOUR_APP_CLIENT_SECRET", options: notifOptions)
	```
		{: codeblock}

1. Implement the new callback method on AppDelegate:
	```
	 func userNotificationCenter(_ center: UNUserNotificationCenter,
       didReceive response: UNNotificationResponse,
       withCompletionHandler completionHandler: @escaping () -> Void) {
            switch response.actionIdentifier {
		    case "FIRST":
		      print("FIRST")
		    case "SECOND":
		      print("SECOND")  
		    default:
		      print("Unknown action")
		    }
		completionHandler
	}
	```
	{: codeblock} 
5. This new callback method is invoked when user clicks the action button. The implementation of this method must perform tasks associated with the specified identifier and execute the block in the `completionHandler` parameter.


### Cordova
{: #send_interactive_notifications_ios_cordova}

To get actionable notification in an Cordova iOS application, complete the steps:

1. Add category field inside `BMSPush.initialize` method.
   ```
	var category =  {"Category_Name":[{"IdentifierName_1":"actionName_1"},{"IdentifierName_2":"actionName_2"}]}
       BMSPush.initialize(appGUID,clientSecret,category);
    ```
	{: codeblock} 
2. Implement the new callback method on AppDelegate.
3. This new callback method is invoked when user clicks the action button. The implementation of this method must perform tasks associated with the specified identifier and execute the block in the completionHandler parameter.

## Handling silent notifications for iOS
{: #send_silent_notifications_for_ios}

Silent notifications do not appear on the device screen. These notifications are received by the application in the background, which wakes up the application for up to 30 seconds to perform the specified background task. A user might not be aware of the notification arrival. To send silent notifications for iOS, use the [REST API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://mobile.{DomainName}/imfpush/){: new_window}.   

1. To send silent push notifications, implement the following method in the `appDelegate.m` file in your project. In Swift, the `contentAvailable` value that is sent by the server for silent notifications is equal to 1.
```
//For Swift
	 func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       let contentAPS = userInfo["aps"] as [NSObject : AnyObject]
       if let contentAvailable = contentAPS["content-available"] as? Int {
           //silent or mixed push
           if contentAvailable == 1 {
               completionHandler(UIBackgroundFetchResult.NewData)
           } else {
               completionHandler(UIBackgroundFetchResult.NoData)
           }
       } else {
    //Default notification 
           completionHandler(UIBackgroundFetchResult.NoData)
       }
    }
```
	{: codeblock}

