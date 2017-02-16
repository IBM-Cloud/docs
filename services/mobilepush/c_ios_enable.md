---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

#Enabling iOS applications to send {{site.data.keyword.mobilepushshort}}
{: #enable-push-ios-notifications}
Last updated: 14 February 2017
{: .last-updated}

You can enable iOS applications to send {{site.data.keyword.mobilepushshort}} to your devices.


##Installing CocoaPods
{: #enable-push-ios-notifications-install}

For an existing Xcode project, you can set up the Bluemix Mobile services client SDK using the CocoaPods dependency management tool. An alternative is to install the SDK manually.

To view the Swift Push readme file, go to [Readme ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}.



1. Install CocoaPods by using the following command in your Mac terminal.
```$ sudo gem install cocoapods
```
	{: codeblock}
2. Enter the `pod init` command in the terminal to initialize CocoaPods. Ensure that you run the command from the directory where your Xcode project is. The `pod init` command creates a Podfile.  
3. In the generated Podfile, add the required SDK dependencies. Copy the following Podfile.
   
	```
		source 'https://github.com/CocoaPods/Specs.git'
		//Copy the following list as is and remove the dependencies you do not need.
		use_frameworks!
		target 'MyApp' do
		platform :ios, '8.0'
		pod 'BMSCore'
		pod 'BMSPush'
		pod 'BMSAnalyticsAPI' end
	```
		{: codeblock}

3. From the terminal, go to your project folder and install the dependencies with the `pod update` command.

The command installs your dependencies and creates a new Xcode workspace.  
**Note**: Ensure that you always open the new Xcode workspace, instead of the original Xcode project file:
```
  $ open App.xcworkspace
```
	{: codeblock}

The workspace contains your original project and Pods project that contains your dependencies. To modify the Bluemix mobile services source folder, you can find it in your Pods project, under `Pods/yourImportedSourceFolder`, for example: `Pods/BMSPush`.

##Adding frameworks using Carthage
{: #carthage}

Add frameworks to your project using [Carthage ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window}. Note that Carthage in Xcode8 is not supported.

1. Add `BMSPush` frameworks to your Cartfile:
```
  github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
```
	{: codeblock}
2. Run the `carthage update` command. When the build completes, drag `BMSPush.framework`, `BMSCore.framework` and `BMSAnalyticsAPI.framework` into your Xcode project.
3. Follow the instructions on the [Carthage ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window} site to complete the integration.

##Setting up the iOS SDK
{: ios-sdk}

Set up the iOS SDK, add the following code to the **AppDelegate.swift** file in your application. Note that this also registers with the APNs.  
```
  func application(_ application: UIApplication,
  didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool 
   {  
   BMSPushClient.sharedInstance.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE")
  }
```
    {: codeblock}

##Using imported frameworks and source folders
{: using-imported-frameworks}

Reference the SDK in your code. Ensure that the following prerequisites are in place.

- iOS 8.0 or greater	
- Xcode 7

Write `#import` directives for the relevant headers, for example:
```
//swift
 import BMSCore
 import BMSPush
```
		{: codeblock}

To read the Swift Push readme file, see [Readme ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}.

**Note**: Updating your Pods project using the CocoaPods commands `pod install` or `pod update` might override the Bluemix Mobile services source folders. If you want to retain your customized versions of the original files, ensure that they are backed up before you issue one of these commands.


##Build Settings
{: build-settings}

Go to **Xcode > Build Settings > Build Options and Set Enable Bitcode** to **No**.

**Attention**: As of iOS 9, changes to the App Transport Security (ATS) feature might affect the way you handle the authentication process. The following blog posts describe more information about the changes: [ATS and Bitcode in iOS 9 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/){: new_window} and [Connect your iOS 9 app to Bluemix today ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/){: new_window}.

## Initializing Push SDK for iOS apps
{: #enable-push-ios-notifications-initialize}

A common place to put the initialization code is in the application delegate for the iOS application. Click the **Mobile Options** link in your Push Dashboard to get the application route and GUID.

###Initializing the Core SDK
{: Initializing-the-core-sdk}


```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstance
myBMSClient.initialize(bluemixRegion: "Location where your app is hosted.") 
```
	{: codeblock}

### Route, GUID, and Bluemix region
{: route-guid-bluemix-region}

####appRoute
{: ios-approute}

Specifies the route that is assigned to the server application that you created on Bluemix.

####GUID
{: ios-guid}

Specifies the unique key that is assigned to the application that you created on Bluemix. This value is case-sensitive.

####bluemixRegionSuffix
{: ios-bluemixRegionSuffix}

Specifies the location where the app is hosted. The `bluemixRegion` parameter specifies which Bluemix deployment you are using. You can set this value with a `BMSClient.REGION` static property and use one of three values:

- BMSClient.Region.usSouth 
- BMSClient.Region.unitedKingdom
- BMSClient.Region.sydney

####AppGUID
{: ios-AppGUID}

Specifies the unique AppGUID key that is assigned to the {{site.data.keyword.mobilepushshort}} service that you created on Bluemix.

###Initializing the client Push SDK
{: initializing-the-client-Push-SDK}

```
	//Initialize client Push SDK for Swift
	let push = BMSPushClient.sharedInstance
	push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


## Registering iOS applications and devices
{: #enable-push-ios-notifications-register}


An application must register with APNs to receive remote notifications, after installation on a device. After the device token generated by APNs is received by the app, it must be passed back to the {{site.data.keyword.mobilepushshort}} service.

To register iOS applications and devices, you need to:

1. Create a back-end application.
2. Pass the token to {{site.data.keyword.mobilepushshort}}.


###Create a back-end application
{: create-a-backend-app}

Create a back-end application in the Boilerplates section Bluemix® catalog, which automatically binds the {{site.data.keyword.mobilepushshort}} service to this application. If you have already created a back-end app, ensure that you bind the app to the {{site.data.keyword.mobilepushshort}} service.


###Passing tokens to {{site.data.keyword.mobilepushshort}}
{: pass-token-push-notifications}

After the token is received from APNs, pass the token to {{site.data.keyword.mobilepushshort}} as part of the `registerWithDeviceToken` method.

After the token is received from APNs, pass the token to Push Notifications as part of the `didRegisterForRemoteNotificationsWithDeviceToken` method.

```
  func application (_application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data){
   let push =  BMSPushClient.sharedInstance
   push.registerWithDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
      if error.isEmpty {
           print( "Response during device registration : \(response)")
           print( "status code during device registration : \(statusCode)")
      }
       else{
           print( "Error during device registration \(error) ")
           print( "Error during device registration \n  - status code: \(statusCode) \n Error :\(error) \n")
       }
   }
  }
```
	{: codeblock}


## Receiving push notifications on iOS devices
{: #enable-push-ios-notifications-receiving}


To receive push notifications on iOS devices, add the following Swift method to the application delegate of your application.

```
  // For Swift
  func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) 
  { //UserInfo dictionary will contain data sent from the server }
```
	{: codeblock}

## Monitoring push notifications on iOS devices
{: ios-monitoring}

To monitor the current status of the notification, add the following Swift method to the application delegate of your application.

```
	// Send notification status when app is opened by clicking the notifications
	func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any]) {
 	let push =  BMSPushClient.sharedInstance
 	let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 	let data = respJson.data(using: String.Encoding.utf8)
 	let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 	let messageId:String = jsonResponse.value(forKey: "nid") as! String
    push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
      print("Send message status to the Push server")
     }
}
```
	{: codeblock}

```
	// Send notification status when the app is in background mode.
	func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
 	let payLoad = ((((userInfo as NSDictionary).value(forKey: "aps") as! NSDictionary).value(forKey: "alert") as! NSDictionary).value(forKey: "body") as! NSString)
 	self.showAlert(title: "Recieved Push notifications", message: payLoad)
 	let push =  BMSPushClient.sharedInstance
 	let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 	let data = respJson.data(using: String.Encoding.utf8)
 	let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 	let messageId:String = jsonResponse.value(forKey: "nid") as! String
 	push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
       completionHandler(UIBackgroundFetchResult.newData)
   }
}
```
	{: codeblock}


## Sending basic push notifications
{: #send}

After you have developed your applications, you can send basic push notifications.

To send basic push notifications, complete the steps:

1. Select **Send Notifications**, and compose a message by choosing a **Send to** option. The supported options are **Device by Tag**, **Device Id**, **User Id**, **Android devices**, **iOS devices**, **Web Notifications**, and **All Devices**.  
**Note**: When you select the **All Devices** option, all devices subscribed to {{site.data.keyword.mobilepushshort}} will receive notifications.
![Notifications screen](images/tag_notification.jpg)

2. In the **Message** field, compose your message. Choose to configure the optional settings as required.
3. Click **Send**.
3. Verify that your devices have received your notification.

The following image shows an alert box handling a {{site.data.keyword.mobilepushshort}} an iOS device.

![Foreground push notification on iOS](images/iOS_Screenshot.jpg) 

### Optional settings for sending notifications
{: #send_ios_otpional_setting}

You can further customize the {{site.data.keyword.mobilepushshort}} settings for sending notifications to iOS devices. The following optional customization options are supported.

- **Badge**:  Indicates the number that is displayed on the application badge. The default value is zero (0), and this would not display a badge. 
- **Sound**: Indicates a sound clip to be played on the receipt of a notification. Supports default or the name of a sound resource bundled in the app.
- **Additional payload**: Specifies the custom payload values for your notifications.

##Enabling interactive notifications

You can now enrich your iOS notifications with more details like adding an image,  map or a response button through enabling interactive notifications. This provides more context to customers, along with the ability to take immediate action without leaving the current context.  

To enable interactive notifications, use the following code:

```
	// This defines the button action.
	let actionOne = BMSPushNotificationAction(identifierName: "ACCEPT", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
 	let actionTwo = BMSPushNotificationAction(identifierName: "DECLINE", buttonTitle: "Decline", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
```
	{: codeblock}
```
	// This defines category for the buttons
	let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
```
	{: codeblock}
```
	// This updates the registration to include the buttonsPass the defined category into iOS BMSPushClientOptions
	let notificationOptions = BMSPushClientOptions(categoryName: [category])
	let push = BMSPushClient.sharedInstance
	push.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE", options: notificationOptions)
```
	{: codeblock}

To send an interactive notification, complete the steps:

1. In the Compose section, for the Send To drop-down list, select **iOS Devices**.
2. Enter the notification message that you might want to sent.
3. In Optional Settings Section, select **Mobile** and click **iOS**.
4. In the Type drop-down list, select **Mixed**.
5. In Category field, specify the notification type that you have defined in your app. 

![Interactive notification for iOS](images/push_ios_notification_interactive.jpg) 

## Next steps
{: #next_steps_tags}

After you have successfully set up basic notifications, you can configure configure tag-based notifications and advanced options.

Add these Push Notifications Service features to your app.
To use tag-based notifications, see [Tag-based Notifications](c_tag_basednotifications.html).
To use advanced notifications options, see [Enabling advanced push notifications](t_advance_badge_sound_payload.html).
