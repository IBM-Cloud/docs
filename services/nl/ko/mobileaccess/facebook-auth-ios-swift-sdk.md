---

copyright:
  years: 2016

---

# iOS 앱(Swift SDK)에서 Facebook 인증 사용
{: #facebook-auth-ios}

iOS 애플리케이션에서 Facebook을 ID 제공자로 사용하려면 Facebook 애플리케이션에 대한 iOS 플랫폼을 추가하고 구성하십시오.

## 시작하기 전에
{: #facebook-auth-ios-before}

* {{site.data.keyword.amashort}}에서 보호하는 자원 및 {{site.data.keyword.amashort}} 클라이언트 SDK로 계측되는 iOS 프로젝트가 있어야 합니다. 자세한 정보는 [{{site.data.keyword.amashort}} 시작하기](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) 및 [iOS Swift SDK 설정](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html)을 참조하십시오.  
* {{site.data.keyword.amashort}} 서버 SDK로 백엔드 애플리케이션을 수동으로 보호하십시오. 자세한 정보는 [자원 보호](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)를 참조하십시오. 
* Facebook 애플리케이션 ID를 작성하십시오. 자세한 정보는 [Facebook 개발자 포털에서 Facebook 애플리케이션 ID 얻기](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)를 참조하십시오. 

## iOS 플랫폼에 대한 Facebook 애플리케이션 구성
{: #facebook-auth-ios-config}

1. [Facebook 앱의 대시보드](https://developers.facebook.com/apps/)에 로그인하십시오.

1. 사용자 앱의 **앱 ID**를 기록해 두십시오. Facebook 인증을 사용하도록 iOS 프로젝트를 구성할 때 이 값이 필요합니다.

1. **설정 > 플랫폼 추가 > iOS**를 클릭하십시오.

1. iOS 애플리케이션의 *번들 ID*를 지정하십시오. iOS 애플리케이션의 *번들 ID*를 찾으려면, `info.plist` 파일 또는 Xcode 프로젝트 **일반** 탭에서 **번들 ID**를 검색하십시오.
**팁**: 이러한 기능을 사용할 계획이라면 URL 스킴 접미부 또는 Single Sign On 사용을 고려하십시오. 

1. **설정 저장**을 클릭하십시오. 

## Facebook 인증을 사용하도록 {{site.data.keyword.amashort}} 구성
{: #facebook-auth-ios-configmca}

iOS 클라이언트를 제공하도록 Facebook 애플리케이션 ID 및 Facebook 애플리케이션을 구성한 후 {{site.data.keyword.amashort}}에서 Facebook 인증을 사용하도록 설정할 수 있습니다. 

1. {{site.data.keyword.Bluemix}} 대시보드에서 앱을 여십시오. 

1. **모바일 옵션**을 클릭하고 **라우트**(*applicationRoute*) 및 **앱 GUID**(*applicationGUID*)를 기록해 두십시오. SDK를 초기화하는 경우 이 값이 필요합니다. 

1. {{site.data.keyword.amashort}} 타일을 클릭하십시오. {{site.data.keyword.amashort}} 대시보드가 로드됩니다. 

1. **Facebook** 타일을 클릭하십시오.

1. Facebook 애플리케이션 ID를 지정하고 **저장**을 클릭하십시오. 

## iOS용 {{site.data.keyword.amashort}} 클라이언트 SDK 구성
{: #facebook-auth-ios-sdk}

### CocoaPods 설치
{: #facebook-auth-cocoapods}

{{site.data.keyword.amashort}} 클라이언트 SDK는 iOS 프로젝트에 대한 종속 항목 관리자인 CocoaPods를 사용하여 분배됩니다. CocoaPods는 저장소에서 아티팩트를 자동으로 다운로드하고 iOS 애플리케이션에서 아티팩트를 사용할 수 있게 합니다. 

1. 터미널을 열고 `pod --version` 명령을 실행하십시오. 이미 CocoaPods가 설치되어 있는 경우 버전 번호가 표시됩니다. 이 학습서의 다음 섹션으로 건너뛸 수 있습니다. 

1. `sudo gem install cocoapods`를 실행하여 CocoaPods를 설치하십시오. 추가적인 안내가 필요한 경우 [CocoaPods 웹 사이트](https://cocoapods.org/)를 참조하십시오. 

1. XCode를 닫으십시오.

1. 터미널 및 `cd`를 프로젝트 디렉토리로 여십시오.

1.  `pod init`를 실행하십시오.

### CocoaPods로 {{site.data.keyword.amashort}} 클라이언트 Swift SDK 설치
{: #facebook-auth-install-swift-cocoapods}

1. iOS 프로젝트에서 `Podfile`을 편집하여 다음 행을 추가하십시오.

 ```
use_frameworks!
pod 'BMSFacebookAuthentication'
	```
 **팁:** `use_frameworks!`를 Podfile에 삽입하는 대신 Xcode 대상에 추가할 수 있습니다.

1. `Podfile`을 저장하고 명령행에서 `pod install` 명령을 실행하십시오. CocoaPods가 종속 항목을 설치합니다. 진행상태 및 추가된 컴포넌트가 표시됩니다. 

 **중요**: 이제 CocoaPods에서 생성한 `xcworkspace` 파일을 사용하여 프로젝트를 열어야 합니다. 일반적으로 이름은 `{your-project-name}.xcworkspace`입니다.   

1. iOS 프로젝트 작업공간을 열려면 명령행에서 `open {your-project-name}.xcworkspace`를 실행하십시오. 

### Facebook 인증을 사용하도록 iOS 프로젝트 구성
{: #facebook-auth-ios-configproject}

1. `info.plist` 파일을 찾으십시오. 이 파일은 보통 Xcode 프로젝트의 `지원 파일` 폴더에 있습니다. 

1. 다음 특성을 `info.plist` 파일에 추가하여 Facebook 통합을 구성하십시오. 

   ![이미지](images/ios-facebook-infoplist-settings.png)

   Facebook 애플리케이션 ID를 사용하여 URL 스킴 및 FacebookappID 특성을 업데이트하십시오. 

   또는 `info.plist` 파일을 마우스 오른쪽 단추로 클릭하고 **다른 이름으로 열기 > 소스 코드**를 선택한 후 다음 XML을 추가하여 파일을 업데이트할 수도 있습니다. 

   ```XML
	<key>CFBundleURLTypes</key>
	<array>
		<dict>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>fb{your-facebook-application-id}</string>
			</array>
		</dict>
	</array>
	<key>FacebookAppID</key>
	<string>{your-facebook-application-id}</string>
	<key>FacebookDisplayName</key>
	<string>{your-faceebook-application-name}</string>
	<key>LSApplicationQueriesSchemes</key>
	<array>
		<string>fbauth</string>
		<string>fbauth2</string>
	</array>
	<key>NSAppTransportSecurity</key>
	<dict>
	    <key>NSExceptionDomains</key>
	    <dict>
	        <key>facebook.com</key>
	        <dict>
	            <key>NSIncludesSubdomains</key>
	            <true/>                
	            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
	            <false/>
	        </dict>
	        <key>fbcdn.net</key>
	        <dict>
	            <key>NSIncludesSubdomains</key>
	            <true/>
	            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
	            <false/>
	        </dict>
	        <key>akamaihd.net</key>
	        <dict>
	            <key>NSIncludesSubdomains</key>
	            <true/>
	            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
	            <false/>
	        </dict>
	    </dict>
	</dict>
```
   Facebook 애플리케이션 ID를 사용하여 URL 스킴 및 FacebookappID 특성을 업데이트하십시오. Facebook 애플리케이션의 이름을 사용하여 FacebookDisplayName을 업데이트하십시오.

    **중요**: `info.plist` 파일의 기존 특성을 대체하고 있지 않는지 확인하십시오. 중첩된 특성이 있는 경우 수동으로 병합해야 합니다. 자세한 정보는 [Xcode 프로젝트 구성](https://developers.facebook.com/docs/ios/getting-started/) 및 [iOS9를 위한 앱 준비](https://developers.facebook.com/docs/ios/ios9)를 참조하십시오. 

## {{site.data.keyword.amashort}} 클라이언트 Swift SDK 초기화
{: #facebook-auth-ios-initalize-swift}

`applicationGUID` 및 `applicationRoute` 매개변수를 전달하여 클라이언트 SDK를 초기화하십시오. 

필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 애플리케이션 위임자의 `application:didFinishLaunchingWithOptions` 메소드입니다. 

1. 애플리케이션 매개변수 값을 가져오십시오. {{site.data.keyword.Bluemix_notm}} 대시보드에서
앱을 여십시오. **모바일 옵션**을 클릭하십시오. `applicationRoute` 및 `applicationGUID` 값이 **라우트** 및 **앱 GUID** 필드에 표시됩니다.

1. 다음 헤더를 추가하여 {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하려는 클래스에 필수 프레임워크를 가져오십시오. 

 ```swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```
2. 클라이언트 SDK를 초기화하십시오.	`<applicationRoute>` 및 `<applicationGUID>`를 {{site.data.keyword.Bluemix_notm}} 대시보드의 **모바일 옵션**에서 얻은 **라우트** 및 **앱 GUID**의 값으로 바꾸십시오.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {


 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 FacebookAuthenticationManager.sharedInstance.register()
 ```

1. Facebook SDK에 앱 활성화에 대한 알림을 전송하고 앱 위임자의 `application:didFinishLaunchingWithOptions` 메소드에 다음 코드를 추가하여 Facebook 인증 핸들러를 등록하십시오. BMSClient 인스턴스를 초기화한 후에 바로 이 코드를 추가하고 Facebook을 인증 관리자로 등록하십시오.

 ```Swift
  return FacebookAuthenticationManager.sharedInstance.onFinishLaunching(application, withOptions: launchOptions)
 ```

1. `FacebookAuthenticationManager.swift` 파일을 `BMSFacebookAuthentication` pod 소스 파일에서 프로젝트 디렉토리에 복사하십시오.

1. 다음 코드를 앱 위임자에 추가하십시오. 

 ```Swift
	func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?,annotation: AnyObject) -> Bool {


		return FacebookAuthenticationManager.sharedInstance.onOpenURL(application, url: url, sourceApplication: sourceApplication, annotation: annotation)

	}
 ```

## 인증 테스트
{: #facebook-auth-ios-testing}

클라이언트 SDK가 초기화되고 Facebook 인증 관리자가 등록되면 모바일 백엔드에 대한 요청 작성을 시작할 수 있습니다. 

### 시작하기 전에
{: #facebook-auth-ios-testing-before}

{{site.data.keyword.mobilefirstbp}} 표준 유형을 사용해야 하며 이미 `/protected` 엔드포인트에 {{site.data.keyword.amashort}}가 보호하는 자원이 있어야 합니다. `/protected` 엔드포인트를 설정해야 하는 경우
[자원 보호](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)를 참조하십시오. 

1. 브라우저에서 새로 작성된 모바일 백엔드의 보호 엔드포인트에 요청을 전송하십시오. URL `{applicationRoute}/protected`를 여십시오.
(예: `http://my-mobile-backend.mybluemix.net/protected`)
<br/>MobileFirst Services Starter 표준 유형으로 작성된 모바일 백엔드의 `/protected` 엔드포인트는 {{site.data.keyword.amashort}}를 사용하여 보호됩니다. 브라우저에 `Unauthorized` 메시지가 리턴됩니다. 이 엔드포인트는 {{site.data.keyword.amashort}} 클라이언트 SDK를 갖춘 모바일 애플리케이션에서만 액세스할 수 있으므로 이 메시지가 리턴됩니다.

1. iOS 애플리케이션을 사용하여 동일한 엔드포인트에 대해 요청을 작성하십시오. 

	```Swift
  let protectedResourceURL = "<Your protected resource URL>" // any protected resource
  let request = Request(url: protectedResourceURL , method: HttpMethod.GET)
  let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) in

  if error == nil {
         
     print ("response:\(response?.responseText), no error")
  } else {
     print ("error: \(error)")
  }
  }

  request.sendWithCompletionHandler(callBack)
 ```

1. 애플리케이션을 실행하십시오. Facebook 로그인 화면이 팝업으로 표시됩니다. 

   ![이미지](images/ios-facebook-login.png)

   이 화면은 현재 Facebook에 로그인되어 있지 않은 경우 약간 다르게 보일 수 있습니다.

1. 인증을 위해 Facebook 사용자 ID를 사용할 수 있도록 {{site.data.keyword.amashort}}에 권한을 부여하려면 **확인**을 클릭하십시오. 

1. 	요청에 성공하는 경우 다음 출력이 Xcode 콘솔에 표시됩니다. 

 ```
 "onAuthenticationSuccess info = Optional({
     attributes =     {
     };
     deviceId = 218227041863639;
     displayName = "Don+Lon";
     isUserAuthenticated = 1;
     userId = 218227041863639;
 })
 response:Optional("Hello, this is a protected resouce of the mobile backend application!"), no error
 ```

1. 다음 코드를 추가하여 로그아웃 기능을 추가할 수도 있습니다. 

 ```
FacebookAuthenticationManager.sharedInstance.logout(callBack)
```

 Facebook에서 사용자가 로그인한 이후 이 코드를 호출하며 사용자가 다시 로그인을 시도하는 경우,
사용자에게는 인증 용도로 Facebook을 사용하도록 {{site.data.keyword.amashort}} 권한 부여 프롬프트가 제시됩니다. 

 사용자를 전환하려면, 이 코드를 호출해야 하며 사용자는 자체 브라우저에서 Facebook에서 로그아웃해야 합니다. 

 로그아웃 기능에 ```callBack``` 전달은 선택사항입니다. `nil`을 전달할 수도 있습니다. 
