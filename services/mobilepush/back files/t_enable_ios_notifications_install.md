# Initializing Push SDK for iOS apps
{: #enable-push-ios-notifications-install}

For an existing Xcode project, you can set up the Bluemix Mobile Services Client SDK using the CocoaPods dependency management tool. An alternative is to install the SDK manually.

**Note**: To view the Swift Push readme file, go https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master

##Installing CocoaPods

{: #enable-push-ios-notifications-install}

1. Install CocoaPods by using the following command in your Mac terminal.
```
$ sudo gem install cocoapods
```
2. Enter the following command in the terminal to initilalize CocoaPods. When you issue this command, make sure the run it in the directory where your Xcode project is. The `pod init`command creates a file title.  
```
$ pod init
```
3. In the generated Podfile, add the SDK dependencies you need. Copy the following Podfile.

   Objective-C

    ```
    source 'https://github.com/CocoaPods/Specs.git'
	Copy the following list as is and remove the dependencies you do not need
	pod 'IMFCore'
	pod 'IMFPush'
	```

   Swift

	```
	source 'https://github.com/CocoaPods/Specs.git'
	// Copy the following list as is and remove the dependencies you do not need.
	use_frameworks!

	target 'MyApp' do
	    platform :ios, '8.0'
	    pod 'BMSCore'
	    pod 'BMSPush'
	end
	```
3. From the Terminal, go to your project folder and install the dependencies with the following command:
```
$ pod update
```
That command installs your dependencies and creates a new Xcode workspace.  **Note**: Ensure that you always open the new Xcode workspace, instead of the original Xcode project file:

	```
	$ open App.xcworkspace
	```
The workspace contains your original project and Pods project that contains your dependencies. If you would like to modify an Bluemix Mobile Services source folder, you can find it in your Pods project, under `Pods/yourImportedSourceFolder`, for example: `Pods/IMFGoogleAuthentication`.

##Using imported frameworks and source folders

Reference the SDK in your code.


### Objective-C

Write #import directives for the relevant headers, for example:

```
//Objective-C
#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**Note**: Updating your Pods project using the CocoaPods commands `pod install` or `pod update` might override the Bluemix Mobile Services source folders. If you want to retain your customized versions of the original files, ensure that they are backed up before you issue one of these commands.

###Swift

**Pre-requisites**

- iOS 8.0 or greater
- Xcode 7


Write #import directives for the relevant headers, for example:

```
//swift
import BMSCore
import BMSPush
```


##Build Settings

Go to **Xcode > Build Settings > Build Options and Set Enable Bitcode** to **No**.

**Attention**: As of iOS 9, changes to the App Transport Security (ATS) feature might affect the way you handle the authentication process. The following blog posts describe more information about the changes:[ATS and Bitcode in iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) and [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)




# Initializing Push SDK for iOS apps
{: #enable-push-ios-notifications-initialize}

A common place to put the initialization code is in the application delegate for the iOS application.
Click the **Mobile Options** link in your Bluemix Application Dashboard to get the application route and GUID.

##Initializing the Core SDK

###Objective-C

```
// Initialize the SDK for Object-C with IBM Bluemix GUID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```

###Swift

```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstance

myBMSClient.initializeWithBluemixAppRoute("BluemixAppRoute", bluemixAppGUID: "APPGUID", bluemixRegion:"Location where your app Hosted")
myBMSClient.defaultRequestTimeout = 10.0 // Timput in seconds
```


##Initializing the client Push SDK

###Objective-C

```
//Initialize client Push SDK for Objective-C
IMFPushClient _pushService = [IMFPushClient sharedInstance];
```

###Swift

```
//Initialize client Push SDK for Swift
let push = BMSPushClient.sharedInstance
```

## Route, GUID, and Bluemix region

**appRoute**

Specifies the route that is assigned to the server application that you created on Bluemix.

**GUID**

Specifies the unique key that is assigned to the application that you created on Bluemix. This value is case-sensitive.

**bluemixRegionSuffix**

Specifies the location where the app is hosted. The ```bluemixRegion``` parameter specifies which Bluemix deployment you are using. You can set this value with a ```BMSClient.REGION``` static property and use one of three values:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY




# Registering iOS applications and devices
{: #enable-push-ios-notifications-register}


An application (app) must register with APNs to receive remote notifications, which usually happen after the app is installed on a device. After the device token generated by APNs is received by the app, it must be passed back to the Push Notifications Service.

To register iOs applications and devices:

1. Create a backend application
2. Pass the token to Push Notifications


##Create a backend application

Create a backend application in the Boilerplates section Bluemix® catalog, which automatically binds the Push service to this application. If you already created a backend app, make sure that you bind the app to the Push Notification Service.

###Objective-C

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

###Swift

```
	//For Swift
	func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
		let notificationTypes: UIUserNotificationType = UIUserNotificationType.Badge | UIUserNotificationType.Alert | UIUserNotificationType.Sound
		let notificationSettings: UIUserNotificationSettings = UIUserNotificationSettings(forTypes: notificationTypes, categories: categories)
		application.registerUserNotificationSettings(notificationSettings)
		application.registerForRemoteNotifications()
	}
```

##Pass the token to Push Notifications

After the token is received from APNs, pass the token to Push Notifications as part of the ```registerDevice:withDeviceToken``` method.

###Objective-C

```
//For Objective-C
-( void) application:( UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:( NSData *)deviceToken{

   IMFClient *client = [IMFClient sharedInstance];

 [client initializeWithBackendRoute: @"your-backend-route-here" backendGUID: @"Your-backend-GUID-here"];


 // get Push instance
IMFPushClient* push = [IMFPushClient sharedInstance];
[push registerDeviceToken:deviceToken completionHandler:^(IMFResponse *response,  NSError *error) {
   if (error){
     [ self  updateMessage:error .description];
  }  else {
    [ self updateMessage:response .responseJson .description];
}
}];
```

###Swift

After the token is received from APNS, pass the token to Push Notifications as part of the ```didRegisterForRemoteNotificationsWithDeviceToken``` method.

```
func application (application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   let push =  BMSPushClient.sharedInstance
   push.registerDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
        if error.isEmpty {
            print( "Response during device registration : \(response)")
            print( "status code during device registration : \(statusCode)")
        }
        else{
            print( "Error during device registration \(error) ")
            Print( "Error during device registration \n  - status code: \(statusCode) \n Error :\(error) \n")
        }
    }

}
```



# Receiving push notifications on iOS devices
{: #enable-push-ios-notifications-receiving}

Receive push notifications on iOS devices.

##Objective-C
To receive push notifications on iOS devices, add the following Objective-C method to the application delegate of your application.

```
// For Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
}
```

##Swift
To receive push notifications on iOS devices, add the following Swift method to the application delegate of your application.

```
 // For Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       //UserInfo dictionary will contain data sent from the server
   }

```



# Sending basic push notifications
{: #push-send-notifications}

After you have developed your applications, you can send basic push notifications (without using tags, badges, additional payloads, or sound files). 


Send basic push notifications.

1. In **Choose the Audience**, select one of the following audiences: **All Devices**, or by platform: **Only iOS devices** or **Only Anroid devices**. 

	**Note**: When you select the **All Devices** option, all the devices that have subscribed to push notifications receive your notification.
	
	![Notifications screen](images/tag_notification.jpg)

2. In the **Create your Notification**, enter your message and then click **Send**.
3. Verify that your devices have received your notification.

	The following screen shot shows an alert box handling a push 
notification in the foreground on a Android and iOS device.

	![Foreground push notification on Android](images/Android_Screenshot.jpg)

	![Foreground push notification on iOS](images/iOS_Screenshot.jpg)
	
	The following following screen shot shows a push notification in the background for Android.	
	![Background push notification on Android](images/background.jpg)
 


 
# Next steps
{: #next_steps_tags}

After you have successfully set up basic notifications, you can configure configure tag-based notifications and advanced options.

Add these Push Notifications Service features to your app.
To use tag-based notifications, see [Tag-based Notifications](c_tag_basednotifications.html).
To use advanced notifications options, see [Advanced push notifications](t_advance_notifications.html).
