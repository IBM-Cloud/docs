---

copyright:
  years: 2016

---

# 在 iOS 應用程式中啟用 Facebook 鑑別 (Swift SDK)
{: #facebook-auth-ios}

若要使用 Facebook 作為 iOS 應用程式中的身分提供者，請針對 Facebook 應用程式新增及配置 iOS 平台。

## 開始之前
{: #facebook-auth-ios-before}

* 您必須具有 {{site.data.keyword.amashort}} 所保護的資源，以及使用 {{site.data.keyword.amashort}} Client SDK 所檢測的 iOS 專案。如需相關資訊，請參閱[開始使用 {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) 及[設定 iOS Swift SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html)。  
* 使用 {{site.data.keyword.amashort}} Server SDK，手動保護後端應用程式。如需相關資訊，請參閱[保護資源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。
* 建立「Facebook 應用程式 ID」。如需相關資訊，請參閱[從 Facebook 開發人員入口網站取得 Facebook 應用程式 ID](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)。

## 配置 iOS 平台的 Facebook 應用程式
{: #facebook-auth-ios-config}

1. 登入 [Facebook 應用程式的儀表板](https://developers.facebook.com/apps/)。

1. 記下應用程式的**應用程式 ID**。當您配置 iOS 專案進行 Facebook 鑑別時，需要此值。

1. 按一下**設定 > 新增平台 > iOS**。

1. 指定 iOS 應用程式的 *bundleId*。若要尋找 iOS 應用程式的 *bundleId*，請在 `info.plist` 檔案或 Xcode 專案**一般**標籤中尋找**軟體組 ID**。
**提示**：如果您計劃使用這些特性，則請考慮啟用「URL 架構字尾」或「單一登入」。

1. 按一下**儲存設定**。

## 配置 {{site.data.keyword.amashort}} 進行 Facebook 鑑別
{: #facebook-auth-ios-configmca}

配置「Facebook 應用程式 ID」及「Facebook 應用程式」來服務 iOS 用戶端之後，即可在 {{site.data.keyword.amashort}} 中啟用 Facebook 鑑別。

1. 在 {{site.data.keyword.Bluemix}} 儀表板中開啟應用程式。

1. 按一下**行動式選項**，並記下**路徑** (*applicationRoute*) 及 **應用程式 GUID** (*applicationGUID*)。起始設定 SDK 時，您需要這些值。

1. 按一下 {{site.data.keyword.amashort}} 磚。即會載入 {{site.data.keyword.amashort}} 儀表板。

1. 按一下 **Facebook** 磚。

1. 指定「Facebook 應用程式 ID」，然後按一下**儲存**。

## 配置 {{site.data.keyword.amashort}} Client SDK for iOS
{: #facebook-auth-ios-sdk}

### 安裝 CocoaPods
{: #facebook-auth-cocoapods}

{{site.data.keyword.amashort}} Client SDK 是使用 CocoaPods（iOS 專案的相依關係管理程式）進行配送。CocoaPods 會從儲存庫中自動下載構件，並使它們可供 iOS 應用程式使用。

1. 開啟「終端機」，並執行 `pod --version` 指令。如果您已經安裝 CocoaPods，則會顯示版本號碼。您可以跳到本指導教學的下一節。

1. 執行 `sudo gem install cocoapods`，以安裝 CocoaPods。如果需要其他指引，請參閱 [CocoaPods 網站](https://cocoapods.org/)。

1. 關閉 XCode。

1. 開啟「終端機」，並 `cd` 至您的專案目錄。

1.  執行 `pod init`。

### 使用 CocoaPods 安裝 {{site.data.keyword.amashort}} Client Swift SDK
{: #facebook-auth-install-swift-cocoapods}

1. 在 iOS 專案中，編輯 `Podfile` 並新增下列這幾行：

 ```
use_frameworks!
pod 'BMSFacebookAuthentication'
	```
 **提示：**您可以將 `use_frameworks!` 新增至 Xcode 目標，而不是將它置於 Podfile。

1. 儲存 `Podfile`，並從指令行執行 `pod install` 指令。CocoaPods 將安裝相依關係。即會顯示進度及新增的元件。

 **重要事項**：您現在必須使用 CocoaPods 所產生的 `xcworkspace` 檔案來開啟專案。名稱通常為 `{your-project-name}.xcworkspace`。  

1. 從指令行執行 `open {your-project-name}.xcworkspace`，以開啟您的 iOS 專案工作區。

### 配置 iOS 專案進行 Facebook 鑑別
{: #facebook-auth-ios-configproject}

1. 尋找 `info.plist` 檔案（通常位於 Xcode 專案的 `Supporting files` 資料夾下）。

1. 將下列內容新增至 `info.plist` 檔案，以配置 Facebook 整合：

   ![影像](images/ios-facebook-infoplist-settings.png)

   使用「Facebook 應用程式 ID」更新 URL 架構及 FacebookappID 內容

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
   使用「Facebook 應用程式 ID」更新 URL 架構及 FacebookappID 內容。將 FacebookDisplayName 更新為 Facebook 應用程式的名稱。

    **重要事項**：請確定您未置換 `info.plist` 檔案中的任何現有內容。如果您具有重疊的內容，則必須手動進行合併。如需相關資訊，請參閱[配置 Xcode 專案](https://developers.facebook.com/docs/ios/getting-started/)及[準備 iOS9 的應用程式](https://developers.facebook.com/docs/ios/ios9)。

## 起始設定 {{site.data.keyword.amashort}} Client Swift SDK
{: #facebook-auth-ios-initalize-swift}

傳遞 `applicationGUID` 及 `applicationRoute` 參數，以起始設定 Client SDK。

放置起始設定碼的一般（但非強制）位置是在應用程式委派的 `application:didFinishLaunchingWithOptions` 方法。

1. 取得應用程式參數值。在 {{site.data.keyword.Bluemix_notm}} 儀表板中開啟應用程式。按一下**行動式選項**。`applicationRoute` 及 `applicationGUID` 值即會顯示在**路徑**及**應用程式 GUID** 欄位中。

1. 新增下列標頭，在您要使用 {{site.data.keyword.amashort}} Client SDK 的類別中匯入必要架構：

 ```swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```
2. 起始設定 Client SDK。將 `<applicationRoute>` 及 `<applicationGUID>` 取代為您取自 {{site.data.keyword.Bluemix_notm}} 儀表板中**行動式選項**的**路徑**及**應用程式 GUID** 值。

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 FacebookAuthenticationManager.sharedInstance.register()
 ```

1. 將下列程式碼新增至應用程式委派中的 `application:didFinishLaunchingWithOptions` 方法，以通知 Facebook SDK 有關應用程式啟動的資訊，並登錄「Facebook 鑑別處理程式」。在起始設定 BMSClient 實例之後立即新增此程式碼，並將 Facebook 登錄為鑑別管理程式。

 ```Swift
  return FacebookAuthenticationManager.sharedInstance.onFinishLaunching(application, withOptions: launchOptions)
 ```

1. 將 `FacebookAuthenticationManager.swift` 檔案從 `BMSFacebookAuthentication` pod 原始檔複製到您的專案目錄。

1. 將下列程式碼新增至應用程式委派。

 ```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		return FacebookAuthenticationManager.sharedInstance.onOpenURL(application, url: url, sourceApplication: sourceApplication, annotation: annotation)

	}
 ```

## 測試鑑別
{: #facebook-auth-ios-testing}

起始設定 Client SDK 並登錄「Facebook 鑑別管理程式」之後，即可開始對行動式後端提出要求。

### 開始之前
{: #facebook-auth-ios-testing-before}

您必須使用 {{site.data.keyword.mobilefirstbp}} 樣板，並且在 `/protected` 端點已具有 {{site.data.keyword.amashort}} 所保護的資源。如果您需要設定 `/protected` 端點，請參閱[保護資源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。

1. 嘗試在瀏覽器中將要求傳送給新建行動式後端的受保護端點。開啟下列 URL：`{applicationRoute}/protected`。
例如：`http://my-mobile-backend.mybluemix.net/protected`。
<br/>使用 MobileFirst Services Starter 樣板所建立之行動式後端的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護。瀏覽器中會傳回 `Unauthorized` 訊息。傳回此訊息的原因是只有使用 {{site.data.keyword.amashort}} Client SDK 所檢測的行動式應用程式才能存取這個端點。

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

1. 執行您的應用程式。即會蹦現 Facebook 登入畫面。

   ![影像](images/ios-facebook-login.png)

   如果您目前並未登入 Facebook，則此畫面可能會稍微不同。

1. 按一下**確定**，以授權 {{site.data.keyword.amashort}} 使用 Facebook 使用者身分來進行鑑別。

1. 	當要求成功時，會在 Xcode 主控台中顯示下列輸出：

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

1. 您也可以新增下列程式碼，來新增登出功能：

 ```
FacebookAuthenticationManager.sharedInstance.logout(callBack)
```

 如果您在使用者使用 Facebook 登入之後呼叫此程式碼，而且使用者嘗試重新登入，則系統會提示他們授權 {{site.data.keyword.amashort}} 使用 Facebook 進行鑑別。

 若要切換使用者，您必須呼叫此程式碼，而且使用者必須在其瀏覽器中登出 Facebook。

 將 ```callBack``` 傳遞給 logout 函數是選用的。您也可以傳遞 `nil`。
