---

copyright:
  years: 2016

---

# iOS용 {{site.data.keyword.amashort}} 클라이언트 SDK(Swift SDK) 구성
{: #custom-ios}

사용자 정의 인증을 사용하는 iOS 애플리케이션이 {{site.data.keyword.amashort}}
클라이언트 SDK를 사용하고 애플리케이션을 {{site.data.keyword.Bluemix}}에 연결하도록 구성하십시오. 

## 시작하기 전에
{: #before-you-begin}

사용자 정의 ID 제공자를 사용하도록 구성된 {{site.data.keyword.amashort}} 서비스
인스턴스의 보호를 받는 자원이 있어야 합니다. 모바일 앱은 {{site.data.keyword.amashort}}
클라이언트 SDK도 갖추고 있어야 합니다. 자세한 정보는 다음 내용을 참조하십시오. 
 * [{{site.data.keyword.amashort}} 시작하기](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [iOS Swift SDK 설정](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html)
 * [사용자 정의 ID 제공자 사용](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [사용자 정의 ID 제공자 작성](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [사용자 정의 인증을 사용하도록 {{site.data.keyword.amashort}} 구성](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## 사용자 정의 인증을 사용하도록 {{site.data.keyword.amashort}} 구성
 {: #custom-auth-ios-configmca}

 1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 앱을 여십시오. 

 1. **모바일 옵션**을 클릭하고 **라우트**(*applicationRoute*) 및 **앱 GUID**(*applicationGUID*)를 기록해 두십시오. SDK를 초기화하는 경우 이 값이 필요합니다. 

 1. {{site.data.keyword.amashort}} 타일을 클릭하십시오. {{site.data.keyword.amashort}} 대시보드가 로드됩니다. 

 1. **사용자 정의** 타일을 클릭하십시오.

 1. **영역 이름**에 사용자 정의 인증 영역을 지정하십시오.

 1. **URL**에 applicationRoute를 지정하십시오.

 1. **저장**을 클릭하십시오.

## iOS용 {{site.data.keyword.amashort}} 클라이언트 SDK 구성
 {: #custom-auth-ios-sdk}

### CocoaPods 설치
 {: #custom-auth-cocoapods}

 {{site.data.keyword.amashort}} 클라이언트 SDK는 iOS 프로젝트에 대한 종속 항목 관리자인 CocoaPods를 사용하여 분배됩니다. CocoaPods는 저장소에서 아티팩트를 자동으로 다운로드하고 iOS 애플리케이션에서 아티팩트를 사용할 수 있게 합니다. 

 1. 터미널을 열고 `pod --version` 명령을 실행하십시오. 이미 CocoaPods가 설치되어 있는 경우 버전 번호가 표시됩니다. 이 학습서의 다음 섹션으로 건너뛸 수 있습니다. 

 1. `sudo gem install cocoapods`를 실행하여 CocoaPods를 설치하십시오. 추가적인 안내가 필요한 경우 [CocoaPods 웹 사이트](https://cocoapods.org/)를 참조하십시오. 

 1. XCode를 닫으십시오.

 1. 터미널 및 `cd`를 프로젝트 디렉토리로 여십시오.

 1.  `pod init`를 실행하십시오.

### CocoaPods로 클라이언트 SDK 설치
{: #custom-ios-sdk-cocoapods}

CocoaPods 종속성 관리자를 사용하여 {{site.data.keyword.amashort}}
클라이언트 SDK를 설치하십시오. 

1. 터미널을 열고 iOS 프로젝트의 루트 디렉토리로 이동하십시오. 

1. `Podfile`을 편집하여 다음 행을 추가하십시오.

 ```
 use_frameworks!
 pod 'BMSSecurity'
 ```
 **팁:** `use_frameworks!`를 Podfile에 삽입하는 대신 Xcode 대상에 추가할 수 있습니다.

1. 명령행에서 `pod install`을 실행하십시오.
CocoaPods가 추가된 종속 항목을 설치합니다. 진행상태 및 추가된 컴포넌트가 표시됩니다. 

 **중요**: 이제 CocoaPods에서 생성한 xcworkspace 파일을
사용하여 프로젝트를 열어야 합니다. 일반적으로 이름은 `{your-project-name}.xcworkspace`입니다.   

1. iOS 프로젝트 작업공간을 열려면 명령행에서 `open {your-project-name}.xcworkspace`를 실행하십시오. 

### 클라이언트 SDK 초기화
{: #custom-ios-sdk-initialize}

`applicationRoute` 및 `applicationGUID` 매개변수를 전달하여 SDK를 초기화하십시오. 필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 애플리케이션 위임자의 `application:didFinishLaunchingWithOptions` 메소드입니다. 

1. 애플리케이션 매개변수 값을 가져오십시오. {{site.data.keyword.Bluemix_notm}} 대시보드에서
앱을 여십시오. **모바일 옵션**을 클릭하십시오. `applicationRoute` 및 `applicationGUID` 값이 **라우트** 및 **앱 GUID** 필드에 표시됩니다.

1. {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하려는 클래스에 필수 프레임워크를 가져오십시오.

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
```

1. {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화하고 권한 관리자를 MCAAuthorizationManager로 변경하고 인증 위임을 정의한 후 이를 등록하십시오. `<applicationRoute>` 및 `<applicationGUID>`를 {{site.data.keyword.Bluemix_notm}} 대시보드의 **모바일 옵션**에서 얻은 **라우트** 및 **앱 GUID**의 값으로 바꾸십시오.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"
 let customRealm = "<your protected resource's realm>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {


 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

  //Auth delegate for handling custom challenge
 class MyAuthDelegate : AuthenticationDelegate {
      func onAuthenticationChallengeReceived(authContext: AuthenticationContext, challenge: AnyObject){
          print("onAuthenticationChallengeReceived")
              let answer = <An answer to the challenge sent by the backend (Should be of type [String:AnyObject])>
              authContext.submitAuthenticationChallengeAnswer(answer)
      }

      func onAuthenticationSuccess(info: AnyObject?) {
           print("onAuthenticationSuccess info = \(info)")
           print("onAuthenticationSuccess")
      }

      func onAuthenticationFailure(info: AnyObject?){
        print("onAuthenticationFailure info = \(info)")
        print("onAuthenticationFailure")
      }
  }

  let delegate = MyAuthDelegate()
  let mcaAuthManager = MCAAuthorizationManager.sharedInstance

 do {
      try mcaAuthManager.registerAuthenticationDelegate(delegate, realm: customRealm)
  } catch {
      print("error with register: \(error)")
  }
 return true
 }   
 ```

## 인증 테스트
{: #custom-ios-testing}

클라이언트 SDK를 초기화하고 사용자 정의 인증 위임을 등록한 후에는 모바일 백엔드에 대한 요청 작성을 시작할 수 있습니다.

### 시작하기 전에
{: #custom-ios-testing-before}

 {{site.data.keyword.mobilefirstbp}} 표준 유형으로 작성된
애플리케이션과 `/protected` 엔드포인트에서 {{site.data.keyword.amashort}}의
보호를 받는 자원이 있어야 합니다. 

1. `{applicationRoute}/protected`(예: `http://my-mobile-backend.mybluemix.net/protected`)를 열어 브라우저에서 모바일 백엔드의 보호 엔드포인트로 요청을
전송하십시오. {{site.data.keyword.mobilefirstbp}} 표준 유형으로 작성된 모바일 백엔드의
`/protected` 엔드포인트는 {{site.data.keyword.amashort}}에서 보호됩니다.
엔드포인트는 {{site.data.keyword.amashort}} 클라이언트 SDK를 갖춘 모바일 애플리케이션에서만
액세스할 수 있습니다. 따라서 `Unauthorized` 메시지는 브라우저에 표시됩니다. 

1. iOS 애플리케이션을 사용하여 동일한 엔드포인트를 요청하십시오.
`BMSClient`를 초기화한 후 다음 코드를 추가하고 사용자 정의 인증 위임을 등록하십시오.

 ```Swift
 let customResourceURL = "<your protected resource's path>"
 let request = Request(url: customResourceURL, method: HttpMethod.GET)
 let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) in
  if error == nil {
      print ("response:\(response?.responseText), no error")
  } else {
      print ("error: \(error)")
  }
 }

 request.sendWithCompletionHandler(callBack)
 ```

1. 	요청이 성공하면 Xcode 콘솔에 다음과 같은 출력이 표시됩니다. 

 ```
 onAuthenticationSuccess info = Optional({
     attributes =     {
     };
     deviceId = don;
     displayName = "Don+Lon";
     isUserAuthenticated = 1;
     userId = don;
 })
 response:Optional("Hello Don Lon"), no error
 ```

1. 다음 코드를 추가하여 로그아웃 기능을 추가할 수도 있습니다. 

 ```
 MCAAuthorizationManager.sharedInstance.logout(callBack)
 ```  

 사용자가 로그인한 후에 이 코드를 호출하면 사용자가 로그아웃됩니다. 
사용자가 다시 로그인을 시도하는 경우, 사용자는 서버에서 수신된 인증 확인에 다시 응답해야 합니다. 

 로그아웃 기능에 `callBack` 전달은 선택사항입니다. `nil`을 전달할 수도 있습니다. 
