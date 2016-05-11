---

copyright:
  years: 2015, 2016

---

# Cordova에 대해 {{site.data.keyword.amashort}} 클라이언트 SDK 구성
{: #custom-cordova}
사용자 정의 인증을 사용하는 Cordova 애플리케이션이 {{site.data.keyword.amashort}}
클라이언트 SDK를 사용하고 애플리케이션을 {{site.data.keyword.Bluemix}}에 연결하도록 구성하십시오. 


## 시작하기 전에
{: #before-you-begin}
사용자 정의 ID 제공자를 사용하도록 구성된 {{site.data.keyword.amashort}} 서비스
인스턴스의 보호를 받는 자원이 있어야 합니다. 모바일 앱은 {{site.data.keyword.amashort}}
클라이언트 SDK도 갖추고 있어야 합니다. 자세한 정보는 다음 내용을 참조하십시오. 
 * [{{site.data.keyword.amashort}} 시작하기](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Cordova SDK 설정](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)
 * [사용자 정의 ID 제공자 사용](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [사용자 정의 ID 제공자 작성](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [사용자 정의 인증을 사용하도록 {{site.data.keyword.amashort}} 구성](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)

## {{site.data.keyword.amashort}} 클라이언트 SDK 초기화
{: #custom-cordova-sdk}
SDK를 초기화하려면 applicationGUID 및 applicationRoute 매개변수를 전달하십시오. 

1. 애플리케이션 매개변수 값을 가져오십시오. {{site.data.keyword.Bluemix_notm}} 대시보드에서
앱을 여십시오. **모바일 옵션**을 클릭하십시오. **라우트**(`applicationRoute`) 및 **앱 GUID**(`applicationGUID`) 값이 표시됩니다.
1. 클라이언트 SDK를 초기화하십시오. 

	```JavaScript
	BMSClient.initialize(applicationRoute, applicationGUID);

	```
 *applicationRoute* 및 *applicationGUID*를 {{site.data.keyword.Bluemix_notm}} 대시보드에서 애플리케이션의 **모바일 옵션** 패널에 있는 **라우트** 및 **앱 GUID** 값으로 바꾸십시오.

## 인증 리스너 인터페이스
{: #custom-cordva-auth}

{{site.data.keyword.amashort}} 클라이언트 SDK는 사용자 정의 인증 플로우를
구현할 수 있도록 인증 리스너 인터페이스를 제공합니다. 인증 프로세스의 서로 다른 단계에서
호출되는 다음 메소드를 추가해야 합니다. 

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...},
	onAuthenticationSuccess: function(info){...},
	onAuthenticationFailure: function(info){...}
}
```

각 메소드는 인증 프로세스의 서로 다른 단계를 처리합니다. 

### onAuthenticationChallengeReceived 메소드
{: #onAuthenticationChallengeReceived}
이 메소드는 {{site.data.keyword.amashort}} 서비스에서 사용자 정의 인증 확인이
수신된 경우에 호출됩니다.
```JavaScript
onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...}
```

#### 인수
{: #onAuthenticationChallengeReceived-args}
* `authenticationContext`: 개발자가 신임 정보 수집 중 인증 확인
응답 또는 실패를 보고할 수 있도록 {{site.data.keyword.amashort}} 클라이언트 SDK에서
제공합니다(예: 사용자가 인증 요청을 취소하는 경우). 
* `challenge`: 사용자 정의 ID 제공자가 리턴하는 사용자 정의 인증 확인이
포함된 JSON 오브젝트입니다. 

`onAuthenticationChallengeReceived` 메소드를 호출하면
{{site.data.keyword.amashort}} 클라이언트 SDK가 제어 권한을 개발자에게
위임합니다. {{site.data.keyword.amashort}}는 신임 정보를 기다립니다. 개발자는 신임 정보를 수집하고
다음 `authContext` 인터페이스 메소드 중 하나를 사용하여
{{site.data.keyword.amashort}} 클라이언트 SDK에 신임 정보를 보고해야 합니다. 

```JavaScript
onAuthenticationSuccess: function(info){...}
```

이 메소드는 인증 성공 후에 호출됩니다. 인수로는 인증 성공에 대한 확장 정보가
포함된 선택적 JSONObject가 있습니다. 

```JavaScript
onAuthenticationFailure: function(info){...}
```

이 메소드는 인증 실패 후에 호출됩니다. 인수로는 인증 실패에 대한 확장 정보가
포함된 선택적 JSONObject가 있습니다. 

## authenticationContext
{: #custom-cordova-authcontext}

`authenticationContext` 값은 사용자 정의 인증 리스너의
`onAuthenticationChallengeReceived` 메소드에 대한 인수로 제공됩니다.
개발자는 신임 정보를 수집하고 `authenticationContext` 메소드를 사용하여 신임 정보를
{{site.data.keyword.amashort}} 클라이언트 SDK로 리턴하거나 실패를 보고해야
합니다. 다음 메소드 중 하나를 사용하십시오. 

```JavaScript
authenticationContext.submitAuthenticationChallengeAnswer(challengeAnswer);

authenticationContext.submitAuthenticationFailure(info);
```

## 사용자 정의 인증 리스너의 샘플 구현
{: #custom-cordova-authlisten-sample}

이 인증 리스너 샘플은 사용자 정의 ID 제공자와 함께 작동하도록 설계되었습니다.
사용자 정의 ID 제공자는 [이
Github 저장소](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)에서 다운로드할 수 있습니다. 

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
		// Access Client SDK will remain in a waiting-for-credentials state
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

## 사용자 정의 인증 리스너 등록
{: #custom-cordova-authreg}

사용자 정의 인증 리스너를 작성한 후 리스너를 사용하기 전에 `BMSClient`에
등록하십시오. 애플리케이션에 다음 코드를 추가하십시오. 보호된 자원에 대한 요청을
전송하기 전에 다음 코드를 호출하십시오. 

```Java
BMSClient.registerAuthenticationListener(realmName, customAuthenticationListener);
```
 {{site.data.keyword.amashort}} 대시보드에서 지정한 *realmName*을
사용하십시오. 


## 인증 테스트
{: #custom-cordova-test}
클라이언트 SDK가 초기화되고 사용자 정의 AuthenticationListener가 등록되면
모바일 백엔드 요청을 시작할 수 있습니다. 

### 시작하기 전에
{: #custom-cordova-testing-before}
{{site.data.keyword.mobilefirstbp}} 표준 유형으로 작성된
애플리케이션과 `/protected` 엔드포인트에서 {{site.data.keyword.amashort}}의
보호를 받는 자원이 있어야 합니다. 


1. `{applicationRoute}/protected`(예: `http://my-mobile-backend.mybluemix.net/protected`)를 열어 브라우저에서 모바일 백엔드의 보호 엔드포인트로 요청을 전송하십시오.
 {{site.data.keyword.mobilefirstbp}} 표준 유형으로 작성된 모바일 백엔드의
`/protected` 엔드포인트는 {{site.data.keyword.amashort}}에서 보호됩니다.
엔드포인트는 {{site.data.keyword.amashort}} 클라이언트 SDK를 갖춘 모바일 애플리케이션에서만
액세스할 수 있습니다. 따라서 `Unauthorized` 메시지는 브라우저에 표시됩니다. 

1. Cordova 애플리케이션을 사용하여 동일한 엔드포인트를 요청하십시오.
`BMSClient`를 초기화하고 사용자 정의 AuthenticationListener를
등록한 후 다음 코드를 추가하십시오. 

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

1. 	요청이 성공하면 LogCat 또는 Xcode 콘솔에 다음과 같은 출력이 표시됩니다. 

	![이미지](images/android-custom-login-success.png)

	![이미지](images/ios-custom-login-success.png)
