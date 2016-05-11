---

copyright:
  years: 2015, 2016

---

# Android 앱에서 Google 인증 사용
{: #google-auth-android}

## 시작하기 전에
{: #before-you-begin}

* {{site.data.keyword.amashort}}에서 보호하는 자원 및 {{site.data.keyword.amashort}} 클라이언트 SDK로 계측되는 Android 프로젝트가 있어야 합니다. 자세한 정보는 [{{site.data.keyword.amashort}} 시작하기](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) 및 [Android SDK 설정](https://console.{DomainName}/docs/services/mobileaccess/getting-started-android.html)을 참조하십시오.  
* {{site.data.keyword.amashort}} 서버 SDK를 사용하여 백엔드 애플리케이션을 수동으로 보호하십시오. 자세한 정보는 [자원 보호](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)를 참조하십시오. 

## Android 플랫폼에 대한 Google 프로젝트 구성
{: #google-auth-android-project}
ID 제공자로 Google 사용을 시작하려면 Google 개발자 콘솔에서 프로젝트를 작성하십시오. 프로젝트 작성의 일부는 Google 클라이언트 ID를 확보하는 것입니다. 
Google 클라이언트 ID는 Google 인증에서 사용하는 애플리케이션의 고유 ID입니다. 

1. [Google 개발자 콘솔](https://console.developers.google.com)에서 프로젝트를 작성하십시오.
이미 프로젝트가 있는 경우 프로젝트 작성에 대해 설명하는 단계를 건너뛰고 신임 정보 추가를 시작할 수 있습니다. 
   1.    새 프로젝트 메뉴를 여십시오.  
         
         ![이미지](images/FindProject.jpg)

   2.    **프로젝트 작성**을 클릭하십시오. 
   
         ![이미지](images/CreateAProject.jpg)


   1. **소셜 API** 목록에서 **Google+ API**를 선택하십시오. 

     ![이미지](images/chooseGooglePlus.jpg)

   1. 다음 화면에서 **사용**을 클릭하십시오. 

1. **동의 화면** 탭을 선택하고 사용자에게 표시된 제품 이름을 제공하십시오. 기타 값은 선택사항입니다. **저장**을 클릭하십시오.

    ![이미지](images/consentScreen.png)
    
1. **신임 정보** 목록에서 OAuth 클라이언트 ID를 선택하십시오. 

     ![이미지](images/chooseCredentials.png)
     


1. 애플리케이션 유형을 선택하십시오. **Android**를 클릭하십시오. Android 클라이언트에 대한 의미있는 이름을 지정하십시오. 

1. Google의 경우 애플리케이션 신뢰성을 확인하려면 서명 인증서 지문을 지정해야 합니다. 

	 **Android 보안에 대해 자세히 알아보기:** Android OS는 Android 디바이스에 설치되어 있는 모든 애플리케이션이 개발자 인증서로 서명되어야 합니다. Android 애플리케이션은 디버그 모드 및 릴리스 모드로 빌드할 수 있습니다. 일반적으로 디버그 및 릴리스 모드에 대해 각기 다른 인증서를 포함하는 것이 좋습니다. 디버그 모드로 Android 애플리케이션을 서명하는 데 사용되는 인증서는 Android SDK와 함께 번들로 포함됩니다. Android SDK는 보통 Android Studio에서 자동으로 설치합니다. 애플리케이션을 Google Play에 릴리스하려는 경우 일반적으로 직접 생성하는 다른 인증서로 앱에 서명해야 합니다. 자세한 정보는 [Android 애플리케이션 서명](http://developer.android.com/tools/publishing/app-signing.html)을 참조하십시오. 

1. 개발 환경에 대한 인증서를 포함하는 키 저장소는 `~/.android/debug.keystore` 파일에 저장됩니다. 기본 키 저장소 비밀번호는 `android`입니다. 이 인증서는 디버그 모드로 애플리케이션을 빌드하는 데 사용됩니다. 

     1. 서명 인증 지문 검색: 

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore -list -v
	```
	릴리스 모드 인증서의 키 해시를 검색하는 데에도 동일한 구문을 사용할 수 있습니다. 명령에서 별명 및 키 저장소 경로를 대체하십시오. 

1. **Certificate Fingerprints** 아래에서 `SHA1`로 시작하는 행을 찾으십시오. **keytool** 명령을 실행하여 확보된 지문을 Google 개발자 콘솔에 복사하십시오. 

1. Android 애플리케이션의 패키지 이름을 지정하십시오. Android 애플리케이션의 패키지 이름을 찾으려면 Android Studio에서 `AndroidManifest.xml` 파일을 열고 `<manifest package="{your-package-name}">`을 검색하십시오. 완료되면 **작성**을 클릭하십시오. 

사용자의 Google 클라이언트 id를 표시하는 대화 상자가 표시됩니다. 이 값을 기록하십시오. 
{{site.data.keyword.Bluemix}}에서 이 값을 등록해야 합니다. 


## Google 인증을 위해 {{site.data.keyword.amashort}} 구성
{: #google-auth-android-config}

이제 Android용 Google 클라이언트 ID를 보유 중이므로 {{site.data.keyword.amashort}} 대시보드에서 Google 인증을 사용할 수 있습니다. 

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 앱을 여십시오. 

1. **모바일 옵션**을 클릭하고 **라우트**(`applicationRoute`) 및 **앱 GUID**(`applicationGUID`)를 기록해 두십시오. SDK를 초기화하는 경우 이 값이 필요합니다. 

1. {{site.data.keyword.amashort}} 타일을 클릭하십시오. {{site.data.keyword.amashort}} 대시보드가 로드됩니다. 

1. **Google** 타일을 클릭하십시오.

1. **Android용 애플리케이션 ID**에서 Android용 Google 클라이언트 ID를 지정하고 **저장**을 클릭하십시오. 

## Android용 {{site.data.keyword.amashort}} 클라이언트 SDK 구성
{: #google-auth-android-sdk}

1. Android Studio로 돌아가십시오. 

1. 앱 모듈의 `build.gradle` 파일을 여십시오. 

	Android 프로젝트에 두 개의 `build.gradle` 파일이 있을 수 있습니다. 하나는 프로젝트용이고 다른 하나는 애플리케이션 모듈용입니다. 애플리케이션 모듈을 사용하십시오. 

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

	`com.ibm.mobilefirstplatform.clientsdk.android` 그룹의 `core` 모듈이 있는 경우 해당 모듈의 종속 항목을 제거할 수 있습니다. `googleauthentication` 모듈이 자동으로 다운로드합니다. `googleauthentication` 모듈이 Google SDK를 다운로드하고 Android 프로젝트에 설치합니다. 

1. **도구 > Android > Gradle 파일로 프로젝트 동기화**를 클릭하여 프로젝트를 Gradle과 동기화하십시오. 

1. Android 프로젝트의 `AndroidManifest.xml` 파일을 여십시오. 

1. `<manifest>` 요소 아래 인터넷 액세스 권한을 추가하십시오. 

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.GET_ACCOUNTS" />
<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	```

1. {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하려면, 컨텍스트, applicationGUID 및 applicationRoute 매개변수를 전달하여 초기화해야 합니다. 

	필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 Android 애플리케이션의 기본 활동의 onCreate 메소드입니다. 

1. 클라이언트 SDK를 초기화하고 Google 인증 관리자를 등록하십시오. *applicationRoute* 및 *applicationGUID*를 대시보드의 **모바일 옵션** 섹션에 있는 **라우트** 및 **앱 GUID** 값으로 바꾸십시오.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");

	GoogleAuthenticationManager.getInstance().register(this);```

1. 다음 코드를 활동에 추가하십시오. 

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		GoogleAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```

## 인증 테스트
{: #google-auth-android-test}
클라이언트 SDK가 초기화되고 Google 인증 관리자가 등록되면 모바일 백엔드에 대한 요청 작성을 시작할 수 있습니다. 

### 시작하기 전에
{: #google-auth-android-testing-before}
MobileFirst Services Starter 표준 유형으로 작성된 모바일 백엔드가 있어야 하며 이미 `/protected` 엔드포인트에 {{site.data.keyword.amashort}}가 보호하는 자원이 있어야 합니다. 자세한 정보는 [자원 보호](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)를 참조하십시오. 

1. `{applicationRoute}/protected`(예: `http://my-mobile-backend.mybluemix.net/protected`)를 열어 데스크탑 브라우저에서 모바일 백엔드의 보호 엔드포인트로 요청을
전송하십시오. MobileFirst 서비스 표준 유형으로 작성된 모바일 백엔드의 `/protected` 엔드포인트는 {{site.data.keyword.amashort}}로 보호됩니다. 따라서, {{site.data.keyword.amashort}} 클라이언트 SDK로 계측되는 모바일 애플리케이션만 액세스할 수 있습니다. 결과적으로 데스크탑 브라우저에 `권한 없음`이 표시됩니다. 

1. Android 애플리케이션을 사용하여 동일한 엔드포인트에 대해 요청을 작성하십시오. `BMSClient` 인스턴스를 초기화하고 `GoogleAuthenticationManager`를 등록한 후에 다음 코드를 추가하십시오. 

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

1. 애플리케이션을 실행하십시오. Google 로그인 화면이 팝업됩니다. 로그인 후에는 앱에서 자원에 액세스하려고 권한을 요청합니다. 

	![이미지](images/android-google-login.png)

	Android 디바이스에 따라 그리고 현재 Google에 로그인되어 있는지에 따라 다른 UI를 가질 수 있습니다. 

  **확인**을 클릭하여 인증하도록 {{site.data.keyword.amashort}}에 Google 사용자 ID를 사용할 수 있는 권한을 부여합니다. 

1. 	요청에 성공하면 LogCat 도구에서 다음 출력을 확인할 수 있습니다. 

	![이미지](images/android-google-login-success.png)

1. 다음 코드를 추가하여 로그아웃 기능을 추가할 수도 있습니다. 

 ```Java
 GoogleAuthenticationManager.getInstance().logout(getApplicationContext(),, listener);
 ```

 Google에서 사용자가 로그인한 후에 이 코드를 호출하면 사용자가 Google에서 로그아웃됩니다. 
사용자가 다시 로그인을 시도하는 경우 다시 로그인되는 Google 계정을 선택해야 합니다. 
이전에 로그인한 Google ID로 로그인을 시도하는 경우, 사용자에게는 다시 해당 신임 정보에 대한 프롬프트가 제시되지 않습니다. 
다시 로그인 신임 정보에 대한 프롬프트를 받으려면, 사용자가 Android 디바이스에서 해당 Google 계정을 제거해야 합니다. 

 로그아웃 기능에 전달된 `listener`의 값은 널일 수 있습니다. 
