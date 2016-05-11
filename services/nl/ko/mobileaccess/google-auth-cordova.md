---

copyright:
  years: 2015, 2016

---

# Cordova 앱에서 Google 인증 사용
{: #google-auth-cordova}
Google 인증 통합을 위해 Cordova 애플리케이션을 구성하려면 Java, Objective-C, Swift와 같은 Cordova 애플리케이션의 원시 코드를 변경해야 합니다. 각 플랫폼은 개별적으로 구성되어야 합니다. 원시 개발 환경을 사용하여 원시 코드(예: Android Studio 또는 Xcode)를 변경하십시오. 

## 시작하기 전에
{: #before-you-begin}
* {{site.data.keyword.amashort}}에서 보호하는 자원 및 {{site.data.keyword.amashort}} 클라이언트 SDK로 계측되는 Cordova 프로젝트가 있어야 합니다. 자세한 정보는 [{{site.data.keyword.amashort}} 시작하기](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) 및 [Cordova 플러그인 설정](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)을 참조하십시오.  
* {{site.data.keyword.amashort}} 서버 SDK를 사용하여 백엔드 애플리케이션을 수동으로 보호하십시오. 자세한 정보는 [자원 보호](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)를 참조하십시오. 
* (선택사항) 다음 절의 내용을 숙지하십시오. 
   * [Android 앱에서 Google 인증 사용](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)
   * [iOS 앱에서 Google 인증 사용](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html)


## Android 플랫폼 구성
{: #google-auth-cordova-android}

Google 인증 통합을 위해 Cordova 애플리케이션의 Android 플랫폼을 구성하는 데 필요한 단계는 원시 애플리케이션에 필요한 단계와 매우 유사합니다. 자세한 정보는 [Android 앱에서 Google 인증 사용](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)을 참조하십시오. 다음 항목을 설정하십시오. 

* Android 플랫폼에 대한 Google 프로젝트 구성
* Google 인증을 위해 {{site.data.keyword.amashort}} 구성
* Android용 {{site.data.keyword.amashort}} 클라이언트 SDK 구성

Cordova 애플리케이션을 구성하는 경우 유일한 차이점은 Java 코드 대신 JavaScript 코드로 {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화해야 한다는 것입니다. `GoogleAuthenticationManager` API는 계속 원시 코드에 등록되어 있어야 합니다. 

## iOS 플랫폼 구성
{: #google-auth-cordova-ios}

Google 인증을 통합하도록 Cordova 애플리케이션의 iOS 플랫폼을 구성하는 데 필요한 단계는 원시 애플리케이션에 대한 단계와 유사합니다. 가장 큰 차이점은 현재 Cordova CLI는 CocoaPods 종속 항목 관리자를 지원하지 않는다는 것입니다. Google 인증 통합에 필요한 파일을 수동으로 추가해야 합니다. 자세한 정보는 [iOS 앱에서 Google 인증 사용](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html)을 참조하십시오. 다음 단계를 완료하십시오. 

* iOS 플랫폼에 대한 Google 프로젝트 구성
* Google 인증을 위해 {{site.data.keyword.amashort}} 구성

### Google 인증 및 Google SDK를 위해 수동으로 {{site.data.keyword.amashort}} SDK 설치
{: #google-auth-cordova-ios-sdk}
1. [iOS용 {{site.data.keyword.Bluemix}} 모바일 서비스 SDK](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master)를 포함하는 아카이브를 다운로드하십시오. 

1. `Sources/Authenticators/IMFGoogleAuthentication` 디렉토리로 이동하여 모든 파일을 Xcode의 iOS 프로젝트에 복사(끌어서 놓기)하십시오. 복사해야 하는 파일은 다음과 같습니다. 

	> * IMFDefaultGoogleAuthenticationDelegate.h

	> * IMFDefaultGoogleAuthenticationDelegate.m

	> * IMFGoogleAuthenticationDelegate.h

	> * IMFGoogleAuthenticationHandler.h

	> * IMFGoogleAuthenticationHandler.m

**파일 복사....** 선택란을 선택하십시오. 

1. [Google+ iOS SDK](http://goo.gl/9cTqyZ)를 다운로드하여 설치하십시오. 

1. [Google+를 iOS 앱으로 통합 시작](https://developers.google.com/+/mobile/ios/getting-started) 학습서의 2단계를 따라 Google+ iOS SDK를 Xcode 프로젝트에 통합하십시오. 

[Google 인증을 위해 iOS 플랫폼 구성](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html)의 **Google 인증을 위해 iOS 프로젝트 구성** 섹션을 계속 진행하십시오. `{{site.data.keyword.amashort}} 클라이언트 SDK 초기화` 섹션에서 설명하는 대로 원시 코드에 `IMFGoogleAuthenticationHandler`를 등록하십시오. 원시 코드에서 `IMFClient`를 초기화할 필요는 없습니다. 이 작업은 JavaScript 코드로 곧 처리됩니다. 

다음 행을 애플리케이션 위임자의 `application:openURL:sourceApplication:annotation` 메소드에 추가하십시오. 이 행은 모든 Cordova 플러그인에서 각각의 이벤트에 대한 알림을 수신하도록 합니다. 

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```

## {{site.data.keyword.amashort}} 클라이언트 SDK 초기화
{: #google-auth-cordova-initialize}

Cordova 애플리케이션에서 다음 JavaScript 코드를 사용하여 {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화하십시오. 

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```

*applicationRoute* 및 *applicationGUID* 값을 대시보드에 있는 애플리케이션의 **모바일 옵션** 섹션에서 얻은 **라우트** 및 **앱 GUID** 값으로 바꾸십시오.

## 인증 테스트
{: #google-auth-cordova-test}
클라이언트 SDK가 초기화되면 모바일 백엔드에 대한 요청 작성을 시작할 수 있습니다. 

### 시작하기 전에
{: #google-auth-cordova-testing-before}
{{site.data.keyword.mobilefirstbp}} 표준 유형을 사용해야 하며 이미 `/protected` 엔드포인트에 {{site.data.keyword.amashort}}가 보호하는 자원이 있어야 합니다. `/protected` 엔드포인트를 설정해야 하는 경우
[자원 보호](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)를 참조하십시오. 


1. `{applicationRoute}/protected`(예: `http://my-mobile-backend.mybluemix.net/protected`)를 열어 데스크탑 브라우저에서 모바일 백엔드의 보호 엔드포인트로 요청을 전송하십시오.

1. MobileFirst 서비스 표준 유형으로 작성된 모바일 백엔드의 `/protected` 엔드포인트는 {{site.data.keyword.amashort}}로 보호되므로 {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하여 계측된 모바일 애플리케이션만 액세스할 수 있습니다. 결과적으로 데스크탑 브라우저에 `권한 없음`이 표시됩니다. 

1. Cordova 애플리케이션을 사용하여 동일한 엔드포인트에 대해 요청을 작성하십시오. `BMSClient`를 초기화한 후에 아래 코드를 추가하십시오. 

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


1. 애플리케이션을 실행하십시오. Google 로그인 화면이 팝업으로 표시됩니다. 

	![이미지](images/android-google-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![이미지](images/ios-google-login.png)
	이 화면은 사용자 디바이스에 Facebook 앱이 설치되어 있지 않거나 현재 Facebook에 로그인되어 있지 않은 경우 약간 다르게 보일 수 있습니다. 
1. **확인**을 클릭하면 인증을 위해 Google 사용자 ID를 사용하도록 {{site.data.keyword.amashort}}에 권한을 부여합니다. 

1. 	요청이 성공적으로 처리되어야 합니다. 사용 중인 플랫폼에 따라 다음 출력이 LogCat/Xcode 콘솔에 표시되어야 합니다. 

	![이미지](images/android-google-login-success.png)

	![이미지](images/ios-google-login-success.png)
