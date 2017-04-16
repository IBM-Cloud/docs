---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Cordova 앱에서 Google 인증 사용
{: #google-auth-cordova}

Google 인증을 위해 {{site.data.keyword.amafull}} Cordova 애플리케이션을 통합하려면 Cordova 애플리케이션 원시 플랫폼 코드(Java 또는 Objective-C) 및 Cordova WebView(Javascript)를 변경해야 합니다. 각 플랫폼은 개별적으로 구성되어야 합니다. 원시 개발 환경을 사용하여 원시 코드(예: Android Studio 또는 Xcode)를 변경하십시오. 

## 시작하기 전에
{: #before-you-begin}

다음이 있어야 합니다.

* {{site.data.keyword.amashort}} 클라이언트 SDK로 인스트루먼트된 Cordova 프로젝트.  자세한 정보는 [Cordova 플러그인 설정](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)을 참조하십시오.  
* {{site.data.keyword.amashort}} 서비스를 통해 보호하는 {{site.data.keyword.Bluemix_notm}} 애플리케이션의 인스턴스입니다. {{site.data.keyword.Bluemix_notm}} 백엔드 서비스 작성 방법에 대한 자세한 정보는 [시작하기](index.html)를 참조하십시오.
* 애플리케이션 라우트. 이는 백엔드 애플리케이션의 URL입니다. 
* **테넌트 ID**. {{site.data.keyword.Bluemix_notm}} 대시보드에서 서비스를 여십시오. **모바일 옵션**을 클릭하십시오. **앱 GUID / TenantId** 필드에 `tenantId`(`appGUID`라고도 함) 값이 표시됩니다. 이 값은 권한 관리자를 초기화하는 데 필요합니다. 
*  {{site.data.keyword.Bluemix_notm}} 애플리케이션이 호스팅되는 지역을 찾으십시오. 헤더에서 **아바타** 아이콘 ![아바타 아이콘](images/face.jpg "아바타 아이콘") 옆에 현재 Bluemix 지역이 표시됩니다. 지역 값은 **미국 남부**, **시드니** 또는 **영국** 중 하나여야 합니다. 이들 이름에 해당하는 정확한 SDK 상수 값은 코드 예제에 표시되어 있습니다. 
* (선택사항) 다음 절의 내용을 숙지하십시오. 
   * [Android 앱에서 Google 인증 사용](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)
   * [iOS 앱에서 Google 인증 사용](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html)


## Android 플랫폼 구성
{: #google-auth-cordova-android}

Google 인증을 위해 Cordova 애플리케이션의 Android 플랫폼을 구성하는 데 필요한 단계는 기본 애플리케이션에 필요한 단계와 매우 유사합니다. [Android 앱에서 Google 인증 사용](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)을 참조하여 다음을 설정하십시오.

   * [Google 개발자 콘솔에서 프로젝트 작성](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html#create-google-project). 여기서는 Google 개발자 웹 사이트에서 인증 서비스를 설정하는 방법을 설명합니다. 
   * [Google 인증용 MCA 구성](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html#google-auth-android-config). 여기서는 Google 인증을 사용하도록 {{site.data.keyword.amashort}}를 설정하는 방법을 설명합니다. 

### Android Cordova용 {{site.data.keyword.amashort}} 클라이언트 SDK 구성

1. Android 프로젝트 폴더에서 앱 모듈의 `build.gradle` 파일(프로젝트 `build.gradle` 파일이 **아님**)을 여십시오.
종속 항목 섹션을 찾은 다음 클라이언트 SDK에 대한 새 컴파일 종속 항목을 추가하십시오. 

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'googleauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```
	{: codeblock}

1. **도구 > Android > Gradle 파일로 프로젝트 동기화**를 클릭하여 프로젝트를 Gradle과 동기화하십시오. 

1. `GoogleAuthenticationManager` API는 계속 원시 코드에 등록되어 있어야 합니다. 다음 코드를 기본 활동 `onCreate` 메소드에 추가하십시오.

	```Java
	String tenantId = "<tenantId>";
	MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
	BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
	GoogleAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
	```
	{: codeblock}

1. 다음 코드를 활동에 추가하십시오. 

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		GoogleAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}

## iOS 플랫폼 구성
{: #google-auth-cordova-ios}

Google 인증을 통합하도록 Cordova 애플리케이션의 iOS 플랫폼을 구성하는 데 필요한 단계는 원시 애플리케이션에 대한 단계와 유사합니다. 주요한 차이점은 현재 Cordova CLI에서는 CocoaPods 종속성 관리자를 지원하지 않는다는 점입니다. Google 인증 통합에 필요한 파일을 수동으로 추가해야 합니다. 자세한 정보는 [iOS 앱에서 Google 인증 사용(Swift SDK)](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html)을 참조하십시오. 다음 단계를 완료하십시오. 

   * [Google 로그인을 위해 앱 준비](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-sign-in-ios): {{site.data.keyword.amashort}} iOS 애플리케이션을 인증하기 위해 Google 로그인을 준비합니다. 

   * [Google 인증용 MCA 구성](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-auth-ios-config): {{site.data.keyword.amashort}} 서비스를 Google 로그인과 상호작용하도록 구성합니다. 

   * [iOS용 MCA 클라이언트 SDK 구성](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-auth-ios-sdk): {{site.data.keyword.amashort}} 클라이언트를 Google 로그인과 상호작용하도록 구성합니다. 


### iOS에서 키 체인 공유 사용
{: #enable_keychain}

`키 체인 공유`를 사용 가능하게 설정하십시오. `기능` 탭으로 이동하여 Xcode 프로젝트에서 `키 체인 공유`를 `On`으로 전환하십시오. 


### iOS 코드에서 권한 관리자 초기화

`AppDelgate.m` 파일의 Objective-C에서 {{site.data.keyword.amashort}} 권한 관리자를 초기화하십시오. 

```
#import "<your_module_name>-Swift.h"

- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

{
	[CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];

	[[GoogleAuthenticationManager sharedInstance] register];

	self.viewController = [[MainViewController alloc] init];

	[[GoogleAuthenticationManager sharedInstance] onFinishLaunchingWithApplication:application withOptions:launchOptions];

	return [super application:application didFinishLaunchingWithOptions:launchOptions];
}

- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(NSString *)sourceApplication annotation:(id)annotation

{
	return [[GoogleAuthenticationManager sharedInstance] onOpenURLWithApplication:application url:url
	sourceApplication:sourceApplication annotation:annotation];
}
```
{: codeblock}

**참고:**

* `<your_module_name>`을 프로젝트의 모듈 이름으로 대체하십시오. 예를 들어, 모듈 이름이 `Cordova`인 경우 import 행은 `#import "Cordova-Swift.h"`여야 합니다.
모듈 이름을 찾으려면 `빌드 설정` 탭, `패키징` > `제품 모듈 이름`으로 이동하십시오. 
* `<tenantId>`를 사용하는 테넌트 ID로 대체하십시오([시작하기 전에](#before-you-begin) 참조).


## Cordova WebView에서 {{site.data.keyword.amashort}} 클라이언트 SDK 초기화
{: #google-auth-cordova-initialize}

모든 플랫폼의 경우, Cordova 애플리케이션에서 다음 Javascript 코드를 사용하여 {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화하십시오. 

```JavaScript
BMSClient.initialize("<applicationBluemixRegion>");
```
{: codeblock}

`<applicationBluemixRegion>`을 해당 지역으로 대체하십시오([시작하기 전에](#before-you-begin) 참조).

## 인증 테스트
{: #google-auth-cordova-test}

클라이언트 SDK가 초기화되면 모바일 백엔드 애플리케이션에 대한 요청을 시작할 수 있습니다. 

### 시작하기 전에
{: #google-auth-cordova-testing-before}

`/protected` 엔드포인트에서 {{site.data.keyword.amashort}}에 의해 보호되는 백엔드 애플리케이션이 있어야 합니다. `/protected` 엔드포인트를 설정해야 하는 경우 [리소스 보호](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)를 참조하십시오. 

1. `{applicationRoute}/protected`(예: `http://my-mobile-backend.mybluemix.net/protected`)를 열어서 데스크탑 브라우저에서 모바일 백엔드 애플리케이션의 보호 엔드포인트로 요청을 전송하십시오.

1. MobileFirst 서비스 표준 유형으로 작성된 모바일 백엔드 애플리케이션의 `/protected` 엔드포인트는 {{site.data.keyword.amashort}}에서 보호되므로 {{site.data.keyword.amashort}} 클라이언트 SDK로 인스트루먼트된 모바일 애플리케이션에서만 액세스할 수 있습니다. 결과적으로 데스크탑 브라우저에 `권한 없음`이 표시됩니다. 

1. Cordova 애플리케이션을 사용하여 동일한 엔드포인트에 대한 요청을 작성하십시오. 이 경우 전체 URL(예: `http://my-mobile-backend.mybluemix.net/protected`)을 사용하십시오. `BMSClient`를 초기화한 후 다음 코드를 추가하십시오. 

	```JavaScript
	var success = function(data){
		console.log("success", data);
	}
	var failure = function(error){
		console.log("failure", error);
	}
	var request = new BMSRequest("<your-application-route>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}

1. 애플리케이션을 실행하십시오. Google 로그인 화면이 표시됩니다.

	![Google 로그인 화면](images/android-google-login.png)

	![Google 로그인 화면](images/ios-google-login.png)

	디바이스에 Facebook 앱이 설치되어 있지 않거나 현재 Facebook에 로그인하지 않은 경우 이 화면이 약간 다를 수 있습니다. 

1. **확인**을 클릭하여 인증하는 데 Google 사용자 ID를 사용할 수 있도록 {{site.data.keyword.amashort}}에 권한을 부여합니다. 

1. 요청이 성공적으로 처리되어야 합니다. 사용하는 플랫폼에 따라 다음 출력이 LogCat/Xcode 콘솔에 표시됩니다.

	![android의 코드 스니펫](images/android-google-login-success.png)

	![iOS의 코드 스니펫](images/ios-google-login-success.png)
