    ---

copyright:
 years: 2015 2016

---


# Enabling Android applications to receive {{site.data.keyword.mobilepushshort}}
{: #tag_based_notifications}
Last updated: 29 August 2016
{: .last-updated}

You can enable Android applications to receive and send {{site.data.keyword.mobilepushshort}} to your devices.

## Installing the client Push SDK with Gradle
{: #android_install}

This section describes how to install and use the client Push SDK to further develop your Android applications.

Bluemix® Mobile Services Push SDK can be added using Gradle. Gradle automatically downloads artifacts from repositories and makes them available to your Android application. Ensure that you correctly set up Android Studio and the Android Studio SDK. For more information about how to set up your system, see [Android Studio Overview](https://developer.android.com/tools/studio/index.html). For information about Gradle, see [Configuring Gradle Builds](http://developer.android.com/tools/building/configuring-gradle.html).

1. In Android Studio, after creating and opening your mobile application, open your application **build.gradle** file. 
2. Add the following dependencies to your mobile application. These import statements are required for code snippets:

    ```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```
    {: codeblock}

2. Add the following dependencies to your mobile application. The following lines adds Bluemix™ Mobile services Push client SDK and the Google play services SDK to your compile scope dependencies.

	```
	dependencies {
	  compile group: 'com.ibm.mobilefirstplatform.clientsdk.android', 
		name: 'push', 
		version: '2.+',
		ext: 'aar', 
		transitive: true
	}  
	```
    {: codeblock}
3. In the **AndroidManifest.xml** file, add the following permissions. To view a sample manifest, see [Android helloPush Sample Application](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml). To view a sample Gradle file, see [Sample Build Gradle file](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle).

    ```
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="com.ibm.clientsdk.android.app.permission.C2D_MESSAGE" />
	<uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
	<uses-permission android:name="android.permission.WAKE_LOCK" />
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>

	```
	{: codeblock}

   Read more about [Android permissions](http://developer.android.com/guide/topics/security/permissions.html) here.

4. Add the notification intent settings for the activity. This setting starts the application when the user clicks the received notification from the notification area.

	```
	<intent-filter>  
		<action android:name="<Your_Android_Package_Name.IBMPushNotification"/>   
		<category  android:name="android.intent.category.DEFAULT"/>
	</intent-filter>
	```
	{: codeblock}
**Note**: Replace *Your_Android_Package_Name* in the previous action with the application package name used in your application.

5. Add the Google Cloud Messaging (GCM) intent service and intent filters for the RECEIVE event notifications.

	```
	service android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushIntentService" />

	<receiver
	    android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.internal.MFPPushBroadcastReceiver"
	    android:permission="com.google.android.c2dm.permission.SEND">
	    <intent-filter>
	        <action android:name="com.google.android.c2dm.intent.RECEIVE" />

	        <category android:name="com.ibm.mobilefirstplatform.clientsdk.android.app" />
	    </intent-filter>
	    <intent-filter>
	        <action android:name="android.intent.action.BOOT_COMPLETED" />

	        <category android:name="com.ibm.mobilefirstplatform.clientsdk.android.app" />
	    </intent-filter>
	</receiver>
	```
    {: codeblock}

## Initializing the Push SDK for Android apps
{: #android_initialize}

A common place to put the initialization code is in the onCreate method of the main activity in your Android application.

To get your App route and App GUID, select the Configuration option in the navigation pane for your initialized push services and click **Mobile Options**.
Use these values for your route and App GUID. Modify the code snippet to use your Bluemix app appRoute and appGUID parameters.


###Initialize the Core SDK

     ```
     // Initialize the SDK for Java (Android) with IBM Bluemix AppGUID and route
     BMSClient.getInstance().initialize(getApplicationContext(), appRoute , appGuid, bluemixRegionSuffix);

     ```
    {: codeblock}

####appRoute
{: approute}

Specifies the route that is assigned to the server application that you created on Bluemix.

####AppGUID
{: appguid_initilaize_core_sdk}

Specifies the unique key that is assigned to {{site.data.keyword.mobilepushshort}} service instance on Bluemix. This value is case-sensitive. You can get this value from Mobile Options on the Push Dashboard.

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
	push.initialize(getApplicationContext(), "AppGUID");
	```
	{: codeblock}

####AppGUID
{: appguid_initialize_client_push_sdk}

This is the AppGUID key of the {{site.data.keyword.mobilepushshort}} service.

## Registering Android devices
{: #android_register}

Use the `MFPPush.register()` API to register the device with {{site.data.keyword.mobilepushshort}} service. For registering for Android devices, add the Google Cloud Messaging (GCM) information in the Bluemix {{site.data.keyword.mobilepushshort}} service configuration dashboard. For more information, see [Configuring credentials for Google Cloud Messaging](t_push_provider_android.html).

Copy the following code snippets to your Android mobile application.

	```
	//Register Android devices
	push.registerDevice(new MFPPushResponseListener<String>() {
	    @Override
	    public void onSuccess(String deviceId) {
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

1. To register the notificationListener object with push, call the **listen()** method. This method is typically called from the **onResume()** method of the activity that is handling push notifications.

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

2. Build the project and run it on the device or emulator. When the onSuccess() method for the response listener in the register() method is invoked, it confirms that the device has successfully registered with {{site.data.keyword.mobilepushshort}} service. At this time you can send a message as described in Sending basic push notifications.
3. Verify that your devices have received your notification. If the application is in the foreground, the notification is handled by the **MFPPushNotificationListener**. If the application is in the background, a message is displayed in the notification bar.


## Sending basic {{site.data.keyword.mobilepushshort}}
{: #send}

After you have developed your applications, you can send basic push notifications (without using tags, badges, additional payloads, or sound files).

1. In **Choose the Audience**, select one of the following audiences: **All Devices**, or by platform: **Only iOS devices** or **Only Anroid devices**.

	**Note**: When you select the **All Devices** option, all devices subscribed to push notifications will receive notifications.

![Notifications screen](images/tag_notification.jpg)

2. In the **Create your Notification**, enter your message and then click **Send**.
3. Verify that your devices have received your notification. The following screen shot shows an alert box handling a push
notification in the foreground on a Android device.

![Foreground push notification on Android](images/Android_Screenshot.jpg)

The following following screen shot shows a push notification in the background for Android.

![Background push notification on Android](images/background.jpg)

### Optional settings for sending notifications
{: #send_otpional_setting}

You can further customize the {{site.data.keyword.mobilepushshort}} settings for sending notifications to Android devices. The following optional customization options are supported.
![Android custom settings](images/android_custom_settings.jpg)

- **Collapse Key**:  Collapse keys are attached to notifications. If multiple notifications arrive sequentially with the same collapse key when the device is offline, they are collapsed. When a device comes online, it receives notifications from the GCM server, and displays only the latest notification bearing the same collapse key. If the collapse key is not set, both the new and old messages are stored for the future delivery. 
- **Sound**: Indicates a sound clip to be played on the receipt of a notification. Supports default or the name of a sound resource bundled in the app.
- **Priority**: Specifies the options for assigning delivery priority to messages. A priority of `high` or `max` will result in heads-up notification, while `low` or `default` priority messages would not open network connections on a sleeping device. For messages with the option set to `min`, it will be a silent notification. 
- **Visibility**: You can choose to set the notification visibility option to either `public` or `private`. The `private` option restricts public viewing and you can choose to enable it if your device is secure with a pin or pattern, and the notification setting is set to "Hide sensitive notification content". When the visibility is set as `private`, a "redact" field must be mentioned. Only the content specified in the redact field will show up on a secure locked screen on the device. Choosing `public` would render the notifications to be freely read.
- **Time to live**: This value is set in seconds. If this parameter is not specified, the GCM server stores the message for four weeks and will try to deliver. The validity expires after four weeks. The possible value range is from 0 to 2,419,200 seconds.
- **Delay when idle**: Setting this value to `true` instructs the GCM server not to deliver the notification if the device is idle. Set this value to `false`, to ensure delivery of notification even if the device is idle. 
- **Sync**: By setting this option to `true`, notifications across all your registered devices are in sync. If the user with a username has multiple devices with the same application installed, reading the notification on one device ensures deletion of notifications in the other devices. You need to ensure that you are registered with {{site.data.keyword.mobilepushshort}} service with userId for this option to work.  
- **Additional payload**: Specifies the custom payload values for your notifications.
 

## Next steps
{: #next_steps_tags}

After you have successfully set up basic notifications, you can configure configure tag-based notifications and advanced options.

Add these push notifications service features to your app.
To use tag-based notifications, see [Tag-based Notifications](c_tag_basednotifications.html).
To use advanced notifications options, see [Advanced push notifications](t_advance_notifications.html).
