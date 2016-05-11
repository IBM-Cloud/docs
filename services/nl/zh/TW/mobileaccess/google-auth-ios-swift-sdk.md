---

copyright:
  years: 2016

---

# 在 iOS 應用程式中啟用 Google 鑑別 (Swift SDK)
{: #google-auth-ios}

## 開始之前
{: #google-auth-ios-before}

* 您必須具有 {{site.data.keyword.amashort}} 所保護的資源，以及使用 {{site.data.keyword.amashort}} Client SDK 所檢測的 iOS 專案。如需相關資訊，請參閱[開始使用 {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) 及[設定 iOS Swift SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html)。  
* 使用 {{site.data.keyword.amashort}} Server SDK，手動保護後端應用程式。如需相關資訊，請參閱[保護資源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。

## 準備您的應用程式進行 Google 登入
{: #google-sign-in-ios}

遵循 Google 在 Google 所提供的 [Goolge Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start-integrating) 中提供的指示，來準備您的應用程式進行 Google 登入。下列步驟概述您必須執行以準備應用程式的作業。

1. 為您的應用程式啟用 Google Sign-In for iOS。如需相關資訊，請參閱 [Try Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start?ver=swift)。

1. 取得專案的配置檔 (`GoogleService-Info.plist`)。若要取得此檔案，請參閱[為您的應用程式啟用 Google 服務](https://developers.google.com/mobile/add?platform=ios)。

 **重要事項：**取得 `GoogleService-Info.plist` 檔案時，請開啟它並記下 `CLIENT_ID` 值。您稍後需要此值來配置 {{site.data.keyword.amashort}}。

1. 新增 `GoogleService-Info.plist` 檔案至 Xcode 專案。如需相關資訊，請參閱[新增配置檔至專案](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config)

1. 利用 `REVERSE_CLIENT_ID` 及軟體組 ID 更新 Xcode 專案中的「URL 架構」。如需相關資訊，請參閱[新增 URL 架構至專案](https://developers.google.com/identity/sign-in/ios/start-integrating#add_url_schemes_to_your_project)。

1. 利用下列程式碼更新應用程式的 project-Bridging-Header.h 檔案：

 ```
 #import <Google/SignIn.h>
 ```

 如需更新橋接標頭檔的相關資訊，請參閱[啟用登入](https://developers.google.com/identity/sign-in/ios/sign-in#enable_sign-in)中的步驟 1。

## 配置 {{site.data.keyword.amashort}} 進行 Google 鑑別
{: #google-auth-ios-config}

現在，您有「iOS 用戶端 ID」，可以在 {{site.data.keyword.Bluemix}} 儀表板中啟用 Google 鑑別。

1. 在 {{site.data.keyword.Bluemix_notm}} 儀表板中開啟應用程式。

1. 按一下**行動式選項**，並記下**路徑** (*applicationRoute*) 及 **應用程式 GUID** (*applicationGUID*)。起始設定 SDK 時，您需要這些值。

1. 按一下 {{site.data.keyword.amashort}} 磚。即會載入 {{site.data.keyword.amashort}} 儀表板。

1. 按一下 **Google** 磚。

1. 在 **iOS 的應用程式 ID** 中，從您先前取得的 `GoogleService-Info.plist` 檔案中指定 `CLIENT_ID` 值，然後按一下**儲存**。

## 配置 {{site.data.keyword.amashort}} Client SDK for iOS
{: #google-auth-ios-sdk}

### 安裝 CocoaPods
{: #google-auth-cocoapods}

{{site.data.keyword.amashort}} Client SDK 是使用 CocoaPods（iOS 專案的相依關係管理程式）進行配送。CocoaPods 會從儲存庫中自動下載構件，並使它們可供 iOS 應用程式使用。

1. 開啟「終端機」，並執行 `pod --version` 指令。如果您已經安裝 CocoaPods，則會顯示版本號碼。您可以跳到本指導教學的下一節。

1. 執行 `sudo gem install cocoapods`，以安裝 CocoaPods。如果需要其他指引，請參閱 [CocoaPods 網站](https://cocoapods.org/)。

1. 關閉 XCode。

1. 開啟「終端機」，並 `cd` 至您的專案目錄。

1.  執行 `pod init`。

### 使用 CocoaPods 安裝 {{site.data.keyword.amashort}} Client SWift SDK
{: #google-auth-ios-sdk-cocoapods}

1. 導覽至 iOS 專案。

1. 編輯 `Podfile` 來新增下列這幾行：

 ```
 use_frameworks!
 pod 'BMSGoogleAuthentication'
 ```
 **提示：**您可以將 `use_frameworks!` 新增至 Xcode 目標，而不是將它置於 Podfile。

1. 儲存 `Podfile`，然後從指令行執行 `pod install`。CocoaPods 將安裝相依關係。您會看到進度及新增的元件。

 **重要事項**：您現在必須使用 CocoaPods 所產生的 `xcworkspace` 檔案來開啟專案。名稱通常為 `{your-project-name}.xcworkspace`。  

1. 從指令行執行 `open {your-project-name}.xcworkspace`，以開啟您的 iOS 專案工作區。

1. 將 `GoogleAuthenticationManager.swift` 檔案從 `BMSGoogleAuthentication` pod 原始檔複製到您的專案目錄。

## 起始設定 {{site.data.keyword.amashort}} Client Swift SDK
{: #google-auth-ios-initialize}

若要使用 {{site.data.keyword.amashort}} Client SDK，請傳遞 `applicationGUID` 及 `applicationRoute` 參數來進行起始設定。

放置起始設定碼的一般（但非強制）位置是在應用程式委派的 `application:didFinishLaunchingWithOptions` 方法。

1. 取得應用程式參數值。在 {{site.data.keyword.Bluemix_notm}} 儀表板中開啟應用程式。按一下**行動式選項**。`applicationRoute` 及 `applicationGUID` 值即會顯示在**路徑**及**應用程式 GUID** 欄位中。

1. 在您要使用 {{site.data.keyword.amashort}} Client SDK 的類別中，匯入必要架構。請新增下列標頭：

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```

1. 使用下列程式碼來起始設定 Client SDK。將 `<applicationRoute>` 及 `<applicationGUID>` 取代為您取自 {{site.data.keyword.Bluemix_notm}} 儀表板中**行動式選項**的**路徑**及**應用程式 GUID** 值。

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
      func application(application: UIApplication,
          openURL url: NSURL, sourceApplication: String?, annotation: AnyObject) -> Bool {
             return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, sourceApplication: sourceApplication, annotation: annotation)
      }

 @available(iOS 9.0, *)
 func application(app: UIApplication, openURL url: NSURL, options: [String : AnyObject]) -> Bool {
 return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, options: options)
  }
 ```

## 測試鑑別
{: #google-auth-ios-testing}

起始設定 Client SDK 並登錄「Google 鑑別管理程式」之後，即可開始對行動式後端提出要求。

### 開始之前
{: #google-auth-ios-testing-before}

您必須使用 {{site.data.keyword.mobilefirstbp}} 樣板，並且在 `/protected` 端點已具有 {{site.data.keyword.amashort}} 所保護的資源。如果您需要設定 `/protected` 端點，請參閱[保護資源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。


1. 開啟 `{applicationRoute}/protected`（例如 `http://my-mobile-backend.mybluemix.net/protected`），嘗試在桌面瀏覽器中將要求傳送給行動式後端的受保護端點

1. 使用「MobileFirst Services 樣板」所建立之行動式後端的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護，所以只有使用 {{site.data.keyword.amashort}} Client SDK 所檢測的行動式應用程式才能存取它。因此，您會在桌面瀏覽器中看到 `Unauthorized`。

1. 使用 iOS 應用程式以對相同的端點提出要求。

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

1. 執行您的應用程式。您將看到「Google 登入」蹦現畫面。

 ![影像](images/ios-google-login.png)

1. 當您登入並按一下**確定**時，表示您授權 {{site.data.keyword.amashort}} 使用您的 Google 使用者身分來進行鑑別。

1. 	您的要求應該會成功。您應該會在日誌中看到下列輸出。

 ```
 onAuthenticationSuccess info = Optional({attributes = {};
     deviceId = 105747725068605084657;
     displayName = "donlonqwerty@gmail.com";
     isUserAuthenticated = 1;
     userId = 105747725068605084657;
 })
 response:Optional("Hello, this is a protected resource!"), no error
 ```

1. 您也可以新增下列程式碼，來新增登出功能：

 ```
 GoogleAuthenticationManager.sharedInstance.logout(callBack)
 ```

  如果您在使用者使用 Google 登入之後呼叫此程式碼，而且使用者嘗試重新登入，則系統會提示他們授權 {{site.data.keyword.amashort}} 使用 Google 進行鑑別。此時，使用者可以按一下畫面右上角的使用者名稱來進行選取，並使用另一位使用者來登入。

   將 `callBack` 傳遞給 logout 函數是選用的。您也可以傳遞 `nil`。
