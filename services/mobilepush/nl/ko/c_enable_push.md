---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 모바일 디바이스의 알림 사용
{: #c_enable_push-notifications}
마지막 업데이트 날짜: 2017년 4월 12일
{: .last-updated}

[알림 제공자의 신임 정보 구성](t__main_push_config_provider.html)을 수행했는지 확인하십시오.

이 섹션에서는 모바일, 웹 브라우저 애플리케이션과 같은 클라이언트 애플리케이션과 Chrome 앱 및 확장 프로그램에서 푸시 알림을 수신하도록 설정하는 방법, 기본 알림을 작성하고 SDK 또는 플러그인을 가져와서 초기화하는 방법, 푸시 알림을 수신하기 위해 디바이스 또는 브라우저를 등록하는 방법에 대해 설명합니다. [REST API](t_restapi.html)를 사용하여 모바일 및 웹 브라우저 애플리케이션이 푸시 알림을 수신하도록 설정할 수도 있습니다.

**참고**: 디바이스, 브라우저, Chrome 앱 및 확장 프로그램 등록의 경우 {{site.data.keyword.mobilepushshort}} 서비스는 알림 제공자(Apple의 경우 APNs 또는 Google의 경우 FCM)가 발행한 토큰에 대한
고유 참조를 유지보수합니다. 몇 가지 이유로 {{site.data.keyword.mobilepushshort}} 서비스 알림 제공자가 토큰을 무효화할 수 있습니다.  

예를 들어, 디바이스에서 앱을 설치 제거하는 경우입니다. 이와 같은 시나리오에서 디바이스가 무효화되는 제공자 응답을 기반으로 알림을 전달하려고 하면 {{site.data.keyword.mobilepushshort}} 서비스가 디바이스 또는 웹 브라우저 등록을 제거합니다. 그런 다음 이러한 무효화된 디바이스에 알림을 전송하려는 시도를 제한합니다. 


## 푸시 알림을 수신하도록 Android 애플리케이션 설정
{: #tag_based_notifications}


Android 애플리케이션에서 사용자 디바이스에 푸시 알림을 수신하도록 설정할 수 있습니다. Android Studio는 필수 소프트웨어이며 이를 사용하여 Android 프로젝트를 빌드하는 것이 좋습니다. Android Studio에 대한 기본 지식이 반드시 필요합니다. 

### Gradle을 사용하여 클라이언트 푸시 SDK 설치
{: #android_install}

이 섹션에서는 클라이언트 푸시 SDK를 설치하고 이를 사용하여 추가적으로 Android 애플리케이션을 개발하는 방법에 대해 설명합니다.

저장소에서 아티팩트를 자동으로 다운로드하고 Android 애플리케이션에서 이를 사용할 수 있도록 하는 [Gradle ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://developer.android.com/tools/building/configuring-gradle.html){: new_window}을 사용하여 {{site.data.keyword.Bluemix}} 모바일 서비스 푸시 SDK를 추가할 수 있습니다. [Android Studio ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.android.com/tools/studio/index.html) 및 Android Studio SDK를 올바르게 설정했는지 확인하십시오.  

모바일 애플리케이션이 작성되고 열리면 Android Studio를 사용하여 다음 단계를 완료하십시오. 

1. 모듈 레벨 **build.gradle** 파일에 종속 항목을 추가하십시오.  	

	- 다음 종속 항목을 추가하여 Bluemix™ 모바일 서비스 푸시 클라이언트 SDK 및 Google 플레이 서비스 SDK를 사용자의 컴파일 범위 종속 항목에 추가하십시오. 
	```
	com.ibm.mobilefirstplatform.clientsdk.android:push:3.+
	```
    	{: codeblock}
	
	- 코드 스니펫에 필요한 import 문에 다음 종속 항목을 추가하십시오. 
	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```
    	{: codeblock}

	- 끝에 있는 모듈 레벨 **build.gradle** 파일에 다음 종속 항목을 추가하십시오.
	```
		apply plugin: 'com.google.gms.google-services'
	```
		{: codeblock}
3. 프로젝트 레벨 **build.gradle** 파일에 다음 종속 항목을 추가하십시오. 
```
dependencies {
    classpath 'com.android.tools.build:gradle:2.2.3'
    classpath 'com.google.gms:google-services:3.0.0'
}
``` 
    {: codeblock}
5. **AndroidManifest.xml** 파일에서 다음 권한을 추가하십시오. 샘플 Manifest을 보려면 [Android helloPush 샘플 애플리케이션 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml){: new_window}을 참조하십시오. 샘플 Gradle 파일을 보려면 [샘플 빌드 Gradle 파일 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle){: new_window}을 참조하십시오. 
```
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
```
	{: codeblock}
 여기서 [Android 권한 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://developer.android.com/guide/topics/security/permissions.html){: new_window}에 대해 알아봅니다.

4. 활동에 대한 알림 의도 설정을 추가하십시오. 사용자가 알림 영역에서 수신한 알림을 클릭할 경우 이 설정을 통해 애플리케이션이 시작됩니다. 
```
	<intent-filter>
	<action android:name="Your_Android_Package_Name.IBMPushNotification"/>
	<category  android:name="android.intent.category.DEFAULT"/>
</intent-filter>
```
	{: codeblock}
**참고**: 위의 조치에서 *Your_Android_Package_Name*을 사용자 애플리케이션에서 사용되는 애플리케이션 패키지 이름으로 대체하십시오.

5. RECEIVE 및 REGISTRATION 이벤트 통지용으로 FCM(Firebase Cloud Messaging) 또는 GCM(Google Cloud Messaging) 의도 서비스 및 의도 필터를 추가하십시오. 
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

6. {{site.data.keyword.mobilepushshort}} 서비스는 알림 트레이에서 개별 알림을 검색하도록 지원합니다. 알림 트레이에서 액세스하는 알림의 경우 클릭하는 알림에 대한 핸들만 사용자에게 제공됩니다. 애플리케이션이 정상적으로 열리면 모든 알림이 표시됩니다. 이 기능을 사용하려면 다음 스니펫으로 **AndroidManifest.xml** 파일을 업데이트하십시오. 

```
	<activity android:name="
	com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationHandler"
	android:theme="@android:style/Theme.NoDisplay"/>
```
    {: codeblock}

[알림 제공자의 신임 정보 구성](t__main_push_config_provider.html)을 수행하여 FCM 프로젝트를 설정하고 신임 정보를 가져왔는지 확인하십시오. FCM(Firebase Cloud Messaging) 콘솔을 사용하여 다음 단계를 완료하십시오. 

1. Firebase 콘솔에서 **프로젝트 설정** 아이콘을 클릭하십시오.
	![Firebase 프로젝트 설정](images/FCM_4.jpg)

3. 앱 분할창의 일반 탭에서 **앱 추가** 또는 **Android 앱에 Firebase 추가 아이콘**을 선택하십시오.
    ![Android에 Firebase 추가](images/FCM_5.jpg)

4. Android 앱에 Firebase 추가 창에서 패키지 이름으로 **com.ibm.mobilefirstplatform.clientsdk.android.push**를 추가하십시오. 앱 닉네임 필드는 선택사항입니다. **앱 추가**를 클릭하십시오.
    ![Android에 Firebase 추가 창](images/FCM_1.jpg)

5. 'Android 앱에 Firebase 추가' 창에서 패키지 이름을 입력하여 애플리케이션의 패키지 이름을 포함하십시오. 앱 닉네임 필드는 선택사항입니다. **앱 추가**를 클릭하십시오.  

	![애플리케이션의 패키지 이름 추가](images/FCM_2.jpg)

6. `google-services.json` 파일이 생성됩니다. `google-services.json` 파일을 Android 애플리케이션 모듈 루트 디렉토리에 복사하십시오. `google-service.json` 파일에 추가된 패키지 이름이 포함됩니다. 

    ![애플리케이션의 루트 디렉토리에 json 파일 추가](images/FCM_7.jpg)

5. Android 앱에 Firebase 추가 창에서 **계속**을 클릭하고 **완료**를 클릭하십시오. 

  

애플리케이션을 빌드하고 실행하십시오. 

### Android 앱을 위한 푸시 SDK 초기화
{: #android_initialize}

초기화 코드를 배치하는 공통 위치는 Android 애플리케이션에서 기본 활동의 onCreate 메소드입니다. 초기화해야 하는 두 개의 SDK 컴포넌트가 있습니다. 하나는 코어 SDK이며 다른 하나는 코어 SDK에서 빌드된 푸시 SDK입니다. 

#### Core SDK 초기화
{: #initz_core_sdk}

```
// Initialize the SDK for Android
    BMSClient.getInstance().initialize(this, BMSClient.REGION_US_SOUTH);
```
    {: codeblock}

#### bluemixRegionSuffix
{: #bluemixRegionSuffix}

앱이 호스트된 위치를 지정합니다. 다음 세 값 중 하나를 사용할 수 있습니다. 

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

#### 클라이언트 푸시 SDK 초기화
{: #initiz_client_pushSDK}

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext(), "appGUID", "clientSecret");
```
	{: codeblock}

#### AppGUID
{: #appguid_initialize_client_push_sdk}

{{site.data.keyword.mobilepushshort}} 서비스의 AppGUID 키입니다. 이 값은 대소문자를 구분합니다. Push Notification 대시보드를 열고 구성 탭을 선택하십시오. Push Notification 서비스 대시보드에 있는 구성 탭의 모바일 옵션에서 이 값을 가져올 수 있습니다.  

### Android 디바이스 등록
{: #android_register}

`MFPPush.register()` API를 사용하여 {{site.data.keyword.mobilepushshort}} 서비스에 디바이스를 등록합니다. Android 디바이스를 등록하려면 Bluemix {{site.data.keyword.mobilepushshort}} 서비스 구성 대시보드에서 FCM(Firebase Cloud Messaging) 정보를 추가하십시오. 자세한 정보는 [알림 제공자의 신임 정보 구성](t__main_push_config_provider.html)을 참조하십시오. 

다음 코드 스니펫을 Android 모바일 애플리케이션에 복사하십시오. 

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

### Android 디바이스에서 푸시 알림 수신
{: #android_receive}

1. Push Notifications 서비스에서 notificationListener 오브젝트를 등록하려면 `MFPPush.listen()` 메소드를 사용하십시오. 이 메소드는 일반적으로 푸시 알림을 처리하는 활동의 `onResume()` 및 `onPause` 메소드에서 호출됩니다. 
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

2. 프로젝트를 빌드하고 디바이스 또는 에뮬레이터에서 이를 실행하십시오. register() 메소드의 응답 리스너에 대해 onSuccess() 메소드가 호출되는 경우, 이는 디바이스가 {{site.data.keyword.mobilepushshort}} 서비스에 정상적으로 등록되었는지 확인하며 이제 사용자는 푸시 알림을 전송할 수 있습니다. 
3. 디바이스가 알림을 수신했는지 확인하십시오. 애플리케이션이 포그라운드에 있는 경우 `MFPPushNotificationListener`에 의해 알림이 처리됩니다. 애플리케이션이 백그라운드에 있는 경우 알림 막대에 메시지가 표시됩니다. 

### Android 디바이스에서 푸시 알림 모니터링
{: #android_monitor}

`com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener` 인터페이스를 구현하고 onStatusChange(String messageId, MFPPushNotificationStatus status) 메소드를 정의하여 애플리케이션 내의 현재 알림 상태를 모니터할 수 있습니다.  

`messageId`는 서버에서 발송한 메시지의 ID입니다. `MFPPushNotificationStatus`는 알림 상태를 값으로 정의합니다. 

- RECEIVED - 앱에서 알림을 수신했습니다.  
- QUEUED - 앱에서 알림 리스너의 호출을 위해 알림을 큐에 지정합니다.  
- OPENED - 트레이의 알림을 클릭하거나 앱 아이콘에서 이를 실행하여 또는 앱이 포그라운드 상태일 때 사용자가 알림을 엽니다.  
- DISMISSED - 사용자가 트레이의 알림을 지우거나 해제합니다. 

`com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener` 클래스를 MFPPush와 함께 등록해야 합니다. 

```
	push.setNotificationStatusListener(new MFPPushNotificationStatusListener() {
	@Override
	public void onStatusChange(String messageId, MFPPushNotificationStatus status) {
		// Handle status change
	}
	});
```
    {: codeblock}


#### DISMISSED 상태 청취
{: #android_monitor_listen}

다음 조건 중 하나에 대한 DISMISSED 상태를 청취하도록 선택할 수 있습니다. 

- 앱이 활성인 경우(포그라운드 또는 백그라운드에서 실행 중)

  `AndroidManifest.xml` 파일에 스니펫을 추가하십시오. 

```
	<receiver android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationDismissHandler">
	<intent-filter>
	<action android:name="Your_Android_Package_Name.Cancel_IBMPushNotification"/>
	</intent-filter>
	</receiver>
```
	{: codeblock}

- 앱이 활성(포그라운드 또는 백그라운드에서 실행 중)이면서 실행 중이 아닌 경우(종료됨)

`com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationDismissHandler` 브로드캐스트 수신기를 확장하고 `onReceive()` 메소드를 대체하십시오. 여기서 `MFPPushNotificationStatusListener`는 기본 클래스의 `onReceive()` 메소드를 호출하기 전에 등록되어야 합니다. 

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


다음 스니펫을 `AndroidManifest.xml` 파일에 추가하십시오. 

```
	<receiver android:name="Your_Android_Package_Name.Your_Handler">
	<intent-filter>
	<action android:name="Your_Android_Package_Name.Cancel_IBMPushNotification"/>
	</intent-filter>
	</receiver>
```
    {: codeblock}

### 기본 푸시 알림 전송
{: #send-basic-notification}

애플리케이션을 개발한 후에는 기본 푸시 알림을 전송할 수 있습니다. 

기본 푸시 알림을 전송하려면 다음 단계를 완료하십시오. 

1. **알림 전송**을 선택하고 **받는 사람** 옵션을 선택하여 메시지를 작성하십시오. 지원되는 옵션은 **태그별 디바이스**, **디바이스 ID**, **사용자 ID**, **Android 디바이스**, **iOS 디바이스**, **웹 알림** 및 **모든 디바이스**입니다.
**참고**: **모든 디바이스** 옵션을 선택하는 경우 {{site.data.keyword.mobilepushshort}}를 구독하는 모든 디바이스가 알림을 수신합니다.
![알림 화면](images/tag_notification.jpg)

2. **메시지** 필드에 메시지를 작성하십시오. 필요에 따라 선택적 옵션을 구성하도록 선택하십시오.
3. **전송**을 클릭하십시오. 
3. 디바이스가 알림을 수신했는지 확인하십시오. 

다음 스크린샷은 Android 디바이스의 포그라운드에서 푸시
알림을 처리하는 경보 상자를 표시합니다.

![Android의 포그라운드 푸시 알림](images/Android_Screenshot.jpg)

다음 스크린샷은 Android의 백그라운드에 있는 푸시 알림을 보여줍니다.

![Android의 백그라운드 푸시 알림](images/background.jpg)

### 알림 전송을 위한 선택적 Android 설정
{: #send_otpional_setting}

Android 디바이스에 알림을 전송하기 위해 {{site.data.keyword.mobilepushshort}} 설정을 추가로 사용자 정의할 수 있습니다. 다음의 선택적 사용자 정의 옵션이 지원됩니다.
![Android 사용자 정의 설정](images/android_custom_settings.jpg)

- 접기 키: 접기 키는 알림에 첨부됩니다. 디바이스가 오프라인 상태일 때 접기 키가 동일한 여러 개의 알림이 순차적으로 도착하는 경우 해당 알림은 접혀 있습니다. 디바이스가 온라인 상태가 되면 FCM/GCM 서버에서 알림을 수신하고 동일한 접기 키가 있는 최신 알림만 표시합니다. 접기 키가 설정되어 있지 않는 경우에는 나중에 전달할 수 있도록 새 메시지와 이전 메시지가 모두 저장됩니다.
- 사운드: 알림을 수신할 때 재생되는 사운드 클립을 표시합니다. 기본값 또는 앱에 번들링된 사운드 리소스의 이름을 지원합니다. 
- 아이콘: 알림에 대해 표시할 아이콘의 이름을 지정합니다. 클라이언트 애플리케이션에서 `res/drawable` 폴더의 아이콘을 패키징했는지 확인하십시오. 
- 우선순위: 메시지에 전달 우선순위를 지정하기 위한 옵션을 지정합니다. `high` 또는 `max` 우선순위를 지정한 메시지는 heads-up 알림이 되는 반면, `low` 또는 `default` 우선순위 메시지는 휴면 디바이스에서 네트워크 연결을 열지 않습니다. 이 옵션을 `min`으로 설정한 메시지는 자동 알림이 됩니다.
- 가시성: 알림 가시성 옵션을 `public` 또는 `private`로 설정하도록 선택할 수 있습니다. `private` 옵션은 공용 보기를 제한하며, 사용자는 디바이스가 핀 또는 패턴으로 보호되고 알림 설정이 **민감한 알림 컨텐츠 숨기기**로 설정된 경우에 이를 사용하도록 선택할 수 있습니다. 가시성이 `private`로 설정되면 `redact` 필드가 언급되어야 합니다. `redact` 필드에 지정된 컨텐츠만 디바이스의 보안 잠금 화면에 나타납니다. `public`을 선택하면 알림이 누구나 읽을 수 있도록 렌더링됩니다.
- 유효 기간: 이 값은 초 단위로 설정됩니다. 이 매개변수를 지정하지 않는 경우 FCM/GCM 서버는 메시지를 4주 동안 저장하고 전달하려고 합니다. 4주 후에 유효성이 만료됩니다. 가능한 값 범위는 0 - 2,419,200초입니다.
- 유휴 시 지연: 이 값을 `true`로 설정하면 디바이스가 유휴 상태일 때 알림을 전달하지 않도록 FCM/GCM 서버에 지시합니다. 디바이스가 유휴 상태인 경우에도 알림이 전달되도록 하려면 이 값을 `false`로 설정하십시오.
- 동기화: 이 옵션을 `true`로 설정하면 등록된 모든 디바이스 간에 알림이 동기화됩니다. 하나의 사용자 이름을 갖는 사용자에게 동일한 애플리케이션이 설치된 여러 개의 디바이스가 있는 경우, 하나의 디바이스에서 알림을 읽으면 나머지 디바이스에서 해당 알림이 삭제됩니다. 사용자 ID를 사용하여 {{site.data.keyword.mobilepushshort}} 서비스에 등록한 경우에만 이 옵션이 작동합니다.
- 추가 페이로드: 알림에 대한 사용자 정의 페이로드 값을 지정합니다. 


### 다음 단계
{: #next_steps_tag_based_notifications}

정상적으로 기본 알림을 설정한 후 태그 기반 알림 및 고급 옵션을 구성할 수 있습니다. 

이러한 푸시 알림 서비스 기능을 사용자의 앱에 추가하십시오.
태그 기반 알림을 사용하려면 [태그 기반 알림](c_tag_basednotifications.html)을 참조하십시오.
고급 알림 옵션을 사용하려면 [고급 푸시 알림 사용](t_advance_badge_sound_payload.html)을 참조하십시오. 


## 푸시 알림을 수신하도록 Cordova 애플리케이션 설정
{: #cordova_enable}


Cordova는 JavaScript, CSS 및 HTML을 사용하여 하이브리드 애플리케이션을 빌드하는 플랫폼입니다. {{site.data.keyword.mobilepushshort}} 서비스는 Cordova 기반 iOS 및 Android 애플리케이션의 개발을 지원합니다. 

Cordova 애플리케이션에서 사용자 디바이스에 푸시 알림을 수신하도록 설정할 수 있습니다. 

### Cordova 푸시 플러그인 설치
{: #cordova_install}

클라이언트 푸시 플러그인을 설치하고 이를 사용하여 추가적으로 Cordova 애플리케이션을 개발할 수 있습니다. 이 때 사용자와 Bluemix의 연결을 초기화하는 Cordova 코어 플러그인도 설치됩니다. 

1. 최신 Android Studio SDK 및 Xcode 버전을 다운로드하십시오. 
1. 에뮬레이터를 설정하십시오. Android Studio의 경우 Google Play API를 지원하는 에뮬레이터를 사용하십시오.
1. Git 명령행 도구를 설치하십시오. Windows의 경우 **Window 명령 프롬프트에서 Git 실행** 옵션을 선택하십시오. 이 도구를 다운로드하고 설치하는 방법에 대한 정보는 [Git ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://git-scm.com/downloads){: new_window}을 참조하십시오. 
1. Node.js 및 NPM(Node Package Manager) 도구를 설치하십시오. NPM 명령행 도구는 Node.js와 함께 번들로 제공됩니다. Node.js를 다운로드하고 설치하는 방법에 대한 정보는 [Node.js ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://nodejs.org/en/download/){: new_window}을 참조하십시오. 
1. 명령행에서 **npm install -g cordova** 명령을 사용하여 Cordova 명령행 도구를 설치하십시오. Cordova 푸시 플러그인을 사용하려면 필요합니다. Cordova를 설치하고 Cordova 앱을 설정하는 방법에 대한 정보는 [Cordova Apache ![외부 링크 아콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cordova.apache.org/#getstarted){: new_window}을 참조하십시오. 자세한 정보는 Cordova 푸시 플러그인 [Readme 파일 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window}을 참조하십시오. 
1. Cordova 앱을 작성하려는 폴더로 변경하고 다음 명령을 실행하여 Cordova 애플리케이션을 작성하십시오. 기존의 Cordova 앱이 있을 경우 3단계로 가십시오. 
```cordova create your_app_name
cd your_app_name
```
	{: codeblock}
- 선택사항: **config.xml** 파일을 편집하고 <name> 요소의 애플리케이션 이름을 기본값인 HelloCordova 이름이 아닌 사용자가 선택하는 이름으로 변경할 수 있습니다. 

올바른 번들 ID를 지정했는지 확인하십시오. 올바르지 않은 번들 ID를 지정하면 Xcode에 다음 오류 메시지가 표시됩니다. 

* 실행 파일이 올바르지 않은 인타이틀먼트로 서명되었습니다.
* 애플리케이션의 코드 서명 인타이틀먼트에 지정된 인타이틀먼트가 프로비저닝 프로파일에 지정된 인타이틀먼트와 일치하지 않습니다. 이 문제를 수정하려면 Xcode 또는 Cordova 앱 **config.xml** 파일에서 올바른 번들 ID를 지정하십시오. 

1. Corova 애플리케이션의 config.xml 파일에 최소 지원 API 또는 배치 대상 선언을 추가하십시오. minSdkVersion 값은 15보다 커야 합니다. targetSdkVersion 값은 항상 Google을 통해 제공받을 수 있는 최신 Android SDK를 반영해야 합니다. 
	
	* Android - 편집기에서 **config.xml** 파일을 열고 최소의 대상 SDK 버전으로
`<platform name="android">` 요소를 업데이트하십시오. 

	```
	<platform name="android">
    	<preference name="android-minSdkVersion" value="15" />
    	<preference name="android-targetSdkVersion" value="23" />
    	<!-- add minimum and target Android API level declaration -->
	</platform>
	```
    	{: codeblock}

   * iOS - 배치 대상 선언으로 <platform name="ios"> 요소를 업데이트하십시오. 

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- add deployment target declaration -->
	</platform>
	```
		{: codeblock}

1. Cordova 명령행 인터페이스(CLI)에서 다음 명령을 사용하여 플랫폼(iOS, Android 또는 둘 다)을 추가하십시오. 
```
cordova platform add ios
cordova platform add android
```
	{: codeblock}

1. Cordova 애플리케이션 루트 디렉토리에서 다음 명령을 입력하여 Cordova 푸시 플러그인을 설치하십시오. **cordova plugin add bms-push**. 추가한 플랫폼에 따라 다음과 같이 표시됩니다. 
```
Installing "bms-push" for android
Installing "bms-push" for ios
```
	{: codeblock}

1. your-app-root-folder에서 다음 명령을 사용하여 Cordova 코어 플러그인과 푸시 플러그인이 정상적으로 설치되었는지 확인하십시오. **cordova plugin list**. 추가한 플랫폼에 따라 다음과 같이 표시됩니다. 
```
bms-core <version> "BMSCore"
bms-push <version> "BMSPush" 
```
	{: codeblock}

1. iOS 개발 환경을 구성하십시오.
2. Xcode를 사용하여 애플리케이션을 빌드하고 실행하십시오.
1. Android용 Firebase `google-services.json`을 다운로드하고 Cordova 프로젝트의 루트 폴더인 `[your-app-name]/platforms/android에 두십시오.
	1. `[your-app-name]/platforms/android`로 이동하십시오.
	2. `build.gradle` 파일을 여십시오(경로 : 플랫폼 > android > build.gradle).
	3. `build.gradle` 파일에서 `buildscript` 텍스트를 찾으십시오.
	4. classpath 행 다음에 classpath 'com.google.gms:google-services:3.0.0'이라는 행을 추가하십시오.
	5. 그런 다음 "dependencies"를 찾으십시오. `compile` 텍스트가 있는 종속 항목과 해당 종속 항목이 종료되는 위치를 선택한 후, 그 다음에 :apply plugin: 'com.google.gms.google-services'라는 행을 추가하십시오.
	6. Cordova Android 프로젝트를 준비하고 빌드하십시오.
		```
		cordova prepare android
		cordova build android
		```
			{: codeblock}
	**참고**: Android Studio에서 프로젝트를 열기 전에 먼저 Cordova CLI를 통해 Cordova 애플리케이션을 빌드하십시오. 그러면 빌드 오류를 방지하는 데 유용합니다.

### Cordova 플러그인 초기화
{: #cordova_initialize}

{{site.data.keyword.mobilepushshort}} 서비스 Cordova 플러그인을 사용하려면 먼저 애플리케이션 라우트와 애플리케이션 GUID를 전달하여 플러그이니을 초기화해야 합니다. 플러그인을 초기화한 후 Bluemix 대시보드에서 작성한 서버 앱에 연결할 수 있습니다. Cordova 플러그인은 Cordova 앱이 Bluemix 서비스와 통신할 수 있도록 해주는 Android 및 iOS 클라이언트 SDK용 랩퍼입니다. 

1. 다음 코드 스니펫을 복사하여 기본 JavaScript 파일(일반적으로 **www/js** 디렉토리 아래에 있음)에 붙여넣어 BMSClient를 초기화하십시오. 

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

애플리케이션의 영역을 전달하십시오. 다음 상수가 제공됩니다. 

```
REGION_US_SOUTH // ".ng.bluemix.net";
REGION_UK //".eu-gb.bluemix.net";
REGION_SYDNEY // ".au-syd.bluemix.net";
```

예: 

```
BMSClient.initialize(BMSClient.REGION_US_SOUTH);
```

**참고**: Cordova CLI(예: Cordova create app-name 명령)를 사용하여 Cordova 앱을 작성한 경우 이 Javascript 코드를 index.js 파일에서 onDeviceReady: function() 함수의 app.receivedEvent 함수 뒤에 넣어서 `BMSClient`를 초기화하십시오. 


### 디바이스 등록
{: #cordova_register}


디바이스를 {{site.data.keyword.mobilepushshort}} 서비스에 등록하려면 등록 메소드를 호출하십시오. 다음 코드 스니펫을 Cordova 애플리케이션에 복사하여 디바이스를 등록하십시오. 

```
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure);
```
	{: codeblock}

다음 JavaScript 코드 스니펫은 Bluemix 모바일 서비스 클라이언트 SDK를 초기화하고, 디바이스를 {{site.data.keyword.mobilepushshort}} 서비스에 등록하고, 푸시 알림을 청취하는 방법을 표시합니다. 이 코드를 Javascript 파일에 포함하십시오. 

**onDeviceReady: function()**에서 다음을 수행하십시오. 

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

다음의 Swift 코드 스니펫을 애플리케이션 위임 클래스에 추가하십시오. 

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

### 다음 단계
{: #cordova_register_next}

프로젝트를 빌드하고 다음 명령을 사용하여 프로젝트를 실행하십시오. 

#### Android
{: #android-next-steps}

```
cordova build android
```
	{: codeblock}

```
cordova run android
```
	{: codeblock}

#### iOS
{: #ios-next-steps}

```
cordova build ios
```
	{: codeblock}

```
cordova run ios
```
	{: codeblock}

### 디바이스에서 푸시 알림 수신
{: #cordova_receive}

디바이스에서 푸시 알림을 받으려면 다음 코드 스니펫을 복사하십시오. 

#### JavaScript
{: #jvscrpt}

다음의 JavaScript 코드 스니펫을 Cordova 애플리케이션의 웹 파트에 추가하십시오. 
```
var showNotification = function(notif) {
  alert(JSON.stringify(notif));
        };
        BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

#### Android 알림 특성
{: #And_notif}

다음 섹션에는 Android 알림 특성이 나열되어 있습니다. 

* **메시지** - 푸시 알림 메시지
* **페이로드** - 알림 페이로드를 포함하는 JSON 오브젝트


#### iOS 알림 특성
{: #ios_notif}

다음 섹션에는 iOS 알림 특성이 나열되어 있습니다. 

* **메시지** - 푸시 알림 메시지
* **페이로드** - 알림 페이로드를 포함한 JSON 오브젝트
action-loc-key - 이 문자열은 `View` 대신 현재 번역에서 자국어로 지원된 문자열을 가져와 해당 단추 제목에 사용하는 키로 사용됩니다. 
* **배지** - 앱 아이콘의 배지로 표시할 숫자입니다. 이 특성을 비워두면 배지가 변경되지 않습니다. 배지를 제거하려면 이 특성의 값을 0으로 설정하십시오. 
* **사운드** - 앱 번들 또는 앱 데이터 컨테이너의 라이브러리/사운드 폴더에 있는 사운드 파일의 이름입니다. 


다음의 Swift 코드 스니펫을 애플리케이션 위임 클래스에 추가하십시오. 
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

### 기본 푸시 알림 전송
{: #push-send-notifications}

애플리케이션을 개발한 후에는 기본 푸시 알림을 전송할 수 있습니다. 

기본 푸시 알림을 전송하려면 다음 단계를 완료하십시오. 

1. **알림 전송**을 선택하고 **받는 사람** 옵션을 선택하여 메시지를 작성하십시오. 지원되는 옵션은 **태그별 디바이스**, **디바이스 ID**, **사용자 ID**, **Android 디바이스**, **iOS 디바이스**, **웹 알림** 및 **모든 디바이스**입니다.
**참고**: **모든 디바이스** 옵션을 선택하는 경우 {{site.data.keyword.mobilepushshort}}를 구독하는 모든 디바이스가 알림을 수신합니다.
![알림 화면](images/tag_notification.jpg)

2. **메시지** 필드에 메시지를 작성하십시오. 필요에 따라 선택적 옵션을 구성하도록 선택하십시오.
3. **전송**을 클릭하십시오. 
3. 디바이스가 알림을 수신했는지 확인하십시오. 

다음 스크린샷은 Android 디바이스와 iOS 디바이스의 포그라운드에서 {{site.data.keyword.mobilepushshort}}를 처리하는 경보 상자를 표시합니다. 

![Android의 포그라운드 푸시 알림](images/Android_Screenshot.jpg)

![iOS의 포그라운드 푸시 알림](images/iOS_Screenshot.jpg)

   다음 이미지는 Android에서 사용되는 백그라운드의 {{site.data.keyword.mobilepushshort}}를 표시합니다.
![Android의 백그라운드 푸시 알림](images/background.jpg)

#### 다음 단계
{: #next_steps_basic_notifications}

정상적으로 기본 알림을 설정한 후 태그 기반 알림 및 고급 옵션을 구성할 수 있습니다. 

{{site.data.keyword.mobilepushshort}} 서비스 기능을 사용자의 앱에 추가하십시오.
태그 기반 알림을 사용하려면 [태그 기반 알림](c_tag_basednotifications.html)을 참조하십시오.
고급 알림 옵션을 사용하려면 [고급 푸시 알림 사용](t_advance_badge_sound_payload.html)을 참조하십시오. 


## iOS 애플리케이션을 사용하여 푸시 알림 전송
{: #enable-push-ios-notifications}

iOS 애플리케이션이 {{site.data.keyword.mobilepushshort}}를 사용자 디바이스에 전송하도록 설정할 수 있습니다.


### CocoaPods 설치
{: #enable-push-ios-notifications-install}

기존 Xcode 프로젝트의 경우 CocoaPods 종속 항목 관리 도구를 사용하여 Bluemix Mobile Services Client SDK를 설정할 수 있습니다. 또는 SDK를 수동으로 설치할 수 있습니다. 

Swift 푸시 Readme 파일을 보려면 [Readme ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}으로 이동하십시오. 



1. Mac 터미널에서 다음 명령을 사용하여 CocoaPods를 설치하십시오.
	```
		$ sudo gem install cocoapods
	```
	{: codeblock}
2. 터미널에 `pod init` 명령을 입력하여 CocoaPods를 초기화하십시오. Xcode 프로젝트가 있는 디렉토리에서 명령을 실행하십시오. `pod init` 명령에서 Podfile을 작성합니다.  
3. 생성된 Podfile에 필요한 SDK 종속 항목을 추가하십시오. 다음 Podfile을 복사하십시오.
   
	```
		source 'https://github.com/CocoaPods/Specs.git'
		//Copy the following list as is and remove the dependencies you do not need.
		use_frameworks!
		target 'MyApp' do
		platform :ios, '8.0'
		pod 'BMSCore'
		pod 'BMSPush'
		pod 'BMSAnalyticsAPI' end
	```
		{: codeblock}

3. 터미널에서 프로젝트 폴더로 이동한 후 `pod update` 명령을 사용하여 종속 항목을 설치하십시오. 

이 명령은 종속 항목을 설치하고 새 Xcode 작업공간을 작성합니다.   
**참고**: 원래 Xcode 프로젝트 파일 대신, 반드시 항상 새 Xcode 작업공간을 여십시오. 
```
  $ open App.xcworkspace
```
	{: codeblock}

작업공간에는 원래 프로젝트 및 종속 항목이 포함된 Pods 프로젝트가 있습니다. Bluemix Mobile Services 소스 폴더를 수정하려는 경우 Pods 프로젝트의 `Pods/yourImportedSourceFolder`에서 이 폴더를 찾을 수 있습니다(예: `Pods/BMSPush`).

### Carthage를 사용하여 프레임워크 추가
{: #carthage}

[Carthage ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window}을 사용하여 프로젝트에 프레임워크를 추가하십시오. Xcode8의 Carthage는 지원되지 않습니다. 

1. `BMSPush` 프레임워크를 Cartfile에 추가하십시오. 
	```
	github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
	```
	{: codeblock}
2. `carthage update` 명령을 실행하십시오. 빌드가 완료되면 `BMSPush.framework`, `BMSCore.framework`, `BMSAnalyticsAPI.framework`를 Xcode 프로젝트로 끌어오십시오. 
3. [Carthage ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window} 사이트의 지시사항에 따라 통합을 완료하십시오. 

### iOS SDK 설정
{: #ios-sdk}

iOS SDK를 설치하고 다음 코드를 애플리케이션의 **AppDelegate.swift** 파일에 추가하십시오. 이 코드도 APNs에 등록됩니다.  
```
  func application(_ application: UIApplication,
  didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool
   {
   BMSPushClient.sharedInstance.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE")
  }
```
    {: codeblock}

### 가져온 프레임워크 및 소스 폴더 사용
{: #using-imported-frameworks}

코드에서 SDK를 참조하십시오. 다음 전제조건이 충족되는지 확인하십시오.

- iOS 8.0 이상	
- Xcode 7

관련 헤더에 대해 `#import` 지시문을 작성합니다. 예: 
```
	 //swift
 	 import BMSCore
	 import BMSPush
```
		{: codeblock}

Swift 푸시 Readme 파일을 읽어보려면 [Readme ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}을 참조하십시오. 

**참고**: CocoaPods 명령 `pod install` 또는 `pod update`를 사용하여 Pods 프로젝트를 업데이트하면 Bluemix Mobile Services 소스 폴더를 대체할 수 있습니다. 원래 파일의 사용자 정의한 버전을 유지하려면, 이러한 명령을 실행하기 전에 해당 버전을 백업해야 합니다. 


### 빌드 설정
{: #build-settings}

**Xcode > 빌드 설정 > 빌드 옵션 및 Bitcode 사용 설정**으로 이동하여 **No**로 설정하십시오.

**주의**: iOS 9의 경우, ATS(App Transport Security) 기능을 변경하면 인증 프로세스의 처리 방식에 영향이 미칠 수 있습니다. 다음 블로그 게시물에서 변경사항에 대한 자세한 정보를 설명합니다. [ATS and Bitcode in iOS 9 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/){: new_window} 및 [Connect your iOS 9 app to Bluemix today ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/){: new_window}.

### iOS 앱을 위한 푸시 SDK 초기화
{: #enable-push-ios-notifications-initialize}

초기화 코드를 배치하는 공통 위치는 iOS 애플리케이션에 대한 애플리케이션 위임자입니다. 푸시 대시보드의 **모바일 옵션** 링크를 클릭하여 애플리케이션 라우트와 GUID를 가져오십시오. 

#### Core SDK 초기화
{: #Initializing-the-core-sdk}

IBM Bluemix GUID, 라우트 및 지역으로 Swift의 Core SDK를 초기화하려면 다음 코드 스니펫을 사용하십시오. 
```
	let myBMSClient = BMSClient.sharedInstance
	myBMSClient.initialize(bluemixRegion: "Location where your app is hosted.") 
```
	{: codeblock}

#### 라우트, GUID 및 Bluemix 지역
{: #route-guid-bluemix-region}


- **appRoute**: Bluemix에서 사용자가 작성한 서버 애플리케이션에 지정된 라우트를 지정합니다. 


- **GUID**: Bluemix에서 사용자가 작성한 서버 애플리케이션에 지정된 고유 키를 지정합니다. 이 값은 대소문자를 구분합니다. 


- **bluemixRegionSuffix**: 앱이 호스트된 위치를 지정합니다. `bluemixRegion` 매개변수는 사용 중인 Bluemix 배치를 지정합니다. 이 값을 `BMSClient.REGION` 정적 특성으로 설정하고 세 값 중 하나를 사용할 수 있습니다. 

	- BMSClient.Region.usSouth 
	- BMSClient.Region.unitedKingdom
	- BMSClient.Region.sydney


- **AppGUID**: Bluemix에서 사용자가 작성한 {{site.data.keyword.mobilepushshort}} 서비스에 지정된 고유 AppGUID 키를 지정합니다. 

#### 클라이언트 푸시 SDK 초기화
{: #initializing-the-client-Push-SDK}

```
	let push = BMSPushClient.sharedInstance
	push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


### iOS 애플리케이션 및 디바이스 등록
{: #enable-push-ios-notifications-register}

디바이스에 애플리케이션을 설치한 후 원격 알림을 수신하려면 애플리케이션을 APNs에 등록해야 합니다. APNs에서 생성한 디바이스 토큰을 앱에서 수신한 후에는 {{site.data.keyword.mobilepushshort}} 서비스에 이를 되돌려 보내야 합니다. 

iOS 애플리케이션과 디바이스를 등록하려면 다음을 수행해야 합니다. 

1. 백엔드 애플리케이션을 작성하십시오. 
2. 토큰을 {{site.data.keyword.mobilepushshort}}에 전달하십시오. 


#### 백엔드 애플리케이션 작성
{: #create-a-backend-app}

표준 유형 섹션 Bluemix® 카탈로그에서 {{site.data.keyword.mobilepushshort}} 서비스를 이 애플리케이션에 자동으로 바인드하는 백엔드 애플리케이션을 작성하십시오. 백엔드 앱을 이미 작성한 경우에는 앱을 {{site.data.keyword.mobilepushshort}} 서비스에 바인드했는지 확인하십시오. 


#### Push Notifications에 토큰 전달
{: #pass-token-push-notifications}

APNs에서 토큰이 수신되면 `registerWithDeviceToken` 메소드의 일부로 {{site.data.keyword.mobilepushshort}}에 토큰을 전달하십시오. 

```
  func application (_application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data){
   let push =  BMSPushClient.sharedInstance
   push.registerWithDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
      if error.isEmpty {
           print( "Response during device registration : \(response)")
           print( "status code during device registration : \(statusCode)")
      }
       else{
           print( "Error during device registration \(error) ")
           print( "Error during device registration \n  - status code: \(statusCode) \n Error :\(error) \n")
       }
   }
  }
```
	{: codeblock}


### iOS 디바이스에서 푸시 알림 수신
{: #enable-push-ios-notifications-receiving}

iOS 디바이스에서 푸시 알림을 수신하려면 애플리케이션의 위임자에 다음 Swift 메소드를 추가하십시오.

```
   func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) 
  { //UserInfo dictionary will contain data sent from the server }
```
	{: codeblock}

### iOS 디바이스에서 푸시 알림 모니터링
{: #ios-monitoring}


사용자는 전송된 푸시 알림의 개수와 현재 상태를 모니터할 수 있습니다. 모니터링을 사용하려면 이벤트를 기반으로 애플리케이션의 애플리케이션 위임자에 다음 Swift 메소드 중 하나를 추가하십시오. 



- 알림을 클릭하여 앱이 열릴 때 알림 상태를 전송합니다. 
	```
		func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any]) { 					let push =  BMSPushClient.sharedInstance
				let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
				let data = respJson.data(using: String.Encoding.utf8)
				let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
		 		let messageId:String = jsonResponse.value(forKey: "nid") as! String
		    	push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
    		  print("Send message status to the Push server")
    	 }
		}
	```
			{: codeblock}



- 앱이 백그라운드 모드일 때 알림 상태를 전송합니다. 
	```
		func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
 	let payLoad = ((((userInfo as NSDictionary).value(forKey: "aps") as! NSDictionary).value(forKey: "alert") as! NSDictionary).value(forKey: "body") as! NSString)
	 	 	let push =  BMSPushClient.sharedInstance
			let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
	 	let data = respJson.data(using: String.Encoding.utf8)
	 	let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
	 	let messageId:String = jsonResponse.value(forKey: "nid") as! String
		push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
       completionHandler(UIBackgroundFetchResult.newData)
	}
	}
	```
			{: codeblock}


### 기본 푸시 알림 전송
{: #send}

애플리케이션을 개발한 후에는 기본 푸시 알림을 전송할 수 있습니다. 

기본 푸시 알림을 전송하려면 다음 단계를 완료하십시오. 

1. **알림 전송**을 선택하고 **받는 사람** 옵션을 선택하여 메시지를 작성하십시오. 지원되는 옵션은 **태그별 디바이스**, **디바이스 ID**, **사용자 ID**, **Android 디바이스**, **iOS 디바이스**, **웹 알림** 및 **모든 디바이스**입니다.  
**참고**: **모든 디바이스** 옵션을 선택하는 경우 {{site.data.keyword.mobilepushshort}}를 구독하는 모든 디바이스가 알림을 수신합니다.
![알림 화면](images/tag_notification.jpg)

2. **메시지** 필드에 메시지를 작성하십시오. 필요에 따라 선택적 옵션을 구성하도록 선택하십시오.
3. **전송**을 클릭하십시오. 
3. 디바이스가 알림을 수신했는지 확인하십시오. 

다음 이미지는 iOS 디바이스에서 {{site.data.keyword.mobilepushshort}}를 처리하는 경보 상자를 표시합니다.

![iOS의 포그라운드 푸시 알림](images/iOS_Screenshot.jpg) 

#### 알림 전송을 위한 선택적 설정
{: #send_ios_otpional_setting}

iOS 디바이스에 알림을 전송하기 위해 {{site.data.keyword.mobilepushshort}} 설정을 추가로 사용자 정의할 수 있습니다. 다음과 같은 선택적 사용자 정의 옵션이 지원됩니다.

- **배지**: 애플리케이션 배지에 표시되는 숫자를 나타냅니다. 기본값은 영(0)이며, 이 값은 배지를 표시하지 않습니다. 
- **사운드**: 알림을 수신할 때 재생되는 사운드 클립을 표시합니다. 기본값 또는 앱에 번들링된 사운드 리소스의 이름을 지원합니다.
- **추가 페이로드**: 알림에 대한 사용자 정의 페이로드 값을 지정합니다.

### 대화식 알림 사용
{: #enb_snd_ios_otpional}

대화식 알림을 설정하여 이미지, 맵 또는 응답 단추 추가와 같은 추가 세부사항으로 iOS 알림을 보강할 수 있습니다. 이를 통해 현재 컨텍스트를 종료하지 않고도 즉시 조치를 수행할 수 있는 기능과 추가 컨텍스트를 제공할 수 있습니다.   

  대화식 알림을 사용하려면 다음 코드를 사용하십시오. 



- 단추 조치 정의
	```
		let actionOne = BMSPushNotificationAction(identifierName: "ACCEPT", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
		let actionTwo = BMSPushNotificationAction(identifierName: "DECLINE", buttonTitle: "Decline", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
	```
		{: codeblock}


- 단추의 카테고리 정의
	```
		let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
	```
		{: codeblock}


- 단추를 포함하도록 등록 업데이트
	```
		Pass the defined category into iOS BMSPushClientOptions
		let notificationOptions = BMSPushClientOptions(categoryName: [category])
		let push = BMSPushClient.sharedInstance
		push.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE", options: notificationOptions)
	```
		{: codeblock}

대화식 알림을 보내려면 다음 단계를 완료하십시오. 

1. 작성 섹션의 받는 사람 드롭 다운 목록에서 **iOS 디바이스**를 선택합니다. 
2. 보내려는 알림 메시지를 입력합니다. 
3. 선택적 설정 섹션에서 **모바일**을 선택하고 **iOS**를 클릭합니다.
4. 유형 드롭 다운 목록에서 **혼합**을 선택합니다.
5. 카테고리 필드에서 앱에서 정의한 알림 유형을 지정합니다.  

![iOS용 대화식 알림](images/push_ios_notification_interactive.jpg) 

#### 다음 단계
{: #next_steps_02}

정상적으로 기본 알림을 설정한 후 태그 기반 알림 및 고급 옵션을 구성할 수 있습니다. 

다음의 Push Notifications 서비스 기능을 사용자의 앱에 추가하십시오.
태그 기반 알림을 사용하려면 [태그 기반 알림](c_tag_basednotifications.html)을 참조하십시오.
고급 알림 옵션을 사용하려면 [고급 푸시 알림 사용](t_advance_badge_sound_payload.html)을 참조하십시오. 
