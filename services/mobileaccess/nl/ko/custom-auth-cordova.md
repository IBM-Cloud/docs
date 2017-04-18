---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.amashort}} Cordova 앱용 사용자 정의 인증 구성
{: #custom-cordova}

사용자 정의 인증 및 {{site.data.keyword.amafull}} 클라이언트 SDK를 사용하여 보호 애플리케이션에 액세스하도록 Cordova 애플리케이션을 인스트루먼트합니다. 

## 시작하기 전에
{: #before-you-begin}
* 사용자 정의 ID 제공자를 사용하도록 구성된 {{site.data.keyword.amashort}} 서비스 인스턴스에 의해 보호되는 리소스([사용자 정의 인증 구성 참조](custom-auth-config-mca.html)).  
* **테넌트 ID** 값. {{site.data.keyword.amashort}} 대시보드에서 서비스를 여십시오. **모바일 옵션** 단추를 클릭하십시오. **앱 GUID / TenantId** 필드에 `tenantId`(`appGUID`라고도 함) 값이 표시됩니다. 이 값은 권한 관리자를 초기화하는 데 필요합니다. 
* **영역** 이름. 이 값은 {{site.data.keyword.amashort}} 대시보드의 **관리** 탭에서 **사용자 정의** 섹션의 **영역 이름** 필드에 지정한 값입니다. 
* {{site.data.keyword.Bluemix_notm}} **지역**. 헤더에서 **아바타** 아이콘 ![아바타 아이콘](images/face.jpg "아바타 아이콘") 옆에 현재 {{site.data.keyword.Bluemix_notm}} 지역이 표시됩니다. 표시되는 지역 값은 `US South`, `United Kingdom` 및 `Sydney` 중 하나여야 합니다. 코드 예제에서 해당하는 SDK 상수의 정확한 구문을 제공합니다. 

자세한 정보는 다음 내용을 참조하십시오. 

 * [사용자 정의 인증용 {{site.data.keyword.amashort}} 구성](custom-auth-config-mca.html). 여기서는 사용자 정의 인증용으로 {{site.data.keyword.amashort}} 서비스를 설정하는 방법을 설명합니다. 또한 **영역** 값을 정의합니다. 
 * [Cordova SDK 설정](getting-started-cordova.html). Cordova 클라이언트 앱 설정에 관한 정보를 제공합니다. 
 * [사용자 정의 ID 제공자 사용](custom-auth.html). 사용자 정의 ID 제공자를 사용하여 사용자를 인증하는 방법을 설명합니다. 
 * [사용자 정의 ID 제공자 작성](custom-auth-identity-provider.html). 사용자 정의 ID 제공자가 작동하는 방법의 몇 가지 예를 제공합니다. 

## Cordova WebView 코드 구성
### Cordova WebView에서 {{site.data.keyword.amashort}} 클라이언트 SDK 초기화
{: #custom-cordova-sdk}
`index.js` 파일에서 `<applicationBluemixRegion>` 매개변수를 전달하여 SDK를 초기화하십시오. 

```JavaScript
BMSClient.initialize("<applicationBluemixRegion>");
```
{: codeblock}

`<applicationBluemixRegion>`을 해당 지역으로 대체하십시오([시작하기 전에](#before-you-begin) 참조).


### 인증 리스너 인터페이스
{: #custom-cordva-auth}

{{site.data.keyword.amashort}} 클라이언트 SDK는 사용자 정의 인증 플로우를 구현할 수 있도록 인증 리스너 인터페이스를 제공합니다. 인증 프로세스의 서로 다른 단계에서 호출되는 다음 메소드를 추가해야 합니다. 

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...},
	onAuthenticationSuccess: function(info){...},
	onAuthenticationFailure: function(info){...}
}
```
{: codeblock}

각 메소드는 인증 프로세스의 서로 다른 단계를 처리합니다. 

### onAuthenticationChallengeReceived 메소드
{: #onAuthenticationChallengeReceived}
이 메소드는 {{site.data.keyword.amashort}} 서비스에서 사용자 정의 인증 확인이 수신된 경우에 호출됩니다. 
```JavaScript
onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...}
```
{: codeblock}

* `authenticationContext`: 개발자가 신임 정보 수집 중 인증 확인 응답 또는 실패를 보고할 수 있도록 {{site.data.keyword.amashort}} 클라이언트 SDK에서 제공합니다(예: 사용자가 인증 요청을 취소하는 경우).
* `challenge`: 사용자 정의 ID 제공자가 리턴하는 사용자 정의 인증 확인이 포함된 JSON 오브젝트입니다. 

`onAuthenticationChallengeReceived` 메소드를 호출하면 {{site.data.keyword.amashort}} 클라이언트 SDK가 제어를 개발자에게 위임합니다. {{site.data.keyword.amashort}}는 신임 정보를 기다립니다. 개발자는 신임 정보를 수집하고 다음 `authContext` 인터페이스 메소드 중 하나를 사용하여 {{site.data.keyword.amashort}} 클라이언트 SDK에 수집한 신임 정보를 다시 보고해야 합니다.

```JavaScript
onAuthenticationSuccess: function(info){...}
```
{: codeblock}

이 메소드는 인증 성공 후에 호출됩니다. 인수로는 인증 성공에 대한 확장 정보가 포함된 선택적 JSON 오브젝트가 있습니다. 

```JavaScript
onAuthenticationFailure: function(info){...}
```
{: codeblock}

이 메소드는 인증 실패 후에 호출됩니다. 인수로는 인증 실패에 대한 확장 정보가 포함된 선택적 JSON 오브젝트가 있습니다. 

### authenticationContext
{: #custom-cordova-authcontext}

`authenticationContext` 값은 사용자 정의 인증 리스너의 `onAuthenticationChallengeReceived` 메소드에 대한 인수로 제공됩니다. 개발자는 신임 정보를 수집하고 `authenticationContext` 메소드를 사용하여 신임 정보를 {{site.data.keyword.amashort}} 클라이언트 SDK로 리턴하거나 실패를 보고해야 합니다. 다음 메소드 중 하나를 사용하십시오. 

```JavaScript
authenticationContext.submitAuthenticationChallengeAnswer(challengeAnswer);
```
{: codeblock}

```JavaScript
authenticationContext.submitAuthenticationFailure(info);
```
{: codeblock}

다음 코드는 고객 인증 리스너가 신임 정보를 수집하고 인증 확인을 처리하며 인증 응답을 제공하는 방법을 설명합니다. 

## 사용자 정의 인증 리스너 워크플로우의 샘플 구현
{: #custom-cordova-authlisten-sample}

이 인증 리스너 샘플은 사용자 정의 ID 제공자와 함께 작동하도록 설계되었습니다. [이 Github 저장소 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "외부 링크 아이콘"){: new_window}에서 사용자 정의 ID 제공자를 다운로드할 수 있습니다. 

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {
		console.log("onAuthenticationChallengeReceived :: ", challenge);

		// In this sample the authentication listener immediatelly returns a hardcoded
		// set of credentials. In a real life scenario this is where developer would
		// show a login screen, collect credentials and invoke
		// authenticationContext.submitAuthenticationChallengeAnswer() API

		var challengeResponse = {
			username: "john.lennon",
			password: "12345"
		}

		authenticationContext.submitAuthenticationChallengeAnswer(challengeResponse);

		// In case there was a failure collecting credentials you need to report
		// it back to the authenticationContext. Otherwise Mobile Client
		// Access client SDK will remain in a waiting-for-credentials state
		// forever

	},

	onAuthenticationSuccess: function(info){
		console.log("onAuthenticationSuccess :: ", info);
	},

	onAuthenticationFailure: function(info){
		console.log("onAuthenticationFailure :: ", info);
	}
}
```
{: codeblock}

## Cordova WebView에서 사용자 정의 인증 리스너 등록
{: #custom-cordova-authreg}

사용자 정의 인증 리스너를 작성한 후에는 `BMSClient`에 리스너를 등록해야만 리스너를 사용할 수 있습니다. 애플리케이션에 다음 코드를 추가하십시오. 보호된 리소스에 대한 요청을 전송하기 전에 다음 코드를 호출하십시오. 

```Java
BMSClient.registerAuthenticationListener(<realmName>, customAuthenticationListener);
```
{: codeblock}
{{site.data.keyword.amashort}} 대시보드에서 지정한 `realmName`을 사용하십시오.

## 원시 코드에 권한 관리자 설정

{{site.data.keyword.amashort}} 권한 관리자는 원시 플랫폼 코드에 등록되어야 합니다. 

**Android**(기본 활동의 `onCreate`에 추가)

```
String tenantId = "<tenantId>";
MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
```
{: codeblock}

**iOS Objective-C**(`AppDelegate.m`에 추가)

Xcode의 버전에 따라 권한 관리자를 등록하십시오. 

```
# import "<your_module_name>-Swift.h"

- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

{  

    //[CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];
 }
```
{: codeblock}

참고: 올바른 Swift 헤더 파일 이름을 지정하려면 `your_module_name`을 프로젝트의 모듈 이름으로 대체하십시오. 예를 들어, 모듈 이름이 `Cordova`이면 이는 `#import "Cordova-Swift.h"`가 되어야 합니다. 모듈 이름을 찾으려면 **빌드 설정 > 패키징` > 제품 모듈 이름**으로 이동하십시오. 

**참고:** `tenantId`를 {{site.data.keyword.amashort}} 서비스 대시보드의 **모바일 옵션** 단추에 있는 테넌트 ID로 대체하십시오. 


## iOS에서 키 체인 공유 사용

`기능` 탭으로 이동한 후 Xcode 프로젝트에서 `키 체인 공유`를 `On`으로 전환하여 `키 체인 공유`를 사용 가능하게 설정하십시오. 


## 인증 테스트
{: #custom-cordova-test}
클라이언트 SDK를 초기화하고 사용자 정의 `AuthenticationListener`를 등록한 후에는 모바일 백엔드 애플리케이션에 대한 요청을 시작할 수 있습니다. 

### 시작하기 전에
{: #custom-cordova-testing-before}
{{site.data.keyword.mobilefirstbp}} 표준 유형으로 작성된 애플리케이션과 `/protected` 엔드포인트에서 {{site.data.keyword.amashort}}의 보호를 받는 리소스가 있어야 합니다. 


1. `{applicationRoute}/protected`(예: `http://my-mobile-backend.mybluemix.net/protected`)를 열어 브라우저에서 모바일 백엔드 애플리케이션의 보호 엔드포인트로 요청을 전송하십시오.
 {{site.data.keyword.mobilefirstbp}} 표준 유형으로 작성된 모바일 백엔드 애플리케이션의 `/protected` 엔드포인트는 {{site.data.keyword.amashort}}로 보호됩니다. 이 엔드포인트는 {{site.data.keyword.amashort}} 클라이언트 SDK로 인스트루먼트된 모바일 애플리케이션에서만 액세스할 수 있습니다. 따라서 `Unauthorized` 메시지는 브라우저에 표시됩니다. 

1. Cordova 애플리케이션을 사용하여 동일한 엔드포인트를 요청하십시오. `BMSClient`를 초기화하고 사용자 정의 AuthenticationListener를 등록한 후 다음 코드를 추가하십시오. 

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new BMSRequest("<your-application-route>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}

	`<your-application-route>`를 백엔드 애플리케이션 URL로 대체하십시오([시작하기 전에](#before-you-begin) 참조).

1. 	요청이 성공하면 `LogCat` 또는 Xcode 콘솔에 다음과 같은 출력이 표시됩니다. 

	![이미지](images/android-custom-login-success.png)

	![이미지](images/ios-custom-login-success.png)
