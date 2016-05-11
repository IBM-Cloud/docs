---

copyright:
  years: 2015, 2016

---

# Cordova 앱에서 Facebook 인증 사용
{: #facebook-auth-cordova}
Facebook 인증 통합을 위해 Cordova 애플리케이션을 구성하려면 Java, Objective-C 또는 Swift로 Cordova 애플리케이션의 원시 코드를 변경해야 합니다. 플랫폼마다 별도로 구성하십시오. Android Studio 또는 Xcode 등에서 원시 코드를 변경하려면 기본 개발 환경을 사용하십시오. 

## 시작하기 전에
{: #facebook-auth-before}
* {{site.data.keyword.amashort}}에서 보호하는 자원 및 {{site.data.keyword.amashort}} 클라이언트 SDK를 갖춘 Cordova 프로젝트가 있어야 합니다. 자세한 정보는 [{{site.data.keyword.amashort}} 시작하기](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) 및 [Cordova 플러그인 설정](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)을 참조하십시오.
* {{site.data.keyword.amashort}} 서버 SDK로 백엔드 애플리케이션을 수동으로 보호하십시오. 자세한 정보는 [자원 보호](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)를 참조하십시오. 
* Facebook 애플리케이션 ID를 작성하십시오. 자세한 정보는 [Facebook 개발자 포털에서 Facebook 애플리케이션 ID 얻기](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)를 참조하십시오. 
* (선택사항) 다음 절의 내용을 숙지하십시오. 
   * [Android 앱에서 Facebook 인증 사용](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html)
   * [iOS 앱에서 Facebook 인증 사용](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html)


## Android 플랫폼 구성
{: #facebook-auth-cordova-android}

Facebook 인증 통합을 위해 Cordova 애플리케이션의 Android 플랫폼을 구성하는 데 필요한 단계는 기본 Android 애플리케이션에 필요한 단계와 매우 유사합니다. 자세한 정보는 [Android 앱에서 Facebook 인증 사용](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html)을 참조하십시오. 다음 단계를 수행하십시오. 

* Android 플랫폼에 대해 Facebook 애플리케이션 구성
* Facebook 인증을 사용하도록 {{site.data.keyword.amashort}} 구성
* Android용 {{site.data.keyword.amashort}} 클라이언트 SDK 구성

Cordova 애플리케이션을 구성할 때 유일한 차이점은 {{site.data.keyword.amashort}} 클라이언트 SDK를 Java 코드 대신 Javascript 코드로 초기화해야 한다는 점입니다. `FacebookAuthenticationManager` API는 여전히 사용자의 원시 코드에 등록해야 합니다. 

## iOS 플랫폼 구성
{: #facebook-auth-cordova-ios}

Facebook 인증을 통합하도록 Cordova 애플리케이션의 iOS 플랫폼을 구성하는 데 필요한 단계는 기본 iOS 애플리케이션에 필요한 단계와 유사합니다. 주요한 차이점은 현재 Cordova CLI에서는 CocoaPods 종속성 관리자를 지원하지 않는다는 점입니다. 따라서 Facebook 인증과 통합하는 데 필요한 파일을 수동으로 추가해야 합니다. 자세한 정보는 [iOS 앱에서 Facebook 인증 사용](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html)을 참조하십시오. 다음 단계를 수행하십시오. 

* iOS 플랫폼에 대해 Facebook 애플리케이션 구성
* Facebook 인증을 사용하도록 {{site.data.keyword.amashort}} 구성

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

1. 	Xcode의 왼쪽 분할창에서 프로젝트 루트를 클릭하고 **빌드 단계**를 선택하십시오. 

1. **라이브러리와 2진 링크**에서 링크된 라이브러리 목록에 `FacebookSDK.framework` 파일을 추가하십시오.

 [Facebook 인증을 사용하도록 iOS 플랫폼 구성](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html)을 참조하십시오. **{{site.data.keyword.amashort}} 클라이언트 SDK 초기화** 절에 설명된 대로 `IMFFacebookAuthenticationHandler` API를 원시 코드로 등록하십시오. `IMFClient`는 원시 코드로 초기화하지 마십시오.

애플리케이션 위임자의 `application:openURL:sourceApplication:annotation` 메소드에 다음 행을 추가하십시오. 이 코드는 모든 Cordova 플러그인에서 각각의 이벤트에 대한 알림을 수신하도록 합니다.

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```

## {{site.data.keyword.amashort}} 클라이언트 SDK 초기화
{: #facebook-auth-cordova-init}

{{site.data.keyword.amashort}} 클라이언트 SDK를 초기화하려면 Cordova 애플리케이션에서 다음 JavaScript 코드를 사용하십시오. 

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```

*applicationRoute* 및 *applicationGUID*를 **모바일 옵션**에서 **라우트** 및 **앱 GUID**에 대해 얻은 값으로 바꾸십시오.

## 인증 테스트
{: #facebook-auth-cordova-test}
클라이언트 SDK가 초기화되고 Facebook 인증 관리자가 등록되면 모바일 백엔드에 대한 요청 작성을 시작할 수 있습니다.

### 시작하기 전에
{{site.data.keyword.mobilefirstbp}} 표준 유형을 사용하고 있어야 하며, `/protected` 엔드포인트에서 {{site.data.keyword.amashort}}의 보호를 받은 자원이 있어야 합니다. 자세한 정보는 [자원 보호](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)를 참조하십시오. 

1. 브라우저에서 새로 작성한 모바일 백엔드의 보호 엔드포인트로 요청을 전송해 보십시오. URL `{applicationRoute}/protected`를 여십시오. 예를 들면 `http://my-mobile-backend.mybluemix.net/protected`와 같습니다. 
<br/>MobileFirst Services Starter 표준 유형으로 작성된 모바일 백엔드의 `/protected` 엔드포인트는 {{site.data.keyword.amashort}}에서 보호됩니다. `Unauthorized` 메시지가 브라우저에 리턴됩니다. 이 엔드포인트는 {{site.data.keyword.amashort}} 클라이언트 SDK를 갖춘 모바일 애플리케이션에서만 액세스할 수 있으므로 이 메시지가 리턴됩니다.

1. Cordova 애플리케이션을 사용하여 동일한 엔드포인트를 요청하십시오. `BMSClient`를 초기화한 후 아래 코드를 추가하십시오. 

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

1. 애플리케이션을 실행하십시오. Facebook 로그인 화면이 팝업됩니다. 

	![image](images/android-facebook-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![image](images/ios-facebook-login.png)

	> 디바이스에 Facebook 앱이 설치되어 있지 않거나 현재 Facebook에 로그인하지 않은 경우 이 화면이 약간 다를 수 있습니다.

1. **확인**을 클릭하여 {{site.data.keyword.amashort}}가 인증을 위해 Facebook 사용자 ID를 사용하도록 권한을 부여하십시오. 

1. 	요청이 성공하면 LogCat 유틸리티 또는 Xcode 콘솔에 다음과 같은 출력이 표시됩니다.

	![Android의 경우 Facebook 인증 성공 메시지](images/android-facebook-login-success.png)

	![iOS의 경우 Facebook 인증 성공 메시지](images/ios-facebook-login-success.png)
