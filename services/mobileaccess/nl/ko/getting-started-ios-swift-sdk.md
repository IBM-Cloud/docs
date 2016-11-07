---

copyright:
  years: 2016
lastupdated: "2016-10-10"
---
{:shortdesc: .shortdesc}
{:screen: .screen}


# iOS Swift SDK 설정
{: #getting-started-ios}

{{site.data.keyword.amafull}}에서 기존 {{site.data.keyword.amashort}} Objective-C SDK에서 제공하는 기능에 추가되어 해당 기능을 향상시키는 새로운 Swift SDK를 릴리스했으며 앱을 더 쉽게 인증할 수 있고 백엔드 리소스에 대한 안전한 보호를 제공합니다. {{site.data.keyword.amashort}} SDK를 사용하여 iOS Swift 애플리케이션을 인스트루먼트하고, SDK를 초기화하며 보호 및 비보호 리소스에 대한 요청을 작성하십시오. 

{:shortdesc}

**참고:** Objective-C SDK는 {{site.data.keyword.amashort}} 서비스의 모니터링 콘솔에 대한 모니터링 데이터를 보고합니다. {{site.data.keyword.amashort}} 서비스의 모니터링 기능을 사용하는 경우 Objective-C SDK를 계속 사용해야 합니다. 

Objective-C SDK는 그대로 완벽하게 지원되며 여전히 {{site.data.keyword.Bluemix_notm}} 모바일 서비스의 기본 SDK로 간주되지만, 이 새로운 Swift SDK를 위해 올해 말에 Objective-C SDK를 중단할 계획입니다.  


## 시작하기 전에
{: #before-you-begin}
다음이 있어야 합니다.
* {{site.data.keyword.amashort}} 서비스를 통해 보호하는 {{site.data.keyword.Bluemix_notm}} 애플리케이션의 인스턴스입니다. {{site.data.keyword.Bluemix_notm}} 백엔드 애플리케이션 작성 방법에 대한 자세한 정보는 [시작하기](index.html)를 참조하십시오.




* Xcode 프로젝트. iOS 개발 환경을 설정하는 방법에 대한 자세한 정보는 [Apple 개발자 웹 사이트](https://developer.apple.com/support/xcode/)를 참조하십시오. 


## {{site.data.keyword.amashort}} 클라이언트 SDK 설치
{: #install-mca-sdk-ios}
{{site.data.keyword.amashort}} SDK는 iOS 프로젝트용 종속성 관리자인 CocoaPods를 사용하여 분배됩니다. CocoaPods는 저장소에서 아티팩트를 자동으로 다운로드하고 iOS 애플리케이션에서 아티팩트를 사용할 수 있게 합니다. 


### CocoaPods 설치
{: #install-cocoapods}

1. 터미널 창에서 **pod --version** 명령을 실행하십시오. 이미 CocoaPods가 설치되어 있는 경우 버전 번호가 표시되고 SDK를 설치하는 다음 섹션으로 건너뛸 수 있습니다. 

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

1. `Podfile` 파일을 저장하고 명령행에서 `pod install`을 실행하십시오. CocoaPods는 관련 종속 항목을 설치하고, 추가된 종속 항목 및 pod을 표시합니다. <br/>

   **중요**: CocoaPods는 `xcworkspace` 파일을 생성합니다. 앞으로 프로젝트에 대해 작업하려면 이 파일을 열어야 합니다. 

1. iOS 프로젝트 작업공간을 여십시오. CocoaPods에서 생성한 `xcworkspace` 파일을 여십시오. 예를 들어, `{your-project-name}.xcworkspace`의 경우 다음을 실행하십시오. 

	`open {your-project-name}.xcworkspace`

## {{site.data.keyword.amashort}} 클라이언트 SDK 초기화
{: #init-mca-sdk-ios}

 `applicationGUID` 매개변수를 전달하여 SDK를 초기화하십시오. 필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 애플리케이션 위임자의 `application:didFinishLaunchingWithOptions` 메소드입니다. 
 

1. 서비스 매개변수 값을 가져오십시오. {{site.data.keyword.Bluemix_notm}} 대시보드에서 서비스를 여십시오. **모바일 옵션**을 클릭하십시오. `applicationRoute` 값과 `tenantId`(`appGUID`라고도 함) 값이 **라우트** 필드와 **앱 GUID/TenantId** 필드에 표시됩니다. 이들 값은 SDK를 초기화하고 백엔드 애플리케이션에 요청을 보내는 데 필요합니다. 

1. {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하려는 클래스에 필수 프레임워크를 가져오십시오.

 ```Swift
 import BMSCore
 import BMSSecurity
 ```

1. {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화하십시오. 

```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

	func application(_ application: UIApplication, 
	    didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {

 let mcaAuthManager = MCAAuthorizationManager.sharedInstance
    mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
      // possible values for regionName: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, BMSClient.Region.sydney
	BMSClient.sharedInstance.authorizationManager = mcaAuthManager	
	return true
	}
 ```

* `tenantId`를 **모바일 옵션**에서 얻은 값으로 바꾸십시오. **1단계**를 참조하십시오. 
*  {{site.data.keyword.Bluemix_notm}} 애플리케이션을 호스트하는 지역으로 `<applicationBluemixRegion>`을 바꾸십시오. {{site.data.keyword.Bluemix_notm}} 지역을 보려면 메뉴 표시줄의 **아바타** 아이콘 ![아바타 아이콘](images/face.jpg "아바타 아이콘")을 클릭하여 **계정 및 지원** 위젯을 여십시오.

표시되는 지역 값은 **미국 남부**, **영국** 또는 **시드니** 중 하나여야 하며 코드 `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` 또는 `BMSClient.Region.sydney`에 필요한 상수 값에 해당해야 합니다. 

   
## 모바일 백엔드 애플리케이션에 대한 요청 작성
{: #request}

{{site.data.keyword.amashort}} 클라이언트 SDK가 설치되고 나면 모바일 백엔드 애플리케이션에 대한 요청 작성을 시작할 수 있습니다. 

1. 브라우저에서 모바일 백엔드 애플리케이션의 보호 엔드포인트에 요청을 전송하십시오. `{applicationRoute}`를 **모바일 옵션**에서 검색한 **applicationRoute** 값으로 바꿔 URL `{applicationRoute}/protected`를 여십시오([Mobile Client Access 클라이언트 SDK 초기화](#init-mca-sdk-ios) 참조). 예를 들면 다음과 같습니다.  

	`http://my-mobile-backend.mybluemix.net/protected
	`

	MobileFirst Services Starter 표준 유형으로 작성된 모바일 백엔드의 `/protected` 엔드포인트는 {{site.data.keyword.amashort}}로 보호됩니다. 이 엔드포인트는 {{site.data.keyword.amashort}} 클라이언트 SDK로 인스트루먼트된 모바일 애플리케이션에서만 액세스될 수 있으므로 브라우저에 `Unauthorized` 메시지가 리턴됩니다.



1. iOS 애플리케이션을 사용하여 동일한 엔드포인트에 대해 요청을 작성하십시오. `BMSClient`를 초기화한 후에 다음 코드를 추가하십시오. 

 ```Swift
	let customResourceURL = "<your protected resource absolute path>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

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

1.  요청에 성공하면 다음 출력이 Xcode 콘솔에 표시됩니다. 

 ```
 response:Optional("Hello, this is a protected resource of the mobile backend application!"), no error
 ```
{: screen}
 
## 다음 단계
{: #next-steps}
보호 엔드포인트에 연결된 경우 신임 정보는 필요하지 않습니다. 사용자가 애플리케이션에 로그인하게 하려면 Facebook, Google 또는 사용자 정의 인증을 구성해야 합니다. 
  * [Facebook](facebook-auth-ios-swift-sdk.html)
  * [Google](google-auth-ios-swift-sdk.html)
  * [사용자 정의](custom-auth-ios-swift-sdk.html)
