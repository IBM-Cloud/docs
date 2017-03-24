---

copyright:
  years: 2017
  lastupdated: "2017-03-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:pre: .pre}


# iOS Swift SDK 설정
{: #getting-started-ios}

{{site.data.keyword.appid_short}} 클라이언트 SDK를 사용하여 Swift 애플리케이션을 빌드하고, SDK를 초기화하고, 사용자를 인증하고, 보호 및 비보호 리소스를 요청하십시오.
{:shortdesc}


## 시작하기 전에
{: #before-you-begin}

다음 정보가 필요합니다.
  * {{site.data.keyword.appid_short_notm}}의 인스턴스. 
  * 테넌트 ID.
    * 서비스 대시보드의 **서비스 신임 정보** 탭에서 **신임 정보 보기**를 클릭하십시오. 테넌트 ID가 **테넌트 ID** 필드에 표시됩니다. 이 값은 앱을 초기화하는 데 사용됩니다.
  * {{site.data.keyword.Bluemix_notm}} 지역.
  UI에서 보고 지역을 찾을 수 있습니다. 이 값은 앱을 초기화하는 데 사용됩니다.
<table> <caption> 표 1. {{site.data.keyword.Bluemix_notm}} 지역 및 해당 SDK 값 </caption>
    <tr>
      <th> Bluemix 지역 </th>
      <th> SDK 값 </th>
    </tr>
    <tr>
      <td> 미국 남부</td>
      <td> BMSClient.Region.usSouth </td>
    </tr>
    <tr>
      <td> 시드니</td>
      <td> BMSClient.Region.sydney </td>
    </tr>
    <tr>
      <td> 영국</td>
      <td> BMSClient.Region.unitedKingdom </td>
    </tr>
  </table>

  * Xcode 프로젝트(버전 8.1 이상).
  * CocoaPods(버전 1.1.0 이상).


## {{site.data.keyword.appid_short_notm}} 클라이언트 SDK 설치
{: #install-appid-sdk}

{{site.data.keyword.appid_short_notm}} 클라이언트 SDK는 Swift 및 Objective-C Cocoa 프로젝트의 종속성 관리자인 CocoaPods를 사용하여 분배됩니다. CocoaPods는 아티팩트를 다운로드하고 프로젝트에서 아티팩트를 사용할 수 있게 합니다. 

1. Xcode 프로젝트를 작성하거나 기존 프로젝트를 여십시오. 
2. 프로젝트의 디렉토리에서 Podfile을 열거나 작성하십시오.
3. 프로젝트의 대상 아래에 'BluemixAppID' 팟(pod)에 대한 종속성을 추가하십시오. `use_frameworks!` 명령도 대상 아래에 있는지 확인하십시오.
  예를 들면 다음과 같습니다. 

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'BluemixAppID'
  end
  ```
  {:pre}

4. `BluemixAppID` 종속성을 다운로드하려면 다음 명령을 실행하십시오. 

  ```swift
  pod install --repo-update
  ```
  {:pre}

6. Xcode 프로젝트를 열고 키 체인 공유를 사용 설정하십시오. **프로젝트 설정** 아래에서 **기능** > **키 체인 공유**를 클릭하십시오.
7. **프로젝트 설정** > **정보** > **URL 유형** 아래에 URL 유형을 추가하십시오. **ID** 텍스트 상자 및 **URL 체계** 텍스트 상자를 모두 $(PRODUCT_BUNDLE_IDENTIFIER) 값으로 채우십시오. 


## {{site.data.keyword.appid_short_notm}} 클라이언트 SDK 초기화
{: #initialize-client-sdk}

1. AppDelegate.swift 파일에 다음과 같이 가져오기를 추가하십시오. 

  ```swift
  import BluemixAppID
  ```
  {:pre}

2. initialize 메소드에 테넌트 ID 및 지역 매개변수를 전달하여 클라이언트 SDK를 초기화하십시오. 필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 application:didFinishLaunchingWithOptions: Swift 애플리케이션에서 AppDelegate의 메소드에 있습니다. 

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.<region>)
  ```
  {:pre}

  * tenantId를 사용자의 App ID 서비스에 대한 테넌트 ID로 바꾸십시오.
  * region을 사용자의 {{site.data.keyword.appid_short_notm}} 지역으로 바꾸십시오.

3. AppDelegate 파일에 다음 코드를 추가하십시오. 

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {;pre}

## 로그인 위젯을 사용하여 사용자 인증
{: #authenticate-login}

{{site.data.keyword.appid_short_notm}} 클라이언트 SDK가 초기화된 후에 로그인 위젯을 실행하여 사용자를 인증할 수 있습니다. 로그인 위젯 기본 구성에서는 인증 옵션으로 Facebook, Google 또는 둘 다 사용합니다. 그 중에서 하나만 구성하는 경우에는 로그인 위젯이 실행되지 않으며 구성된 IDP 인증 화면으로 사용자가 경로 재지정됩니다. 



1. SDK를 사용하려는 파일에 다음 가져오기를 추가하십시오.

  ```swift
  import BluemixAppID
  ```
  {:pre}

2. 다음 명령을 실행하여 위젯을 시작하십시오. 

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //User authenticated
      }

      public func onAuthorizationCanceled() {
          //Authentication canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Exception occurred
      }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {:pre}

## 사용자 속성 액세스
{: #accessing}

액세스 토큰을 확보할 때 사용자 보호 속성 엔드포인트에 대한 액세스 권한을 얻을 수 있습니다. 이는 다음과 같은 API 메소드를 사용하여 수행됩니다. 

  ```
  func setAttribute(key: String, value: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func setAttribute(key: String, value: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttributes(completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttributes(accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func deleteAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func deleteAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  ```
  {:pre}

액세스 토큰이 명시적으로 전달되지 않을 때 {{site.data.keyword.appid_short_notm}}는 마지막으로 수신된 토큰을 사용합니다. 

예를 들어, 이 코드를 호출하여 새 속성을 설정하거나 기존 속성을 대체할 수 있습니다. 

  ```
  AppID.sharedInstance.userAttributeManager?.setAttribute("key", "value", completionHandler: { (error, result) in
      if error = nil {
          //Attributes recieved as a Dictionary
      } else {
          // An error has occurred
      }
  })
  ```
  {:pre}


### 익명 로그인
{: #anonymous notoc}

{{site.data.keyword.appid_short_notm}}로 익명으로 로그인할 수 있습니다. [익명 ID](/docs/services/appid/user-profile.html#anonymous)를 참조하십시오. 

  ```
  class delegate : AuthorizationDelegate {

      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //User authenticated
      }

      public func onAuthorizationCanceled() {
          //Authentication canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Error occurred
      }
   }

  AppID.sharedInstance.loginAnonymously( authorizationDelegate: delegate())`
  ```
  {:pre}

### 점진적 인증
{: #progressive notoc}

익명 액세스 토큰을 보유하고 있는 경우 사용자는 해당 토큰을 loginWidget.launch 메소드에 전달하여 식별된 사용자가 될 수 있습니다. 

  ```
  func launch(accessTokenString: String? , delegate: AuthorizationDelegate)
  ```
  {:pre}

익명 로그인 후에는 서비스가 마지막으로 수신된 토큰을 사용했기 때문에 액세스 토큰을 전달하지 않고 로그인 위젯이 호출되는 경우에도 점진적 인증이 발생합니다. 저장된 토큰을 지우려면 다음 명령을 실행하십시오.

  ```
  var appIDAuthorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)
  appIDAuthorizationManager.clearAuthorizationData()
  ```
  {:pre}



## 다음 단계
{: #next-steps}

{{site.data.keyword.appid_short_notm}}는 ID 제공자를 처음 설정할 때 기본 구성을 제공합니다. 개발 모드에서만 기본 구성을 사용할 수 있습니다. 애플리케이션을 공개하기 전에 기본 [Facebook](/docs/services/appid/identity-providers.html#facebook) 및 [Google](/docs/services/appid/identity-providers.html#google) 구성을 사용자 자신의 신임 정보에 업데이트하십시오.
