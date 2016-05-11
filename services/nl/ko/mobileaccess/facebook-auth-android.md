---

copyright:
  years: 2015, 2016

---

# Android 앱에서 Facebook 인증 사용
{: #facebook-auth-android}
Android 애플리케이션에서 Facebook을 ID 제공자로 사용하려면 Android 플랫폼을 추가하고 Facebook 애플리케이션용으로 구성하십시오. 

## 시작하기 전에
{: #facebook-auth-android-before}
 * {{site.data.keyword.amashort}}에서 보호하는 자원 및 {{site.data.keyword.amashort}} 클라이언트 SDK를 갖춘 Android 프로젝트가 있어야 합니다.
자세한 정보는 [{{site.data.keyword.amashort}} 시작하기](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) 및 [Android SDK 설정](https://console.{DomainName}/docs/services/mobileaccess/getting-started-android.html)을 참조하십시오.  
 * {{site.data.keyword.amashort}} 서버 SDK로 백엔드 애플리케이션을 수동으로 보호하십시오. 자세한 정보는 [자원 보호](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)를 참조하십시오. 
 * Facebook 애플리케이션 ID를 작성하십시오. 자세한 정보는 [Facebook 개발자 포털에서 Facebook 애플리케이션 ID 얻기](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)를 참조하십시오. 


## Android 플랫폼에 대해 Facebook 애플리케이션 구성
{: #facebook-auth-android-config}
Android 애플리케이션에서 Facebook을 ID 제공자로 사용하려면 Android 플랫폼을 추가하고 Facebook 애플리케이션용으로 구성해야 합니다. 

1. Facebook 개발자 포털에서 Facebook 애플리케이션을 여십시오. 

1. **설정 &gt; 플랫폼 추가 &gt; Android**를 클릭하십시오. 

1. Google Play 패키지 이름 프롬프트에서 Android 애플리케이션의 패키지 이름을 지정하십시오. Android 애플리케이션의 패키지 이름을 찾으려면 Android Studio에서 `AndroidManifest.xml` 파일을 열고 `<manifest ..... package="{your-package-name}">`을 찾으십시오.

1. **클래스 이름** 프롬프트에서 기본 활동의 클래스 이름을 지정하십시오. Android 애플리케이션의 기본 활동 클래스 이름을 찾으려면 `AndroidManifest.xml` 파일을 열고 다음 코드 스니펫과 유사한 intent 필터가 포함된 활동 선언을 찾으십시오. 

	```XML
	<activity
		android:name=".MainActivity"
		android:label="@string/app_name">
		<intent-filter>
			<action android:name="android.intent.action.MAIN"/>
			<category android:name="android.intent.category.LAUNCHER"/>
		</intent-filter>
	</activity>
	```

1. Facebook이 애플리케이션의 신뢰성을 보증할 수 있도록 개발자 인증서 SHA1의 해시를 지정해야 합니다. 

	**Android 보안에 대한 추가 정보:** Android OS에서는 개발자 인증서를 사용하여 Android 디바이스에 설치된 모든 애플리케이션에 서명해야 합니다. Android 애플리케이션은 디버그 및 릴리스라는 두 개의 모드로 빌드할 수 있습니다. <br/>
  디버그 및 릴리스 모드에 대해 서로 다른 인증서를 사용하십시오. 디버그 모드에서 Android 애플리케이션 서명에 사용되는 인증서는 Android SDK와 함께 제공되며, 보통 Android Studio에서 자동으로 설치합니다. 앱을 Google Play Store로 릴리스하려는 경우에는 일반적으로 직접 생성하는 다른 인증서로 앱에 서명해야 합니다. <br/>Facebook에서 두 세트의 키 해시를 입력할 수 있습니다. 하나는 디버그 인증서를 사용하여 디버그 모드로 빌드되는 애플리케이션용 키 해시이고, 다른 하나는 릴리스 인증서를 사용하여 릴리스 모드로 빌드되는 애플리케이션용 키 해시입니다. 자세한 정보는 [Android
애플리케이션 서명](http://developer.android.com/tools/publishing/app-signing.html)을 참조하십시오. 

1. 개발 환경용 인증서가 포함된 키 저장소는 `~/.android/debug.keystore` 파일에 저장됩니다. 기본 키 저장소 비밀번호는 `android`입니다. 애플리케이션을 디버그 모드로 빌드하려면 이 인증서를 사용하십시오. 

1. 디버그 모드 인증서의 키 해시를 검색하십시오. 

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore | openssl sha1 -binary | openssl base64
	```

	**팁**: 릴리스 모드 인증서의 키 해시를 검색하는 경우에도 동일한 구문을 사용할 수 있습니다. 명령에서 별명 및 키 저장소 경로를 대체하십시오. 

1. **keytool** 명령으로 얻은 키 해시를 복사하여 Facebook 개발자 포털의 개발/릴리스 키 해시 프롬프트에 붙여넣으십시오. 

	**팁**: 이 기능을 사용하려는 경우 Single Sign-On 사용을 고려하십시오. 

1. **설정 저장**을 클릭하십시오. 

## Facebook 인증을 사용하도록 {{site.data.keyword.amashort}} 구성
{: #facebook-auth-android-mca}
Facebook 애플리케이션 ID를 얻고 Android 클라이언트를 서비스하도록 Facebook 애플리케이션을 구성한 후에는 {{site.data.keyword.amashort}} 대시보드에서 Facebook 인증을 사용으로 설정할 수 있습니다. 

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 앱을 여십시오. 

1. **모바일 옵션**을 클릭하고 **라우트**(`applicationRoute`) 및 **앱 GUID**(`applicationGUID`)를 기록해 두십시오. SDK를 초기화하는 경우 이 값이 필요합니다. 

1. {{site.data.keyword.amashort}} 타일을 클릭하십시오. {{site.data.keyword.amashort}} 대시보드가 로드됩니다. 

1. **Facebook** 타일을 클릭하십시오.

1. Facebook 애플리케이션 ID를 지정하고 **저장**을 클릭하십시오. 

## Android에 대해 {{site.data.keyword.amashort}} 클라이언트 SDK 구성
{: #facebook-auth-android-sdk}
Android에 대해 클라이언트 SDK를 구성하려면 Android Studio에서 Gradle 종속성 관리자를 사용하십시오. 

1.  앱 모듈의 `build.gradle` 파일을 여십시오.
Android 프로젝트에는 두 개의 `build.gradle` 파일(프로젝트용 및 애플리케이션 모듈용)이 있습니다. 애플리케이션 모듈 파일을 사용하십시오. 

1. `build.gradle` 파일의 dependencies 섹션을 찾아 클라이언트 SDK에 대한 새 컴파일 종속성을 추가하십시오. 

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    
        name:'facebookauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
```

	`com.ibm.mobilefirstplatform.clientsdk.android` 그룹의 `core` 모듈이 파일에 있는 경우 이 모듈에 대한 종속성을 제거할 수 있습니다. `facebookauthentication` 모듈이 자동으로 `core` 모듈을 다운로드합니다. 

  업데이트 사항을 저장하면 `facebookauthentication` 모듈이 Facebook SDK를 다운로드하여 Android 프로젝트에 설치합니다. 


1. 프로젝트를 Gradle과 동기화하십시오. **도구 > Android > Gradle 파일과 프로젝트 동기화**를 클릭하십시오. 

1. `res/values/strings.xml` 파일을 열고 Facebook 애플리케이션 ID를 포함하는 `facebook_app_id` 문자열을 추가하십시오. 

	```XML
	<resources>
		<string name="app_name">HelloWorld</string>
		<string name="action_settings">Settings</string>
		<string name="facebook_app_id">522733366802111</string>
	</resources>
```

1. Android 프로젝트의 `AndroidManifest.xml` 파일에서 다음을 수행하십시오. 
   1. `<manifest>` 요소 아래에 인터넷 액세스 권한을 추가하십시오. 

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
```
  2. Facebook SDK에 필요한 메타데이터를 `<application>` 요소에 추가하십시오. 

	```XML
	<application .......>

		<meta-data android:name="com.facebook.sdk.ApplicationId" android:value="@string/facebook_app_id"/>

		<activity ...../>
		<activity ...../>
	</application>
```

   1. 기존 활동 아래에 Facebook 활성 요소를 추가하십시오. 

	```XML
	<application .....>
		<activity ...../>
		<activity ...../>

		<activity 	android:name="com.facebook.FacebookActivity"
					android:configChanges=
						"keyboard|keyboardHidden|screenLayout|screenSize|orientation"
					android:theme="@android:style/Theme.Translucent.NoTitleBar"
					android:label="@string/app_name" />

	</application>
```

1. 클라이언트 SDK를 초기화하고 Facebook 인증 관리자를 등록하십시오. 컨텍스트, 앱 GUID(`applicationGUID`) 및 라우트(`applicationRoute`) 매개변수를 전달하여 {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화하십시오.<br/>
 초기화 코드를 삽입하는 일반 위치(필수는 아님)는 Android 애플리케이션에서 기본 활동의 `onCreate` 메소드에 있습니다.<br/>
 *applicationRoute* 및 *applicationGUID*를 Bluemix 대시보드에서 앱의 기본 페이지에 있는 **모바일 옵션** 메뉴의 **라우트** 및 **앱 GUID** 값으로 바꾸십시오.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");

	FacebookAuthenticationManager.getInstance().register(this);```


1. 활동에 다음 코드를 추가하십시오. 

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
```

## 인증 테스트
클라이언트 SDK가 초기화되고 Facebook 인증 관리자가 등록되면 모바일 백엔드 요청을
시작할 수 있습니다. 

### 시작하기 전에
{: #facebook-auth-android-testing-before}
{{site.data.keyword.mobilefirstbp}} 표준 유형을 사용하고 있어야 하며,
`/protected` 엔드포인트에서 {{site.data.keyword.amashort}}의
보호를 받은 자원이 있어야 합니다. `/protected` 엔드포인트를 설정해야 하는 경우
[자원 보호](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)를 참조하십시오. 

1. 브라우저에서 새로 작성한 모바일 백엔드의 보호 엔드포인트로 요청을 전송해 보십시오. URL `{applicationRoute}/protected`를 여십시오. 예를 들면 `http://my-mobile-backend.mybluemix.net/protected`와 같습니다. 
<br/>MobileFirst Services Starter 표준 유형으로 작성된 모바일 백엔드의 `/protected` 엔드포인트는 {{site.data.keyword.amashort}}에서 보호됩니다. `Unauthorized` 메시지가 브라우저에 리턴됩니다. 이 엔드포인트는 {{site.data.keyword.amashort}} 클라이언트 SDK를 갖춘 모바일 애플리케이션에서만 액세스할 수 있으므로 이 메시지가 리턴됩니다.

1. Android 애플리케이션을 사용하여 동일한 엔드포인트를 요청하십시오. `BMSClient`를 초기화한 후 다음 코드를 추가하고 `FacebookAuthenticationManager`를 등록하십시오.

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

1. 애플리케이션을 실행하십시오. Facebook 로그인 화면이 표시됩니다. 

	![이미지](images/android-facebook-login.png)

	디바이스에 Facebook 앱이 설치되어 있지 않거나 현재 Facebook에 로그인하지 않은 경우 이 화면이 약간 다를 수 있습니다. 

1. **확인**을 클릭하여 {{site.data.keyword.amashort}}가 인증을 위해 Facebook 사용자 ID를 사용하도록 권한을 부여하십시오. 

1. 	요청이 성공하면 LogCat 유틸리티에 다음과 같은 출력이 표시됩니다. 

	![이미지](images/android-facebook-login-success.png)

1. 다음 코드를 추가하여 로그아웃 기능을 추가할 수도 있습니다. 

 ```
FacebookAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
 ```

 Facebook에서 사용자가 로그인한 후에 이 코드를 호출하면 사용자가 Facebook에서 로그아웃됩니다. 
다시 로그인을 시도하는 경우, 사용자에게는 자체 Facebook 신임 정보에 대한 프롬프트가 제시됩니다. 

 로그아웃 기능에 전달된 `listener`의 값은 널일 수 있습니다. 
