---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 啟用 iOS 應用程式的 Google 鑑別 (Swift SDK)
{: #google-auth-ios}

在 {{site.data.keyword.amafull}} iOS Swift 應用程式上，使用「Google 登入」來鑑別使用者。


## 開始之前
{: #before-you-begin}

您必須具有：

* {{site.data.keyword.amafull}} 服務實例和 {{site.data.keyword.Bluemix_notm}} 應用程式。如需如何建立 {{site.data.keyword.Bluemix_notm}} 後端應用程式的相關資訊，請參閱[開始使用](index.html)。




* 後端應用程式的 URL（**應用程式路徑**）。在傳送要求至後端應用程式的受保護端點時，將需要此值。
* **承租戶 ID** 值。在 {{site.data.keyword.amashort}} 儀表板中，開啟服務。按一下**行動選項**按鈕。`tenantId`（也稱為 `appGUID`）值會顯示在**應用程式 GUID/承租戶 ID** 欄位中。您需要此值來起始設定「授權管理程式」。
* {{site.data.keyword.Bluemix_notm}} **地區**。您可以在標頭中找到您目前的 {{site.data.keyword.Bluemix_notm}} 地區，就在**虛擬人像**圖示 ![「虛擬人像」圖示](images/face.jpg "「虛擬人像」圖示") 的旁邊。出現的地區值應該是下列其中一項：**美國南部**、**英國**或**雪梨**，並對應至程式碼中所需的值：`BMSClient.Region.usSouth`、`BMSClient.Region.unitedKingdom` 或 `BMSClient.Region.sydney`。
* Xcode 中的 iOS 專案。它不需要使用 {{site.data.keyword.amashort}} 用戶端 SDK 進行檢測。  


## 準備您的應用程式進行 Google 登入
{: #google-sign-in-ios}

遵循 Google 在 [Google Sign-In for iOS ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developers.google.com/identity/sign-in/ios/start-integrating "外部鏈結圖示"){: new_window} 中所提供的指示，來準備您的應用程式進行 Google 登入。

此處理程序：

* 在 Google Developers 網站中準備新的專案。
* 建立 `GoogleService-Info.plist` 檔案及 `REVERSE_CLIENT_ID` 值以新增至您的 Xcode 專案，以及
* 建立 **Google 用戶端 ID** 以新增至 {{site.data.keyword.Bluemix_notm}} 後端應用程式。

下列步驟概述準備應用程式所需的作業。

**附註：**不需要新增 Google 登入 CocoaPod。必要的 SDK 是透過 `BMSGoogleAuthentication` CocoaPod 所新增。

1. 從主要目標之**一般**標籤的**身分**區段中，記下 Xcode 專案中的**軟體組 ID**。您需要它才能建立「Google 登入」專案。

1. 在 [Google Developer 網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developers.google.com/mobile/add?platform=ios "外部鏈結圖示"){: new_window} 上，為 Google Sign-In for iOS 建立專案。

1. 將「Google 登入 API」新增至專案。

1. 擷取 `GoogleService-Info.plist`。

   **重要事項：**取得 `GoogleService-Info.plist` 檔案後，請開啟它並記下 `CLIENT_ID` 值。您稍後需要此值，才能配置 {{site.data.keyword.amashort}} 後端應用程式。

1. 新增 `GoogleService-Info.plist` 檔案至 Xcode 專案。如需相關資訊，請參閱[將配置檔新增至您的專案 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config "外部鏈結圖示"){: new_window}。

1. 利用 `REVERSE_CLIENT_ID` 及軟體組 ID 更新 Xcode 專案中的「URL 架構」。如需相關資訊，請參閱[將 URL 架構新增至您的專案 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developers.google.com/identity/sign-in/ios/start-integrating#add_a_url_scheme_to_your_project "外部鏈結圖示"){: new_window}。

1. 以下列程式碼來更新應用程式的 `project-Bridging-Header.h` 檔案：

	```
	#import <Google/SignIn.h>
	```
	{: codeblock}

	如需更新橋接標頭檔的相關資訊，請參閱[啟用登入 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developers.google.com/identity/sign-in/ios/sign-in#enable_sign-in "外部鏈結圖示"){: new_window}。

## 配置 {{site.data.keyword.amashort}} 進行 Google 鑑別
{: #google-auth-ios-config}

現在您已經有 iOS 用戶端 ID，可以在 {{site.data.keyword.amashort}} 服務中啟用 Google 鑑別。

1. 在 {{site.data.keyword.amashort}} 儀表板中，開啟服務。
1. 在**管理**標籤中，將**授權**切換為開啟。
1. 展開 **Google** 區段。
1. 在**適用於 iOS 的應用程式 ID** 中，指定您從 `GoogleService-Info.plist` 檔案取得的 `CLIENT_ID` 值。
1. 按一下**儲存**。

## 配置適用於 iOS 的 {{site.data.keyword.amashort}} 用戶端 SDK
{: #google-auth-ios-sdk}

### 安裝 CocoaPods
{: #install-cocoapods}

1. 開啟「終端機」，並執行 **pod --version** 指令。如果您已經安裝 CocoaPods，則會顯示版本號碼。您可以跳到下一節來安裝 SDK。

1. 如果您未安裝 CocoaPods，請執行：


	```
	sudo gem install cocoapods
```
	{: codeblock}

如需相關資訊，請參閱 [CocoaPods 網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cocoapods.org/ "外部鏈結圖示"){: new_window}。

### 使用 CocoaPods 安裝 {{site.data.keyword.amashort}} 用戶端 Swift SDK
{: #facebook-auth-install-swift-cocoapods}

1. 如果您的 iOS 專案中沒有 `Podfile`，請執行 `pod init` 來建立檔案。

1. 編輯 `Podfile`，並在相關目標中新增下列幾行：

	```
	use_frameworks!
	pod 'BMSGoogleAuthentication'
	```
	{: codeblock}

	**附註：**如果您已安裝 {{site.data.keyword.amashort}} 核心 SDK，則可以移除此行：`pod 'BMSSecurity'`。`BMSGoogleAuthentication` Pod 會安裝所有必要的架構。

	**提示：**您可以將 `use_frameworks!` 新增至 Xcode 目標，而不是將它置於 Podfile。

1. 儲存 `Podfile`，然後從指令行執行 `pod install`。CocoaPods 將安裝相依關係。您會看到進度及新增的元件。

	**重要事項**：您現在必須使用 CocoaPods 所產生的 `xcworkspace` 檔案來開啟專案。名稱通常為 `{your-project-name}.xcworkspace`。  

1. 從指令行執行 `open {your-project-name}.xcworkspace`，以開啟您的 iOS 專案工作區。

1. 將 `GoogleAuthenticationManager.swift` 檔案從 `BMSGoogleAuthentication` pod 原始檔複製到您的專案目錄。

### 針對 iOS 啟用金鑰鏈共用
{: #enable_keychain}

啟用 `Keychain Sharing`。移至 `Capabilities` 標籤，並將 Xcode 專案中的 `Keychain Sharing` 切換為 `On`。


## 起始設定 {{site.data.keyword.amashort}} 用戶端 Swift SDK
{: #google-auth-ios-initialize}

若要使用 {{site.data.keyword.amashort}} 用戶端 SDK，請傳遞 `tenantID` 參數來進行起始設定。

放置起始設定碼的一般（但非強制）位置是在應用程式委派的 `application:didFinishLaunchingWithOptions` 方法。

1. 在您要使用 {{site.data.keyword.amashort}} 用戶端 SDK 的類別中，匯入必要架構。請新增下列標頭：

	```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {

 let mcaAuthManager = MCAAuthorizationManager.sharedInstance
		mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
		//the regionName should be one of the following: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney   
		BMSClient.sharedInstance.authorizationManager = mcaAuthManager
		GoogleAuthenticationManager.sharedInstance.register()
		return true
	}

	// [START openurl]
	func application(_ application: UIApplication,
		open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
			return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url,
			sourceApplication: sourceApplication, annotation: annotation)
	    }

	@available(iOS 9.0, *)
	func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any]) -> Bool {
		return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, options: options)
	}

	```
	{: codeblock}

	在程式碼中：

      * 將 `<serviceTenantID>` 取代為您從**行動選項**擷取的值。
      * 將 `<applicationBluemixRegion>` 取代為您的 {{site.data.keyword.Bluemix_notm}} **地區**。

	如需取得這些值的相關資訊，請參閱[開始之前](#before-you-begin)。


## 測試鑑別
{: #google-auth-ios-testing}

起始設定用戶端 SDK 並登錄「Google 鑑別管理程式」之後，即可開始對行動後端應用程式提出要求。

### 開始之前
{: #google-auth-ios-testing-before}

您必須使用 {{site.data.keyword.mobilefirstbp}} 樣板，並且在 `/protected` 端點已具有 {{site.data.keyword.amashort}} 所保護的資源。如果您需要設定 `/protected` 端點，請參閱[保護資源](protecting-resources.html)。

1. 開啟 `{applicationRoute}/protected`，嘗試在桌面瀏覽器中將要求傳送給行動後端應用程式的受保護端點。例如 `http://my-mobile-backend.mybluemix.net/protected`。

1. 使用「MobileFirst Services 樣板」所建立之行動後端應用程式的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護，所以只有使用 {{site.data.keyword.amashort}} 用戶端 SDK 所檢測的行動應用程式才能存取它。因此，您會在桌面瀏覽器中看到 `Unauthorized`。

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

1. 執行您的應用程式。您將看到「Google 登入」蹦現畫面。

 ![影像](images/ios-google-login.png)

1. 當您登入並按一下**確定**時，表示您授權 {{site.data.keyword.amashort}} 使用您的 Google 使用者身分來進行鑑別。

1. 您的要求應該會成功。下列輸出會出現在日誌中。

	```
	 response:Optional("Hello, this is a protected resource of the mobile backend application!"), no error
 ```
	{: screen}

1. 您也可以新增下列程式碼，來新增登出功能：

	```
	GoogleAuthenticationManager.sharedInstance.logout(callBack)
 ```
	{: codeblock}

	如果您在使用者使用 Google 登入之後呼叫此程式碼，而且使用者嘗試重新登入，則系統會提示他們授權 {{site.data.keyword.amashort}} 使用 Google 進行鑑別。此時，使用者可以按一下使用者名稱<!--in the upper-right corner of the screen-->來進行選取，並利用另一個使用者來登入。

	將 `callBack` 傳遞給 logout 函數是選用性的作業。您也可以傳遞 `nil`。
