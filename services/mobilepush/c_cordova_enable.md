---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Enabling Cordova applications to receive push notifications
{: #cordova_enable}
Last updated: 18 January 2017
{: .last-updated}

Cordova is a platform for building hybrid applications with JavaScript, CSS, and HTML. The {{site.data.keyword.mobilepushshort}} service supports development of Cordova-based iOS and Android applications.

You can enable Cordova applications to receive push notifications to your devices.

## Installing the Cordova push plug-in
{: #cordova_install}

Install and use the client push plug-in to further develop your Cordova applications. This also installs the Cordova core plug-in, which initializes your connection to Bluemix.

### Before you begin

1. Download the latest Android Studio SDK and Xcode versions.
1. Set up your emulator. For Android Studio, use an emulator that supports Google Play API.
1. Install the Git command-line tool. For Windows, make sure you select the **Run Git from the Window Command Prompt** option. For information about how to download and install this tool, see [Git ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git-scm.com/downloads){: new_window}.
1. Install the Node.js and Node Package Manager (NPM) tool. The NPM command-line tool is bundled with Node.js. For information about how to download and install Node.js, see [Node.js ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://nodejs.org/en/download/){: new_window}.
1. From the command line, install the Cordova command-line tools by using the **npm install -g cordova** command. This is required to use the Cordova push plug-in. For information about how to install Cordova and set up your Cordova app, see [Cordova Apache ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cordova.apache.org/#getstarted){: new_window}. For more information, see the Cordova push plug-in [Readme file ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window}.
1. Change to the folder that you want to create your Cordova app in and run the following command to create a Cordova application. If you have an existing Cordova app, go to step 3.
```cordova create your_app_name
cd your_app_name
```
	{: codeblock}
- Optional: You can edit the **config.xml** file and change the application name in the <name> element to a name that you choose, rather than the default HelloCordova name.

Ensure that you specify the correct Bundle ID. The following error messages might result in Xcode, if an incorrect Bundle ID is specified.

* The executable was signed with invalid entitlements.
* The entitlements specified in your application’s Code Signing Entitlements file do not match those specified in your provisioning profile. To fix this issue, specify the correct Bundle ID in Xcode or in your Cordova app **config.xml**  file.

1. Add the minimum supported API or the deployment target declaration to the config.xml file for your Cordova application. The minSdkVersion value must be higher than 15. The targetSdkVersion value must always reflect the latest Android SDK that is available from Google.
	
	* Android - With your editor, open the **config.xml** file and update the
`<platform name="android">` element with minimum and target SDK versions:

	```
	<platform name="android">
    	<preference name="android-minSdkVersion" value="15" />
    	<preference name="android-targetSdkVersion" value="23" />
    	<!-- add minimum and target Android API level declaration -->
	</platform> 
	```
    	{: codeblock}

   * iOS - Update the <platform name="ios"> element with a deployment target declaration:

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- add deployment target declaration -->
	</platform>
	```
		{: codeblock}

1. From the Cordova command-line interface (CLI), add your platforms: iOS, Android, or both by using the command:
```
cordova platform add ios
cordova platform add android
```
	{: codeblock}

1. From your Cordova application root directory, enter the following command to install the Cordova push plug-in: **cordova plugin add bms-push**. Depending on the platforms that you added, you might see:
```
Installing "bms-push" for android
Installing "bms-push" for ios
```
	{: codeblock}

1. From your-app-root-folder, verify that the Cordova core and push plug-in were installed successfully by using the following command: **cordova plugin list**. Depending on the platforms that you added, you might see:
```
bms-core <version> "BMSCore"
bms-push <version> "BMSPush" 
```
	{: codeblock}

1. Configure your iOS development environment.
2. Build and run your application with Xcode.
1. Download your Firebase `google-services.json` for android, and place them in the root folder of your Cordova project, in `[your-app-name]/platforms/android.
	1. Go to `[your-app-name]/platforms/android`.
	2. Open file `build.gradle` (Path : platform > android > build.gradle).
	3. Find `buildscript` text in `build.gradle` file.
	4. After the classpath line, add the line, classpath 'com.google.gms:google-services:3.0.0'
	5. Then find "dependencies". Select dependencies where you have text `compile` and where that dependencies is getting ended, just after that, add this line :apply plugin: 'com.google.gms.google-services'.
	6. Prepare and build your Cordova Android project.
		```
		cordova prepare android
		cordova build android
		```
			{: codeblock}
	**Note**: Before opening your project in Android Studio, build your Cordova application through the Cordova CLI. This will help avoid build errors.

## Initializing the Cordova plug-in
{: #cordova_initialize}

Before you can use the {{site.data.keyword.mobilepushshort}} service Cordova plug-in, you need to initialize it by passing the application route and application GUID. After initializing the plug-in, you can connect to the server app that you have created in the Bluemix dashboard. The Cordova plug-in is the wrapper for the Android and iOS client SDKs to enable a Cordova app to communicate with Bluemix services.

1. Initialize the BMSClient by copying and pasting the following code snippet into your main JavaScript file (typically located under the **www/js** directory).

```
onDeviceReady: function() {
	app.receivedEvent('deviceready');
	BMSClient.initialize("YOUR APP REGION");
	var category =  {};
	BMSPush.initialize(appGUID,clientSecret,category);
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	BMSPush.registerDevice({}, success, failure);
	var showNotification = function(notif)
	{
	alert(JSON.stringify(notif));
	};
	BMSPush.registerNotificationsCallback(showNotification);
    } 
```
	{: codeblock}

Pass in the region for your application. The following constants are provided:

```
REGION_US_SOUTH // ".ng.bluemix.net";
REGION_UK //".eu-gb.bluemix.net";
REGION_SYDNEY // ".au-syd.bluemix.net";
```

For example:

```
BMSClient.initialize(BMSClient.REGION_US_SOUTH);
```

**Note**: If you have created a Cordova app using the Cordova CLI, for example, Cordova create app-name command, put this Javascript code in the index.js file, after the app.receivedEvent function within the onDeviceReady: function() function to initialize the `BMSClient`. 


## Registering devices
{: #cordova_register}


To register a device with the {{site.data.keyword.mobilepushshort}} service, call the register method. Copy the following code snippet into your Cordova application to register a device.

```
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure);
```
	{: codeblock}

The following JavaScript code snippet shows how to initialize your Bluemix Mobile Services client SDK, register a device with {{site.data.keyword.mobilepushshort}} service, and listen to push notifications. Include this code in your Javascript file.

Within the **onDeviceReady: function()**.

```
onDeviceReady: function() {
app.receivedEvent('deviceready');
BMSClient.initialize("YOUR APP REGION");
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure); 
 var showNotification = function(notif)
 {
 alert(JSON.stringify(notif));
 };
BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

Add the following Swift code snippet to your application delegate class.

```
// Register the device token with Bluemix Push Notification Service
func application(application: UIApplication,
  didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData) {
   CDVBMSPush.sharedInstance().didRegisterForRemoteNotificationsWithDeviceToken(deviceToken)
} 
// Handle error when failed to register device token with APNs
func application(application: UIApplication,
    didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer) {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(error)
} 
```
	{: codeblock}

## Next steps

{: #cordova_register_next}

Build your project and then run your project by using the following commands:

#### Android
{: android-next-steps}

```
cordova build android
```
	{: codeblock}

```
cordova run android
```
	{: codeblock}

#### iOS
{: ios-next-steps}

```
cordova build ios
```
	{: codeblock}

```
cordova run ios
```
	{: codeblock}

## Receiving push notifications on devices
{: #cordova_receive}

Copy the following code snippet to receive push notifications on devices.

### JavaScript

Add the following JavaScript code snippet to the web part of your Cordova application.
```
var showNotification = function(notif) {
  alert(JSON.stringify(notif));
        };
        BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

### Android notification properties

The following section lists the Android notification properties:

* **message** - Push notification message
* **payload** - JSON object containing a notification payload


### iOS notification properties

The following section lists the iOS notification properties:

* **message** - Push notification message
* **payload** - JSON object that contains a notification payload
action-loc-key - The string is used as a key to get a localized string in the current localization, to use for the appropriate button title, instead of `View`.
* **badge** - The number to display as the badge of the app icon. If this property is absent, the badge is not changed. To remove the badge, set the value of this property to 0.
* **sound** - The name of a sound file in the app bundle or in the Library/Sounds folder of the app data container.


Add the following Swift code snippets to your application delegate class.
```
// Handle receiving a remote notification
func application(application: UIApplication,
   didReceiveRemoteNotification userInfo: [NSObject : AnyObject],  fetchCompletionHandler completionHandler: ) {
   CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(userInfo)
}
```
	{: codeblock}

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
  let remoteNotif = launchOptions?[UIApplicationLaunchOptionsKey.remoteNotification] as? NSDictionary
  if remoteNotif != nil {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationOnLaunchWithLaunchOptions(launchOptions)
  }
} 
```
	{: codeblock}

## Sending basic push notifications
{: #push-send-notifications}

After you have developed your applications, you can send basic push notifications.

To send basic push notifications, complete the steps:

1. Select **Send Notifications**, and compose a message by choosing a **Send to** option. The supported options are **Device by Tag**, **Device Id**, **User Id**, **Android devices**, **iOS devices**, **Web Notifications**, and **All Devices**.
**Note**: When you select the **All Devices** option, all devices subscribed to {{site.data.keyword.mobilepushshort}} will receive notifications.
![Notifications screen](images/tag_notification.jpg)

2. In the **Message** field, compose your message. Choose to configure the optional settings as required.
3. Click **Send**.
3. Verify that your devices have received your notification.

The following screen shot shows an alert box handling a {{site.data.keyword.mobilepushshort}} in the foreground on an Android and iOS device.

![Foreground push notification on Android](images/Android_Screenshot.jpg)

![Foreground push notification on iOS](images/iOS_Screenshot.jpg)

   The following image shows {{site.data.keyword.mobilepushshort}} in the background for Android.
![Background push notification on Android](images/background.jpg)

## Next steps
{: #next_steps_tags}

After you have successfully set up basic notifications, you can configure configure tag-based notifications and advanced options.

Add the {{site.data.keyword.mobilepushshort}} service features to your app.
To use tag-based notifications, see [Tag-based Notifications](c_tag_basednotifications.html).
To use advanced notifications options, see [Enabling advanced push notifications](t_advance_badge_sound_payload.html).
