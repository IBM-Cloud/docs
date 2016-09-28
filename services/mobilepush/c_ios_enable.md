---

copyright:
 years: 2015, 2016

---

#Enabling iOS applications to receive and send {{site.data.keyword.mobilepushshort}}
{: #enable-push-ios-notifications}
Last updated: 22 September 2016
{: .last-updated}

You can enable iOS applications to receive and send {{site.data.keyword.mobilepushshort}} to your devices.


##Installing CocoaPods
{: #enable-push-ios-notifications-install}

For an existing Xcode project, you can set up the Bluemix Mobile services client SDK using the CocoaPods dependency management tool. An alternative is to install the SDK manually.

To view the Swift Push readme file, go to [Readme](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master).



1. Install CocoaPods by using the following command in your Mac terminal.
```
$ sudo gem install cocoapods
```
	{: codeblock}
2. Enter the `pod init` command in the terminal to initialize CocoaPods. Ensure that you run the command from the directory where your Xcode project is. The `pod init` command creates a Podfile.  
3. In the generated Podfile, add the required SDK dependencies. Copy either of the following Podfiles, based on your preference.
 
**Objective-C**
   
```
source 'https://github.com/CocoaPods/Specs.git'
	# Copy the following list as is and remove the dependencies you do not need.
	pod 'IMFCore'
	pod 'IMFPush'
```
	{: codeblock}

**Swift**
   
```
source 'https://github.com/CocoaPods/Specs.git'
	# Copy the following list as is and remove the dependencies you do not need.
use_frameworks!
target 'MyApp' do
platform :ios, '9.0'
pod 'BMSCore'
pod 'BMSPush'
pod 'BMSAnalyticsAPI'
end
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

##Carthage
{: #carthage}

Add frameworks to your project using [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos). Note that Carthage in Xcode8 is not supported.

1. Add `BMSPush` frameworks to your Cartfile:
```
github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
```
	{: codeblock}
2. Run the `carthage update` command. When the build completes, drag `BMSPush.framework`, `BMSCore.framework` and `BMSAnalyticsAPI.framework` into your Xcode project.
3. Follow the instructions on the [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) site to complete the integration.


##Using imported frameworks and source folders
{: using-imported-frameworks}

Reference the SDK in your code. Use either of the following methods, based on your preference.

**Objective-C**

Write `#import` directives for the relevant headers, for example:

```
	//Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFPush/IMFPush.h>
```
	{: codeblock}

**Note**: Updating your Pods project using the CocoaPods commands `pod install` or `pod update` might override the Bluemix Mobile services source folders. If you want to retain your customized versions of the original files, ensure that they are backed up before you issue one of these commands.

**Swift**

Ensure that the following prerequisites are in place:

- iOS 8.0 or greater
- Xcode 7


Write `#import` directives for the relevant headers, for example:
```
//swift
import BMSCore
import BMSPush
```
	{: codeblock}
To view the Swift Push readme file, go to [Readme](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master).

##Build Settings
{: build-settings}

Go to **Xcode > Build Settings > Build Options and Set Enable Bitcode** to **No**.

**Attention**: As of iOS 9, changes to the App Transport Security (ATS) feature might affect the way you handle the authentication process. The following blog posts describe more information about the changes: [ATS and Bitcode in iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) and [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/).

## Initializing Push SDK for iOS apps
{: #enable-push-ios-notifications-initialize}

A common place to put the initialization code is in the application delegate for the iOS application. Click the **Mobile Options** link in your Push Dashboard to get the application route and GUID.

###Initializing the Core SDK
{: Initializing-the-core-sdk}

**Objective-C**

```
// Initialize the SDK for Object-C with IBM Bluemix GUID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```
	{: codeblock}

**Swift**

```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstance
myBMSClient.initialize(bluemixRegion: "Location where your app is hosted.") 
myBMSClient.defaultRequestTimeout = 10.0 // Timeout in seconds
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

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

####AppGUID
{: ios-AppGUID}

Specifies the unique AppGUID key that is assigned to the {{site.data.keyword.mobilepushshort}} service that you created on Bluemix.

###Initializing the client Push SDK
{: initializing-the-client-Push-SDK}

**Objective-C**

```
//Initialize client Push SDK for Objective-C
IMFPushClient *push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID"];
```
	{: codeblock}

**Swift**

```
//Initialize client Push SDK for Swift
let push = BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID")
```
	{: codeblock}


## Registering iOS applications and devices
{: #enable-push-ios-notifications-register}


An application must register with APNs to receive remote notifications, after installation on a device. After the device token generated by APNs is received by the app, it must be passed back to the {{site.data.keyword.mobilepushshort}} service.

To register iOS applications and devices, you need to:

1. Create a backend application.
2. Pass the token to {{site.data.keyword.mobilepushshort}}.


###Create a backend application
{: create-a-backend-app}

Create a backend application in the Boilerplates section Bluemix® catalog, which automatically binds the {{site.data.keyword.mobilepushshort}} service to this application. If you already created a backend app, ensure that you bind the app to the {{site.data.keyword.mobilepushshort}} service.

**Objective-C**

```
//For Objective-C
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
if ([[[UIDevice currentDevice] systemVersion] floatValue] >= 8.0){
    [[UIApplication sharedApplication] registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge) categories:categories]];
    [[UIApplication sharedApplication] registerForRemoteNotifications];
    }
    else{
    [[UIApplication sharedApplication] registerForRemoteNotificationTypes:
    (UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)];
    }
    return YES;
	}
```
	{: codeblock}

**Swift**

```
//For Swift
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
	let settings = UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound], categories: nil) UIApplication.sharedApplication().registerUserNotificationSettings(settings) UIApplication.sharedApplication().registerForRemoteNotifications()
	}
```
	{: codeblock}

###Passing tokens to {{site.data.keyword.mobilepushshort}}
{: pass-token-push-notifications}

After the token is received from APNs, pass the token to {{site.data.keyword.mobilepushshort}} as part of the `registerWithDeviceToken` method.

**Objective-C**

```
//For Objective-C
-( void) application:( UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:( NSData *)deviceToken{
    IMFClient *client = [IMFClient sharedInstance];
	[client initializeWithBackendRoute: @"your-backend-route-here" backendGUID: @"Your-backend-GUID-here"];
	// get Push instance
	IMFPushClient* push = [IMFPushClient sharedInstance];
	[push initializeWithAppGUID:@"appGUID"];
	[push registerWithDeviceToken:deviceToken completionHandler:^(IMFResponse *response,  NSError *error) {
    if (error){
     NSLog(@"%@",error.description);
    }  else 
		{
    NSLog(@"%@",response.responseJson.description);
		}
	}];
 }
```
	{: codeblock}

**Swift**

After the token is received from APNs, pass the token to Push Notifications as part of the `didRegisterForRemoteNotificationsWithDeviceToken` method.

```
func application (application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   let push =  BMSPushClient.sharedInstance
   push.initializeWithAppGUID("appGUID")
   push.registerWithDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
   push.initializeWithAppGUID("appGUID")
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

You can receive push notifications on iOS devices using either of the following methods.

**Objective-C**

To receive push notifications on iOS devices, add the following Objective-C method to the application delegate of your application.

```
// For Objective-C
 -(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
	}
```
	{: codeblock}

**Swift**

To receive push notifications on iOS devices, add the following Swift method to the application delegate of your application.
```
// For Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
//UserInfo dictionary will contain data sent from the server
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


## Next steps
{: #next_steps_tags}

After you have successfully set up basic notifications, you can configure configure tag-based notifications and advanced options.

Add these Push Notifications Service features to your app.
To use tag-based notifications, see [Tag-based Notifications](c_tag_basednotifications.html).
To use advanced notifications options, see [Advanced push notifications](t_advance_notifications.html).
