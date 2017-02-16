---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Enabling Android applications to receive {{site.data.keyword.mobilepushshort}}
{: #tag_based_notifications}
Last updated: 14 February 2017
{: .last-updated}

You can enable Android applications to receive push notifications to your devices. Android Studio is a prerequisite and is the recommended method to build Android projects. A basic knowledge of Android Studio is essential.

## Installing the client Push SDK with Gradle
{: #android_install}

This section describes how to install and use the client Push SDK to further develop your Android applications.

Bluemix® Mobile Services Push SDK can be added using Gradle. Gradle automatically downloads artifacts from repositories and makes them available to your Android application. Ensure that you correctly set up Android Studio and the Android Studio SDK. For more information about how to set up your system, see [Android Studio Overview ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.android.com/tools/studio/index.html){: new_window}. For information about Gradle, see [Configuring Gradle Builds ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://developer.android.com/tools/building/configuring-gradle.html){: new_window}.

After creating and opening your mobile application, complete the following steps using the Android Studio.

1. Add dependencies to your Module level **build.gradle** file. 	

	- Add the following dependency to include the Bluemix™ Mobile services Push client SDK and the Google play services SDK to your compile scope dependencies.
	```
	com.ibm.mobilefirstplatform.clientsdk.android:push:3.+
	```
    	{: codeblock}
	
	- Add the following dependencies to import statements that are required for code snippets.
	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```
    	{: codeblock}

	- Add the following dependency to your Module level **build.gradle** file at the end.
	```
		apply plugin: 'com.google.gms.google-services'
	```
		{: codeblock}
3. Add the following dependencies to your Project level **build.gradle** file.
```
dependencies {
    classpath 'com.android.tools.build:gradle:2.2.3'
    classpath 'com.google.gms:google-services:3.0.0'
}
``` 
    {: codeblock}
5. In the **AndroidManifest.xml** file, add the following permissions. To view a sample manifest, see [Android helloPush Sample Application ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml){: new_window}. To view a sample Gradle file, see [Sample Build Gradle file ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle){: new_window}.
```
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
```
	{: codeblock}
 Read more about [Android permissions ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://developer.android.com/guide/topics/security/permissions.html){: new_window} here.

4. Add the notification intent settings for the activity. This setting starts the application when the user clicks the received notification from the notification area.
```
	<intent-filter>
		<action android:name="Your_Android_Package_Name.IBMPushNotification"/>
		<category  android:name="android.intent.category.DEFAULT"/>
	</intent-filter>
```
	{: codeblock}
**Note**: Replace *Your_Android_Package_Name* in the previous action with the application package name used in your application.

5. Add the Firebase Cloud Messaging (FCM) or Google Cloud Messaging (GCM) intent service and intent filters for the RECEIVE and REGISTRATION event notifications.
```
	<service android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushIntentService"
    	android:exported="true" >
    	<intent-filter>
    	    <action android:name="com.google.firebase.MESSAGING_EVENT" />
    </intent-filter>
	</service>
	<service
    android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush"
    android:exported="true" >
    <intent-filter>
        <action android:name="com.google.firebase.INSTANCE_ID_EVENT" />
    </intent-filter>
	</service>
```
    {: codeblock}

6. {{site.data.keyword.mobilepushshort}} service supports retrieval of  individual notifications from the notification tray. For notifications accessed from the notification tray, you are provided with a handle only to the notification that is being clicked. All notifications are displayed when the application is openend normally. Update your **AndroidManifest.xml** file with the following snippet to use this functionality:

```
	<activity android:name="
	com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationHandler"
	android:theme="@android:style/Theme.NoDisplay"/>
```
    {: codeblock}

To setup the FCM project and obtain your credentials, see [Getting Your Sender ID and API key](t_push_provider_android.html). Complete the following steps using the Firebase Cloud Messaging (FCM) console.

1. In the Firebase console, click the **Project Settings** icon.
    ![Firebase Project Settings](images/FCM_4.jpg)

3. Select **ADD APP** or **Add Firebase to your Android app icon** from the General tab on the Your apps pane.
    ![Adding Firebase to Android](images/FCM_5.jpg)

4. In Add Firebase to your Android app window, add **com.ibm.mobilefirstplatform.clientsdk.android.push** as the Package Name. The App nickname field is optional. Click **ADD APP**. 
    ![Adding Firebase to your Android window](images/FCM_1.jpg)

5. Include the package name of your application, by entering the package name in Add Firebase to your Android app window. The App nickname field is optional. Click **ADD APP**. 

	![Adding the package name of your application](images/FCM_2.jpg)

6. The `google-services.json` file is generated. Copy the `google-services.json` file to your Android application module root directory. Note that the `google-service.json` file includes the added package names.

    ![Adding the json file to the root directory of your application](images/FCM_7.jpg)

5. In Add Firebase to your Android app window, click **Continue** and then **Finish**. 

  

Build and run your application.

## Initializing the Push SDK for Android apps
{: #android_initialize}

A common place to put the initialization code is in the onCreate method of the main activity in your Android application. There are two components of the the SDK that need to be initialized. One is the core SDK and the other is the push SDK built on top of the core SDK.

###Initialize the Core SDK

```
// Initialize the SDK for Android
    BMSClient.getInstance().initialize(this, BMSClient.REGION_US_SOUTH);
```
    {: codeblock}

####bluemixRegionSuffix
{: bluemixRegionSuffix}

Specifies the location where the app is hosted. You can use one of the three values:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

###Initialize the client Push SDK

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext(), "appGUID", "clientSecret");
```
	{: codeblock}

####AppGUID
{: appguid_initialize_client_push_sdk}

This is the AppGUID key of the {{site.data.keyword.mobilepushshort}} service. This value is case-sensitive. Open the Push Notification dashboard and select the Configure tab. You can get this value from Mobile Options in the configure tab on the Push Notification service dashboard. 

## Registering Android devices
{: #android_register}

Use the `MFPPush.register()` API to register the device with {{site.data.keyword.mobilepushshort}} service. For registering for Android devices, add the Firebase Cloud Messaging (FCM) or Google Cloud Messaging (GCM) information in the Bluemix {{site.data.keyword.mobilepushshort}} service configuration dashboard. For more information, see [Configuring credentials for Google Cloud Messaging](t_push_provider_android.html).

Copy the following code snippets to your Android mobile application.

```
	//Register Android devices
	push.registerDevice(new MFPPushResponseListener<String>() {
    	@Override
    	public void onSuccess(String response) {
    		//handle success here
    	}
		@Override
    	public void onFailure(MFPPushException ex) {
    		//handle failure here
		}
		});
```
	{: codeblock}


```
	//Handles the notification when it arrives
	MFPPushNotificationListener notificationListener = new MFPPushNotificationListener() {
    @Override
    public void onReceive (final MFPSimplePushNotification message){
		// Handle Push Notification
   		 }
		};
```
	{: codeblock}

## Receiving push notifications on Android devices
{: #android_receive}

To register the notificationListener object with push, call the **MFPPush.listen()** method. This method is typically called from the **onResume()** method of the activity that is handling push notifications.

1. To register the notificationListener object with push, call the **listen()** method. This method is typically called from the **onResume()** and **onPause** methods of the activity that is handling push notifications.


```
	@Override
	protected void onResume(){
   	super.onResume();
   	if(push != null) {
       push.listen(notificationListener);
   }
	}
```
	{: codeblock}



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

2. Build the project and run it on the device or emulator. When the onSuccess() method for the response listener in the register() method is invoked, it confirms that the device has successfully registered with {{site.data.keyword.mobilepushshort}} service. At this time you can send a message as described in Sending basic push notifications.
3. Verify that your devices have received your notification. If the application is in the foreground, the notification is handled by the **MFPPushNotificationListener**. If the application is in the background, a message is displayed in the notification bar.

## Monitoring push notifications on Android devices
{: #android_monitor}

To monitor the current status of the notification within the application, you can implement the  `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener` interface and define the method onStatusChange(String messageId, MFPPushNotificationStatus status). 

The **messageId** is the identifier of the message sent from the server.  **MFPPushNotificationStatus** defines the status of the notifications as values:

- **RECEIVED** - App has received the notification. 
- **QUEUED** - App queues the notification for invoking the notification listener. 
- **OPENED** - User opens the notification by clicking the notification in the tray or by launching it from app icon or when the app is in foreground. 
- **DISMISSED** - User clears/dismisses the notification in the tray.

You need to register the **com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener** class with MFPPush.

```
	push.setNotificationStatusListener(new MFPPushNotificationStatusListener() {
	@Override
	public void onStatusChange(String messageId, MFPPushNotificationStatus status) {
		// Handle status change
	}
	});
```
    {: codeblock}


### Listening to the DISMISSED status

You can choose to listen to the DISMISSED status on either of the following conditions:

- When the app is active (running in foreground or background)

  Add the snippet to your `AndroidManifest.xml` file:

```
	<receiver android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationDismissHandler">
	<intent-filter>
	<action android:name="Your_Android_Package_Name.Cancel_IBMPushNotification"/>
	</intent-filter>
	</receiver>
```
	{: codeblock}

- When the app is both active (running in foreground or background) and not running (closed)

You need to extend the  **com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationDismissHandler** broadcast receiver and override the method **onReceive()**, where the **MFPPushNotificationStatusListener** should be registered before calling  method **onReceive()**of the base class.

```
	public class MyDismissHandler extends MFPPushNotificationDismissHandler {
	@Override
	public void onReceive(Context context, Intent intent) {
	MFPPush.getInstance().setNotificationStatusListener(new MFPPushNotificationStatusListener() {
	@Override
	public void onStatusChange(String messageId, MFPPushNotificationStatus status) {
	// Handle status change
	}
	});
	super.onReceive(context, intent);
	}
	}
```
    {: codeblock}


Add the following snippet to you `AndroidManifest.xml` file:

```
	<receiver android:name="Your_Android_Package_Name.Your_Handler">
	<intent-filter>
	<action android:name="Your_Android_Package_Name.Cancel_IBMPushNotification"/>
	</intent-filter>
	</receiver>
```
    {: codeblock}

## Sending basic {{site.data.keyword.mobilepushshort}}
{: #send}

After you have developed your applications, you can send basic push notifications.

To send basic push notifications, complete the steps:

1. Select **Send Notifications**, and compose a message by choosing a **Send to** option. The supported options are **Device by Tag**, **Device Id**, **User Id**, **Android devices**, **iOS devices**, **Web Notifications**, and **All Devices**.
**Note**: When you select the **All Devices** option, all devices subscribed to {{site.data.keyword.mobilepushshort}} will receive notifications.
![Notifications screen](images/tag_notification.jpg)

2. In the **Message** field, compose your message. Choose to configure the optional settings as required.
3. Click **Send**.
3. Verify that your devices have received your notification.

The following screen shot shows an alert box handling a push
notification in the foreground on a Android device.

![Foreground push notification on Android](images/Android_Screenshot.jpg)

The following following screen shot shows a push notification in the background for Android.

![Background push notification on Android](images/background.jpg)

### Optional Android settings for sending notifications
{: #send_otpional_setting}

You can further customize the {{site.data.keyword.mobilepushshort}} settings for sending notifications to Android devices. The following optional customization options are supported.
![Android custom settings](images/android_custom_settings.jpg)

- **Collapse Key**:  Collapse keys are attached to notifications. If multiple notifications arrive sequentially with the same collapse key when the device is offline, they are collapsed. When a device comes online, it receives notifications from the FCM/GCM server, and displays only the latest notification bearing the same collapse key. If the collapse key is not set, both the new and old messages are stored for the future delivery.
- **Sound**: Indicates a sound clip to be played on the receipt of a notification. Supports default or the name of a sound resource bundled in the app.
- **Icon**: Specify the name of the icon to be displayed for the notification. Ensure that you have packaged the icon in the res/drawable folder, with the client application.
- **Priority**: Specifies the options for assigning delivery priority to messages. A priority of `high` or `max` will result in heads-up notification, while `low` or `default` priority messages would not open network connections on a sleeping device. For messages with the option set to `min`, it will be a silent notification.
- **Visibility**: You can choose to set the notification visibility option to either `public` or `private`. The `private` option restricts public viewing and you can choose to enable it if your device is secure with a pin or pattern, and the notification setting is set to "Hide sensitive notification content". When the visibility is set as `private`, a "redact" field must be mentioned. Only the content specified in the redact field will show up on a secure locked screen on the device. Choosing `public` would render the notifications to be freely read.
- **Time to live**: This value is set in seconds. If this parameter is not specified, the FCM/GCM server stores the message for four weeks and will try to deliver. The validity expires after four weeks. The possible value range is from 0 to 2,419,200 seconds.
- **Delay when idle**: Setting this value to `true` instructs the FCM/GCM server not to deliver the notification if the device is idle. Set this value to `false`, to ensure delivery of notification even if the device is idle.
- **Sync**: By setting this option to `true`, notifications across all your registered devices are in sync. If the user with a username has multiple devices with the same application installed, reading the notification on one device ensures deletion of notifications in the other devices. You need to ensure that you are registered with {{site.data.keyword.mobilepushshort}} service with userId for this option to work.
- **Additional payload**: Specifies the custom payload values for your notifications.


## Next steps
{: #next_steps_tags}

After you have successfully set up basic notifications, you can configure configure tag-based notifications and advanced options.

Add these push notifications service features to your app.
To use tag-based notifications, see [Tag-based Notifications](c_tag_basednotifications.html).
To use advanced notifications options, see [Enabling advanced push notifications](t_advance_badge_sound_payload.html).
