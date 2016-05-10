---

copyright:
  years: 2015, 2016

---

# 在 iOS 應用程式中啟用 Google 鑑別
{: #google-auth-ios}

**提示：**如果您是以 Swift 開發 iOS 應用程式，請考量使用 {{site.data.keyword.amashort}} Client Swift SDK。此頁面上的指示適用於 {{site.data.keyword.amashort}} Client Objective-C SDK。如需使用 Swift SDK 的相關指示，請參閱[在 iOS 應用程式中啟用 Google 鑑別 (Swift SDK)](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html)

## 開始之前
{: #google-auth-ios-before}
* 您必須具有 {{site.data.keyword.amashort}} 所保護的資源，以及使用 {{site.data.keyword.amashort}} Client SDK 所檢測的 iOS 專案。如需相關資訊，請參閱[開始使用 {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) 及[設定 iOS Objective-C SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html)。  
* 使用 {{site.data.keyword.amashort}} Server SDK，手動保護後端應用程式。如需相關資訊，請參閱[保護資源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。


## 配置 iOS 平台的 Google 專案
{: #google-auth-ios-project}
若要開始使用 Google 作為身分提供者，請在 Google Developer Console 中建立專案來取得 Google 用戶端 ID。此用戶端 ID 是唯一 ID，可讓 Google 知道哪一個應用程式正在嘗試連接。如果您已有 Google 專案，則可以跳過說明專案建立的步驟，並開始新增認證。



1. 在 [Google Developer Console](https://console.developers.google.com) 中建立專案。
如果您已有專案，則可以跳過說明專案建立的步驟，並開始新增認證。
   1.    開啟新建專案功能表。 
         
         ![影像](images/FindProject.jpg)

   2.    按一下**建立專案**。
   
         ![影像](images/CreateAProject.jpg)


1. 從**社交 API** 清單中，選擇 **Google+ API**。

     ![影像](images/chooseGooglePlus.jpg)

1. 從下一個畫面中，按一下**啟用**。

1. 選取**同意畫面**標籤，並提供向使用者顯示的產品名稱。其他值是選用的。按一下**儲存**。

    ![影像](images/consentScreen.png)
    
1. 從**認證**清單中，選擇 OAuth 用戶端 ID。

     ![影像](images/chooseCredentials.png)
     


1. 此時會向您呈現應用程式類型選項。請選取 **iOS**。

1. 提供 iOS 用戶端的有意義名稱。指定 iOS 應用程式的軟體組 ID。若要尋找 iOS 應用程式的軟體組 ID，請在 `info.plist` 檔案或 Xcode 專案的**一般**標籤中尋找**軟體組 ID**。

1. 記下您的新「iOS 用戶端 ID」。當您在 {{site.data.keyword.Bluemix}} 中設定應用程式時，需要這個值。


## 配置 {{site.data.keyword.amashort}} 進行 Google 鑑別
{: #google-auth-ios-config}

現在，您有「iOS 用戶端 ID」，可以在 {{site.data.keyword.Bluemix_notm}} 儀表板中啟用 Google 鑑別。

1. 在 {{site.data.keyword.Bluemix_notm}} 儀表板中開啟應用程式。

1. 按一下**行動式選項**，並記下您的**路徑** (`applicationRoute`) 及 **應用程式 GUID** (`applicationGUID`)。起始設定 SDK 時，您需要這些值。

1. 按一下 {{site.data.keyword.amashort}} 磚。即會載入 {{site.data.keyword.amashort}} 儀表板。

1. 按一下 **Google** 磚。

1. 在 **iOS 的應用程式 ID** 中，指定 Android 的「iOS 用戶端 ID」，然後按一下**儲存**。

	附註：除了 Google 用戶端 ID 之外，還需要反向值以進行用戶端配置（請參閱下面）。若要存取這兩個值，請使用鉛筆圖示來下載範例 plist：![info.plist file download](images/download_plist.png)

## 配置 {{site.data.keyword.amashort}} Client SDK for iOS
{: #google-auth-ios-sdk}

### 使用 CocoaPods 安裝 {{site.data.keyword.amashort}} Client SDK
{: #google-auth-ios-sdk-cocoapods}

1. 導覽至 iOS 專案。

1. 編輯 `Podfile` 來新增下列這一行：

	```
	pod 'IMFGoogleAuthentication'
	```

1. 儲存 `Podfile`，然後從指令行執行 `pod install`。CocoaPods 將安裝相依關係。您會看到進度及新增的元件。

  **重要事項**：您現在必須使用 CocoaPods 所產生的 `xcworkspace` 檔案來開啟專案。名稱通常為 `{your-project-name}.xcworkspace`。  

1. 從指令行執行 `open {your-project-name}.xcworkspace`，以開啟您的 iOS 專案工作區。

### 配置 iOS 專案進行 Google 鑑別
{: #google-auth-ios-googleauth}
更新 `info.plist` 檔案來配置 Google 整合。`info.plist` 檔案通常位於 Xcode 專案的 `Supporting files` 資料夾中。您可以在內容清單編輯器中或使用文字編輯器編輯檔案。

* 將下列 URL 綱目新增至 `info.plist` 檔案，以配置 Google 整合。
	![info.plist file](images/ios-google-infoplist-settings.png)

	第一個「URL 綱目」為反向的「用戶端 ID」版本（來自「Google 開發人員主控台」）。例如，如果「用戶端 ID」為 `123123-abcabc.apps.googleusercontent.com`，則「URL 綱目」為 `com.googleusercontent.apps.123123-abcabc`。 

	第二個「URL 綱目」為應用程式的軟體組 ID。

* 使用文字編輯器。在 `info.plist` 上按一下滑鼠右鍵，然後選取**開啟方式 > 原始碼**。將下列 XML 新增至檔案：

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
	更新兩個 URL 綱目。

	**重要事項**：請不要置換 `info.plist` 檔案中的任何現有內容。如果有重疊的內容，則需要手動合併這些內容。如需相關資訊，請參閱 [Try Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start)。

## 起始設定 {{site.data.keyword.amashort}} Client SDK
{: #google-auth-ios-initialize}

若要使用 {{site.data.keyword.amashort}} Client SDK，請傳遞 applicationGUID 及 applicationRoute 參數來進行起始設定。

放置起始設定碼的一般（但非強制）位置是在應用程式委派的 `application:didFinishLaunchingWithOptions` 方法。

1. 取得 applicationGUID 及 applicationRoute 值。從「{{site.data.keyword.Bluemix_notm}} 儀表板」中，按一下您的應用程式。按一下**行動式選項**。即會顯示「應用程式路徑」及「應用程式 GUID」值。

1. 在您要使用 {{site.data.keyword.amashort}} Client SDK 的類別中，匯入必要架構。請新增下列標頭：

	Objective-C：

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```

	Swift：

	{{site.data.keyword.amashort}} Client SDK 是使用 Objective-C 進行實作。您可能需要將橋接標頭新增至 Swift 專案，才能使用 SDK。

	1. 在 Xcode 中的專案上按一下滑鼠右鍵，然後選取**新建檔案...**。
	2. 在 **iOS 來源**種類中，挑選**標頭檔**。
	3. 將它命名為 `BridgingHeader.h`
	4. 將下列匯入項目新增至橋接標頭：

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```
	5. 在 Xcode 中按一下您的專案，然後選取**建置設定**標籤。
	6. 搜尋 `Objective-C Bridging Header`。
	7. 將值設為 `BridgingHeader.h` 檔案的位置（例如：`$(SRCROOT)/MyApp/BridgingHeader.h`）。
	8. 建置專案，以確定 Xcode 取得橋接標頭。

3. 使用下列程式碼來起始設定 Client SDK。將 *applicationRoute* 及 *applicationGUID* 取代為您取自**行動式選項**的**路徑**及**應用程式 GUID** 值。

	Objective-C：

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	Swift：

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```



1. 將下面程式碼新增至應用程式委派中的 `application:didFinishLaunchingWithOptions` 方法，以登錄「Google 鑑別處理程式」。請在起始設定 IMFClient 之後立即新增此程式碼：

	Objective-C：

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```

	Swift：

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```

1. 將下列程式碼新增至應用程式委派。

	Objective-C：

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

	Swift：

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

## 測試鑑別
{: #google-auth-ios-testing}
起始設定 Client SDK 之後，即可開始對行動式後端提出要求。

### 開始之前
{: #google-auth-ios-testing-before}
您必須使用 {{site.data.keyword.mobilefirstbp}} 樣板，並且在 `/protected` 端點已具有 {{site.data.keyword.amashort}} 所保護的資源。如果您需要設定 `/protected` 端點，請參閱[保護資源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。


1. 開啟 `{applicationRoute}/protected`（例如 `http://my-mobile-backend.mybluemix.net/protected`），嘗試在桌面瀏覽器中將要求傳送給行動式後端的受保護端點

1. 使用「MobileFirst Services 樣板」所建立之行動式後端的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護，所以只有使用 {{site.data.keyword.amashort}} Client SDK 所檢測的行動式應用程式才能存取它。因此，您會在桌面瀏覽器中看到 `Unauthorized`。

1. 使用 iOS 應用程式以對相同的端點提出要求。

	Objective-C：

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

	Swift：

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

1. 執行您的應用程式。您將看到「Google 登入」蹦現畫面。

	![影像](images/ios-google-login.png)

	如果您未在裝置上安裝 Facebook 應用程式，或目前未登入 Facebook，則此畫面可能會稍微不同。

1. 按一下**確定**，即會授權 {{site.data.keyword.amashort}} 使用 Google 使用者身分來進行鑑別。

1. 	您的要求應該會成功。您應該會在 LogCat 中看到下列輸出：

	![影像](images/ios-google-login-success.png)
	
	
	您也可以新增下列程式碼，來新增登出功能：
	
	Objective C:
	
	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] logout : callBack]
	```

	Swift：

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().logout(callBack)
	```


	如果您在使用者使用 Google 登入之後呼叫此程式碼，而且使用者嘗試重新登入，則系統會提示他們授權 Mobile Client Access 使用 Google 進行鑑別。此時，使用者可以按一下畫面右上角的使用者名稱來進行選取，並使用另一位使用者來登入。

	將 `callBack` 傳遞給 logout 函數是選用的。您也可以傳遞 `nil`。
