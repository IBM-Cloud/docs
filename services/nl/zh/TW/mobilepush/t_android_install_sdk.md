---

copyright:
 years: 2015, 2016

---

# 使用 Gradle 安裝 Client Push SDK
{: #android_install}

本節說明如何安裝及使用 Client Push SDK 來進一步開發 Android 應用程式。

Bluemix® Mobile Services Push SDK 可以使用 Gradle 進行新增。Gradle 會從儲存庫中自動下載構件，並讓它們可供 Android 應用程式使用。請確定您已正確設定 Android Studio 及 Android Studio SDK。如需如何設定系統的相關資訊，請參閱 [Android Studio 概觀](https://developer.android.com/tools/studio/index.html)。如需 Gradle 的相關資訊，請參閱[配置 Gradle 建置](http://developer.android.com/tools/building/configuring-gradle.html)。

1. 在 Android Studio 中，建立並開啟行動式應用程式之後，開啟應用程式 **build.gradle** 檔案。然後，將下列相依關係新增至行動式應用程式。下面列出的程式碼 Snippet 需要這些 import 陳述式。

	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```


1. 將下列相依關係新增至行動式應用程式。下列數行會將 Bluemix™ Mobile Services Push Client SDK 及 Google Play Services SDK 新增至您的編譯範圍相依關係。

	```
	dependencies {
	  compile 'com.ibm.mobilefirstplatform.clientsdk.android:push:1.+' 
compile 'com.google.android.gms:play-services:7.8.0' 
}  
	```
1. 在 **AndroidManifest.xml** 檔案中，新增下列許可權。若要檢視範例資訊清單，請參閱 [Android helloPush 範例應用程式](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml)。若要檢視範例 Gradle 檔案，請參閱[範例建置 Gradle 檔案](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle)。

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

	您可以在這裡閱讀 [Android 許可權](http://developer.android.com/guide/topics/security/permissions.html)的相關資訊。

1. 新增活動的通知目的設定。此設定會在使用者按一下通知區域中的接收通知時啟動應用程式。

	```
	<intent-filter>  
		<action android:name="<Your_Android_Package_Name.IBMPushNotification"/>   
		<category  android:name="android.intent.category.DEFAULT"/>
	</intent-filter>
	```
	**附註**：將上面動作中的 *Your_Android_Package_Name* 取代為您應用程式中所使用的應用程式套件名稱。

1. 新增 RECEIVE 事件通知的 Google Cloud Messaging (GCM) 目的服務及目的過濾器。

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
