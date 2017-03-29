---

copyright:
  years: 2017
  lastupdated: "2017-03-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:pre: .pre}


# 設定 iOS Swift SDK
{: #getting-started-ios}

使用 {{site.data.keyword.appid_short}} 用戶端 SDK 建置 Swift 應用程式、起始設定 SDK、鑑別使用者，以及對受保護資源及未受保護資源提出要求。
{:shortdesc}


## 開始之前
{: #before-you-begin}

您需要下列資訊：
  * {{site.data.keyword.appid_short_notm}} 的實例。
  * 您的承租戶 ID。
    * 在服務儀表板的**服務認證**標籤中，按一下**檢視認證**。您的「承租戶 ID」會顯示在 **TenantID** 欄位中。此值用於起始設定應用程式。
  * 您的 {{site.data.keyword.Bluemix_notm}} 地區。
  您可以在使用者介面中尋找，以找到您的地區。此值用於起始設定應用程式。
    <table> <caption> 表 1. {{site.data.keyword.Bluemix_notm}} 地區及對應的 SDK 值</caption>
    <tr>
      <th> Bluemix 地區</th>
      <th> SDK 值</th>
    </tr>
    <tr>
      <td> 美國南部</td>
      <td> BMSClient.Region.usSouth </td>
    </tr>
    <tr>
      <td> 雪梨</td>
      <td> BMSClient.Region.sydney </td>
    </tr>
    <tr>
      <td> 英國</td>
      <td> BMSClient.Region.unitedKingdom </td>
    </tr>
  </table>

  * Xcode 專案（8.1 版或更新版本）。
  * CocoaPods（1.1.0 版或更新版本）。


## 安裝 {{site.data.keyword.appid_short_notm}} 用戶端 SDK
{: #install-appid-sdk}

{{site.data.keyword.appid_short_notm}} 用戶端 SDK 是使用 CocoaPods（Swift 及 Objective-C Cocoa 專案的相依關係管理程式）進行配送。CocoaPods 會下載構件，並讓它們可供您的專案使用。

1. 建立 Xcode 專案，或開啟現有專案。
2. 在專案的目錄中，開啟或建立 Podfile。
3. 在專案的目標下，新增 'BluemixAppID' 欄的相依關係。請確定，您的目標下也有 `use_frameworks!` 指令。
  例如：

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'BluemixAppID'
  end
  ```
  {:pre}

4. 若要下載 `BluemixAppID` 相依關係，請執行下列指令：

  ```swift
  pod install --repo-update
  ```
  {:pre}

6. 開啟 Xcode 專案，並啟用金鑰鏈共用。在**專案設定**下，按一下**功能** > **金鑰鏈共用**。
7. 在**專案設定** > **資訊** > **URL 類型**下，新增「URL 類型」。請將下列值填入 **ID** 文字框及 **URL 架構**文字框：$(PRODUCT_BUNDLE_IDENTIFIER)


## 起始設定 {{site.data.keyword.appid_short_notm}} 用戶端 SDK
{: #initialize-client-sdk}

1. 將下列 import 新增至 AppDelegate.swift 檔案：

  ```swift
  import BluemixAppID
  ```
  {:pre}

2. 將承租戶 ID 及地區參數傳遞給起始設定方法，以起始設定用戶端 SDK。放置起始設定碼的一般（但非強制）位置是在 Swift 應用程式中 AppDelegate 的 application:didFinishLaunchingWithOptions: 方法。

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.<region>)
  ```
  {:pre}

  * 將 tenantId 取代為「應用程式 ID」服務的承租戶 ID。
  * 將 region 取代為您的 {{site.data.keyword.appid_short_notm}} 地區。

3. 將下列程式碼新增至 AppDelegate 檔案。

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {:pre}

## 使用登入小組件鑑別使用者
{: #authenticate-login}

起始設定 {{site.data.keyword.appid_short_notm}} 用戶端 SDK 之後，即可執行登入小組件來鑑別使用者。登入小組件預設配置會使用 Facebook 及（或）Google 作為鑑別選項。如果您只配置其中一個，不會啟動登入小組件，並且會將使用者重新導向至已配置的 IDP 鑑別畫面。



1. 將下列 import 新增至您要在其中使用 SDK 的檔案。

  ```swift
  import BluemixAppID
  ```
  {:pre}

2. 執行下列指令，以啟動小組件。

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

## 存取使用者屬性
{: #accessing}

取得存取記號時，即可存取使用者保護的屬性端點。使用下列 API 方法，即可完成這項作業：

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

若未明確地傳遞存取記號，{{site.data.keyword.appid_short_notm}} 會使用最後一個收到的記號。

例如，您可以呼叫此程式碼來設定新屬性，或置換現有屬性：

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


### 匿名登入
{: #anonymous notoc}

使用 {{site.data.keyword.appid_short_notm}}，您可以匿名登入，請參閱[匿名身分](/docs/services/appid/user-profile.html#anonymous)。

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

### 漸進鑑別
{: #progressive notoc}

當您保留匿名存取記號時，使用者可以變成已識別的使用者，方法是將它傳遞給 loginWidget.launch 方法：

  ```
  func launch(accessTokenString: String? , delegate: AuthorizationDelegate)
  ```
  {:pre}

匿名登入之後，即使因服務已使用最後一個收到的記號而在未傳遞存取記號的情況下呼叫登入小組件，還是會進行漸進鑑別。如果您要清除儲存的記號，請執行下列指令：

  ```
  var appIDAuthorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)
  appIDAuthorizationManager.clearAuthorizationData()
  ```
  {:pre}



## 後續步驟
{: #next-steps}

{{site.data.keyword.appid_short_notm}} 會在您一開始設定身分提供者時提供預設配置。您只能在開發模式中使用預設配置。發佈應用程式之前，請將預設 [Facebook](/docs/services/appid/identity-providers.html#facebook) 及 [Google](/docs/services/appid/identity-providers.html#google) 配置更新為您自己的認證。
