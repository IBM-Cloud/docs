---

copyright:
 years: 2015, 2016

---

# Installing the client Push SDK with Gradle
{: #android_install}

This section describes how to install and use the client Push SDK to further develop your Android applications.

Bluemix® mobile services Push SDK can be added using Gradle. Gradle automatically downloads artifacts from repositories and makes them available to your Android application. Make sure that you correctly set up Android Studio and the Android Studio SDK. For more information about how to set up your system, see [Android Studio Overview](https://developer.android.com/tools/studio/index.html). For information about Gradle, see [Configuring Gradle Builds](http://developer.android.com/tools/building/configuring-gradle.html).

1. In Android Studio, after creating and opening your mobile application, open your application **build.gradle** file. Then add the following dependencies to your mobile application. These import statements are required for the code snippets that are listed below.

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
