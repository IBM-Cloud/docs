---

copyright:
 years: 2015 2016

---


# 讓 Android 應用程式可接收推送通知
{: #tag_based_notifications}


讓 Android 應用程式可接收推送通知，以及將推送通知傳送給您的裝置。

## 使用 Gradle 安裝 Client Push SDK
{: #android_install}

本節說明如何安裝及使用 Client Push SDK 來進一步開發 Android 應用程式。

Bluemix® Mobile Services Push SDK 可以使用 Gradle 進行新增。Gradle 會從儲存庫中自動下載構件，並讓它們可供 Android 應用程式使用。請確定您已正確設定 Android Studio 及 Android Studio SDK。如需如何設定系統的相關資訊，請參閱 [Android Studio 概觀](https://developer.android.com/tools/studio/index.html)。如需 Gradle 的相關資訊，請參閱[配置 Gradle 建置](http://developer.android.com/tools/building/configuring-gradle.html)。

1. 在 Android Studio 中，建立並開啟行動式應用程式之後，開啟應用程式 **build.gradle** 檔案。然後，將下列相依關係新增至行動式應用程式。程式碼 Snippet 需要這些 import 陳述式：

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


## 起始設定 Push SDK for Android 應用程式
{: #android_initialize}

放置起始設定碼的一般位置位於 Android 應用程式之主要活動的 onCreate 方法中。

按一下「Bluemix 應用程式儀表板」中的**行動式選項**鏈結，以取得應用程式的路徑及應用程式 GUID。將這些值用於您的路徑和應用程式 GUID。修改程式碼 Snippet，以使用 Bluemix 應用程式 appRoute 及 appGUID 參數。


###起始設定 Core SDK

```
// Initialize the SDK for Java (Android) with IBM Bluemix AppGUID and route
BMSClient.getInstance().initialize(getApplicationContext(), "applicationRoute","applicationGUID", bluemixRegion:"Location where your app Hosted");
```


**appRoute**

指定指派給您在 Bluemix 上所建立之伺服器應用程式的路徑。

**AppGUID**

指定指派給您在 Bluemix 上所建立之應用程式的唯一索引鍵。此值區分大小寫。

**bluemixRegionSuffix**

指定管理應用程式的位置。您可以使用下列三個值的其中一個：

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

###起始設定 Client Push SDK

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext());
```

## 登錄 Android 裝置
{: #android_register}

使用 ```IMFPush.register()``` API，以向 Push Notification Service 登錄裝置。如需登錄 Android 裝置，您要先在 Bluemix Push 服務配置儀表板中新增 Google Cloud Messaging (GCM) 資訊。如需相關資訊，請參閱[配置 Google Cloud Messaging 的認證](t_push_provider_android.html)。

複製下列程式碼 Snippet，並將其貼入 Android 行動式應用程式。

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


## 在 Android 裝置上接收推送通知
{: #android_receive}

若要向 Push 登錄 notificationListener 物件，請呼叫 **MFPPush.listen()** 方法。此方法一般是透過處理推送通知之活動的 **onResume()** 方法所呼叫。

1. 若要向 Push 登錄 notificationListener 物件，請呼叫 **listen()** 方法。此方法一般是透過處理推送通知之活動的 **onResume()** 方法所呼叫。

	```
	@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
	       push.listen(notificationListener);
	   }
	}
```
2. 建置專案，並在裝置或模擬器上執行該專案。在 register() 方法中呼叫回應接聽器的 onSuccess() 方法時，它會確認已順利向 Push Notification Service 登錄裝置。此時，您可以如「傳送基本推送通知」所述傳送訊息。
3. 驗證您的裝置已接收到通知。如果應用程式是在前景中，則 **MFPPushNotificationListener** 會處理通知。如果應用程式是在背景中，則會在通知列中顯示一則訊息。


## 傳送基本推送通知
{: #send}

開發應用程式之後，您可以傳送基本推送通知（不需要使用標籤、徽章、其他有效負載或音效檔）。


傳送基本推送通知。

1. 在**選擇對象**中，選取下列其中一個對象：**所有裝置**，或依平台：**僅限 IOS 裝置**或**僅限 Anroid 裝置**。

	**附註**：當您選取**所有裝置**選項時，所有已訂閱推送通知的裝置都會接收到您的通知。

	![通知畫面](images/tag_notification.jpg)

2. 在**建立您的通知**中，輸入您的訊息，然後按一下**傳送**。
3. 驗證您的裝置已接收到通知。

	下列擷取畫面顯示在 Android 及 iOS 裝置的前景中處理推送通知的警示框。

	![Android 上的前景推送通知](images/Android_Screenshot.jpg)

	![iOS 上的前景推送通知](images/iOS_Screenshot.jpg)

	下列擷取畫面顯示 Android 背景中的推送通知。
	![Android 上的背景推送通知](images/background.jpg)



## 後續步驟
{: #next_steps_tags}

順利設定基本通知之後，您就可以配置標籤型通知及進階選項。

將這些 Push Notifications Service 特性新增至您的應用程式。
若要使用標籤型通知，請參閱[標籤型通知](c_tag_basednotifications.html)。
若要使用進階通知選項，請參閱[進階推送通知](t_advance_notifications.html)。
