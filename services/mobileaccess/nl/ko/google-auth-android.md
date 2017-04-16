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

# Android 앱에서 Google 인증 사용
{: #google-auth-android}

Google을 사용하여 {{site.data.keyword.amafull}} Android 애플리케이션에서 사용자를 인증하십시오.{{site.data.keyword.amashort}} 보안 기능을 추가하십시오.

## 시작하기 전에
{: #before-you-begin}

다음이 있어야 합니다.

* {{site.data.keyword.Bluemix_notm}} 애플리케이션 및 {{site.data.keyword.amafull}} 서비스의 인스턴스. {{site.data.keyword.Bluemix_notm}} 백엔드 애플리케이션 작성 방법에 대한 자세한 정보는 [시작하기](index.html)를 참조하십시오. 
* 백엔드 애플리케이션의 URL(**앱 라우트**). 이 값은 백엔드 애플리케이션의 보호 엔드포인트에 요청을 전송하는 데 필요합니다. 
* **테넌트 ID** 값. {{site.data.keyword.amashort}} 대시보드에서 서비스를 여십시오. **모바일 옵션** 단추를 클릭하십시오. **앱 GUID / TenantId** 필드에 `tenantId`(`appGUID`라고도 함) 값이 표시됩니다. 이 값은 권한 관리자를 초기화하는 데 필요합니다. 
* {{site.data.keyword.Bluemix_notm}} **지역**. 헤더에서 **아바타** 아이콘 ![아바타 아이콘](images/face.jpg "아바타 아이콘") 옆에 현재 {{site.data.keyword.Bluemix_notm}} 지역이 표시됩니다. 표시되는 지역 값은 `US South`, `United Kingdom` 및 `Sydney` 중 하나여야 하며 WebView Javascript 코드 `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` 또는 `BMSClient.REGION_UK`에 필요한 SDK 값에 해당해야 합니다. 이 값은 {{site.data.keyword.amashort}} 클라이언트를 초기화하는 데 필요합니다. 
* Gradle과 작동하도록 구성된 Android 프로젝트. 이 프로젝트는 {{site.data.keyword.amashort}} 클라이언트 SDK로 인스트루먼트되지 않아도 됩니다.  

{{site.data.keyword.amashort}} Android 앱에 맞게 Google 인증을 설정하려면 추가로 다음을 구성해야 합니다.

* {{site.data.keyword.Bluemix_notm}} 애플리케이션
* Android Studio 프로젝트

## Google 개발자 콘솔에서 프로젝트 작성
{: #create-google-project}

ID 제공자로서 Google 사용을 시작하려면 [Google 개발자 콘솔 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.developers.google.com "외부 링크 아이콘"){: new_window}에서 프로젝트를 작성하십시오.
프로젝트 작성의 일부로 Google 클라이언트 ID를 확보해야 합니다. Google 클라이언트 ID는 Google 인증에서 사용하는 애플리케이션의 고유 ID이며 {{site.data.keyword.amashort}} 서비스를 설정하는 데 필요합니다. 

콘솔에서 다음을 수행하십시오.

1. **Google+** API를 사용하여 프로젝트를 작성하십시오.
2. **OAuth** 사용자 액세스를 추가하십시오.
3. 신임 정보를 추가하기 전에 플랫폼을 선택하십시오(Android).
4. 신임 정보를 추가하십시오. 

신임 정보 작성을 완료하려면 **서명 인증 지문**을 추가해야 합니다.


### 서명 인증서 설정
{: #signing_cert}

Google의 경우 애플리케이션 신뢰성을 확인하려면 서명 인증 지문을 지정해야 합니다. 

Android OS에서는 Android 디바이스에 설치된 모든 애플리케이션을 개발자 인증서로 서명해야 합니다. Android 애플리케이션은 디버그 모드 및 릴리스 모드로 빌드할 수 있습니다. 일반적으로 디버그 및 릴리스 모드에 대해 각기 다른 인증서를 포함하는 것이 좋습니다. 디버그 모드로 Android 애플리케이션을 서명하는 데 사용되는 인증서는 Android SDK와 함께 번들로 포함됩니다. Android SDK는 보통 Android Studio에서 자동으로 설치합니다. 애플리케이션을 Google Play에 릴리스하려는 경우 일반적으로 직접 생성하는 다른 인증서로 앱에 서명해야 합니다. 자세한 정보는 [Android 애플리케이션 서명 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://developer.android.com/tools/publishing/app-signing.html "외부 링크 아이콘"){: new_window}을 참조하십시오. 

개발 환경에 대한 인증서를 포함하는 키 저장소는 `~/.android/debug.keystore` 파일에 저장됩니다. 기본 키 저장소 비밀번호는 `android`입니다. 이 인증서는 디버그 모드로 애플리케이션을 빌드하는 데 사용됩니다. 

1. 클라이언트 개발 환경에서 서명 인증 지문을 검색하십시오.

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore -list -v
	```
	{: codeblock}

	릴리스 모드 인증서의 키 해시를 검색하는 데에도 동일한 구문을 사용할 수 있습니다. 명령에서 별명 및 키 저장소 경로를 대체하십시오. 

1. Google 콘솔 신임 정보 대화 상자에서 **인증 지문** 아래 `SHA1`로 시작하는 행을 찾으십시오. **keytool** 명령을 실행하여 확보한 지문 값을 텍스트 상자에 복사하십시오.

### 패키지 이름

1. 신임 정보 대화 상자에서 Android 애플리케이션의 패키지 이름을 입력하십시오.

	Android 애플리케이션의 패키지 이름을 찾으려면 Android Studio에서 `AndroidManifest.xml` 파일을 열고 다음을 찾으십시오. 

	```
	<manifest package="{your-package-name}">
	```
	{: codeblock}

1. 완료되면 **작성**을 클릭하십시오. 신임 정보 작성이 완료됩니다. 

### Google 클라이언트 ID
{: #google-client-id}

신임 정보 작성을 완료하면 신임 정보 페이지에 Google 클라이언트 ID가 표시됩니다. 이 값을 기록하십시오. {{site.data.keyword.Bluemix}} 애플리케이션에서 이 값을 등록해야 합니다.


## Google 인증용 {{site.data.keyword.amashort}} 구성
{: #google-auth-android-config}

Android용 Google 클라이언트 ID가 있으므로 {{site.data.keyword.amashort}} 대시보드에서 Google 인증을 사용하도록 설정할 수 있습니다.

1. {{site.data.keyword.amashort}} 대시보드에서 서비스를 여십시오. 
1. **관리** 탭에서 **권한**을 토글하여 켜십시오. 
1. **Google** 섹션을 펼치십시오. 
1. **Android용 클라이언트 ID**에서 Android용 Google 클라이언트 ID를 지정하고 **저장**을 클릭하십시오.

## Android용 {{site.data.keyword.amashort}} 클라이언트 SDK 구성
{: #google-auth-android-sdk}

Android Studio 프로젝트에서 다음을 수행하십시오. 

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
	{: codeblock}

	**참고:** `com.ibm.mobilefirstplatform.clientsdk.android` 그룹의 `core` 모듈이 있는 경우 해당 모듈의 종속 항목을 제거할 수 있습니다. `googleauthentication` 모듈이 자동으로 다운로드합니다. `googleauthentication` 모듈이 Android 프로젝트에서 Google+ SDK를 다운로드하고 설치합니다. 

1. **도구 > Android > Gradle 파일로 프로젝트 동기화**를 클릭하여 프로젝트를 Gradle과 동기화하십시오. 

1. Android 프로젝트의 `AndroidManifest.xml` 파일을 여십시오. 

1. `<manifest>` 요소 아래 인터넷 액세스 권한을 추가하십시오. 

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	```
	{: codeblock}

1. {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하려면 **context** 매개변수와 **region** 매개변수를 전달하여 해당 클라이언트 SDK를 초기화해야 합니다. 

	필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 Android 애플리케이션 기본 활동의 `onCreate` 메소드입니다. 

1. 클라이언트 SDK를 초기화하고 Google 인증 관리자를 등록하십시오. 

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

	BMSClient.getInstance().setAuthorizationManager(
		MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));

	GoogleAuthenticationManager.getInstance().register(this);
	```
	{: codeblock}

	* `BMSClient.REGION_UK`를 해당 {{site.data.keyword.Bluemix_notm}} **지역**으로 대체하십시오.
	* `<MCAServiceTenantId>`를 **TenantId** 값으로 대체하십시오. 

	이러한 값을 얻는 방법에 대한 자세한 정보는 [시작하기 전에](##before-you-begin)를 참조하십시오. 

	**참고:** Android 애플리케이션이 Android 버전 6.0(API 레벨 23) 이상을 대상으로 하는 경우, `register`를 호출하기 전에 애플리케이션에 `android.permission.GET_ACCOUNTS` 호출이 있는지 확인해야 합니다. 자세한 정보는 [Android에서 권한 요청 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.android.com/training/permissions/requesting.html "외부 링크 아이콘"){: new_window}을 참조하십시오. 

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

## 인증 테스트
{: #google-auth-android-test}

클라이언트 SDK가 초기화되고 Google 인증 관리자가 등록되면 백엔드 애플리케이션에 대한 요청을 작성할 수 있습니다.

테스트를 시작하기 전에, **MobileFirst Services Starter** 표준 유형으로 작성된 모바일 백엔드 애플리케이션이 있어야 하며 {{site.data.keyword.amashort}} `/protected` 엔드포인트에서 보호되는 리소스가 이미 있어야 합니다. 자세한 정보는 [리소스 보호](protecting-resources.html)를 참조하십시오. 

1. `{applicationRoute}/protected`(예: `http://my-mobile-backend.mybluemix.net/protected`)를 열어 데스크탑 브라우저에서 모바일 백엔드 애플리케이션의 보호 엔드포인트로 요청을 전송하십시오. `{applicationRoute}` 값을 얻는 방법에 대한 정보는 [시작하기 전에](#before-you-begin)를 참조하십시오. 

	MobileFirst 서비스 표준 유형으로 작성된 모바일 백엔드 애플리케이션의 `/protected` 엔드포인트는 {{site.data.keyword.amashort}}로 보호됩니다. 따라서 {{site.data.keyword.amashort}} 클라이언트 SDK로 인스트루먼트된 모바일 애플리케이션에서만 해당 엔드포인트에 액세스할 수 있습니다. 결과적으로 데스크탑 브라우저에 `권한 없음`이 표시됩니다. 

1. Android 애플리케이션을 사용하여 동일한 보호 엔드포인트에 요청하십시오. `BMSClient` 인스턴스를 초기화하고 `GoogleAuthenticationManager`를 등록한 후에 다음 코드를 추가하십시오. 

	```Java
	Request request = new Request("{applicationRoute}/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp", MCAAuthorizationManager.getInstance().getUserIdentity().toString());
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
	{: codeblock}

1. 애플리케이션을 실행하십시오. Google 로그인 화면이 팝업됩니다. 로그인 후에는 앱에서 리소스에 액세스하려고 권한을 요청합니다.

	![이미지](images/android-google-login.png)

	Android 디바이스에 따라, 그리고 현재 Google에 로그인되어 있는지에 따라, 다른 UI를 가질 수 있습니다. 

	**확인**을 클릭하여, 인증하는 데 Google 사용자 ID를 사용할 수 있도록 {{site.data.keyword.amashort}}에 권한을 부여합니다.

1. 	요청에 성공하면 LogCat 도구에서 다음 출력을 확인할 수 있습니다.

	![이미지](images/android-google-login-success.png)

	다음 코드를 추가하여 로그아웃 기능을 추가할 수도 있습니다. 

	```Java
	GoogleAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
	```
	{: codeblock}

	Google에서 사용자가 로그인한 후에 이 코드를 호출하면 사용자가 Google에서 로그아웃됩니다. 사용자가 로그인을 다시 시도하는 경우, 다시 로그인하기 위해 Google 계정을 선택해야 합니다. 이전에 로그인한 Google ID로 로그인을 시도하는 경우, 사용자에게는 다시 해당 신임 정보에 대한 프롬프트가 제시되지 않습니다. 다시 로그인 신임 정보에 대한 프롬프트를 받으려면, 사용자가 Android 디바이스에서 해당 Google 계정을 제거해야 합니다. 

	로그아웃 기능에 전달된 `listener` 값은 `null`일 수 있습니다.
