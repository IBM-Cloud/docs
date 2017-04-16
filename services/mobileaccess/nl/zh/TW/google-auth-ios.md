---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-01"

---

{:screen: .screen}
{:shortdesc: .shortdesc}


# 啟用 iOS Objective C 應用程式的 Google 鑑別
{: #google-auth-ios}


在 {{site.data.keyword.amafull}} iOS 應用程式上，使用「Google 登入」來鑑別使用者。

**附註：**雖然仍然完全支援 Objective-C SDK 且將它視為 {{site.data.keyword.Bluemix_notm}} Mobile Services 的主要 SDK，不過預計在今年稍晚停止使用此 SDK，改用新的 Swift SDK。對於新的應用程式，強烈建議使用 Swift SDK。此頁面上的指示適用於 {{site.data.keyword.amashort}} 用戶端 Objective-C SDK。如需使用 Swift SDK 的相關指示，請參閱[在 iOS 應用程式中啟用 Google 鑑別 (Swift SDK)](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html)。

## 開始之前
{: #before-you-begin}
您必須具有：
* {{site.data.keyword.amafull}} 服務實例和 {{site.data.keyword.Bluemix_notm}} 應用程式。如需如何建立 {{site.data.keyword.Bluemix_notm}} 後端應用程式的相關資訊，請參閱[開始使用](index.html)。
* 後端應用程式的 URL（**應用程式路徑**）。在傳送要求至後端應用程式的受保護端點時，將需要此值。
* **承租戶 ID** 值。在 {{site.data.keyword.amashort}} 儀表板中，開啟服務。按一下**行動選項**按鈕。`tenantId`（也稱為 `appGUID`）值會顯示在**應用程式 GUID/承租戶 ID** 欄位中。您需要此值來起始設定「授權管理程式」。

## 配置 iOS 平台的 Google 專案
{: #google-auth-ios-project}
若要開始使用 Google 作為身分提供者，請在 Google Developer Console 中建立專案來取得 Google 用戶端 ID。此用戶端 ID 是唯一 ID，可讓 Google 知道哪一個應用程式正在嘗試連接。   

1. 如果您尚未建立 Google iOS 專案，請遵循 [Google Developer Console](https://console.developers.google.com) 網站上的步驟。

1. 從**社交 API** 清單中，選擇 **Google+ API**，然後按一下**啟用**。

1. 從**認證**清單中，按一下**建立認證**按鈕，然後選擇 **OAuth 用戶端 ID**。

1. 此時會向您呈現應用程式類型選項。請選取 **iOS**。

1. 提供 iOS 用戶端的有意義名稱。指定 iOS 應用程式的軟體組 ID。若要尋找 iOS 應用程式的軟體組 ID，請在 `info.plist` 檔案或 Xcode 專案的**一般**標籤中尋找**軟體組 ID**。

1. 記下您的新 Google iOS 用戶端 ID。當您在 {{site.data.keyword.Bluemix}} 中設定應用程式時，需要這個值。




## 配置 {{site.data.keyword.amashort}} 進行 Google 鑑別
{: #google-auth-ios-config}

現在，您有 Google iOS 用戶端 ID，可以在 {{site.data.keyword.Bluemix_notm}} 儀表板中啟用 Google 鑑別。

1. 在 {{site.data.keyword.amashort}} 儀表板中，開啟服務。
1. 在**管理**標籤中，將**授權**切換為開啟。
1. 展開 **Google** 區段。
1. 在**適用於 iOS 的應用程式 ID** 中，指定適用於 iOS 的 Google 用戶端 ID。
1. 按一下**儲存**。


## 針對 iOS 配置 {{site.data.keyword.amashort}} Google 用戶端 SDK
{: #google-auth-ios-sdk}

### 使用 CocoaPods 安裝 {{site.data.keyword.amashort}} 用戶端 SDK
{: #google-auth-ios-sdk-cocoapods}

1. 導覽至 iOS 專案。

1. 編輯 `Podfile` 來新增下列這一行：

	```
	pod 'IMFGoogleAuthentication'
	```
{: codeblock}

1. 儲存 `Podfile`，然後從指令行執行 `pod install`。CocoaPods 將安裝相依關係。您會看到進度及新增的元件。

  **重要事項**：您現在必須使用 CocoaPods 所產生的 `xcworkspace` 檔案來開啟專案。名稱通常為 `{your-project-name}.xcworkspace`。  

1. 從指令行執行 `open {your-project-name}.xcworkspace`，以開啟您的 iOS 專案工作區。

### 配置 iOS 專案進行 Google 鑑別
{: #google-auth-ios-googleauth}
更新 `info.plist` 檔案來配置 Google 整合。`info.plist` 檔案通常位於 Xcode 專案的 `Supporting files` 資料夾中。您可以在內容清單編輯器中或使用文字編輯器編輯檔案。

* 將下列 URL 綱目新增至 `info.plist` 檔案，以配置 Google 整合。
	![info.plist 檔案](images/ios-google-infoplist-settings.png)

	第一個「URL 綱目」為來自 Google Developer Console 的用戶端 ID 的反向版本。例如，如果用戶端 ID 為 `123123-abcabc.apps.googleusercontent.com`，則「URL 綱目」為 `com.googleusercontent.apps.123123-abcabc`。

	第二個「URL 綱目」為應用程式的軟體組 ID。

* 使用文字編輯器。在 `info.plist` 上按一下滑鼠右鍵，然後選取**開啟為 > 原始碼**。將下列 XML 新增至檔案：

	```XML
	<key>CFBundleURLTypes</key>
	<array>
		<dict>
			<key>CFBundleTypeRole</key>
			<string>Editor</string>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>com.googleusercontent.apps.123123-abcabc</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeRole</key>
			<string>Editor</string>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>com.ibm.HelloWorld</string>
			</array>
		</dict>
	</array>

	```
{: codeblock}

	更新兩個 URL 綱目。

	**重要事項**：請不要置換 `info.plist` 檔案中的任何現有內容。如果有重疊的內容，則需要手動合併這些內容。如需相關資訊，請參閱 [Try Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start)。

## 起始設定 {{site.data.keyword.amashort}} 用戶端 SDK
{: #google-auth-ios-initialize}

若要使用 {{site.data.keyword.amashort}} 用戶端 SDK，請傳遞「承租戶 ID」和「應用程式路徑」參數來進行起始設定。

放置起始設定碼的一般（但非強制）位置是在應用程式委派的 `application:didFinishLaunchingWithOptions` 方法。

1. 在您要使用 {{site.data.keyword.amashort}} 用戶端 SDK 的類別中，匯入必要架構。請新增下列標頭：

	#### Objective-C：

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```
{: codeblock}

	#### Swift：

	{{site.data.keyword.amashort}} 用戶端 SDK 是使用 Objective-C 進行實作。您可能需要將橋接標頭新增至 Swift 專案，才能使用 SDK。

	1. 在 Xcode 中的專案上按一下滑鼠右鍵，然後選取 **New File...**。

	2. 在 **iOS Source** 種類中，挑選 **Header file**。

	3. 將它命名為 `BridgingHeader.h`。

	4. 將下列匯入項目新增至橋接標頭：
		
	   `#import <IMFCore/IMFCore.h>`
		
	   `#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>`
	
	5. 在 Xcode 中按一下您的專案，然後選取 **Build Settings** 標籤。

	6. 搜尋 `Objective-C Bridging Header`。

	7. 將值設為 `BridgingHeader.h` 檔案的位置（例如：`$(SRCROOT)/MyApp/BridgingHeader.h`）。

	8. 建置專案，以確定 Xcode 取得橋接標頭。

3. 使用下列程式碼來起始設定用戶端 SDK。將 `<applicationRoute>` 和 `<TenantID>` 取代為您的**路徑**和**承租戶 ID**。

	#### Objective-C：

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"<applicationRoute>"
			backendGUID:@"<TenantID>"];
	```
{: codeblock}

	#### Swift：

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("<applicationRoute>",
	 							backendGUID: "<TenantID>")
	```
{: codeblock}

1. 傳遞 {{site.data.keyword.amashort}} 服務 `tenantId` 參數，以起始設定 `AuthorizationManager`。 
  ####Objective-C
	
  ```Objective-C
     [[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"tenantId"];
  ```
 {: codeblock}

  ####Swift

  ```Swift
  IMFAuthorizationManager.sharedInstance().initializeWithTenantId("tenantId")
 ```
 {: codeblock}

1. 將下面程式碼新增至應用程式委派中的 `application:didFinishLaunchingWithOptions` 方法，以登錄「Google 鑑別處理程式」。請在起始設定 IMFClient 之後立即新增此程式碼：

	#### Objective-C：

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```
{: codeblock}

	#### Swift：

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```
{: codeblock}

1. 將下列程式碼新增至應用程式委派。

	#### Objective-C：

	```Objective-C
	- (void)applicationDidBecomeActive:(UIApplication *)application {
		[[IMFGoogleAuthenticationHandler sharedInstance] handleDidBecomeActive];
	}

	- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url
					sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {

		BOOL shouldHandleGoogleURL = [GPPURLHandler handleURL:url
					sourceApplication:sourceApplication annotation:annotation];

		[[IMFGoogleAuthenticationHandler sharedInstance] handleOpenURL:shouldHandleGoogleURL];
		return  shouldHandleGoogleURL;
	}
	```
{: codeblock}

	#### Swift：

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		let shouldHandleGoogleURL = GPPURLHandler.handleURL(url,
				sourceApplication: sourceApplication, annotation: annotation)

		IMFGoogleAuthenticationHandler.sharedInstance()
							.handleOpenURL(shouldHandleGoogleURL)

		return shouldHandleGoogleURL;
	}
```
{: codeblock}

## 測試鑑別
{: #google-auth-ios-testing}
起始設定用戶端 SDK 之後，即可開始對行動後端提出要求。

### 開始之前
{: #google-auth-ios-testing-before}
您必須使用 {{site.data.keyword.mobilefirstbp}} 樣板，並且在 `/protected` 端點已具有 {{site.data.keyword.amashort}} 所保護的資源。如果您需要設定 `/protected` 端點，請參閱[保護資源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。


1. 開啟 `{applicationRoute}/protected`（例如 `http://my-mobile-backend.mybluemix.net/protected`），嘗試在桌面瀏覽器中將要求傳送給行動後端的受保護端點

1. 使用「MobileFirst Services 樣板」所建立之行動後端的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護，所以只有使用 {{site.data.keyword.amashort}} 用戶端 SDK 所檢測的行動應用程式才能存取它。因此，您會在桌面瀏覽器中看到 `Unauthorized`。

1. 使用 iOS 應用程式以對相同的端點提出要求。

	#### Objective-C：

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
{: codeblock}

	#### Swift：

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
{: codeblock}

1. 執行您的應用程式。您將看到「Google 登入」蹦現畫面。

	![影像](images/ios-google-login.png)

	如果您未在裝置上安裝 Facebook 應用程式，或目前未登入 Facebook，則此畫面可能會稍微不同。

1. 按一下**確定**，即會授權 {{site.data.keyword.amashort}} 使用您的 Google 使用者身分來進行鑑別。

1. 	您的要求應該會成功。您應該會在 LogCat 中看到下列輸出：

	![影像](images/ios-google-login-success.png)
		
	您也可以新增下列程式碼，來新增登出功能：

	#### Objective C：

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] logout : callBack]
	```
{: codeblock}

	#### Swift：

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().logout(callBack)
	```
{: codeblock}

	如果您在使用者使用 Google 登入之後呼叫此程式碼，而且使用者嘗試重新登入，則系統會提示他們授權 {{site.data.keyword.amashort}} 使用 Google 進行鑑別。此時，使用者可以按一下使用者名稱<!--in the upper-right corner of the screen-->來進行選取，並利用另一個使用者來登入。

	將 `callBack` 傳遞給 logout 函數是選用性的作業。您也可以傳遞 `nil`。
