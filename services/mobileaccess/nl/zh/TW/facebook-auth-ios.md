---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-03"

---
{:shortdesc: .shortdesc}

# 啟用 iOS 應用程式的 Facebook 鑑別 (Objective-C SDK)
{: #facebook-auth-ios}

若要在 {{site.data.keyword.amafull}} iOS 應用程式中，使用 Facebook 做為身分提供者，請針對 Facebook 應用程式新增並配置 iOS 平台。

{:shortdesc}

**附註：**雖然仍然完全支援 Objective-C SDK 且將它視為 {{site.data.keyword.Bluemix}} Mobile Services 的主要 SDK，不過預計在今年稍晚停止使用它，改用新的 Swift SDK（請參閱[設定 iOS Swift SDK](facebook-auth-ios-swift-sdk.html)）。

## 開始之前
{: #before-you-begin}

您必須具有：
* 設定成使用 CocoaPods 的 iOS 專案。如需相關資訊，請參閱[設定 iOS SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html) 中的**安裝 CocoaPods**。
   **附註：**您不需要安裝核心 {{site.data.keyword.amashort}} 用戶端 SDK，即可繼續進行。
* {{site.data.keyword.amashort}} 服務所保護的 {{site.data.keyword.Bluemix_notm}} 應用程式實例。如需如何建立 {{site.data.keyword.Bluemix_notm}} 後端的相關資訊，請參閱[開始使用](index.html)。
* **AppGUID** 值。在 {{site.data.keyword.amashort}} 儀表板中，開啟服務。按一下**行動選項**按鈕。`appGUID`（也稱為 `tenantId`）值會顯示在**應用程式 GUID/承租戶 ID** 欄位中。您需要此值來起始設定「授權管理程式」。
* Facebook 應用程式及應用程式 ID。如需相關資訊，請參閱[在 Facebook for Developers 網站上建立應用程式](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)。

## 針對 iOS 平台配置 Facebook 應用程式
{: #facebook-auth-ios-config}
在 Facebook for Developers 網站上，執行下列動作：

1. 在 [Facebook for Developers](https://developers.facebook.com) 上，登入您的帳戶。 

1. 確保 iOS 平台已新增至您的應用程式。在新增或配置 iOS 平台時，您需要提供 iOS 應用程式的 **bundleId**。若要尋找 iOS 應用程式的 **bundleId**，請在 `info.plist` 檔案或 Xcode 專案**一般**標籤中尋找**軟體組 ID**。

1. 按一下**儲存設定**。

	**提示**：如果您計劃使用「URL 架構字尾」或「單一登入」，則請考慮啟用這些特性。

1. 按一下**儲存設定**。

## 配置 {{site.data.keyword.amashort}} 進行 Facebook 鑑別
{: #facebook-auth-ios-configmca}

配置「Facebook 應用程式 ID」及「Facebook 應用程式」來服務 iOS 用戶端之後，即可在 {{site.data.keyword.amashort}} 中啟用 Facebook 鑑別。

1. 在 {{site.data.keyword.amashort}} 儀表板中，開啟服務。
1. 在**管理**標籤中，將**授權**切換為開啟。
	1. 展開 **Facebook** 區段。
	1. 新增 **Facebook 應用程式 ID**，然後按一下**儲存**。

## 針對 iOS 配置 {{site.data.keyword.amashort}} Facebook 用戶端 SDK
{: #facebook-auth-ios-sdk}

### 安裝 CocoaPods
{: #facebook-auth-cocoapods}

{{site.data.keyword.amashort}} 用戶端 SDK 是使用 CocoaPods（iOS 專案的相依關係管理程式）進行配送。CocoaPods 會從儲存庫中自動下載構件，並使它們可供 iOS 應用程式使用。

1. 開啟「終端機」，並執行 `pod --version` 指令。如果您已經安裝 CocoaPods，則會顯示版本號碼。您可以跳到本指導教學的下一節。

1. 執行 `sudo gem install cocoapods`，以安裝 CocoaPods。如果需要其他指引，請參閱 [CocoaPods 網站](https://cocoapods.org/)。

### 使用 CocoaPods 安裝 {{site.data.keyword.amashort}} Facebook 用戶端 SDK
{: #facebook-auth-install-cocoapods}

1. 在 iOS 專案中，編輯 `Podfile` 及下行：

	```
	pod 'IMFFacebookAuthentication'
	```
{: codeblock}

1. 儲存 `Podfile`，並從指令行執行 `pod install` 指令。CocoaPods 將安裝相依關係。即會顯示進度及新增的元件。
 **重要事項**：您現在必須使用 CocoaPods 所產生的 `xcworkspace` 檔案來開啟專案。名稱通常為 `{your-project-name}.xcworkspace`。  

1. 從指令行執行 `open {your-project-name}.xcworkspace`，以開啟您的 iOS 專案工作區。

### 配置 iOS 專案進行 Facebook 鑑別
{: #facebook-auth-ios-configproject}

1. 尋找 `info.plist` 檔案（通常位於 Xcode 專案的 `Supporting files` 資料夾下）。

1. 將下列內容新增至 `info.plist` 檔案，以配置 Facebook 整合：

	![影像](images/ios-facebook-infoplist-settings.png)

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
<string>MyApp</string>
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

使用 **Facebook 應用程式 ID** 來更新 URL 架構和 `FacebookappID` 內容。

 **重要事項**：請確定您未置換 `info.plist` 檔案中的任何現有內容。如果您具有重疊的內容，則必須手動進行合併。如需相關資訊，請參閱[設定 Xcode 專案](https://developers.facebook.com/docs/ios/getting-started/)及[讓應用程式在 iOS9 環境下運作無礙](https://developers.facebook.com/docs/ios/ios9)。


## 起始設定 {{site.data.keyword.amashort}} 用戶端 SDK
{: #facebook-auth-ios-initalize}

透過傳遞應用程式路徑 (`applicationRoute`) 及應用程式 GUID (`applicationGUID`) 來起始設定用戶端 SDK。

放置起始設定碼的一般（但非強制）位置是在應用程式委派的 `application:didFinishLaunchingWithOptions` 方法。


1. 新增下列標頭，在您要使用 {{site.data.keyword.amashort}} 用戶端 SDK 的類別中匯入必要架構：

	####Objective-C
	{: #framework-objc}

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFFacebookAuthentication/IMFFacebookAuthenticationHandler.h>
	#import <FacebookSDK/FacebookSDK.h>
```	

	####Swift
	{: #bridgingheader-swift}

	{{site.data.keyword.amashort}} 用戶端 SDK 是使用 Objective-C 進行實作，因此您可能需要將橋接標頭新增至 Swift 專案。

	1. 在 Xcode 中的專案上按一下滑鼠右鍵，然後選取 **New File...**。
		1. 在 **iOS Source** 種類中，挑選 `Header file`。
		1. 將它命名為 `BridgingHeader.h`。
		1. 將匯入項目新增至橋接標頭：

			```Objective-C
			#import <IMFCore/IMFCore.h>
			#import <IMFFacebookAuthentication/IMFFacebookAuthenticationHandler.h>
			#import <FacebookSDK/FacebookSDK.h>
			```

	1. 在 Xcode 中按一下您的專案，然後選取 **Build Settings** 標籤。
		1. 搜尋 **Objective-C Bridging Header**。
		1. 將值設為 `BridgingHeader.h` 檔案的位置（例如：`$(SRCROOT)/MyApp/BridgingHeader.h`）。
		1. 建置專案，以確定 Xcode 取得橋接標頭。您應該不會看到任何失敗訊息。

2. 起始設定用戶端 SDK。如需取得 `applicationRoute` 和 `applicationGUID` 的相關資訊，請參閱[開始之前](#before-you-begin)。

	####Objective-C
	{: #approute-objc}

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	####Swift
	{: #approute-swift}

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```

1. 藉由傳遞 {{site.data.keyword.amashort}} 服務 `tenantId` 參數，起始設定 `AuthorizationManager`。請參閱[開始之前](#before-you-begin)。

	####Objective-C
	{: #authman-objc}

	```Objective-C
     [[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"tenantId"];
  ```

	####Swift
	{: #authman-swift}

	```Swift
  IMFAuthorizationManager.sharedInstance().initializeWithTenantId("tenantId")
 ```

1. 將下列程式碼新增至應用程式委派中的 `application:didFinishLaunchingWithOptions` 方法，以通知 Facebook SDK 有關應用程式啟動的資訊，並登錄「Facebook 鑑別處理程式」。起始設定 IMFClient 實例之後，請新增此程式碼。

	####Objective-C
	{: #activate-objc}

	```Objective-C
		[FBAppEvents activateApp];
		[[IMFFacebookAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
```

	####Swift
	{: #activate-swift}

	```Swift
		FBAppEvents.activateApp()
		IMFFacebookAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
```

1. 將下列程式碼新增至應用程式委派。

	####Objective-C
	{: #appdelegate-objc}

	```Objective-C
	- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url
			sourceApplication:(NSString *)sourceApplication annotation:(id)annotation {

		return [FBAppCall handleOpenURL:url sourceApplication:sourceApplication];
	}
	```

	####Swift
	{: #appdelegate-swift}

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		return FBAppCall.handleOpenURL(url, sourceApplication: sourceApplication)}
```


## 測試鑑別
{: #facebook-auth-ios-testing}
起始設定用戶端 SDK 並登錄「Facebook 鑑別管理程式」之後，即可開始對行動後端提出要求。

### 開始之前
{: #facebook-auth-ios-testing-before}
您必須使用 {{site.data.keyword.mobilefirstbp}} 樣板，並且在 `/protected` 端點已具有 {{site.data.keyword.amashort}} 所保護的資源。如果您需要設定 `/protected` 端點，請參閱[保護資源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。

1. 嘗試在瀏覽器中將要求傳送給新建行動後端的受保護端點。開啟下列 URL：`{applicationRoute}/protected`。
例如：`http://my-mobile-backend.mybluemix.net/protected`。
<br/>使用 MobileFirst Services Starter 樣板所建立之行動後端的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護。瀏覽器中會傳回 `Unauthorized` 訊息。傳回此訊息的原因是只有使用 {{site.data.keyword.amashort}} 用戶端 SDK 所檢測的行動應用程式才能存取這個端點。

1. 使用 iOS 應用程式以對相同的端點提出要求。

	####Objective-C
	{: #requestpath-objc}

	```Objective-C
	NSString *requestPath = [NSString stringWithFormat:@"%@/protected",
								[[IMFClient sharedInstance] backendRoute]];

	IMFResourceRequest *request =  [IMFResourceRequest requestWithPath:requestPath
																method:@"GET"];

	[request sendWithCompletionHandler:^(IMFResponse *response, NSError *error) {
		if (error){
			NSLog(@"Error :: %@", [error description]);
		} else {
			NSLog(@"Response :: %@", [response responseText]);
			NSLog(@"%@", [[IMFAuthorizationManager sharedInstance] userIdentity]);
		}
	}];
	```

	####Swift
	{: #requestpath-swift}

	```Swift
	let requestPath = IMFClient.sharedInstance().backendRoute + "/protected"

	let request = IMFResourceRequest(path: requestPath, method: "GET");
	request.sendWithCompletionHandler { (response, error) -> Void in
		if (nil != error){
			NSLog("Error :: %@", error.description)
		} else {
			NSLog("Response :: %@", response.responseText)
			NSLog("%@", IMFAuthorizationManager.sharedInstance().userIdentity)
		}
	};
 ```

1. 執行您的應用程式。即會蹦現 Facebook 登入畫面。

	![影像](images/ios-facebook-login.png)

	如果您未在裝置上安裝 Facebook 應用程式，或目前未登入 Facebook，則此畫面可能會稍微不同。

1. 按一下**確定**，以授權 {{site.data.keyword.amashort}} 使用您的 Facebook 使用者身分來進行鑑別。

1. 	當要求成功時，會在 Xcode 主控台中顯示下列輸出：![影像](images/ios-facebook-login-success.png)

	您也可以新增下列程式碼，來新增登出功能：

	####Objective-C
	{: #logout-objc}

	```Objective-C
	[[IMFFacebookAuthenticationHandler sharedInstance] logout : callBack]
	```
{: codeblock}

	####Swift
	{: #logout-swift}

	```Swift
	IMFFacebookAuthenticationHandler.sharedInstance().logout(callBack)
	```
{: codeblock}

	如果您在使用者使用 Facebook 登入之後呼叫此程式碼，而且使用者嘗試重新登入，則系統會提示他們授權 {{site.data.keyword.amashort}} 使用 Facebook 進行鑑別。

	若要切換使用者，您必須呼叫此程式碼，而且使用者必須在其瀏覽器中登出 Facebook。

  將 `callBack` 傳遞給 logout 函數是選用性的作業。您也可以傳遞 `nil`。
