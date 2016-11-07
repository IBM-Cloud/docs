---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"
---
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Cordova 앱에서 Facebook 인증 사용
{: #facebook-auth-cordova}


Facebook 인증 통합을 위해 {{site.data.keyword.amafull}} Cordova 애플리케이션을 구성하려면 Java, Objective-C 또는 Swift로 Cordova 애플리케이션의 원시 코드를 변경하십시오. 플랫폼마다 별도로 구성하십시오. 이 Cordova 애플리케이션은 먼저 {{site.data.keyword.amashort}} SDK로 인스트루먼트되야 합니다. 


원시 개발 환경을 사용하여 원시 코드(예: Android Studio 또는 Xcode)를 변경하십시오.
{:shortdesc}

## 시작하기 전에
{: #facebook-auth-before}
다음이 있어야 합니다.
* {{site.data.keyword.amashort}} 클라이언트 SDK로 인스트루먼트된 Cordova 프로젝트는 [Cordova 플러그인 설정](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)을 참조하십시오.
* {{site.data.keyword.amashort}} 서비스를 통해 보호하는 {{site.data.keyword.Bluemix_notm}} 애플리케이션의 인스턴스. {{site.data.keyword.Bluemix_notm}} 백엔드 애플리케이션 작성 방법에 대한 자세한 정보는 [시작하기](index.html)를 참조하십시오. 
* Facebook 앱 ID. 자세한 정보는 [Facebook 개발자 포털에서 Facebook 앱 ID 얻기](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)를 참조하십시오. 



## Android 플랫폼 구성
{: #facebook-auth-cordova-android}

Facebook 인증 통합을 위해 Cordova 애플리케이션의 Android 플랫폼을 구성하는 데 필요한 단계는 기본 Android 애플리케이션에 필요한 단계와 매우 유사합니다. 자세한 정보는 [Android 앱에서 Facebook 인증 사용](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html)을 참조하십시오. 다음 단계를 수행하십시오. 

* Android 플랫폼용 Facebook 애플리케이션 구성
* Facebook 인증용 {{site.data.keyword.amashort}} 구성

### Android용 {{site.data.keyword.amashort}} 클라이언트 SDK 구성

Cordova 애플리케이션내에서 Android용 {{site.data.keyword.amashort}} 클라이언트 SDK를 구성하십시오.

1. Android 프로젝트 폴더에서 앱 모듈의 `build.gradle` 파일(프로젝트 `build.gradle` 파일이 **아님**)을 여십시오. 종속 항목 섹션을 찾은 다음 클라이언트 SDK에 대한 새 컴파일 종속 항목을 추가하십시오. 

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
     		name:'facebookauthentication',
     		version: '1.+',
     		ext: 'aar',
     		transitive: true
     		// other dependencies  
		 }
	```
	
2. **도구 > Android > Gradle 파일로 프로젝트 동기화**를 클릭하여 프로젝트를 Gradle과 동기화하십시오. 

3. `android/res/values/strings.xml` 파일을 열고 Facebook 앱 ID가 포함된 `facebook_app_id` 문자열을 추가하십시오. 

	```XML
	<resources>
		<string name="app_name">HelloCordova</string>
		<string name="launcher_name">@string/app_name</string>
		<string name="activity_name">@string/launcher_name</string>
		<string name="facebook_app_id">522733366802111</string>
	</resources>
	```
	
4. Android 프로젝트의 `AndroidManifest.xml` 파일(`android/manifests/AndroidManifest.xml`)에서 다음을 수행하십시오. 

	* Facebook SDK의 필수 메타데이터를 <application> 요소에 추가하십시오. 

	```XML
	<application .......>

		<meta-data
			android:name="com.facebook.sdk.ApplicationId"
			android:value="@string/facebook_app_id"/>

		<activity ...../>
		<activity ...../>
	</application>
	```

	* 기존 활동 아래에 Facebook 활성 요소를 추가하십시오. 

	```XML
	<application .....>
		<activity ...../>
		<activity ...../>
	<activity   android:name="com.facebook.FacebookActivity"
	              android:configChanges="keyboard|keyboardHidden|screenLayout|screenSize|orientation"
	              android:theme="@android:style/Theme.Translucent.NoTitleBar"
	              android:label="@string/app_name" 
			    />
	</application>
	```

2. Cordova 애플리케이션의 경우, Java 코드 대신 JavaScript 코드로 {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화하십시오. `FacebookAuthenticationManager` API는 여전히 사용자의 원시 코드에 등록해야 합니다. 다음 코드를 기본 활동 `onCreate` 메소드에 추가하십시오.  

	```Java
	FacebookAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
	```

6. 다음 코드를 활동에 추가하십시오. 

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
```

## iOS 플랫폼 구성
{: #facebook-auth-cordova-ios}

Facebook 인증을 통합하도록 Cordova 애플리케이션의 iOS 플랫폼을 구성하는 데 필요한 단계는 기본 iOS 애플리케이션에 필요한 단계와 유사합니다. 주요한 차이점은 현재 Cordova CLI에서는 CocoaPods 종속성 관리자를 지원하지 않는다는 점입니다. 따라서 Facebook 인증과 통합하는 데 필요한 파일을 수동으로 추가해야 합니다. 자세한 정보는 [iOS 앱에서 Facebook 인증 사용](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html)을 참조하십시오. 다음 단계를 수행하십시오. 

* iOS 플랫폼에 대해 Facebook 애플리케이션 구성
* Facebook 인증용 {{site.data.keyword.amashort}} 구성

### Facebook 인증용 {{site.data.keyword.amashort}} SDK 및 Facebook SDK 수동 설치
{: #facebook-auth-cordova-ios-sdk}
1. [{{site.data.keyword.Bluemix_notm}} iOS용 모바일 서비스 SDK](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master)가 포함된 아카이브를 다운로드하십시오. 

1. `Sources/Authenticators/IMFFacebookAuthentication` 디렉토리로 이동한 다음 모든 파일을 Xcode의 iOS 프로젝트로 복사(끌어서 놓기)하십시오. 다음 파일을 복사하십시오. 

	* IMFDefaultFacebookAuthenticationDelegate.h
	* IMFDefaultFacebookAuthenticationDelegate.m
	* IMFFacebookAuthenticationDelegate.h
	* IMFFacebookAuthenticationHandler.h
	* IMFFacebookAuthenticationHandler.m

	Xcode에서 프롬프트를 표시하면 **파일 복사...**를 선택하십시오. 

1. [Facebook SDK v3.19](https://developers.facebook.com/resources/facebook-ios-sdk-3.19.pkg)를 다운로드하고 설치하십시오. 

1. Facebook SDK가 `~/Documents/FacebookSDK` 디렉토리에 설치됩니다. 해당 디렉토리로 이동하여 `FacebookSDK.framework` 파일을 Xcode의 사용자 iOS 프로젝트로 복사(끌어서 놓기)하십시오. 

1. Xcode에서 프로젝트 루트를 클릭하고 **단계 빌드**를 선택하십시오.

1. **라이브러리와 2진 링크**에서 링크된 라이브러리 목록에 `FacebookSDK.framework` 파일을 추가하십시오.

 [Facebook 인증용 iOS 플랫폼 구성](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html)을 참조하십시오. **{{site.data.keyword.amashort}} 클라이언트 SDK 초기화** 섹션에 설명된 대로 `IMFFacebookAuthenticationHandler` API를 원시 코드로 등록하십시오. `IMFClient`는 원시 코드로 초기화하지 마십시오.

애플리케이션 위임자의 `application:openURL:sourceApplication:annotation` 메소드에 다음 행을 추가하십시오. 이 코드는 모든 Cordova 플러그인에서 각각의 이벤트에 대한 알림을 수신하도록 합니다.

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```
{: codeblock}

## {{site.data.keyword.amashort}} 클라이언트 SDK 초기화
{: #facebook-auth-cordova-init}

Cordova 애플리케이션에서 다음 JavaScript 코드를 사용하여 {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화하십시오.

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```
{: codeblock}

`applicationRoute` 및 `applicationGUID`를 **모바일 옵션**에서 **라우트** 및 **앱 GUID**에 대해 얻은 값으로 바꾸십시오.
	



##{{site.data.keyword.amashort}} AuthorizationManager 초기화
Cordova 애플리케이션에서 다음 JavaScript 코드를 사용하여 {{site.data.keyword.amashort}} AuthorizationManager를 초기화하십시오.
```JavaScript
  MFPAuthorizationManager.initialize("tenantId");
  ```
{: codeblock}

`tenantId` 값을 {{site.data.keyword.amashort}} 서비스 `tenantId`로 바꾸십시오. {{site.data.keyword.amashort}} 서비스 타일의 **신임 정보 표시** 단추를 클릭하여 이 값을 얻을 수 있습니다. 



## 인증 테스트
{: #facebook-auth-cordova-test}
클라이언트 SDK가 초기화되고 Facebook 인증 관리자가 등록되면 모바일 백엔드 애플리케이션에 대한 요청을 시작할 수 있습니다. 

### 시작하기 전에
{{site.data.keyword.mobilefirstbp}} 표준 유형을 사용 중 이어야 하며, `/protected` 엔드포인트에서 {{site.data.keyword.amashort}}의 보호를 받은 리소스가 있어야 합니다. 자세한 정보는 [리소스 보호](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)를 참조하십시오. 

1. 브라우저에서 새로 작성한 모바일 백엔드 애플리케이션의 보호 엔드포인트로 요청을 전송해 보십시오. URL `{applicationRoute}/protected`를 여십시오. 예를 들면 `http://my-mobile-backend.mybluemix.net/protected`와 같습니다. 
<br/>MobileFirst Services Starter 표준 유형으로 작성된 모바일 백엔드 애플리케이션의 `/protected` 엔드포인트는 {{site.data.keyword.amashort}}로 보호됩니다. `Unauthorized` 메시지가 브라우저에 리턴됩니다. 이 엔드포인트는 {{site.data.keyword.amashort}} 클라이언트 SDK로 인스트루먼트된 모바일 애플리케이션에서만 액세스될 수 있으므로 이 메시지가 리턴됩니다.

1. Cordova 애플리케이션을 사용하여 동일한 엔드포인트를 요청하십시오. `BMSClient`를 초기화한 후에 다음 코드를 추가하십시오. 

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error){
    	console.log("failure", error);
    }
	var request = new MFPRequest("/protected", MFPRequest.GET);
	request.send(success, failure);
	```
{: codeblock}

1. 애플리케이션을 실행하십시오. Facebook 로그인 화면이 팝업됩니다. 

	![image](images/android-facebook-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![image](images/ios-facebook-login.png)

	디바이스에 Facebook 앱이 설치되어 있지 않거나 현재 Facebook에 로그인하지 않은 경우 이 화면이 약간 다를 수 있습니다. 

1. **확인**을 클릭하여 {{site.data.keyword.amashort}}가 인증을 위해 Facebook 사용자 ID를 사용하도록 권한을 부여하십시오. 

1. 	요청이 성공하면 LogCat 유틸리티 또는 Xcode 콘솔에 다음과 같은 출력이 표시됩니다.

	![Android용 Facebook 인증 성공 메시지](images/android-facebook-login-success.png)

	![iOS용 Facebook 인증 성공 메시지](images/ios-facebook-login-success.png)
