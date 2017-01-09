---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Interactive notifications
{: #interactive-notifications}
Last updated: 09 January 2017
{: .last-updated}

Interactive notifications allow users to act when a notification arrives without opening the application. When an interactive notification arrives, the device shows the action buttons along with the notification message. Interactive notifications are supported on iOS devices with version 8 and later. If an interactive notification is sent to iOS devices with version earlier than 8, the notification actions are not displayed.

##Sending interactive {{site.data.keyword.mobilepushshort}}


Interactive notification can be sent by using the Push dashboard or by using the [REST API documentation](t_restapi.html).

From the {{site.data.keyword.mobilepushshort}} console: 

1. Under the notification tab in Push dashboard, click **Send Notification**. 
2. Choose your notification recipients and click **Next**. 
3. In the compose notification page, interactive push can be sent by setting the Type to either Default or Mixed and specifying the Category value under Advanced Options tab. To configure the category value on the client, check **Handling interactive {{site.data.keyword.mobilepushshort}}** in native iOS application section.

## Handling interactive {{site.data.keyword.mobilepushshort}} in an iOS application


### Swift

Complete the steps to receive interactive notifications:

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

To get actionable notification in an Cordova iOS application, complete the steps:

1. Add category field inside `BMSPush.initialize` method.
   ```
	var category =  {"Category_Name":[{"IdentifierName_1":"actionName_1"},{"IdentifierName_2":"actionName_2"}]}
       BMSPush.initialize(appGUID,clientSecret,category);
    ```
	{: codeblock} 
2. Implement the new callback method on AppDelegate.
3. This new callback method is invoked when user clicks the action button. The implementation of this method must perform tasks associated with the specified identifier and execute the block in the completionHandler parameter.
