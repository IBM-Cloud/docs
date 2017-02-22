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


# Cordova 플러그인 설정
{: #getting-started-cordova}

{{site.data.keyword.amafull}} 클라이언트 SDK로 Cordova 클라이언트 애플리케이션을 인스트루먼트하십시오. Android(Java) 또는 iOS 코드(관련 헤더 파일 및 Swift SDK를 사용하는 Objective C)에서 권한 관리자를 초기화하십시오. 클라이언트를 초기화하고 WebView에서 보호 및 비보호 리소스에 대한 요청을 작성하십시오. 

{:shortdesc}

## 시작하기 전에
{: #before-you-begin}
다음이 있어야 합니다.

* {{site.data.keyword.Bluemix_notm}} 애플리케이션의 인스턴스. {{site.data.keyword.Bluemix_notm}} 백엔드 애플리케이션 작성 방법에 대한 자세한 정보는 [시작하기](index.html)를 참조하십시오.
* {{site.data.keyword.amafull}} 서비스의 인스턴스
* 백엔드 애플리케이션의 URL(**앱 라우트**). 이 값은 백엔드 애플리케이션의 보호 엔드포인트에 요청을 전송하는 데 필요합니다. 
* **테넌트 ID** 값. {{site.data.keyword.amashort}} 대시보드에서 서비스를 여십시오. **모바일 옵션** 단추를 클릭하십시오. **앱 GUID / TenantId** 필드에 `tenantId`(`appGUID`라고도 함) 값이 표시됩니다. 이 값은 권한 관리자를 초기화하는 데 필요합니다. 
* {{site.data.keyword.Bluemix_notm}} **지역**. 헤더에서 **아바타** 아이콘 ![아바타 아이콘](images/face.jpg "아바타 아이콘") 옆에 현재 {{site.data.keyword.Bluemix_notm}} 지역이 표시됩니다. 표시되는 지역 값은 `US South`, `United Kingdom` 및 `Sydney` 중 하나여야 하며 WebView Javascript 코드 `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` 또는 `BMSClient.REGION_UK`에 필요한 SDK 값에 해당해야 합니다. 이 값은 {{site.data.keyword.amashort}} 클라이언트를 초기화하는 데 필요합니다. 
* Cordova 애플리케이션 또는 기존 프로젝트. Cordova 애플리케이션을 설정하는 방법에 대한 자세한 정보는 [Cordova 웹 사이트 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cordova.apache.org/){: new_window}를 참조하십시오. 

## {{site.data.keyword.amashort}} Cordova 플러그인 설치
{: #getting-started-cordova-plugin}

Cordova용 {{site.data.keyword.amashort}} 클라이언트 SDK는 원시 {{site.data.keyword.amashort}} 클라이언트 SDK를 랩핑하는 Cordova 플러그인입니다. Cordova CLI(Command Line Interface) 및 `npmjs`, Cordova 프로젝트에 대한 플러그인 저장소를 사용하여 분배됩니다. Cordova CLI는 저장소에서 자동으로 플러그인을 다운로드하고 Cordova 애플리케이션에서 플러그인을 사용할 수 있게 합니다. 

1. Android 및/또는 iOS 플랫폼을 Cordova 애플리케이션에 추가하십시오. 명령행에서 다음 명령 중 하나 또는 둘 다 실행하십시오. 

	###Android
	{: #install-cordova-android}

	```
	cordova platform add android
	```
	{: codeblock}

	###iOS
	{: #install-cordova-ios}

	```Bash
	cordova platform add ios
	```
	{: codeblock}

2. Android 플랫폼을 추가한 경우 지원되는 최소 API를 Cordova 애플리케이션의 `config.xml` 파일에 추가해야 합니다. `config.xml` 파일을 열고 `<platform name="android">` 요소에 다음 행을 추가하십시오. 

	```XML
	<platform name="android">  
		<preference name="android-minSdkVersion" value="15"/>
		<preference name="android-targetSdkVersion" value="23"/>
		<!-- add minimum and target Android API level declaration -->
	</platform>
	```
	{: codeblock}

	*minSdkVersion* 값은 `15` 이상이어야 합니다. Android SDK용으로 지원되는 *targetSdkVersion*의 최신 상태를 유지하려면 [Android 플랫폼 안내서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cordova.apache.org/docs/en/latest/guide/platforms/android/){: new_window}를 참조하십시오. 

3. iOS 운영 체제를 추가한 경우 `<platform name="ios">` 요소를 대상 선언으로 업데이트하십시오. 

	```XML
 	  <platform name="ios">
		<preference name="deployment-target" value="8.0"/>
		<!-- add deployment target declaration -->
	 </platform>
	```
	{: codeblock}

4. {{site.data.keyword.amashort}} Cordova 플러그인을 설치하십시오. 

 	```Bash
	cordova plugin add bms-core
	```
	{: codeblock}

5. Android, iOS 또는 둘 다에 대해 플랫폼을 구성하십시오. 

	####Android
	{: #cordova-android}

	Android Studio에서 프로젝트를 열기 전에 빌드 오류를 방지하기 위해 명령행 인터페이스(CLI)를 통해 Cordova 애플리케이션을 빌드하십시오.

	```Bash
	cordova build android
	```
	{: codeblock}

	####iOS
	{: #cordova-ios}

	다음과 같이 Xcode 프로젝트를 구성하십시오. 

	1. 최신 Xcode 버전을 사용하여 `<app_name>/platforms/ios` 디렉토리에서 `xcode.proj` 파일을 여십시오. 

		**중요:** 최신 Swift 구문으로 변환하라는 메시지를 수신하는 경우 **취소**를 클릭하십시오. 

	2. Xcode로 애플리케이션을 빌드하고 실행하십시오.

	**참고**: `cordova build ios`를 실행할 때 다음 오류가 수신될 수 있습니다. 이 문제는 [문제 12 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/blakgeek/cordova-plugin-cocoapods-support/issues/12 "외부 링크 아이콘"){: new_window}에서 추적 중인 종속성 플러그인의 버그 때문에 발생합니다. 시뮬레이터 또는 디바이스를 통해 XCode에서 iOS 프로젝트를 계속 실행할 수 있습니다. 

	```
	xcodebuild: error: Unable to find a destination matching the provided destination specifier:
			{ platform:iOS Simulator }

		Missing required device specifier option.
		The device type “iOS Simulator” requires that either “name” or “id” be specified.
		Please supply either “name” or “id”.
	```

6. 다음 명령을 실행하여 플러그인이 설치되었는지 확인하십시오. 

	```Bash
	cordova plugin list
	```
	{: codeblock}

7. **기능** 탭에서 **키 체인 공유**를 `On`으로 전환하여 iOS에 대해 키 체인 공유를 사용 가능하게 설정하십시오. 

8. **빌드 설정** > **패키징** 탭에서 **모듈 정의**를 `YES`로 전환하여 iOS에 대해 **모듈 정의**를 사용 가능하게 설정하십시오. 


## Cordova WebView(Javascript)에서 {{site.data.keyword.amashort}} 클라이언트 초기화
{: #getting-started-cordova-initialize}

{{site.data.keyword.amashort}} 클라이언트 SDK를 사용하려면 `applicationBluemixRegion`을 전달하여 SDK를 초기화해야 합니다. 

다음 호출을 `index.js` 파일에 추가하여 {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화하십시오. 

```JavaScript
BMSClient.initialize(<applicationBluemixRegion>);
```
{: codeblock}

**NB:** `<applicationBluemixRegion>`을 {{site.data.keyword.Bluemix_notm}} 서비스가 호스트되는 지역으로 대체하십시오([시작하기 전에](#before-you-begin) 참조).

##원시 코드에서 {{site.data.keyword.amashort}} 권한 관리자 초기화
{: #initializing-auth-manager}

`BMSAuthorizationManager`를 사용하려면 다음 코드 스니펫을 추가해야 합니다. 다음 원시 코드는 `BMSAuthorizationManager`를 {{site.data.keyword.amashort}} 서비스 `tenantId`로 초기화합니다([시작하기 전에](#before-you-begin) 참조).

### Android(Java)

`MainActivity.java` 파일의 `OnCreate` 메소드에서 `loadUrl` 앞에 코드를 추가하십시오.
```Java
MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),"<tenantId>");
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
```
{: codeblock}
### iOS(Objective C)
사용하는 Xcode의 버전에 따라 `AppDelegate.m`에서 권한 관리자 초기화를 추가하십시오. 

```Objective-C
  #import "<your_module_name>-Swift.h"
  [CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];
```
{: codeblock}

**참고:** 가져오는 헤더 파일 이름은 모듈 이름과 `-Swift.h` 문자열로 구성됩니다. 예를 들어, 모듈 이름이 `Cordova`이면 import 행은 `#import "Cordova-Swift.h"`가 됩니다. 모듈 이름을 찾으려면
`빌드 설정` > `패키징` > `제품 모듈 이름`으로 이동하십시오.
`<tenantId>`를 사용하는 테넌트 ID로 대체하십시오([시작하기 전에](#before-you-begin) 참조).


## 모바일 백엔드 서비스에 대한 요청 작성
{: #getting-started-request}

{{site.data.keyword.amashort}} 클라이언트 SDK가 초기화되면 모바일 백엔드 서비스에 대한 요청을 작성할 수 있습니다. 

1. 모바일 백엔드 애플리케이션의 보호 엔드포인트로 요청을 전송하십시오. 브라우저에서 URL `{applicationRoute}/protected`(예: `http://my-mobile-backend.mybluemix.net/protected`)를 여십시오.

	MobileFirst Services Starter 표준 유형으로 작성된 모바일 백엔드의 `/protected` 엔드포인트는 {{site.data.keyword.amashort}}로 보호됩니다. 브라우저에 `Unauthorized` 메시지가 리턴됩니다. 이 엔드포인트는 {{site.data.keyword.amashort}} 클라이언트 SDK로 인스트루먼트된 모바일 애플리케이션에서만 액세스되므로 이 메시지가 리턴됩니다.

2. Cordova 애플리케이션을 사용하여 동일한 엔드포인트에 대해 요청을 작성하십시오. `BMSClient`를 초기화한 후에 다음 코드를 추가하십시오. 

	```Javascript
	var success = function(data){
	 console.log("success", data);
	 }

	 var failure = function(error){
	 console.log("failure", error);
	 }

	 var request = new BMSRequest("<your route>/protected", BMSRequest.GET);

	 request.send(success, failure);
	```
	{: codeblock}

3. 요청에 성공하는 경우 LogCat 또는 Xcode 콘솔에 다음 출력이 표시됩니다(사용 중인 플랫폼에 따라 다름). 

	![성공 메시지](images/getting-started-android-success.png)

	## 다음 단계
	{: #next-steps}

	보호 엔드포인트에 연결된 경우 신임 정보는 필요하지 않습니다. 사용자가 애플리케이션에 로그인하게 하려면 Facebook, Google 또는 사용자 정의 인증을 구성해야 합니다. 
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [사용자 정의 ](custom-auth-cordova.html)
