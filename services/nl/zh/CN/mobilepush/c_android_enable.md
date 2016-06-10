---

copyright:
 years: 2015 2016

---


# 使 Android 应用程序能够接收推送通知
{: #tag_based_notifications}


使 Android 应用程序能够接收推送通知，并向您的设备发送推送通知。

## 使用 Gradle 安装客户机推送 SDK
{: #android_install}

本部分描述如何安装和使用客户机推送 SDK 来进一步开发 Android 应用程序。

可以使用 Gradle 来添加 Bluemix® Mobile Services 推送 SDK。Gradle 会从存储库自动下载工件，并使这些工件可用于您的 Android 应用程序。确保正确设置了 Android Studio 和 Android Studio SDK。有关如何设置系统的更多信息，请参阅 [Android Studio 概述](https://developer.android.com/tools/studio/index.html)。有关 Gradle 的信息，请参阅[配置 Gradle 构建](http://developer.android.com/tools/building/configuring-gradle.html)。

1. 在 Android Studio 中，创建并打开移动应用程序后，打开应用程序 **build.gradle** 文件。然后，将以下依赖关系添加到移动应用程序中。代码片段需要这些导入语句：

	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```


1. 将以下依赖关系添加到移动应用程序中。以下这些行会将 Bluemix™ Mobile Services 推送客户机 SDK 和 Google 播放服务 SDK 添加到编译作用域依赖关系中。

	```
	dependencies {
	  compile 'com.ibm.mobilefirstplatform.clientsdk.android:push:1.+' 
compile 'com.google.android.gms:play-services:7.8.0' 
}  
	```
1. 在 **AndroidManifest.xml** 文件中，添加以下许可权，要查看样本清单，请参阅 [Android helloPush 样本应用程序](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml)。要查看样本 Gradle 文件，请参阅[样本构建 Gradle 文件](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle)。

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

	您可以在此阅读有关 [Android 许可权](http://developer.android.com/guide/topics/security/permissions.html)的更多信息。

1. 添加活动的通知意向设置。此设置会在用户单击通知区域中收到的通知时启动应用程序。

	```
	<intent-filter>  
		<action android:name="<Your_Android_Package_Name.IBMPushNotification"/>   
		<category  android:name="android.intent.category.DEFAULT"/>
	</intent-filter>
	```
	**注**：将上述操作中的 *Your_Android_Package_Name* 替换为应用程序中使用的应用程序包名称。

1. 针对 RECEIVE 事件通知，添加 Google 云消息传递 (GCM) 意向服务和意向过滤器。

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


## 为 Android 应用程序初始化推送 SDK
{: #android_initialize}

在 Android 应用程序中，通常会将初始化代码放置在主活动的 onCreate 方法中。

单击 Bluemix 应用程序仪表板中的**移动选项**链接，以获取应用程序路径和应用程序 GUID。将这些值用于您的路径和应用程序 GUID。修改代码片段以使用 Bluemix 应用程序的 appRoute 和 appGUID 参数。


###初始化核心 SDK

```
// Initialize the SDK for Java (Android) with IBM Bluemix AppGUID and route
BMSClient.getInstance().initialize(getApplicationContext(), "applicationRoute","applicationGUID", bluemixRegion:"Location where your app Hosted");
```


**appRoute**

指定分配给在 Bluemix 上创建的服务器应用程序的路径。

**AppGUID**

指定分配给在 Bluemix 上创建的应用程序的唯一键。此值区分大小写。

**bluemixRegionSuffix**

指定托管应用程序的位置。可以使用以下三个值中的一个值：

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

###初始化客户机推送 SDK

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext());
```

## 注册 Android 设备
{: #android_register}

使用 ```IMFPush.register()``` API 可向 Push Notification Service 注册设备。对于注册 Android 设备，您首先要在 Bluemix 推送服务配置仪表板中添加 Google 云消息传递 (GCM) 信息。有关更多信息，请参阅[为 Google 云消息传递配置凭证](t_push_provider_android.html)。

将以下代码片段复制并粘贴到 Android 移动应用程序中。

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


## 在 Android 设备上接收推送通知
{: #android_receive}

要向 Push 注册 notificationListener 对象，请调用 **MFPPush.listen()** 方法。此方法通常是通过处理推送通知的活动的 **onResume()** 方法进行调用。

1. 要向 Push 注册 notificationListener 对象，请调用 **listen()** 方法。此方法通常是通过处理推送通知的活动的 **onResume()** 方法进行调用。

	```
	@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
	       push.listen(notificationListener);
	   }
	}
```
2. 构建项目，然后在设备或仿真器上运行该项目。在 register() 方法中针对响应侦听器调用 onSuccess() 方法时，这证实设备已成功向 Push Notification Service 进行注册。此时，可以如“发送基本推送通知”中所述发送消息。
3. 验证设备是否收到通知。如果应用程序在前台运行，那么通知将由 **MFPPushNotificationListener** 进行处理。如果应用程序在后台运行，那么通知栏中会显示一条消息。


## 发送基本推送通知
{: #send}

开发应用程序后，可以发送基本推送通知（不使用标记、角标、其他有效内容或声音文件）。


发送基本推送通知。

1. 在**选择受众**中，选择以下某个受众：**所有设备**，或者按平台选择：**仅限 iOS 设备**或**仅限 Android 设备**。

	**注**：选择**所有设备**选项时，预订了推送通知的所有设备都会收到您的通知。

	![“通知”屏幕](images/tag_notification.jpg)

2. 在**创建通知**中，输入消息，然后单击**发送**。
3. 验证设备是否收到通知。

	以下屏幕快照显示了在 Android 和 iOS 设备上前台处理推送通知的警报框。

	![Android 上的前台推送通知](images/Android_Screenshot.jpg)

	![iOS 上的前台推送通知](images/iOS_Screenshot.jpg)

	以下屏幕快照显示了 Android 后台的推送通知。
 ![Android 上的后台推送通知](images/background.jpg)



## 后续步骤
{: #next_steps_tags}

成功设置基本通知后，可以配置基于标记的通知和高级选项。

将这些 Push Notifications Service 功能添加到应用程序中。要使用基于标记的通知，请参阅[基于标记的通知](c_tag_basednotifications.html)。要使用高级通知选项，请参阅[高级推送通知](t_advance_notifications.html)。
