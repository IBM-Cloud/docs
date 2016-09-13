---

copyright:
 years: 2015, 2016

---

# Gradle을 사용하여 클라이언트 푸시 SDK 설치
{: #android_install}

이 섹션에서는 클라이언트 푸시 SDK를 설치하고 이를 사용하여 추가적으로 Android 애플리케이션을 개발하는 방법에 대해 설명합니다.

Gradle을 사용하여 Bluemix® 모바일 서비스 푸시 SDK를 추가할 수 있습니다. Gradle은 저장소에서 아티팩트를 자동으로 다운로드하여 Android 애플리케이션에 제공합니다. Android Studio 및 Android Studio SDK를 올바로 설정해야 합니다. 시스템 설정 방법에 대한 자세한 정보는 [Android Studio 개요](https://developer.android.com/tools/studio/index.html)를 참조하십시오. Gradle에 대한 자세한 정보는 [Gradle 빌드 구성](http://developer.android.com/tools/building/configuring-gradle.html)을 참조하십시오.

1. Android Studio에서 모바일 애플리케이션을 작성하고 연 다음에 애플리케이션 **build.gradle** 파일을 여십시오. 다음 종속 항목을 모바일 애플리케이션에 추가하십시오. 이러한 가져오기 명령은 다음에 나열된 코드 스니펫에 필요합니다.

	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```


1. 다음 종속 항목을 모바일 애플리케이션에 추가하십시오. 다음 행이 Bluemix™ Mobile Services Push 클라이언트 SDK 및 Google 플레이 서비스 SDK를 사용자의 컴파일 범위 종속 항목에 추가합니다. 

	```
	dependencies {
	  compile 'com.ibm.mobilefirstplatform.clientsdk.android:push:1.+' 
compile 'com.google.android.gms:play-services:7.8.0' 
}  
	```
1. **AndroidManifest.xml** 파일에서 다음 권한을 추가하십시오. 샘플 Manifest를 보려면 [Android helloPush 샘플 애플리케이션](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml)을 참조하십시오. 샘플 Gradle 파일을 보려면 [샘플 빌드 Gradle 파일](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle)을 참조하십시오.

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

	여기에서 [Android 권한](http://developer.android.com/guide/topics/security/permissions.html)에 대한 정보를 볼 수 있습니다. 

1. 활동에 대한 알림 의도 설정을 추가하십시오. 사용자가 알림 영역에서 수신한 알림을 클릭할 경우 이 설정을 통해 애플리케이션이 시작됩니다. 

	```
	<intent-filter>  
		<action android:name="<Your_Android_Package_Name.IBMPushNotification"/>   
		<category  android:name="android.intent.category.DEFAULT"/>
	</intent-filter>
	```
	**참고**: 위의 조치에서 *Your_Android_Package_Name*을 사용자 애플리케이션에서 사용되는 애플리케이션 패키지 이름으로 대체하십시오. 

1. GCM(Google Cloud Messaging) 의도 서비스 및 RECEIVE 이벤트 알림에 대한 의도 필터를 추가하십시오.

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
