---

copyright:
  years: 2016

---

# iOS용 {{site.data.keyword.amashort}} 클라이언트 SDK(Swift SDK) 구성
{: #custom-ios}

사용자 정의 인증을 사용하는 iOS 애플리케이션이 {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하고 애플리케이션을 {{site.data.keyword.Bluemix}}에 연결하도록 구성하십시오.새로 릴리스된 {{site.data.keyword.amashort}} Swift SDK가 기존 모바일 클라이언트 액세스 Objective-C SDK에서 제공하는 기능에 추가되어 해당 기능을 향상시킵니다. 

**참고:** Objective-C SDK는 그대로 완벽하게 지원되며 여전히 {{site.data.keyword.Bluemix_notm}} 모바일 서비스의 기본 SDK로 간주되지만 새로운 Swift SDK를 위해 올해 말해 중단될 계획입니다. 

## 시작하기 전에
{: #before-you-begin}

사용자 정의 ID 제공자를 사용하도록 구성된 {{site.data.keyword.amashort}} 서비스 인스턴스의 보호를 받는 자원이 있어야 합니다. 또한 모바일 앱이 {{site.data.keyword.amashort}} 클라이언트 SDK로 인스트루먼트되어야 합니다. 자세한 정보는 다음 내용을 참조하십시오. 
 * [{{site.data.keyword.amashort}} 시작하기](https://console.{DomainName}/docs/services/mobileaccess/index.html)
 * [iOS Swift SDK 설정](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html)
 * [사용자 정의 ID 제공자 사용](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [사용자 정의 ID 제공자 작성](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [사용자 정의 인증용 {{site.data.keyword.amashort}} 구성](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## 사용자 정의 인증용 {{site.data.keyword.amashort}} 구성
 {: #custom-auth-ios-configmca}

 1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 앱을 여십시오. 

 1. **모바일 옵션**을 클릭하고 **라우트**(*applicationRoute*) 및 **앱 GUID**(*applicationGUID*)를 기록해 두십시오. SDK를 초기화하는 경우 이 값이 필요합니다. 

 1. {{site.data.keyword.amashort}} 타일을 클릭하십시오. {{site.data.keyword.amashort}} 대시보드가 로드됩니다. 

 1. **사용자 정의** 타일을 클릭하십시오.

 1. **영역 이름**에 사용자 정의 인증 영역을 지정하십시오.

 1. **URL**에 applicationRoute를 지정하십시오.

 1. **저장**을 클릭하십시오.




### 클라이언트 SDK 초기화
{: #custom-ios-sdk-initialize}

`applicationRoute` 및 `applicationGUID` 매개변수를 전달하여 SDK를 초기화하십시오. 필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 애플리케이션 위임자의 `application:didFinishLaunchingWithOptions` 메소드입니다. 

1. 애플리케이션 매개변수 값을 가져오십시오. {{site.data.keyword.Bluemix_notm}} 대시보드에서 앱을 여십시오. **모바일 옵션**을 클릭하십시오. `applicationRoute` 및 `applicationGUID` 값이 **라우트** 및 **앱 GUID** 필드에 표시됩니다.

1. {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하려는 클래스에 필수 프레임워크를 가져오십시오.

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
```

1. {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화하고 권한 관리자를 MCAAuthorizationManager로 변경하고 인증 위임을 정의한 후 이를 등록하십시오. `<applicationRoute>` 및 `<applicationGUID>`를 {{site.data.keyword.Bluemix_notm}} 대시보드의 **모바일 옵션**에서 얻은 **라우트** 및 **앱 GUID**의 값으로 바꾸십시오.

   {{site.data.keyword.Bluemix_notm}} 애플리케이션을 호스트하는 지역으로 `<applicationBluemixRegion>`을 바꾸십시오. {{site.data.keyword.Bluemix_notm}} 지역을 보려면 대시보드의 왼쪽 상단 구석에 있는 페이스 아이콘(![Face](/face.png "Face"))을 클릭하십시오.

  `<yourProtectedRealm>`의 경우 {{site.data.keyword.amashort}} 대시보드의 **사용자 정의** 타일에 정의한 **영역 이름**을 사용하십시오.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"
 let customRealm = "<yourProtectedRealm>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<applicationBluemixRegion>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

  //Auth delegate for handling custom challenge
 class MyAuthDelegate : AuthenticationDelegate {
      func onAuthenticationChallengeReceived(authContext: AuthenticationContext, challenge: AnyObject){
          print("onAuthenticationChallengeReceived")
              let answer = <백엔드에서 보낸 인증 확인에 대한 응답([String:AnyObject] 유형이어야 함)>
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

클라이언트 SDK를 초기화하고 사용자 정의 인증 위임을 등록한 후에는 모바일 백엔드 요청을 시작할 수 있습니다.

### 시작하기 전에
{: #custom-ios-testing-before}

{{site.data.keyword.mobilefirstbp}} 표준 유형으로 작성된 애플리케이션과 `/protected` 엔드포인트에서 {{site.data.keyword.amashort}}의 보호를 받는 자원이 있어야 합니다.

1. `{applicationRoute}/protected`(예: `http://my-mobile-backend.mybluemix.net/protected`)를 열어 브라우저에서 모바일 백엔드의 보호 엔드포인트로 요청을 전송하십시오.
  {{site.data.keyword.mobilefirstbp}} 표준 유형으로 작성된 모바일 백엔드의 `/protected` 엔드포인트는 {{site.data.keyword.amashort}}에서 보호됩니다. 이 엔드포인트는 {{site.data.keyword.amashort}} 클라이언트 SDK로 인스트루먼트된 모바일 애플리케이션에서만 액세스할 수 있습니다. 따라서 `Unauthorized` 메시지는 브라우저에 표시됩니다.

1. iOS 애플리케이션을 사용하여 동일한 엔드포인트에 대해 요청을 작성하십시오. `BMSClient`를 초기화한 후 다음 코드를 추가하고 사용자 정의 인증 위임을 등록하십시오.

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

사용자가 로그인한 후에 이 코드를 호출하면 사용자가 로그아웃됩니다. 사용자가 다시 로그인을 시도하는 경우, 사용자는 서버에서 수신된 인증 확인에 다시 응답해야 합니다.

 로그아웃 기능에 `callBack` 전달은 선택사항입니다. `nil`을 전달할 수도 있습니다. 
