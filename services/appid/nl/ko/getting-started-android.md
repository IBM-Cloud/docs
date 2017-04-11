---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:pre: .pre}

# Android SDK 설정
{: #android-sdk}

{{site.data.keyword.appid_short}} 클라이언트 SDK를 사용하여 Android 앱을 빌드하고, SDK를 초기화하고, 사용자를 인증하고, 보호 및 비보호 리소스를 요청하십시오.
{:shortdesc}


## 시작하기 전에
{: #before-you-begin}

다음 정보가 필요합니다.
  * {{site.data.keyword.appid_short_notm}} 서비스의 인스턴스.
  * 테넌트 ID.
    * 서비스 대시보드의 **서비스 신임 정보** 탭에서 **신임 정보 보기**를 클릭하십시오. 테넌트 ID가 **tenantID** 필드에 표시됩니다. 이 값은 앱을 초기화하는 데 사용됩니다.
  * {{site.data.keyword.Bluemix}} 지역. UI에서 보고 지역을 찾을 수 있습니다. 이 값은 앱을 초기화하는 데 사용됩니다.
    <table> <caption> 표 1. {{site.data.keyword.Bluemix_notm}} 지역 및 해당 SDK 값</caption>
    <tr>
      <th> Bluemix 지역 </th>
      <th> SDK 값 </th>
    </tr>
    <tr>
      <td> 미국 남부</td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> 시드니</td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> 영국</td>
      <td> AppID.REGION_UK </td>
    </tr>
  </table>

  * Gradle과 작동하도록 설정된 Android Studio 프로젝트. 
    * Android 개발 환경을 설정하는 방법에 대한 자세한 정보는 <a href="https://developers.google.com/web/tools/setup/" target="_blank">Google 개발자 도구 문서 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>을 참조하십시오. 

## 클라이언트 SDK 설치
{: #install-appid-sdk}

1. Android Studio 프로젝트를 작성하거나 기존 프로젝트를 여십시오. 
2.  루트 `build.gradle` 파일에 JitPack 저장소를 추가하십시오.

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {:pre}

3. 사용자의 애플리케이션에 대한 `build.gradle` 파일을 여십시오. 

    **참고**: 프로젝트 `build.gradle` 파일이 아니라, 반드시 사용자의 앱에 대한 파일을 여십시오.
4. 파일의 종속성 섹션을 찾아서 {{site.data.keyword.appid_short_notm}} 클라이언트 SDK에 대한 컴파일 종속성을 추가하십시오. 

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {:pre}

5. defaultConfig 섹션을 찾아서 다음의 코드 행을 추가하십시오. 

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {:pre}

6. 프로젝트를 Gradle과 동기화하십시오. **도구** > **Android** > **Gradle 파일과 프로젝트 동기화**를 클릭하십시오.

## 클라이언트 SDK 초기화
{: #initialize-client-sdk}

initialize 메소드에 컨텍스트, 테넌트 ID 및 지역 매개변수를 전달하여 클라이언트 SDK를 초기화하십시오. 필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 Android 애플리케이션에서 기본 활동의 onCreate 메소드에 있습니다. 

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {:pre}

1. "tenantId"를 {{site.data.keyword.appid_short_notm}} 서비스 tenantId로 바꾸십시오.
2. AppID.REGION_UK를 사용자의 {{site.data.keyword.Bluemix_notm}} 지역으로 바꾸십시오.


## 로그인 위젯을 사용하여 사용자 인증
{: #authenticate-login-widget}

로그인 위젯 기본 구성에서는 인증을 위해 Facebook 및 Google을 사용해야 합니다. 그 중에서 하나만 구성하는 경우에는 로그인 위젯이 실행되지 않으며 구성된 IDP 인증 화면으로 사용자가 경로 재지정됩니다. 

{{site.data.keyword.appid_short_notm}} 클라이언트 SDK가 초기화된 후에 로그인 위젯을 실행하여 사용자를 인증할 수 있습니다. 

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launch(this, new AuthorizationListener() {
        @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
        }

        @Override
        public void onAuthorizationCanceled () {
          //Authentication canceled by the user
        }

        @Override
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          //User authenticated
        }
      });
  ```
  {:pre}


## 사용자 속성 액세스
{: #accessing}

액세스 토큰을 확보할 때 사용자 보호 속성 엔드포인트에 대한 액세스 권한을 얻을 수 있습니다. 다음과 같은 API 메소드를 사용하여 액세스 권한을 얻을 수 있습니다. 

  ```java
  void setAttribute(@NonNull String name, @NonNull String value, UserAttributeResponseListener listener);
  void setAttribute(@NonNull String name, @NonNull String value, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void getAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void deleteAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void deleteAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAllAttributes(@NonNull UserAttributeResponseListener listener);
  void getAllAttributes(@NonNull AccessToken accessToken, @NonNull UserAttributeResponseListener listener);
  ```
  {:pre}

액세스 토큰이 명시적으로 전달되지 않을 때 {{site.data.keyword.appid_short_notm}}는 마지막으로 수신된 토큰을 사용합니다. 

예를 들어, 이 코드를 호출하여 새 속성을 설정하거나 기존 속성을 대체할 수 있습니다. 

  ```java
  appId.getUserAttributeManager().setAttribute(name, value, useThisToken,new UserAttributeResponseListener() {
		@Override
		public void onSuccess(JSONObject attributes) {
			//attributes received in JSON format on successful response
		}

		@Override
		public void onFailure(UserAttributesException e) {
			//Exception occurred
		}
	});
  ```
  {:pre}

### 익명 로그인
{: #anonymous notoc}

{{site.data.keyword.appid_short_notm}}를 사용하여 익명으로 로그인할 수 있습니다. [익명 사용자](/docs/services/appid/user-profile.html#anonymous)를 참조하십시오. 

  ```java
  appId.loginAnonymously(getApplicationContext(), new AuthorizationListener() {
		@Override
		public void onAuthorizationFailure(AuthorizationException exception) {
			//Exception occurred
		}

		@Override
		public void onAuthorizationCanceled() {
			//Authentication canceled by the user
		}

		@Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
			//User authenticated
		}
	});
  ```
  {:pre}

### 점진적 인증
{: #progressive notoc}

사용자가 익명 액세스 토큰을 보유하고 있는 경우 해당 토큰을 `loginWidget.launch`
메소드에 전달하여 식별된 사용자가 될 수 있습니다. 

  ```java
  void launch (@NonNull final Activity activity, @NonNull final AuthorizationListener authorizationListener, String accessTokenString);
  ```
  {:pre}

익명 로그인 후에는 서비스가 마지막으로 수신된 토큰을 사용했기 때문에 액세스 토큰을 전달하지 않고 로그인 위젯이 호출되는 경우에도 점진적 인증이 발생합니다. 저장된 토큰을 지우려면 다음 명령을 실행하십시오.

  ```java
  	appIDAuthorizationManager = new AppIDAuthorizationManager(this.appId);
  appIDAuthorizationManager.clearAuthorizationData();
  ```
  {:pre}


## 다음 단계
{: #next-steps}

{{site.data.keyword.appid_short_notm}}는 ID 제공자를 처음 설정할 때 기본 구성을 제공합니다. 개발 모드에서만 기본 구성을 사용할 수 있습니다. 애플리케이션을 공개하기 전에 기본 [Facebook](/docs/services/appid/identity-providers.html#facebook) 및 [Google](/docs/services/appid/identity-providers.html#google) 구성을 사용자 자신의 신임 정보에 업데이트하십시오.
