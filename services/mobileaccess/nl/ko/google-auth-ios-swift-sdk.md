---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

{{site.data.keyword.amafull}} 서비스가 {{site.data.keyword.appid_full}} 서비스로 대체되었습니다.

# iOS 앱에서 Google 인증 사용(Swift SDK)
{: #google-auth-ios}

Google 로그인을 사용하여 {{site.data.keyword.amafull}} iOS Swift 앱에서 사용자를 인증하십시오. 


## 시작하기 전에
{: #before-you-begin}

다음이 있어야 합니다.

* {{site.data.keyword.Bluemix_notm}} 애플리케이션 및 {{site.data.keyword.amafull}} 서비스의 인스턴스. {{site.data.keyword.Bluemix_notm}} 백엔드 애플리케이션 작성 방법에 대한 자세한 정보는 [시작하기](index.html)를 참조하십시오.
* 백엔드 애플리케이션의 URL(**앱 라우트**). 이 값은 백엔드 애플리케이션의 보호 엔드포인트에 요청을 전송하는 데 필요합니다. 
* **테넌트 ID** 값. {{site.data.keyword.amashort}} 대시보드에서 서비스를 여십시오. **모바일 옵션** 단추를 클릭하십시오. **앱 GUID / TenantId** 필드에 `tenantId`(`appGUID`라고도 함) 값이 표시됩니다. 이 값은 권한 관리자를 초기화하는 데 필요합니다. 
* {{site.data.keyword.Bluemix_notm}} **지역**. 헤더에서 **아바타** 아이콘 ![아바타 아이콘](images/face.jpg "아바타 아이콘") 옆에 현재 {{site.data.keyword.Bluemix_notm}} 지역이 표시됩니다. 표시되는 지역 값은 **미국 남부**, **영국** 또는 **시드니** 중 하나여야 하며 코드 `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` 또는 `BMSClient.Region.sydney`에 필요한 값에 해당해야 합니다. 
* Xcode의 iOS 프로젝트. {{site.data.keyword.amashort}} 클라이언트 SDK로 인스트루먼트되지 않아도 됩니다.  


## Google 로그인을 위해 앱 준비
{: #google-sign-in-ios}

[iOS용 Google 로그인 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developers.google.com/identity/sign-in/ios/start-integrating){: new_window}에서 Google이 제공하는 지시사항에 따라 Google 로그인을 위한 앱을 준비하십시오. 

이 프로세스에서는 다음을 수행합니다.

* Google 개발자 사이트에서 새로운 프로젝트를 준비합니다.
* Xcode 프로젝트에 추가할 `REVERSE_CLIENT_ID` 값과 `GoogleService-Info.plist` 파일을 작성합니다.
* {{site.data.keyword.Bluemix_notm}} 백엔드 애플리케이션에 추가할 **Google 클라이언트 ID**를 작성합니다.

다음 단계에서는 앱을 준비하는 데 필요한 단계를 간략하게 설명합니다.

**참고:** Google Sign-In CocoaPod를 추가할 필요가 없습니다. 필수 SDK는 `BMSGoogleAuthentication` CocoaPod에서 추가합니다.

1. 기본 대상의 **일반** 탭에 있는 **ID** 섹션에서 Xcode 프로젝트의 **번들 ID**를 기록하십시오. Google 로그인 프로젝트를 작성하는 데 필요합니다. 

1. [Google 개발자 사이트 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developers.google.com/mobile/add?platform=ios){: new_window}에서 iOS용 Google 로그인을 위한 프로젝트를 작성하십시오. 

1. 프로젝트에 Google 로그인 API를 추가하십시오.

1. `GoogleService-Info.plist`를 검색하십시오.

   **중요:** `GoogleService-Info.plist` 파일을 가져올 때 파일을 열고 `CLIENT_ID` 값을 기록해 두십시오. 나중에 {{site.data.keyword.amashort}} 백엔드 애플리케이션을 구성하는 데 해당 값이 필요합니다.

1. `GoogleService-Info.plist` 파일을 Xcode 프로젝트에 추가하십시오. 자세한 정보는 [프로젝트에 구성 파일 추가 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config){: new_window}를 참조하십시오. 

1. `REVERSE_CLIENT_ID` 및 번들 ID를 사용하여 Xcode 프로젝트의 URL 스킴을 업데이트하십시오. 자세한 정보는 [프로젝트에 URL 스킴 추가 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developers.google.com/identity/sign-in/ios/start-integrating#add_a_url_scheme_to_your_project){: new_window}를 참조하십시오. 

1. 사용하는 앱의 `project-Bridging-Header.h` 파일을 다음 코드로 업데이트하십시오. 

	```
	#import <Google/SignIn.h>
	```
	{: codeblock}

	브릿지 헤더 파일 업데이트에 대한 자세한 정보는 [로그인 사용 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developers.google.com/identity/sign-in/ios/sign-in#enable_sign-in){: new_window}을 참조하십시오. 

## Google 인증용 {{site.data.keyword.amashort}} 구성
{: #google-auth-ios-config}

이제 iOS 클라이언트 ID가 있으므로 {{site.data.keyword.amashort}} 서비스에서 Google 인증을 사용 가능하게 설정할 수 있습니다.

1. {{site.data.keyword.amashort}} 대시보드에서 서비스를 여십시오. 
1. **관리** 탭에서 **권한**을 토글하여 켜십시오. 
1. **Google** 섹션을 펼치십시오. 
1. **iOS용 애플리케이션 ID**에 `GoogleService-Info.plist` 파일에서 얻은 `CLIENT_ID` 값을 지정하십시오. 
1. **저장**을 클릭하십시오.

## iOS용 {{site.data.keyword.amashort}} 클라이언트 SDK 구성
{: #google-auth-ios-sdk}

### CocoaPods 설치
{: #install-cocoapods}

1. 터미널을 열고 **pod --version** 명령을 실행하십시오. 이미 CocoaPods가 설치되어 있는 경우 버전 번호가 표시됩니다. SDK를 설치하기 위해 다음 섹션으로 건너뛸 수 있습니다. 

1. CocoaPods가 설치되어 있지 않은 경우에는 다음을 실행하십시오. 

	```
	sudo gem install cocoapods
	```
	{: codeblock}

자세한 정보는 [CocoaPods 웹 사이트 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cocoapods.org/){: new_window}를 참조하십시오. 

### CocoaPods를 사용하여 {{site.data.keyword.amashort}} 클라이언트 Swift SDK 설치
{: #facebook-auth-install-swift-cocoapods}

1. iOS 프로젝트에 `Podfile`이 없으면 `pod init`을 실행하여 파일을 작성하십시오.

1. `Podfile`을 편집하고 다음 행을 적절한 대상에 추가하십시오.

	```
	use_frameworks!
	pod 'BMSGoogleAuthentication'
	```
	{: codeblock}

	**참고:** 이미 {{site.data.keyword.amashort}} 코어 SDK를 설치한 경우 `pod 'BMSSecurity'` 행을 제거할 수 있습니다. `BMSGoogleAuthentication` pod에서 필요한 모든 프레임워크를 설치합니다.

	**팁:** `use_frameworks!`를 Podfile에 삽입하는 대신 Xcode 대상에 추가할 수 있습니다.

1. `Podfile`을 저장하고 명령행에서 `pod install`을 실행하십시오. CocoaPods가 종속 항목을 설치합니다. 진행상태 및 추가된 컴포넌트를 확인할 수 있습니다. 

	**중요**: 이제 CocoaPods에서 생성한 `xcworkspace` 파일을 사용하여 프로젝트를 열어야 합니다. 일반적으로 이름은 `{your-project-name}.xcworkspace`입니다.   

1. 명령행에서 `open {your-project-name}.xcworkspace`를 실행하여 iOS 프로젝트 작업공간을 여십시오.

1. `GoogleAuthenticationManager.swift` 파일을 `BMSGoogleAuthentication` pod 소스 파일에서 프로젝트 디렉토리에 복사하십시오.

### iOS에서 키 체인 공유 사용
{: #enable_keychain}

`키 체인 공유`를 사용 가능하게 설정하십시오. `기능` 탭으로 이동하여 Xcode 프로젝트에서 `키 체인 공유`를 `On`으로 전환하십시오. 


## {{site.data.keyword.amashort}} 클라이언트 Swift SDK 초기화
{: #google-auth-ios-initialize}

{{site.data.keyword.amashort}} 클라이언트 SDK를 사용하려면 `tenantID` 매개변수를 전달하여 해당 클라이언트 SDK를 초기화하십시오. 

필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 애플리케이션 위임자의 `application:didFinishLaunchingWithOptions` 메소드입니다. 

1. {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하려는 클래스에 필수 프레임워크를 가져오십시오. 다음 헤더를 추가하십시오.

	```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {

		let mcaAuthManager = MCAAuthorizationManager.sharedInstance
		mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
		//the regionName should be one of the following: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney   
		BMSClient.sharedInstance.authorizationManager = mcaAuthManager
		GoogleAuthenticationManager.sharedInstance.register()
		return true
	}

	// [START openurl]
	func application(_ application: UIApplication,
		open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
			return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url,
			sourceApplication: sourceApplication, annotation: annotation)
	    }

	@available(iOS 9.0, *)
	func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any]) -> Bool {
		return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, options: options)
	}

	```
	{: codeblock}

	코드에서: 

      * `<serviceTenantID>`를 **모바일 옵션**에서 수신한 값으로 대체하십시오. 
      * `<applicationBluemixRegion>`을 해당 {{site.data.keyword.Bluemix_notm}} **지역**으로 대체하십시오.

	이러한 값을 얻는 방법에 대한 자세한 정보는 [시작하기 전에](#before-you-begin)를 참조하십시오. 


## 인증 테스트
{: #google-auth-ios-testing}

클라이언트 SDK가 초기화되고 Google 인증 관리자가 등록되면 모바일 백엔드 애플리케이션에 대한 요청을 시작할 수 있습니다. 

### 시작하기 전에
{: #google-auth-ios-testing-before}

{{site.data.keyword.mobilefirstbp}} 표준 유형을 사용 중 이어야 하며 이미 `/protected` 엔드포인트에 {{site.data.keyword.amashort}}가 보호하는 리소스가 있어야 합니다. `/protected` 엔드포인트를 설정해야 하는 경우 [리소스 보호](protecting-resources.html)를 참조하십시오. 

1. `{applicationRoute}/protected`를 열어 데스크탑 브라우저에서 모바일 백엔드 애플리케이션의 보호 엔드포인트에 요청을 보내십시오. 예를 들면, `http://my-mobile-backend.mybluemix.net/protected`입니다. 

1. MobileFirst 서비스 표준 유형으로 작성된 모바일 백엔드 애플리케이션의 `/protected` 엔드포인트는 {{site.data.keyword.amashort}}에서 보호되므로 {{site.data.keyword.amashort}} 클라이언트 SDK로 인스트루먼트된 모바일 애플리케이션에서만 액세스할 수 있습니다. 결과적으로 데스크탑 브라우저에 `권한 없음`이 표시됩니다. 

1. iOS 애플리케이션을 사용하여 동일한 엔드포인트를 요청하십시오. 

	```Swift
	let protectedResourceURL = "<your protected resource absolute path>"
	let request = Request(url: protectedResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
		if error == nil {
			print ("response:\(response?.responseText), no error")
		} else {
			print ("error: \(error)")
		}
	}

	request.send(completionHandler: callBack)

	```
	{: codeblock}

1. 애플리케이션을 실행하십시오. Google 로그인 화면이 팝업으로 표시됩니다. 

 ![이미지](images/ios-google-login.png)

1. 로그인하여 **확인**을 클릭하면 인증을 위해 Google 사용자 ID를 사용할 수 있는 권한을 {{site.data.keyword.amashort}}에 부여합니다.

1. 요청이 성공적으로 처리되어야 합니다. 로그에 다음 출력이 표시됩니다. 

	```
	response:Optional("Hello, this is a protected resource of the mobile backend application!"), no error
	```
	{: screen}

1. 다음 코드를 추가하여 로그아웃 기능을 추가할 수도 있습니다. 

	```
	GoogleAuthenticationManager.sharedInstance.logout(callBack)
	```
	{: codeblock}

	Google에서 사용자가 로그인한 이후 이 코드를 호출하며 사용자가 다시 로그인을 시도하는 경우, 사용자에게는 인증 용도로 Google을 사용하도록 {{site.data.keyword.amashort}} 권한 부여 프롬프트가 제시됩니다. 이 시점에서 사용자는 사용자 이름을 클릭하여 <!--in the upper-right corner of the screen--> 다른 사용자를 선택하고 다른 사용자로 로그인할 수 있습니다.

	로그아웃 기능에 `callBack` 전달은 선택사항입니다. `nil`을 전달할 수도 있습니다. 
