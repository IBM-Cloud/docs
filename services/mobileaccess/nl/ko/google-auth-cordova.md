---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"
---
{:screen: .screen}
{:shortdesc: .shortdesc}

# Cordova 앱에서 Google 인증 사용
{: #google-auth-cordova}


Google 인증 통합을 위해 {{site.data.keyword.amafull}} Cordova 애플리케이션을 구성하려면, Cordova 애플리케이션의 원시 코드를 변경해야 합니다(Java, Objective-C 또는 Swift). 각 플랫폼은 개별적으로 구성되어야 합니다. 원시 개발 환경을 사용하여 원시 코드(예: Android Studio 또는 Xcode)를 변경하십시오. 

## 시작하기 전에
{: #before-you-begin}
다음이 있어야 합니다.
* {{site.data.keyword.amashort}} 클라이언트 SDK로 인스트루먼트된 Cordova 프로젝트.  자세한 정보는 [Cordova 플러그인 설정](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)을 참조하십시오.  
* {{site.data.keyword.amashort}} 서비스를 통해 보호하는 {{site.data.keyword.Bluemix_notm}} 애플리케이션의 인스턴스입니다. {{site.data.keyword.Bluemix_notm}} 백엔드 애플리케이션 작성 방법에 대한 자세한 정보는 [시작하기](index.html)를 참조하십시오.
* (선택사항) 다음 절의 내용을 숙지하십시오. 
   * [Android 앱에서 Google 인증 사용](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)
   * [iOS 앱에서 Google 인증 사용](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html)


## Android 플랫폼 구성
{: #google-auth-cordova-android}

Google 인증 통합을 위해 Cordova 애플리케이션의 Android 플랫폼을 구성하는 데 필요한 단계는 원시 애플리케이션에 필요한 단계와 매우 유사합니다. [Android 앱에서 Google 인증 사용](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)을 참조하여 다음을 설정하십시오.

* Android 플랫폼용 Google 프로젝트 구성
* Google 인증용 {{site.data.keyword.amashort}} 구성

### Android Cordova용 {{site.data.keyword.amashort}} 클라이언트 SDK 구성


2. Android 프로젝트 폴더에서 앱 모듈의 `build.gradle` 파일(프로젝트 `build.gradle` 파일이 **아님**)을 여십시오.
종속 항목 섹션을 찾은 다음 클라이언트 SDK에 대한 새 컴파일 종속 항목을 추가하십시오. 

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'googleauthentication',
        version: '1.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```

2. **도구 > Android > Gradle 파일로 프로젝트 동기화**를 클릭하여 프로젝트를 Gradle과 동기화하십시오. 

3. Cordova 애플리케이션의 경우, Java 코드 대신 JavaScript 코드로 {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화하십시오. `GoogleAuthenticationManager` API는 계속 원시 코드에 등록되어 있어야 합니다. 다음 코드를 기본 활동 `onCreate` 메소드에 추가하십시오. 

	```Java
	GoogleAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
	```

1. 다음 코드를 활동에 추가하십시오. 
 
 	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		GoogleAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
```

## iOS 플랫폼 구성
{: #google-auth-cordova-ios}

Google 인증을 통합하도록 Cordova 애플리케이션의 iOS 플랫폼을 구성하는 데 필요한 단계는 원시 애플리케이션에 대한 단계와 유사합니다. 주요한 차이점은 현재 Cordova CLI에서는 CocoaPods 종속성 관리자를 지원하지 않는다는 점입니다. Google 인증 통합에 필요한 파일을 수동으로 추가해야 합니다. 자세한 정보는 [iOS 앱에서 Google 인증 사용](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html)을 참조하십시오. 다음 단계를 완료하십시오. 

* iOS 플랫폼에 대한 Google 프로젝트 구성
* Google 인증용 {{site.data.keyword.amashort}} 구성

### Google 인증용 {{site.data.keyword.amashort}} SDK 및 Google SDK 수동 설치
{: #google-auth-cordova-ios-sdk}
1. [iOS용 {{site.data.keyword.Bluemix}} 모바일 서비스 SDK](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master)를 포함하는 아카이브를 다운로드하십시오. 

1. `Sources/Authenticators/IMFGoogleAuthentication` 디렉토리로 이동하여 모든 파일을 Xcode의 iOS 프로젝트에 복사(끌어서 놓기)하십시오. 복사해야 하는 파일은 다음과 같습니다. 

	* IMFDefaultGoogleAuthenticationDelegate.h
	* IMFDefaultGoogleAuthenticationDelegate.m
	* IMFGoogleAuthenticationDelegate.h
	* IMFGoogleAuthenticationHandler.h
	* IMFGoogleAuthenticationHandler.m

	**파일 복사....** 선택란을 선택하십시오. 

1. [Google+ iOS SDK](http://goo.gl/9cTqyZ)를 다운로드하여 설치하십시오. 

1. [Google+를 iOS 앱으로 통합 시작](https://developers.google.com/+/mobile/ios/getting-started) 튜토리얼의 2단계를 따라 Google+ iOS SDK를 Xcode 프로젝트에 통합하십시오. 

[Google 인증을 위해 iOS 플랫폼 구성](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html)의 **Google 인증을 위해 iOS 프로젝트 구성** 섹션을 계속 진행하십시오. `{{site.data.keyword.amashort}} 클라이언트 SDK 초기화` 섹션에 설명된 대로 `IMFGoogleAuthenticationHandler`를 원시 코드로 등록하십시오. 원시 코드로 `IMFClient`를 초기화하지 마십시오(해당 클라이언트는 다음 섹션에서 JavaScript로 초기화됨). 

애플리케이션 위임자의 `application:openURL:sourceApplication:annotation` 메소드에 다음 행을 추가하십시오. 모든 Cordova 플러그인에서 각 이벤트에 대한 알림을 수신하도록 합니다. 

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```
{: codeblock}

## {{site.data.keyword.amashort}} 클라이언트 SDK 초기화
{: #google-auth-cordova-initialize}

Cordova 애플리케이션에서 다음 JavaScript 코드를 사용하여 {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화하십시오.

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```
{: codeblock}

`applicationRoute` 및 `applicationGUID` 값을 애플리케이션 **라우트** 및 **앱 GUID** 값으로 바꾸십시오. 대시보드에서 애플리케이션 페이지 내의 **모바일 옵션** 단추를 클릭하여 이 값을 찾을 수 있습니다. 
	



##{{site.data.keyword.amashort}} AuthorizationManager 초기화
Cordova 애플리케이션에서 다음 JavaScript 코드를 사용하여 {{site.data.keyword.amashort}} AuthorizationManager를 초기화하십시오.

```JavaScript
  MFPAuthorizationManager.initialize("tenantId");
  ```
{: codeblock}

`tenantId` 값을 {{site.data.keyword.amashort}} 서비스 `tenantId`로 바꾸십시오. {{site.data.keyword.amashort}} 서비스 타일의 **신임 정보 표시** 단추를 클릭하여 이 값을 찾을 수 있습니다. 





## 인증 테스트
{: #google-auth-cordova-test}
클라이언트 SDK가 초기화되면 모바일 백엔드 애플리케이션에 대한 요청을 시작할 수 있습니다. 

### 시작하기 전에
{: #google-auth-cordova-testing-before}
`/protected` 엔드포인트에서 {{site.data.keyword.amashort}}에 의해 보호되는 백엔드 애플리케이션이 있어야 합니다. `/protected` 엔드포인트를 설정해야 하는 경우 [리소스 보호](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)를 참조하십시오. 


1. `{applicationRoute}/protected`(예: `http://my-mobile-backend.mybluemix.net/protected`)를 열어서 데스크탑 브라우저에서 모바일 백엔드 애플리케이션의 보호 엔드포인트로 요청을 전송하십시오.

1. MobileFirst 서비스 표준 유형으로 작성된 모바일 백엔드 애플리케이션의 `/protected` 엔드포인트는 {{site.data.keyword.amashort}}에서 보호되므로 {{site.data.keyword.amashort}} 클라이언트 SDK로 인스트루먼트된 모바일 애플리케이션에서만 액세스할 수 있습니다. 결과적으로 데스크탑 브라우저에 `권한 없음`이 표시됩니다. 

1. Cordova 애플리케이션을 사용하여 동일한 엔드포인트에 대해 요청을 작성하십시오. `BMSClient`를 초기화한 후 다음 코드를 추가하십시오. 

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new MFPRequest("/protected", MFPRequest.GET);
	request.send(success, failure);
	```
{: codeblock}

1. 애플리케이션을 실행하십시오. Google 로그인 화면이 표시됩니다.

	![Google 로그인 화면](images/android-google-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![Google 로그인 화면](images/ios-google-login.png)
	
	디바이스에 Facebook 앱이 설치되어 있지 않거나 현재 Facebook에 로그인하지 않은 경우 이 화면이 약간 다를 수 있습니다.
1. **확인**을 클릭하여 인증하는 데 Google 사용자 ID를 사용할 수 있도록 {{site.data.keyword.amashort}}에 권한을 부여합니다. 

1. 요청이 성공적으로 처리되어야 합니다. 사용하는 플랫폼에 따라 다음 출력이 LogCat/Xcode 콘솔에 표시됩니다.

	![android의 코드 스니펫](images/android-google-login-success.png)

	![iOS의 코드 스니펫](images/ios-google-login-success.png)
