---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 푸시 알림을 수신하도록 Cordova 애플리케이션 설정
{: #cordova_enable}
마지막 업데이트 날짜: 2017년 1월 18일
{: .last-updated}

Cordova는 JavaScript, CSS 및 HTML을 사용하여 하이브리드 애플리케이션을 빌드하는 플랫폼입니다. {{site.data.keyword.mobilepushshort}} 서비스는 Cordova 기반 iOS 및 Android 애플리케이션의 개발을 지원합니다. 

Cordova 애플리케이션에서 사용자 디바이스에 푸시 알림을 수신하도록 설정할 수 있습니다. 

## Cordova 푸시 플러그인 설치
{: #cordova_install}

클라이언트 푸시 플러그인을 설치하고 이를 사용하여 추가적으로 Cordova 애플리케이션을 개발할 수 있습니다. 이 때 사용자와 Bluemix의 연결을 초기화하는 Cordova 코어 플러그인도 설치됩니다. 

### 시작하기 전에

1. 최신 Android Studio SDK 및 Xcode 버전을 다운로드하십시오. 
1. 에뮬레이터를 설정하십시오. Android Studio의 경우 Google Play API를 지원하는 에뮬레이터를 사용하십시오.
1. Git 명령행 도구를 설치하십시오. Windows의 경우 **Window 명령 프롬프트에서 Git 실행** 옵션을 선택하십시오. 이 도구를 다운로드하고 설치하는 방법에 대한 정보는 [Git ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://git-scm.com/downloads){: new_window}을 참조하십시오. 
1. Node.js 및 NPM(Node Package Manager) 도구를 설치하십시오. NPM 명령행 도구는 Node.js와 함께 번들로 제공됩니다. Node.js를 다운로드하고 설치하는 방법에 대한 정보는 [Node.js ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://nodejs.org/en/download/){: new_window}을 참조하십시오. 
1. 명령행에서 **npm install -g cordova** 명령을 사용하여 Cordova 명령행 도구를 설치하십시오. Cordova 푸시 플러그인을 사용하려면 필요합니다. Cordova를 설치하고 Cordova 앱을 설정하는 방법에 대한 정보는 [Cordova Apache ![외부 링크 아콘](../../icons/launch-glyph.svg "External link icon")](https://cordova.apache.org/#getstarted){: new_window}을 참조하십시오. 자세한 정보는 Cordova 푸시 플러그인 [Readme 파일 ![외부 링크 아이콘](../../icons/launch-glyph.svg)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window}을 참조하십시오. 
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

## Cordova 플러그인 초기화
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


## 디바이스 등록
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

## 다음 단계

{: #cordova_register_next}

프로젝트를 빌드하고 다음 명령을 사용하여 프로젝트를 실행하십시오. 

#### Android
{: android-next-steps}

```
cordova build android
```
	{: codeblock}

```
cordova run android
```
	{: codeblock}

#### iOS
{: ios-next-steps}

```
cordova build ios
```
	{: codeblock}

```
cordova run ios
```
	{: codeblock}

## 디바이스에서 푸시 알림 수신
{: #cordova_receive}

디바이스에서 푸시 알림을 받으려면 다음 코드 스니펫을 복사하십시오. 

### JavaScript

다음의 JavaScript 코드 스니펫을 Cordova 애플리케이션의 웹 파트에 추가하십시오. 
```
var showNotification = function(notif) {
  alert(JSON.stringify(notif));
        };
        BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

### Android 알림 특성

다음 섹션에는 Android 알림 특성이 나열되어 있습니다. 

* **메시지** - 푸시 알림 메시지
* **페이로드** - 알림 페이로드를 포함하는 JSON 오브젝트


### iOS 알림 특성

다음 섹션에는 iOS 알림 특성이 나열되어 있습니다. 

* **메시지** - 푸시 알림 메시지
* **페이로드** - 알림 페이로드를 포함한 JSON 오브젝트
action-loc-key - 이 문자열은 `View` 대신 해당 단추 제목에 사용할 현재 로컬라이제이션의 현지화된 문자열을 가져올 키로 사용됩니다. 
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

## 기본 푸시 알림 전송
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

## 다음 단계
{: #next_steps_tags}

정상적으로 기본 알림을 설정한 후 태그 기반 알림 및 고급 옵션을 구성할 수 있습니다. 

이러한 {{site.data.keyword.mobilepushshort}} 서비스 기능을 앱에 추가하십시오.
태그 기반 알림을 사용하려면 [태그 기반 알림](c_tag_basednotifications.html)을 참조하십시오.
고급 알림 옵션을 사용하려면 [고급 푸시 알림 사용](t_advance_badge_sound_payload.html)을 참조하십시오. 
