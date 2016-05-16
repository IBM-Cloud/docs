---

copyright:
 years: 2015, 2016

---

# Installing the client Push SDK with Gradle
{: #android_install}

This section describes how to install and use the client Push SDK to further develop your Android applications.

Bluemix® mobile services Push SDK can be added using Gradle. Gradle automatically downloads artifacts from repositories and makes them available to your Android application. Make sure that you correctly set up Android Studio and the Android Studio SDK. For more information about how to set up your system, see [Android Studio Overview](https://developer.android.com/tools/studio/index.html). For information about Gradle, see [Configuring Gradle Builds](http://developer.android.com/tools/building/configuring-gradle.html).

1. In Android Studio, after creating and opening your mobile application, open your application **build.gradle** file. Then add the following dependencies to your mobile application. These import statements are required for the code snippets:

	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```


1. Add the following dependencies to your mobile application. The following lines add the Bluemix™ Mobile Services Push client SDK and the Google play services SDK to your compile scope dependencies.

	```
	dependencies {
	  compile 'com.ibm.mobilefirstplatform.clientsdk.android:push:1.+'
	  compile 'com.google.android.gms:play-services:7.8.0'
	}  
	```
1. In the **AndroidManifest.xml** file, add the following permissions. To view a sample manifest, see [Android helloPush Sample Application](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml). To view a sample Gradle file, see [Sample Build Gradle file](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle).

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

	You can read more about [Android permissions](http://developer.android.com/guide/topics/security/permissions.html) here.

1. Add the notification intent settings for the activity. This setting starts the application when the user clicks the received notification from the notification area.

	```
	<intent-filter>  
		<action android:name="<Your_Android_Package_Name.IBMPushNotification"/>   
		<category  android:name="android.intent.category.DEFAULT"/>
	</intent-filter>
	```
	**Note**: Replace *Your_Android_Package_Name* in the action above with the application package name used in your application.

1. Add the Google Cloud Messaging (GCM) intent service and intent filters for the RECEIVE event notifications.

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



# Initializing the Push SDK for Android apps
{: #android_initialize}

A common place to put the initialization code is in the onCreate method of the main activity in your Android application.

Click the **Mobile Options** link in your Bluemix Application Dashboard to get the application route and applicationGUID. Use these values for your route and App GUID. Modify the code snippet to use your Bluemix app appRoute and appGUID parameters.


##Initialize the Core SDK

```
// Initialize the SDK for Java (Android) with IBM Bluemix AppGUID and route
BMSClient.getInstance().initialize(getApplicationContext(), "applicationRoute","applicationGUID", bluemixRegion:"Location where your app Hosted");
```


**appRoute**

Specifies the route that is assigned to the server application that you created on Bluemix.

**AppGUID**

Specifies the unique key that is assigned to the application that you created on Bluemix. This value is case-sensitive.

**bluemixRegionSuffix**

Specifies the location where the app hosted. You can use one of three values:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

##Initialize the client Push SDK

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext());
```



# Registering Android devices
{: #android_register}

Use the ```IMFPush.register()``` API to register the device with a Push Notification Service. For registering for Android devices, you first add the Google Cloud Messaging (GCM) information in the Bluemix push service configuration dashboard. For more information, see [Configuring credentials for Google Cloud Messaging](t_push_provider_android.html).

Copy and paste the following code snippets into your Android mobile application.

```
	//Register Android devices
	push.register(new MFPPushResponseListener<String>() {
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

```
	//Handles the notification when it arrives
	MFPPushNotificationListener notificationListener = new MFPPushNotificationListener() {
	    @Override
	    public void onReceive (final MFPSimplePushNotification message){
	      // Handle Push Notification
	    }
	};
```



# Receiving push notifications on Android devices
{: #android_receive}

To register the notificationListener object with Push, call the **MFPPush.listen()** method. This method is typically called from the **onResume()** method of the activity that is handling push notifications.

1. To register the notificationListener object with Push, call the **listen()** method. This method is typically called from the **onResume()** method of the activity that is handling push notifications.

	```
	@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
	       push.listen(notificationListener);
	   }
	}
```
2. Build the project and run it on the device or emulator. When the onSuccess() method for the response listener in the register() method is invoked, it confirms that the device has successfully registered with Push Notification Service. At this time you can send a message as described in Sending basic push notifications.
3. Verify that your devices have received your notification. If the application is in the foreground, the notification is handled by the **MFPPushNotificationListener**. If the application is in the background, a message is displayed in the notification bar.




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
