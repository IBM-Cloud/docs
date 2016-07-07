---

copyright:
  years: 2016

---
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# iOS Swift SDK 설정
{: #getting-started-ios}

*마지막 업데이트 날짜: 2016년 6월 14일*
{: .last-updated}

모바일 클라이언트 액세스에서 기존 모바일 클라이언트 액세스 Objective-C SDK에서 제공하는 기능에 추가되어 해당 기능을 향상시키는 새로운 Swift SDK를 릴리스했으므로, 더 쉽게 앱을 인증할 수 있으며 백엔드 자원의 보호가 향상됩니다.
{{site.data.keyword.amashort}} SDK를 사용하여 iOS Swift 애플리케이션을 인스트루먼테이션하고, SDK를 초기화하며 보호 및 비보호 자원에 대한 요청을 작성하십시오. {:shortdesc}

**참고:** Objective-C SDK에서는 모바일 클라이언트 액세스 서비스의 모니터링 콘솔에 모니터링 데이터를 보고합니다. 모바일 클라이언트 액세스 서비스의 모니터링 기능을 사용하는 경우 계속 Objective-C SDK를 사용해야 합니다.

**참고:** Objective-C SDK는 그대로 완벽하게 지원되며 여전히 {{site.data.keyword.Bluemix_notm}} 모바일 서비스의 기본 SDK로 간주되지만 새로운 Swift SDK를 위해 올해 말해 중단될 계획입니다.  






## 시작하기 전에
{: #before-you-begin}
다음이 있어야 합니다.
* {{site.data.keyword.amashort}} 서비스를 통해 보호하는 {{site.data.keyword.Bluemix_notm}} 애플리케이션의 인스턴스입니다. {{site.data.keyword.Bluemix_notm}} 백엔드 작성 방법에 대한 자세한 정보는 [시작하기](index.html)를 참조하십시오.  
* Xcode 프로젝트. iOS 개발 환경을 설정하는 방법에 대한 자세한 정보는 [Apple 개발자 웹 사이트](https://developer.apple.com/support/xcode/)를 참조하십시오. 


## {{site.data.keyword.amashort}} 클라이언트 SDK 설치
{: #install-mca-sdk-ios}
{{site.data.keyword.amashort}} SDK는 iOS 프로젝트용 종속성 관리자인 CocoaPods를 사용하여 분배됩니다. CocoaPods는 저장소에서 아티팩트를 자동으로 다운로드하고 iOS 애플리케이션에서 아티팩트를 사용할 수 있게 합니다. 


### CocoaPods 설치
{: #install-cocoapods}
1. 터미널을 열고 **pod --version** 명령을 실행하십시오. 이미 CocoaPods가 설치되어 있는 경우 버전 번호가 표시됩니다. SDK를 설치하기 위해 다음 섹션으로 건너뛸 수 있습니다. 

1. CocoaPods가 설치되어 있지 않은 경우에는 다음을 실행하십시오. 
```
sudo gem install cocoapods
```
자세한 정보는 [CocoaPods 웹 사이트](https://cocoapods.org/)를 참조하십시오.

### CocoaPods를 사용하여 {{site.data.keyword.amashort}} 클라이언트 SDK 설치
{: #install-sdk-cocoapods}

1. 터미널 창에서 iOS 프로젝트의 루트 디렉토리로 이동하십시오. 

1. 이미 CocoaPods에 대한 작업공간을 초기화하지 않은 경우 `pod init` 명령을 실행하십시오. <br/>
CocoaPods가 `Podfile` 파일을 작성하고 이 파일에서 사용자는 iOS 프로젝트용 종속성을 정의합니다. 

1. `Podfile` 파일을 편집하고 필요한 대상에 다음 행을 추가하십시오. 

	```
  use_frameworks!
  pod 'BMSSecurity'
	```
  **팁:** `use_frameworks!`를 Podfile에 삽입하는 대신 Xcode 대상에 추가할 수 있습니다.

1. `Podfile` 파일을 저장하고 명령행에서 `pod install`을 실행하십시오. <br/>Cocoapods에서 적절한 종속성을 설치하고 추가된 종속성과 pods를 표시합니다.<br/>
**중요**: CocoaPods에서 `xcworkspace` 파일을 생성합니다. 앞으로 프로젝트에 대해 작업하려면 이 파일을 열어야 합니다. 

1. iOS 프로젝트 작업공간을 여십시오. CocoaPods에서 생성한 `xcworkspace` 파일을 여십시오. 예: `{your-project-name}.xcworkspace`. `open {your-project-name}.xcworkspace`를 실행하십시오. 

## {{site.data.keyword.amashort}} 클라이언트 SDK 초기화
{: #init-mca-sdk-ios}

 `applicationRoute` 및 `applicationGUID` 매개변수를 전달하여 SDK를 초기화하십시오. 필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 애플리케이션 위임자의 `application:didFinishLaunchingWithOptions` 메소드입니다. 

1. 애플리케이션 매개변수 값을 가져오십시오. {{site.data.keyword.Bluemix_notm}} 대시보드에서 앱을 여십시오. **모바일 옵션**을 클릭하십시오. `applicationRoute` 및 `applicationGUID` 값이 **라우트** 및 **앱 GUID** 필드에 표시됩니다.

1. {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하려는 클래스에 필수 프레임워크를 가져오십시오.

 ```Swift
 import BMSCore
 import BMSSecurity
 ```  

1. {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화하십시오. `<applicationRoute>` 및 `<applicationGUID>`를 {{site.data.keyword.Bluemix_notm}} 대시보드의 **모바일 옵션**에서 얻은 **라우트** 및 **앱 GUID**의 값으로 바꾸십시오. {{site.data.keyword.Bluemix_notm}} 애플리케이션을 호스트하는 지역으로 `<applicationBluemixRegion>`을 바꾸십시오. {{site.data.keyword.Bluemix_notm}} 지역을 보려면 대시보드의 왼쪽 상단 구석에 있는 페이스 아이콘(![Face](/face.png "Face"))을 클릭하십시오.   


 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 // Initialize the client SDK.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<applicationBluemixRegion>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 return true
 }
 ```

## 모바일 백엔드 요청
{: #request}

{{site.data.keyword.amashort}} 클라이언트 SDK가 초기화되면 모바일 백엔드 요청을 시작할 수 있습니다. 

1. 브라우저에서 모바일 백엔드의 보호 엔드포인트에 요청을 전송하십시오. URL `{applicationRoute}/protected`를 여십시오. (예: `http://my-mobile-backend.mybluemix.net/protected`)
<br/>MobileFirst Services Starter 표준 유형으로 작성된 모바일 백엔드의 `/protected` 엔드포인트는 {{site.data.keyword.amashort}}에서 보호됩니다. 이 엔드포인트는 {{site.data.keyword.amashort}} 클라이언트 SDK로 인스트루먼트된 모바일 애플리케이션에서만 액세스될 수 있으므로 브라우저에 `Unauthorized` 메시지가 리턴됩니다.

1. iOS 애플리케이션을 사용하여 동일한 엔드포인트에 대해 요청을 작성하십시오. `BMSClient`를 초기화한 후에 다음 코드를 추가하십시오. 

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

1.  요청에 성공하는 경우 Xcode 콘솔에 다음 출력이 표시됩니다. 

 ```
 response:Optional("Hello, this is a protected resouce of the mobile backend application!"), no error
 ```
{: screen}
 
## 다음 단계
{: #next-steps}
보호 엔드포인트에 연결된 경우 신임 정보는 필요하지 않습니다. 사용자가 애플리케이션에 로그인하게 하려면 Facebook, Google 또는 사용자 정의 인증을 구성해야 합니다. 
  * [Facebook](facebook-auth-ios-swift-sdk.html)
  * [Google](google-auth-ios-swift-sdk.html)
  * [사용자 정의](custom-auth-ios-swift-sdk.html)
