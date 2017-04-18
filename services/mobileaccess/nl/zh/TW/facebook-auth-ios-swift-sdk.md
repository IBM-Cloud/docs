---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

**重要事項：{{site.data.keyword.amafull}} 服務取代為 {{site.data.keyword.appid_full}} 服務。**

# 啟用 iOS 應用程式的 Facebook 鑑別 (Swift SDK)
{: #facebook-auth-ios}

若要使用 Facebook 作為 {{site.data.keyword.amafull}} iOS 應用程式中的身分提供者，請針對 Facebook 應用程式新增及配置 iOS 平台。
{: shortdesc}

## 開始之前
{: #before-you-begin}

您必須具有：

* {{site.data.keyword.amafull}} 服務實例和 {{site.data.keyword.Bluemix_notm}} 應用程式。如需如何建立 {{site.data.keyword.Bluemix_notm}} 後端應用程式的相關資訊，請參閱[開始使用](index.html)。
* 後端應用程式的 URL（**應用程式路徑**）。在傳送要求至後端應用程式的受保護端點時，將需要此值。
* **承租戶 ID** 值。在 {{site.data.keyword.amashort}} 儀表板中，開啟服務。按一下**行動選項**按鈕。`tenantId`（也稱為 `appGUID`）值會顯示在**應用程式 GUID/承租戶 ID** 欄位中。您需要此值來起始設定「授權管理程式」。
* {{site.data.keyword.Bluemix_notm}} **地區**。您可以在標頭中找到您目前的 {{site.data.keyword.Bluemix_notm}} 地區，就在**虛擬人像**圖示 ![「虛擬人像」圖示](images/face.jpg "「虛擬人像」圖示") 的旁邊。出現的地區值應該是下列其中一項：`美國南部`、`英國`或`雪梨`，並對應至 Swift SDK 所需的 SDK 值：`BMSClient.Region.usSouth`、`BMSClient.Region.unitedKingdom` 或 `BMSClient.Region.sydney`。您需要此值來起始設定 {{site.data.keyword.amashort}} 用戶端。
* 設定成使用 CocoaPods 的 iOS 專案。如需相關資訊，請參閱[設定 iOS Swift SDK](getting-started-ios-swift-sdk.html) 中的**安裝 CocoaPods**。  
   **附註：**您不需要安裝核心 {{site.data.keyword.amashort}} 用戶端 SDK，即可繼續進行。
* [Facebook for Developers ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developers.facebook.com){: new_window} 網站上的 Facebook 應用程式。

**重要事項：**您不需要個別安裝 Facebook SDK (`com.facebook.FacebookSdk`)。{{site.data.keyword.amashort}} `BMSFacebookAuthentication` Pod 會自動安裝 Facebook SDK。在 Facebook for Developers 網站上新增或配置應用程式時，可跳過**將 Facebook SDK 新增至 Xcode 專案**步驟。

## 針對 iOS 平台配置 Facebook 應用程式
{: #facebook-auth-ios-config}

在 Facebook for Developers 網站上，執行下列動作：

1. 在 [Facebook for Developers ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developers.facebook.com){: new_window} 上登入您的帳戶。

1. 確保 iOS 平台已新增至您的應用程式。在新增或配置 iOS 平台時，您需要提供 iOS 應用程式的 **bundleId**。若要尋找 iOS 應用程式的 **bundleId**，請在 `info.plist` 檔案或 Xcode 專案**一般**標籤中尋找**軟體組 ID**。

  **提示**：如果您計劃使用「URL 架構字尾」或「單一登入」，則請考慮啟用這些特性。

1. 按一下**儲存設定**。

## 配置 {{site.data.keyword.amashort}} 進行 Facebook 鑑別
{: #facebook-auth-ios-configmca}

配置「Facebook 應用程式 ID」和「Facebook 應用程式」來服務 iOS 用戶端之後，即可在 {{site.data.keyword.amashort}} 服務中啟用 Facebook 鑑別。

1. 在 {{site.data.keyword.amashort}} 儀表板中，開啟服務。
1. 在**管理**標籤中，將**授權**切換為開啟。
1. 展開 **Facebook** 區段。
1. 新增 **Facebook 應用程式 ID**，然後按一下**儲存**。

## 配置適用於 iOS 的 {{site.data.keyword.amashort}} 用戶端 SDK
{: #facebook-auth-ios-sdk}

### 安裝 CocoaPods
{: #install-cocoapods}

1. 開啟「終端機」，並執行 **pod --version** 指令。如果已安裝 CocoaPods，則會顯示版本號碼。您可以跳到下一節來安裝 SDK。

1. 如果您未安裝 CocoaPods，請執行：

   ```
   sudo gem install cocoapods
   ```
   {: codeblock}

如需相關資訊，請參閱 [CocoaPods 網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cocoapods.org/){: new_window}。

### 使用 CocoaPods 安裝 {{site.data.keyword.amashort}} 用戶端 Swift SDK
{: #facebook-auth-install-swift-cocoapods}

1. 如果您的 iOS 專案中沒有 `Podfile`，請執行 `pod init` 來建立檔案。

1. 編輯 `Podfile`，並新增下列幾行：

   ```
   use_frameworks!
   pod 'BMSFacebookAuthentication'
   ```
   {: codeblock}

   **附註：**如果您在 Podfile 中有 `pod 'BMSSecurity'` 這一行，則必須先移除它。`BMSFacebookAuthentication` Pod 會安裝所有必要的架構。

   **提示：**您可以將 `use_frameworks!` 新增至 Xcode 目標，而不是將它置於 Podfile。

1. 儲存 `Podfile`，並從指令行執行 `pod install` 指令。CocoaPods 將安裝相依關係。即會顯示進度及新增的元件。

   **重要事項**：您現在必須使用 CocoaPods 所產生的 `xcworkspace` 檔案來開啟專案。名稱通常為 `{your-project-name}.xcworkspace`。  

1. 從指令行執行 `open {your-project-name}.xcworkspace`，以開啟您的 iOS 專案工作區。

### 針對 iOS 啟用金鑰鏈共用
{: #enable_keychain}

啟用 `Keychain Sharing`。移至 `Capabilities` 標籤，並將 Xcode 專案中的 `Keychain Sharing` 切換為 `On`。

### 配置 iOS 專案進行 Facebook 鑑別
{: #facebook-auth-ios-configproject}

1. 尋找 `info.plist` 檔案（通常位於 Xcode 專案的 `Supporting files` 資料夾下）。

1. 將下列內容新增至 `info.plist` 檔案，以配置 Facebook 整合：

   ![影像](images/ios-facebook-infoplist-settings.png)

   使用「Facebook 應用程式 ID」更新 URL 架構及 FacebookAppID 內容。

   您也可以在檔案上按一下滑鼠右鍵，並選取**開啟為 > 原始碼**，然後新增下列 XML，以更新 `info.plist` 檔案：

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
   {: codeblock}

   使用「Facebook 應用程式 ID」更新 `CFBundleURLSchemes` 及 `FacebookappID` 內容。使用 Facebook 應用程式的名稱更新 `FacebookDisplayName`。

   **重要事項**：請確定您未置換 `info.plist` 檔案中的任何現有內容。如果您具有重疊的內容，則必須手動進行合併。如需相關資訊，請參閱[設定 Xcode 專案 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developers.facebook.com/docs/ios/getting-started/){: new_window} 及[讓應用程式在 iOS9 環境下運作無礙 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developers.facebook.com/docs/ios/ios9){: new_window}。

## 起始設定 {{site.data.keyword.amashort}} 用戶端 Swift SDK
{: #facebook-auth-ios-initalize-swift}

傳遞 `tenantId`，以起始設定用戶端 SDK。

放置起始設定碼的一般（但非強制）位置是在應用程式委派的 `application:didFinishLaunchingWithOptions` 方法。

1. 新增下列標頭，在您要使用 {{site.data.keyword.amashort}} 用戶端 SDK 的類別中匯入必要架構：

   ```swift
   import UIKit
   import BMSCore
   import BMSSecurity
   ```
   {: codeblock}

1. 起始設定用戶端 SDK。

   ```Swift
   let tenantId = "<serviceTenantID>"
   let regionName = <applicationBluemixRegion>

   func application(_ application: UIApplication,
      didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
      let mcaAuthManager = MCAAuthorizationManager.sharedInstance
      mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
      //the regionName should be one of the following: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney
      BMSClient.sharedInstance.authorizationManager = mcaAuthManager
      FacebookAuthenticationManager.sharedInstance.register()
   }
   ```
   {: codeblock}

   在程式碼中：

   * 將 `<applicationBluemixRegion>` 取代為管理您 {{site.data.keyword.Bluemix_notm}} 應用程式的地區。
   * 將 `tenantId` 取代為**承租戶 ID/應用程式 GUID** 值。

   如需這些值的相關資訊，請參閱[開始之前](#before-you-begin)。

1. 將下列程式碼新增至應用程式委派中的 `application:didFinishLaunchingWithOptions` 方法，以通知 Facebook SDK 有關應用程式啟動的資訊，並登錄「Facebook 鑑別處理程式」。在起始設定 BMSClient 實例之後新增此程式碼，並將 Facebook 登錄為鑑別管理程式。

   ```Swift
   return FacebookAuthenticationManager.sharedInstance.onFinishLaunching(application, withOptions: launchOptions)
   ```
   {: codeblock}

1. 將 `FacebookAuthenticationManager.swift` 檔案從 `BMSFacebookAuthentication` pod 原始檔複製到您的專案目錄。

1. 將下列程式碼新增至應用程式委派。

   ```Swift
   func application(_ app: UIApplication,
      open url: URL,
      options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool{
         return FacebookAuthenticationManager.sharedInstance.onOpenURL(app, open: url, options: options)
      }
   ```
   {: codeblock}

## 測試鑑別
{: #facebook-auth-ios-testing}

起始設定用戶端 SDK 並登錄「Facebook 鑑別管理程式」之後，即可開始對行動後端應用程式提出要求。

### 開始之前
{: #facebook-auth-ios-testing-before}

您必須使用 {{site.data.keyword.mobilefirstbp}} 樣板，並且在 `/protected` 端點已具有 {{site.data.keyword.amashort}} 所保護的資源。如果您需要設定 `/protected` 端點，請參閱[保護資源](protecting-resources.html)。

1. 嘗試在瀏覽器中將要求傳送給新建的行動後端應用程式的受保護端點。開啟下列 URL：`{applicationRoute}/protected`，並將 `{applicationRoute}` 取代為從**行動選項**中擷取的值（請參閱[配置 Mobile Client Access 進行 Facebook 鑑別](#facebook-auth-ios-configmca)）。
例如：`http://my-mobile-backend.mybluemix.net/protected`。
<br/>使用 MobileFirst Services Starter 樣板所建立之行動後端應用程式的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護。瀏覽器中會傳回 `Unauthorized` 訊息。傳回此訊息的原因是只有使用 {{site.data.keyword.amashort}} 用戶端 SDK 所檢測的行動應用程式才能存取這個端點。

1. 使用 iOS 應用程式以對相同的端點提出要求。

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

1. 執行您的應用程式。即會蹦現 Facebook 登入畫面。

   ![影像](images/ios-facebook-login.png)

   如果您目前並未登入 Facebook，則此畫面可能會稍微不同。

1. 按一下**確定**，以授權 {{site.data.keyword.amashort}} 使用您的 Facebook 使用者身分來進行鑑別。

1. 	當要求成功時，會在 Xcode 主控台中顯示下列輸出：

   ```
response:Optional("Hello, this is a protected resouce of the mobile backend application!"), no error
 ```
   {: screen}

1. 您也可以新增下列程式碼，來新增登出功能：

   ```
   FacebookAuthenticationManager.sharedInstance.logout(callBack)
   ```
   {: codeblock}

   如果您在使用者使用 Facebook 登入之後呼叫此程式碼，而且使用者嘗試重新登入，則系統會提示他們授權 {{site.data.keyword.amashort}} 使用 Facebook 進行鑑別。

   若要切換使用者，您必須呼叫此程式碼，而且使用者必須在其瀏覽器中登出 Facebook。

   將 `callBack` 傳遞給 logout 函數是選用性的作業。您也可以傳遞 `nil`。
