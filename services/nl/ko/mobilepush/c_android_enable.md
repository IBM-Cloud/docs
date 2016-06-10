---

copyright:
 years: 2015 2016

---


# 푸시 알림을 수신하도록 Android 애플리케이션 설정
{: #tag_based_notifications}


푸시 알림을 수신하고 사용자 디바이스에 푸시 알림을 전송하도록 Android 애플리케이션 설정합니다.

## Gradle을 사용하여 클라이언트 푸시 SDK 설치
{: #android_install}

이 섹션에서는 클라이언트 푸시 SDK를 설치하고 이를 사용하여 추가적으로 Android 애플리케이션을 개발하는 방법에 대해 설명합니다.

Gradle을 사용하여 Bluemix® 모바일 서비스 푸시 SDK를 추가할 수 있습니다. Gradle은 저장소에서 아티팩트를 자동으로 다운로드하여 Android 애플리케이션에 제공합니다. Android Studio 및 Android Studio SDK를 올바로 설정해야 합니다. 시스템 설정 방법에 대한 자세한 정보는 [Android Studio 개요](https://developer.android.com/tools/studio/index.html)를 참조하십시오. Gradle에 대한 자세한 정보는 [Gradle 빌드 구성](http://developer.android.com/tools/building/configuring-gradle.html)을 참조하십시오.

1. Android Studio에서 모바일 애플리케이션을 작성하고 연 다음에 애플리케이션 **build.gradle** 파일을 여십시오. 다음 종속 항목을 모바일 애플리케이션에 추가하십시오. 이러한 import 문은 코드 스니펫에 필요합니다.

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


## Android 앱을 위한 푸시 SDK 초기화
{: #android_initialize}

초기화 코드를 배치하는 공통 위치는 Android 애플리케이션에서 기본 활동의 onCreate 메소드입니다. 

Bluemix 애플리케이션 대시보드의 **모바일 옵션** 링크를 클릭하여 애플리케이션 라우트와 애플리케이션 GUID를 확보하십시오. 라우트 및 앱 GUID에 이러한 값을 사용하십시오. Bluemix 앱 appRoute 및 appGUID 매개변수를 사용하려면 코드 스니펫을 수정하십시오. 


###Core SDK 초기화

```
// Initialize the SDK for Java (Android) with IBM Bluemix AppGUID and route
BMSClient.getInstance().initialize(getApplicationContext(), "applicationRoute","applicationGUID", bluemixRegion:"Location where your app Hosted");
```


**appRoute**

Bluemix에서 생성한 서버 애플리케이션에 지정된 라우트를 지정합니다.

**AppGUID**

Bluemix에서 생성한 애플리케이션에 지정된 고유 키를 지정합니다. 이 값은 대소문자를 구분합니다. 

**bluemixRegionSuffix**

앱이 호스트된 위치를 지정합니다. 다음 값 중 하나를 사용할 수 있습니다. 

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

###클라이언트 푸시 SDK 초기화

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext());
```

## Android 디바이스 등록
{: #android_register}

```IMFPush.register()``` API를 사용하여 디바이스를 푸시 알림 서비스에 등록할 수 있습니다. Android 디바이스의 등록인 경우, 우선 Bluemix 푸시 서비스 구성 대시보드에서 GCM(Google Cloud Messaging) 정보를 추가하십시오. 자세한 정보는 [GCM(Google Cloud Messaging)의 신임 정보 구성](t_push_provider_android.html)을 참조하십시오. 

다음 코드 스니펫을 복사하여 Android 모바일 애플리케이션에 붙여넣으십시오. 

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


## Android 디바이스에서 푸시 알림 수신
{: #android_receive}

notificationListener 오브젝트를 푸시에 등록하려면 **MFPPush.listen()** 메소드를 호출하십시오. 푸시 알림을 처리하는 활동의 **onResume()** 메소드에서 일반적으로 이 메소드가 호출됩니다. 

1. notificationListener 오브젝트를 푸시에 등록하려면 **listen()** 메소드를 호출하십시오. 푸시 알림을 처리하는 활동의 **onResume()** 메소드에서 일반적으로 이 메소드가 호출됩니다. 

	```
	@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
	       push.listen(notificationListener);
	   }
	}
```
2. 프로젝트를 빌드하고 디바이스 또는 에뮬레이터에서 이를 실행하십시오. register() 메소드의 응답 리스너에 대해 onSuccess() 메소드가 호출되면 디바이스가 푸시 알림 서비스에 정상적으로 푸시에 등록된 것입니다. 이 때 기본 푸시 알림 전송에 설명된 대로 메시지를 보낼 수 있습니다. 
3. 디바이스가 알림을 수신했는지 확인하십시오. 애플리케이션이 포그라운드에 있는 경우 **MFPPushNotificationListener**에 의해 알림이 처리됩니다. 애플리케이션이 백그라운드에 있는 경우 알림 막대에 메시지가 표시됩니다. 


## 기본 푸시 알림 전송
{: #send}

애플리케이션이 개발된 후에는 (태그, 배지, 추가 페이로드 또는 사운드 파일을 사용하지 않아도) 기본 푸시 알림을 전송할 수 있습니다. 


기본 푸시 알림을 보내십시오. 

1. **청취자 선택**에서 다음 청취자 중 하나를 선택하십시오. **모든 디바이스** 또는 플랫폼 기준으로 **iOS 디바이스만** 또는 **Anroid 디바이스만**. 

	**참고**: **모든 디바이스** 옵션을 선택하는 경우 푸시 알림에 구독된 모든 디바이스가 알림을 수신합니다. 

	![알림 화면](images/tag_notification.jpg)

2. **알림 작성**에서 메시지를 입력하고 **보내기**를 클릭하십시오.
3. 디바이스가 알림을 수신했는지 확인하십시오. 

	다음 스크린샷은 Android와 iOS 디바이스의 포그라운드에서
푸시 알림을 처리하는 경보 상자를 보여줍니다. 

	![Android의 포그라운드 푸시 알림](images/Android_Screenshot.jpg)

	![iOS의 포그라운드 푸시 알림](images/iOS_Screenshot.jpg)

	다음 스크린샷은 Android의 백그라운드에 있는 푸시 알림을 보여줍니다.
	![Android의 백그라운드 푸시 알림](images/background.jpg)



## 다음 단계
{: #next_steps_tags}

정상적으로 기본 알림을 설정한 후 태그 기반 알림 및 고급 옵션을 구성할 수 있습니다. 

다음의 푸시 알림 서비스 기능을 사용자의 앱에 추가하십시오.
태그 기반 알림을 사용하려면 [태그 기반 알림](c_tag_basednotifications.html)을 참조하십시오.
고급 알림 옵션을 사용하려면 [고급 푸시 알림](t_advance_notifications.html)을 참조하십시오. 
