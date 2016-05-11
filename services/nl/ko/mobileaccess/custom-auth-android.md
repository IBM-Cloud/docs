---

copyright:
  years: 2015, 2016

---

# Android에 대해 {{site.data.keyword.amashort}} 클라이언트 SDK 구성
{: #custom-android}
사용자 정의 인증을 사용하는 Android 애플리케이션이 {{site.data.keyword.amashort}}
클라이언트 SDK를 사용하고 애플리케이션을 {{site.data.keyword.Bluemix}}에 연결하도록 구성하십시오. 

## 시작하기 전에
{: #before-you-begin}
사용자 정의 ID 제공자를 사용하도록 구성된 {{site.data.keyword.amashort}} 서비스
인스턴스의 보호를 받는 자원이 있어야 합니다. 모바일 앱은 {{site.data.keyword.amashort}}
클라이언트 SDK도 갖추고 있어야 합니다. 자세한 정보는 다음 내용을 참조하십시오. 
 * [{{site.data.keyword.amashort}} 시작하기](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Android SDK 설정](https://console.{DomainName}/docs/services/mobileaccess/getting-started-android.html)
 * [사용자 정의 ID 제공자 사용](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [사용자 정의 ID 제공자 작성](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [사용자 정의 인증을 사용하도록 {{site.data.keyword.amashort}} 구성](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## {{site.data.keyword.amashort}} 클라이언트 SDK 초기화
{: #custom-android-initialize}
1. Android Studio의 Android 프로젝트에서 앱 모듈의 `build.gradle`
파일을 여십시오. 
<br/>**팁:** Android 프로젝트에는 두 개의 `build.gradle`
파일(프로젝트용 및 애플리케이션 모듈용)이 있습니다. 애플리케이션 모듈 파일을 사용하십시오.
1. `build.gradle` 파일에서 `dependencies` 섹션을
찾아 다음 컴파일 종속성을 확인하십시오. 없는 경우 이 종속성을 추가하십시오. 

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    
        name:'core',
        version: '1.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```

1. 프로젝트를 Gradle과 동기화하십시오. **도구 > Android > Gradle 파일과 프로젝트 동기화**를
클릭하십시오. 

1. Android 프로젝트의 `AndroidManifest.xml` 파일을 여십시오.
`<manifest>` 요소 아래에 인터넷 액세스 권한을 추가하십시오. 

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```

1. SDK를 초기화하십시오. 초기화 코드를 삽입하는 일반 위치(필수는 아님)는 Android 애플리케이션에서
기본 활동의 `onCreate` 메소드에 있습니다. *applicationRoute* 및 *applicationGUID*를 {{site.data.keyword.Bluemix_notm}} 대시보드에서 앱의 **모바일 옵션**을 클릭하면 얻을 수 있는 **라우트** 및 **앱 GUID** 값으로 바꾸십시오.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");					
	```

## AuthenticationListener 인터페이스
{: #custom-android-authlistener}

{{site.data.keyword.amashort}} 클라이언트 SDK는 사용자가 사용자 정의 인증 플로우를
구현할 수 있도록 `AuthenticationListener` 인터페이스를 제공합니다.
`AuthenticationListener` 인터페이스는 인증 프로세스의
서로 다른 단계에서 호출되는 세 개의 메소드를 표시합니다. 

### onAuthenticationChallengeReceived 메소드
{: #custom-onAuth}
이 메소드는 {{site.data.keyword.amashort}} 서비스에서 사용자 정의 인증 확인이
수신된 경우에 호출하십시오. 

```Java
void onAuthenticationChallengeReceived(AuthenticationContext authContext, JSONObject challenge, Context context);
```
#### 인수
{: #custom-android-onAuth-arg}

* `AuthenticationContext`: 사용자가 신임 정보 수집 중 인증 확인
응답 또는 실패를 보고할 수 있도록 {{site.data.keyword.amashort}} 클라이언트 SDK에서
제공합니다. 예를 들어 사용자가 인증을 취소하는 경우입니다. 
* `JSONObject`: 사용자 정의 ID 제공자가 리턴하는 사용자 정의
인증 확인을 포함합니다. 
* `Context`: 요청이 전송될 때 사용된 Android 컨텍스트에 대한 참조입니다.
보통 이 인수는 Android 활동을 나타냅니다. 

`onAuthenticationChallengeReceived` 메소드를 호출하면
{{site.data.keyword.amashort}} 클라이언트 SDK가 제어 권한을 개발자에게
위임합니다. 서비스는 신임 정보를 기다립니다. 개발자는 신임 정보를 수집하고
`AuthenticationContext` 인터페이스 메소드 중 하나를 사용하여
{{site.data.keyword.amashort}} 클라이언트 SDK에 신임 정보를 보고해야 합니다. 

### onAuthenticationSuccess 메소드
{: #custom-android-authlistener-onsuccess}
이 메소드는 인증 성공 후에 호출하십시오. 인수로는 Android 컨텍스트 및 인증 성공에
대한 확장 정보가 포함된 선택적 JSONObject가 있습니다.
```Java
void onAuthenticationSuccess(Context context, JSONObject info);
```

### onAuthenticationFailure 메소드
{: #custom-android-authlistener-onfail}
이 메소드는 인증 실패 후에 호출하십시오. 인수로는 Android 컨텍스트 및 인증 실패에
대한 확장 정보가 포함된 선택적 JSONObject가 있습니다.
```Java
void onAuthenticationFailure(Context context, JSONObject info);
```

## AuthenticationContext 인터페이스
{: #custom-android-authcontext}

`AuthenticationContext`는 사용자 정의 `AuthenticationListener`의
`onAuthenticationChallengeReceived` 메소드에 대한 인수로 제공됩니다.
사용자는 신임 정보를 수집하고 `AuthenticationContext` 메소드를 사용하여 신임 정보를
{{site.data.keyword.amashort}} 클라이언트 SDK로 리턴하거나 실패를 보고해야
합니다. 다음 메소드 중 하나를 사용하십시오. 

```Java
void submitAuthenticationChallengeAnswer(JSONObject answer);
```
```Java
void submitAuthenticationFailure (JSONObject info);
```

## 사용자 정의 AuthenticationListener의 샘플 구현
{: #custom-android-samplecustom}

이 AuthenticationListener 샘플은 사용자 정의 ID 제공자와 함께 작동하도록
설계되었습니다. 이 샘플은 [Github 저장소](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)에서
다운로드할 수 있습니다. 

```Java
package com.ibm.helloworld;
import android.content.Context;
import android.util.Log;
import com.ibm.mobilefirstplatform.clientsdk.android.security.api.AuthenticationContext;
import com.ibm.mobilefirstplatform.clientsdk.android.security.api.AuthenticationListener;
import org.json.JSONException;
import org.json.JSONObject;

public class CustomAuthenticationListener implements AuthenticationListener {

	@Override
	public void onAuthenticationChallengeReceived (AuthenticationContext authContext,
											JSONObject challenge, Context context) {

		log("onAuthenticationChallengeResceived :: " + challenge.toString());

		// In this sample the AuthenticationListener immediatelly returns a hardcoded
		// set of credentials. In a real life scenario this is where developer would
		// show a login screen, collect credentials and invoke
		// authContext.submitAuthenticationChallengeAnswer() API

		JSONObject challengeResponse = new JSONObject();
		try {
			challengeResponse.put("username", "john.lennon");
			challengeResponse.put("password", "12345");
			authContext.submitAuthenticationChallengeAnswer(challengeResponse);
		} catch (JSONException e){

			// In case there was a failure collecting credentials you need to report
			// it back to the AuthenticationContext. Otherwise Mobile Client
			// Access Client SDK will remain in a waiting-for-credentials state
			// forever

			log("This should never happen...");
			authContext.submitAuthenticationFailure(null);
		}
	}

	@Override
	public void onAuthenticationSuccess (Context context, JSONObject info) {
		log("onAuthenticationSuccess :: " + info.toString());
	}

	@Override
	public void onAuthenticationFailure (Context context, JSONObject info) {
		log("onAuthenticationFailure :: " + info.toString());
	}

	private void log(String text){
		Log.d("CustomAuthListener", text);
	}
}
```

## 사용자 정의 AuthenticationListener 등록
{: #custom-android-register}

사용자 정의 AuthenticationListener를 작성한 후 리스너를 사용하기 전에 `BMSClient`에
등록하십시오. 애플리케이션에 다음 코드를 추가하십시오. 이 코드는 보호된 자원에 대한 요청을
전송하기 전에 호출해야 합니다. 

```Java
BMSClient.getInstance().registerAuthenticationListener(realmName,
									new CustomAuthenticationListener());
```

{{site.data.keyword.amashort}} 대시보드에서 지정한 *realmName*을
사용하십시오. 


## 인증 테스트
{: #custom-android-testing}
클라이언트 SDK가 초기화되고 사용자 정의 AuthenticationListener가 등록되면
모바일 백엔드 요청을 시작할 수 있습니다. 

### 시작하기 전에
{: #custom-android-testing-before}
{{site.data.keyword.mobilefirstbp}} 표준 유형으로 작성된
애플리케이션과 `/protected` 엔드포인트에서 {{site.data.keyword.amashort}}의
보호를 받는 자원이 있어야 합니다. 


1. `{applicationRoute}/protected`(예: `http://my-mobile-backend.mybluemix.net/protected`)를 열어 브라우저에서 모바일 백엔드의 보호 엔드포인트로 요청을 전송하십시오.

1. {{site.data.keyword.mobilefirstbp}} 표준 유형으로 작성된 모바일 백엔드의
`/protected` 엔드포인트는 {{site.data.keyword.amashort}}에서 보호됩니다.
엔드포인트는 {{site.data.keyword.amashort}} 클라이언트 SDK를 갖춘 모바일 애플리케이션에서만
액세스할 수 있습니다. 따라서 `Unauthorized` 메시지는 브라우저에 표시됩니다. 

1. Android 애플리케이션을 사용하여 동일한 엔드포인트를 요청하십시오.
`BMSClient`를 초기화하고 사용자 정의 AuthenticationListener를
등록한 후 다음 코드를 추가하십시오. 

	```Java
	Request request = new Request("/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp", AuthorizationManager.getInstance().getUserIdentity().toString());
		}
		@Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
			if (null != t) {
				Log.d("Myapp", "onFailure :: " + t.getMessage());
			} else if (null != extendedInfo) {
				Log.d("Myapp", "onFailure :: " + extendedInfo.toString());
			} else {
				Log.d("Myapp", "onFailure :: " + response.getResponseText());
			}
		}
	});
```

1. 	요청이 성공하면 LogCat 도구에 다음과 같은 출력이 표시됩니다. 

	![이미지](images/android-custom-login-success.png)

1. 다음 코드를 추가하여 로그아웃 기능을 추가할 수도 있습니다. 

 ```Java
 AuthorizationManager.getInstance().logout(getApplicationContext(), listener);
 ```

 사용자가 로그인한 후에 이 코드를 호출하면 사용자가 로그아웃됩니다. 
사용자가 다시 로그인을 시도하는 경우, 사용자는 서버에서 수신된 인증 확인에 다시 응답해야 합니다. 

 로그아웃 기능에 전달된 `listener`의 값은 널일 수 있습니다. 
