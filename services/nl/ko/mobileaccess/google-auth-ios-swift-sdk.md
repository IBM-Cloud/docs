---

copyright:
  years: 2016

---

# iOS 앱(Swift SDK)에서 Google 인증 사용
{: #google-auth-ios}

## 시작하기 전에
{: #google-auth-ios-before}

* {{site.data.keyword.amashort}}에서 보호하는 자원 및 {{site.data.keyword.amashort}} 클라이언트 SDK로 계측되는 iOS 프로젝트가 있어야 합니다. 자세한 정보는 [{{site.data.keyword.amashort}} 시작하기](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) 및 [iOS Swift SDK 설정](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html)을 참조하십시오.  
* {{site.data.keyword.amashort}} 서버 SDK를 사용하여 백엔드 애플리케이션을 수동으로 보호하십시오. 자세한 정보는 [자원 보호](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)를 참조하십시오. 

## Google 로그인을 수행할 수 있도록 앱 준비
{: #google-sign-in-ios}

Google에서 제공하는 [Goolge Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start-integrating)에서 Google이 제공하는 지시사항을 따라 Google 로그인을 수행할 수 있도록 앱을 준비하십시오. 다음 단계는 앱을 준비하기 위해 수행해야 하는 태스크에 대해 간략하게 설명합니다.

1. 앱에서 iOS용 Google 로그인을 사용으로 설정하십시오. 자세한 정보는 [Try Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start?ver=swift)를 참조하십시오.

1. 프로젝트에 대한 구성 파일(`GoogleService-Info.plist`)을 가져오십시오. 파일을 가져오려면 [Enable Google services for your app](https://developers.google.com/mobile/add?platform=ios)을 참조하십시오.

 **중요:** `GoogleService-Info.plist` 파일을 가져올 때 파일을 열고 `CLIENT_ID` 값을 기록해 두십시오. 나중에 {{site.data.keyword.amashort}}를 구성하는 데 이 값이 필요합니다.

1. `GoogleService-Info.plist` 파일을 Xcode 프로젝트에 추가하십시오. 자세한 정보는 [Add the configuration file to your project](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config)를 참조하십시오.

1. `REVERSE_CLIENT_ID` 및 번들 ID를 사용하여 Xcode 프로젝트의 URL 스킴을 업데이트하십시오. 자세한 정보는 [Add URL schemes to your project](https://developers.google.com/identity/sign-in/ios/start-integrating#add_url_schemes_to_your_project)를 참조하십시오.

1. 다음 코드를 사용하여 앱의 project-Bridging-Header.h 파일을 업데이트하십시오.

 ```
 #import <Google/SignIn.h>
 ```

 브리징 헤더 파일 업데이트에 대한 자세한 정보는 [Enable sign-in](https://developers.google.com/identity/sign-in/ios/sign-in#enable_sign-in)의 1단계를 참조하십시오.

## Google 인증을 위해 {{site.data.keyword.amashort}} 구성
{: #google-auth-ios-config}

iOS 클라이언트 ID가 있으므로 {{site.data.keyword.Bluemix}} 대시보드에서 Google 인증을 사용하도록 설정할 수 있습니다. 

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 앱을 여십시오. 

1. **모바일 옵션**을 클릭하고 **라우트**(*applicationRoute*) 및 **앱 GUID**(*applicationGUID*)를 기록해 두십시오. SDK를 초기화하는 경우 이 값이 필요합니다. 

1. {{site.data.keyword.amashort}} 타일을 클릭하십시오. {{site.data.keyword.amashort}} 대시보드가 로드됩니다. 

1. **Google** 타일을 클릭하십시오.

1. **iOS용 애플리케이션 ID**에서 이전에 얻은 `GoogleService-Info.plist` 파일의 `CLIENT_ID` 값을 지정하고 **저장**을 클릭하십시오.

## iOS용 {{site.data.keyword.amashort}} 클라이언트 SDK 구성
{: #google-auth-ios-sdk}

### CocoaPods 설치
{: #google-auth-cocoapods}

{{site.data.keyword.amashort}} 클라이언트 SDK는 iOS 프로젝트에 대한 종속 항목 관리자인 CocoaPods를 사용하여 분배됩니다. CocoaPods는 저장소에서 아티팩트를 자동으로 다운로드하고 iOS 애플리케이션에서 아티팩트를 사용할 수 있게 합니다. 

1. 터미널을 열고 `pod --version` 명령을 실행하십시오. 이미 CocoaPods가 설치되어 있는 경우 버전 번호가 표시됩니다. 이 학습서의 다음 섹션으로 건너뛸 수 있습니다. 

1. `sudo gem install cocoapods`를 실행하여 CocoaPods를 설치하십시오. 추가적인 안내가 필요한 경우 [CocoaPods 웹 사이트](https://cocoapods.org/)를 참조하십시오. 

1. XCode를 닫으십시오.

1. 터미널 및 `cd`를 프로젝트 디렉토리로 여십시오.

1.  `pod init`를 실행하십시오.

### CocoaPods를 사용하여 {{site.data.keyword.amashort}} 클라이언트 SWift SDK 설치
{: #google-auth-ios-sdk-cocoapods}

1. iOS 프로젝트로 이동하십시오.

1. `Podfile`을 편집하여 다음 행을 추가하십시오.

 ```
 use_frameworks!
 pod 'BMSGoogleAuthentication'
 ```
 **팁:** `use_frameworks!`를 Podfile에 삽입하는 대신 Xcode 대상에 추가할 수 있습니다.

1. `Podfile`을 저장하고 명령행에서 `pod install`을 실행하십시오. CocoaPods가 종속 항목을 설치합니다. 진행상태 및 추가된 컴포넌트를 확인할 수 있습니다. 

 **중요**: 이제 CocoaPods에서 생성한 `xcworkspace` 파일을 사용하여 프로젝트를 열어야 합니다. 일반적으로 이름은 `{your-project-name}.xcworkspace`입니다.   

1. 명령행에서 `open {your-project-name}.xcworkspace`를 실행하여 iOS 프로젝트 작업공간을 여십시오.

1. `GoogleAuthenticationManager.swift` 파일을 `BMSGoogleAuthentication` pod 소스 파일에서 프로젝트 디렉토리에 복사하십시오.

## {{site.data.keyword.amashort}} 클라이언트 Swift SDK 초기화
{: #google-auth-ios-initialize}

{{site.data.keyword.amashort}} 클라이언트 SDK를 사용하려면 `applicationGUID` 및 `applicationRoute` 매개변수를 전달하여 해당 클라이언트 SDK를 초기화하십시오.

필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 애플리케이션 위임자의 `application:didFinishLaunchingWithOptions` 메소드입니다. 

1. 애플리케이션 매개변수 값을 가져오십시오. {{site.data.keyword.Bluemix_notm}} 대시보드에서
앱을 여십시오. **모바일 옵션**을 클릭하십시오. `applicationRoute` 및 `applicationGUID` 값이 **라우트** 및 **앱 GUID** 필드에 표시됩니다.

1. {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하려는 클래스에 필수 프레임워크를 가져오십시오. 다음 헤더를 추가하십시오.

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```

1. 다음 코드를 사용하여 클라이언트 SDK를 초기화하십시오. `<applicationRoute>` 및 `<applicationGUID>`를 {{site.data.keyword.Bluemix_notm}} 대시보드의 **모바일 옵션**에서 얻은 **라우트** 및 **앱 GUID**의 값으로 바꾸십시오.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {


 // Initialize the Client SDK.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUId, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 GoogleAuthenticationManager.sharedInstance.register()
      return true
      }

 // [START openurl]
      func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?,annotation: AnyObject) -> Bool {
return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, sourceApplication: sourceApplication, annotation: annotation)
      }

 @available(iOS 9.0, *)
 func application(app: UIApplication, openURL url: NSURL, options: [String : AnyObject]) -> Bool {
 return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, options: options)
  }
 ```

## 인증 테스트
{: #google-auth-ios-testing}

클라이언트 SDK가 초기화되고 Google 인증 관리자가 등록되면 모바일 백엔드에 대한 요청 작성을 시작할 수 있습니다.

### 시작하기 전에
{: #google-auth-ios-testing-before}

{{site.data.keyword.mobilefirstbp}} 표준 유형을 사용해야 하며 이미 `/protected` 엔드포인트에 {{site.data.keyword.amashort}}가 보호하는 자원이 있어야 합니다. `/protected` 엔드포인트를 설정해야 하는 경우
[자원 보호](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)를 참조하십시오. 


1. `{applicationRoute}/protected`(예: `http://my-mobile-backend.mybluemix.net/protected`)를 열어 데스크탑 브라우저에서 모바일 백엔드의 보호 엔드포인트로 요청을 전송하십시오.

1. MobileFirst 서비스 표준 유형으로 작성된 모바일 백엔드의 `/protected` 엔드포인트는 {{site.data.keyword.amashort}}로 보호되므로 {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하여 계측된 모바일 애플리케이션만 액세스할 수 있습니다. 결과적으로 데스크탑 브라우저에 `권한 없음`이 표시됩니다. 

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

1. 애플리케이션을 실행하십시오. Google 로그인 화면이 팝업으로 표시됩니다. 

 ![이미지](images/ios-google-login.png)

1. 로그인하여 **확인**을 클릭하면 인증을 위해 Google 사용자 ID를 사용할 수 있는 권한을 {{site.data.keyword.amashort}}에 부여합니다.

1. 	요청이 성공적으로 처리되어야 합니다. 로그에 다음 출력이 표시되어야 합니다.

 ```
 onAuthenticationSuccess info = Optional({attributes = {};
     deviceId = 105747725068605084657;
     displayName = "donlonqwerty@gmail.com";
     isUserAuthenticated = 1;
     userId = 105747725068605084657;
 })
 response:Optional("Hello, this is a protected resource!"), no error
 ```

1. 다음 코드를 추가하여 로그아웃 기능을 추가할 수도 있습니다. 

 ```
 GoogleAuthenticationManager.sharedInstance.logout(callBack)
 ```

  Google에서 사용자가 로그인한 이후 이 코드를 호출하며 사용자가 다시 로그인을 시도하는 경우,
사용자에게는 인증 용도로 Google을 사용하도록 {{site.data.keyword.amashort}} 권한 부여 프롬프트가 제시됩니다. 
이 시점에, 사용자는 화면 상단 오른쪽 모서리에서 사용자 이름을 클릭하여 다른 사용자를 선택하고 이를 사용하여 로그인할 수 있습니다. 

   로그아웃 기능에 `callBack` 전달은 선택사항입니다. `nil`을 전달할 수도 있습니다. 
