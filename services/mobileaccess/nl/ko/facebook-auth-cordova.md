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


# Cordova 앱에서 Facebook 인증 사용
{: #facebook-auth-cordova}

{{site.data.keyword.amafull}} Cordova 애플리케이션을 Facebook 인증 통합용으로 구성하려면 각 플랫폼을 개별적으로 구성하십시오. 이 Cordova 애플리케이션은 이미 {{site.data.keyword.amashort}} SDK로 인스트루먼트되어 있어야 합니다.

Facebook 인증을 사용하려면 원시 플랫폼 및 Cordova WebView Javascript 코드를 모두 변경해야 합니다. 

원시 개발 환경을 사용하여 원시 코드(예: Android Studio 또는 Xcode)를 변경하십시오.
{:shortdesc}

## 시작하기 전에
{: #facebook-auth-before}

다음이 있어야 합니다.
* {{site.data.keyword.amashort}} 클라이언트 SDK로 인스트루먼트된 Cordova 프로젝트(Android 또는 iOS)([Cordova 플러그인 설정](getting-started-cordova.html#getting-started-cordova-plugin) 참조).
* {{site.data.keyword.amashort}} 서비스를 통해 보호하는 {{site.data.keyword.Bluemix_notm}} 애플리케이션의 인스턴스. {{site.data.keyword.Bluemix_notm}} 백엔드 서비스 작성 방법에 대한 자세한 정보는 [시작하기](index.html)를 참조하십시오.
* 애플리케이션 라우트. 이는 백엔드 애플리케이션의 URL입니다. 
* `tenantId` 값. {{site.data.keyword.amashort}} 서비스 대시보드를 여십시오. **모바일 옵션**을 클릭하십시오. **앱 GUID / TenantId** 필드에 `tenantId`(`appGUID`라고도 함) 값이 표시됩니다. 이 값은 SDK를 초기화하고 백엔드 서비스에 요청을 보내는 데 필요합니다. 
*  {{site.data.keyword.Bluemix_notm}} 서비스가 호스트되는 지역. 헤더에서 메뉴 표시줄의 **아바타** 아이콘 ![아바타 아이콘](images/face.jpg "아바타 아이콘") 옆에 현재 {{site.data.keyword.Bluemix_notm}} 지역이 표시됩니다. 지역 값은 **미국 남부**, **시드니** 또는 **영국** 중 하나여야 합니다. 이들 이름에 해당하는 정확한 SDK 상수 값은 코드 예제에 표시되어 있습니다. 
* Facebook 애플리케이션 및 앱 ID. 자세한 정보는 [Facebook 개발자 포털에서 Facebook 앱 ID 얻기](facebook-auth-overview.html#facebook-appID)를 참조하십시오. 



## Android 플랫폼 구성
{: #facebook-auth-cordova-android}

Facebook 인증 통합을 위해 Cordova 애플리케이션의 Android 플랫폼을 구성하는 데 필요한 단계는 기본 Android 애플리케이션에 필요한 단계와 매우 유사합니다. 자세한 정보는 [Android 앱에서 Facebook 인증 사용](facebook-auth-android.html)을 참조하십시오. 다음 단계를 수행하십시오. 

* [Android 플랫폼에 대해 Facebook 애플리케이션 구성](facebook-auth-android.html#facebook-auth-android-config). 이 단계는 Facebook 개발자 사이트에서 Android 앱에 대한 Facebook 인증을 설정합니다. 
* [Facebook 인증용 MCA 구성](facebook-auth-android.html#facebook-auth-android-mca). 이 단계는 {{site.data.keyword.Bluemix}} 서버에서 {{site.data.keyword.amashort}} 서비스를 Android Facebook 인증용으로 구성합니다. 


### Android 플랫폼용 {{site.data.keyword.amashort}} Facebook 클라이언트 SDK 구성
{: #configure_android}

기본 Android 앱 프로젝트 내에서 Gradle이 {{site.data.keyword.amashort}} Facebook 클라이언트 SDK를 추가해야 합니다. 

1. Android 프로젝트 폴더에서 앱 모듈의 `build.gradle` 파일(프로젝트 `build.gradle` 파일이 **아님**)을 여십시오. 종속 항목 섹션을 찾은 다음 클라이언트 SDK에 대한 새 컴파일 종속 항목을 추가하십시오. 

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
	{: codeblock}

2. **도구 > Android > Gradle 파일과 프로젝트 동기화**를 클릭하여 프로젝트를 Gradle과 동기화하십시오.

3. `android/res/values/strings.xml` 파일을 열고 Facebook 앱 ID가 포함된 `<facebook_app_id>` 문자열을 추가하십시오. 

	```XML
	<resources>
		<string name="app_name">HelloCordova</string>
		<string name="launcher_name">@string/app_name</string>
		<string name="activity_name">@string/launcher_name</string>
		<string name="facebook_app_id">"<facebook_app_id>"</string>
	</resources>
	```
	{: codeblock}

4. Android 프로젝트의 `AndroidManifest.xml` 파일(`android/manifests/AndroidManifest.xml`)에서 다음을 수행하십시오. 

	* Facebook SDK의 필수 메타데이터를 <application> 요소에 추가하십시오. 

    ```XML
    <application .......>
    <meta-data
       android:name="com.facebook.sdk.ApplicationId"
       android:value="@string/facebook_app_id"/>

    <activity ...../>
    <activity ...../>
    </application>
    ```
    {: codeblock}

   * 기존 활동 아래에 Facebook 활성 요소를 추가하십시오. 

    ```XML
    <application .....>
        <activity ...../>
        <activity ...../>

        <activity   android:name="com.facebook.FacebookActivity"
	              android:configChanges="keyboard|keyboardHidden|screenLayout|screenSize|orientation"
	              android:theme="@android:style/Theme.Translucent.NoTitleBar"
	              android:label="@string/app_name"
        />
    </application>
    ```
    {: codeblock}

5. 활동 Java 코드에 다음을 추가하십시오.

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
	   super.onActivityResult(requestCode, resultCode, data);
	    FacebookAuthenticationManager.getInstance()
	      .onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}

### 원시 Android 코드에서 권한 관리자 초기화
{: #initialize_android}

`FacebookAuthenticationManager` API는 여전히 사용자의 원시 코드에 등록해야 합니다. `<tenantId>`를 사용하여 이 코드를 기본 활동 `onCreate` 메소드에 추가하십시오([시작하기 전에](#before-you-begin) 참조).

```
String tenantId = "<tenantId>";
MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
FacebookAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
```
{: codeblock}


## iOS 플랫폼 구성
{: #facebook-auth-cordova-ios}

Facebook 인증 통합을 위해 Cordova 애플리케이션의 iOS 플랫폼을 구성하는 데 필요한 단계는 기본 iOS Swift 애플리케이션에 필요한 단계와 유사합니다(Swift SDK에서 Objective-C 코드를 사용하기 위해 헤더 파일이 필요함). 주요한 차이점은 현재 Cordova CLI에서는 CocoaPods 종속성 관리자를 지원하지 않는다는 점입니다. {{site.data.keyword.amashort}} 클라이언트를 Facebook 인증과 통합하는 데 필요한 파일을 수동으로 추가해야 합니다. 자세한 정보는 [iOS 앱에서 Facebook 인증 사용(Swift SDK)](facebook-auth-ios-swift-sdk.html)을 참조하십시오. 다음 단계를 수행하십시오. 

* [iOS 플랫폼에 대해 Facebook 애플리케이션 구성](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-config). 이 단계는 Facebook 개발자 사이트에서 Facebook 인증을 설정합니다. 
* [Facebook 인증용 MCA 구성](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-configmca). 이 단계는 {{site.data.keyword.Bluemix}} 서버에서 {{site.data.keyword.amashort}} 서비스를 구성합니다. 
* [iOS용 MCA Facebook 클라이언트 SDK 구성](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-sdk). 이 단계는 CocoaPods를 사용하여 Facebook 권한용 {{site.data.keyword.amashort}} iOS Swift SDK를 설치합니다. 


### iOS에서 키 체인 공유 사용
{: #enable_keychain}

`키 체인 공유`를 사용 가능하게 설정하십시오. `기능` 탭으로 이동하여 Xcode 프로젝트에서 `키 체인 공유`를 `On`으로 전환하십시오. 

### Objective-C에서 {{site.data.keyword.amashort}} 권한 관리자 초기화
{: #initialize_objc}

사용하는 Xcode 버전에 따라 `app-delegate.m` 파일의 원시 Objective-C 코드에서 권한 관리자를 초기화해야 합니다. 

```
	#import "<your_module_name>-Swift.h"

	- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

	{

	    [CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];

	    [[FacebookAuthenticationManager sharedInstance] register];

	    self.viewController = [[MainViewController alloc] init];

	    [[FacebookAuthenticationManager sharedInstance] onFinishLaunchingWithApplication:application withOptions:launchOptions];


	    return [super application:application didFinishLaunchingWithOptions:launchOptions];
	}


	- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(NSString *)sourceApplication
			annotation:(id)annotation
	{

	   return [[FacebookAuthenticationManager sharedInstance] onOpenURLWithApplication:application
	   		url:url sourceApplication:sourceApplication annotation:annotation];
	}

```
{: codeblock}

**참고:** 가져오는 헤더 파일 이름은 모듈 이름과 `-Swift.h` 문자열로 구성됩니다. 예를 들어, 모듈 이름이 `Cordova`이면 import 행은 `#import "Cordova-Swift.h"`가 됩니다. 모듈 이름을 찾으려면
`빌드 설정` > `패키징` > `제품 모듈 이름`으로 이동하십시오. 

`<tenantId>`를 사용하는 테넌트 ID로 대체하십시오([시작하기 전에](#facebook-auth-before) 참조).


##Cordova WebView에서 {{site.data.keyword.amashort}} 클라이언트 SDK 초기화
{: #initialize_webview}

모든 플랫폼의 경우, Cordova Javascript WebView에서 다음 JavaScript 코드를 사용하여 {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화하십시오. 

```javascript
BMSClient.initialize(<applicationBluemixRegion>);
```
{: codeblock}

`<applicationBluemixRegion>`을 해당 지역으로 대체하십시오([시작하기 전에](#facebook-auth-before) 참조).

## 인증 테스트
{: #facebook-auth-cordova-test}

클라이언트 SDK가 초기화되고 Facebook 인증 관리자가 등록되면 모바일 백엔드 서비스에 대한 요청을 시작할 수 있습니다. 

### 시작하기 전에
{: #testing_auth_before}

{{site.data.keyword.mobilefirstbp}} 표준 유형을 사용 중 이어야 하며, `/protected` 엔드포인트에서 {{site.data.keyword.amashort}}의 보호를 받은 리소스가 있어야 합니다. 자세한 정보는 [리소스 보호](protecting-resources.html)를 참조하십시오. 

1. 브라우저에서 모바일 백엔드 애플리케이션의 보호 엔드포인트로 요청을 전송하십시오. URL `{applicationRoute}/protected`를 여십시오. 예를 들면, `http://my-mobile-backend.mybluemix.net/protected`입니다. 

	`/protected` 엔드포인트 값은 MobileFirst Services Starter 표준 유형으로 작성된 모바일 백엔드 서비스의 보호 엔드포인트여야 하며 {{site.data.keyword.amashort}}로 보호됩니다. `Unauthorized` 메시지가 브라우저에 리턴됩니다. 이 엔드포인트는 {{site.data.keyword.amashort}} 클라이언트 SDK로 인스트루먼트된 모바일 애플리케이션에서만 액세스될 수 있으므로 이 메시지가 리턴됩니다.

1. Cordova 애플리케이션을 사용하여 동일한 엔드포인트를 요청하십시오. `BMSClient`를 초기화한 후에 다음 코드를 추가하십시오. 

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error){
    	console.log("failure", error);
    }
	var request = new BMSRequest("<applicationRoute}/protected>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}

1. 애플리케이션을 실행하십시오. Facebook 로그인 화면이 팝업됩니다. 

	![image](images/android-facebook-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![image](images/ios-facebook-login.png)

	디바이스에 Facebook 앱이 설치되어 있지 않거나 현재 Facebook에 로그인하지 않은 경우 이 화면이 약간 다를 수 있습니다. 

1. **확인**을 클릭하여 {{site.data.keyword.amashort}}가 인증을 위해 Facebook 사용자 ID를 사용하도록 권한을 부여하십시오. 

1. 	요청이 성공하면 LogCat 유틸리티 또는 Xcode 콘솔에 다음과 같은 출력이 표시됩니다.

	![Android용 Facebook 인증 성공 메시지](images/android-facebook-login-success.png)

	![iOS용 Facebook 인증 성공 메시지](images/ios-facebook-login-success.png)
