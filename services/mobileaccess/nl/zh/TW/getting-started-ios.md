---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"

---
{:shortdesc: .shortdesc}

# 設定 iOS Objective-C SDK
{: #getting-started-ios}

使用 {{site.data.keyword.amafull}} SDK 檢測 iOS 應用程式、起始設定 SDK，以及對受保護資源及未受保護資源提出要求。


{:shortdesc}

**重要事項：**雖然仍然完全支援 Objective-C SDK 且將它視為 {{site.data.keyword.Bluemix_notm}} Mobile Services 的主要 SDK，不過預計在今年稍晚停止使用此 SDK，改用新的 Swift SDK。對於新的應用程式，強烈建議使用 Swift SDK（請參閱[設定 iOS Swift SDK](getting-started-ios-swift-sdk.html)）。

## 開始之前
{: #before-you-begin}
您必須具有：
* {{site.data.keyword.amashort}} 服務所保護的 {{site.data.keyword.Bluemix_notm}} 應用程式實例。如需如何建立 {{site.data.keyword.Bluemix_notm}} 後端應用程式的相關資訊，請參閱[開始使用](index.html)。
* **承租戶 ID**。在 {{site.data.keyword.amashort}} 儀表板中，開啟服務。按一下**行動選項**。`tenantId`（也稱為 `appGUID`）值會顯示在**應用程式 GUID/承租戶 ID** 欄位中。您需要此值來起始設定「{{site.data.keyword.amashort}} 授權管理程式」。
* **應用程式路徑**。這是後端應用程式的 URL。在傳送要求至其受保護端點時，將需要此值。
* Xcode 專案。  


## 安裝 {{site.data.keyword.amashort}} 用戶端 SDK
{: #install-mca-sdk-ios}
{{site.data.keyword.amashort}} SDK 是使用 CocoaPods（iOS 專案的相依關係管理程式）進行配送。CocoaPods 會從儲存庫中自動下載構件，並使它們可供 iOS 應用程式使用。


### 安裝 CocoaPods
{: #install-cocoapods}

1. 開啟「終端機」，並執行 **pod --version** 指令。如果您已經安裝 CocoaPods，則會顯示版本號碼。請跳到下一節來安裝 SDK。

1. 如果您未安裝 CocoaPods，請執行：

```
sudo gem install cocoapods
```

如需相關資訊，請參閱 [CocoaPods 網站](https://cocoapods.org/)。

### 使用 CocoaPods 安裝 {{site.data.keyword.amashort}} 用戶端 SDK
{: #install-sdk-cocoapods}

1. 在「終端機」中，導覽至您 iOS 專案的根目錄。

1. 如果您尚未起始設定 CocoaPods 的工作區，請執行 `pod init` 指令。<br/>CocoaPods 會為您建立 `Podfile` 檔案，其中定義 iOS 專案的相依關係。

1. 編輯 `Podfile` 檔案，並將下行新增至必要目標：


	`pod 'IMFCore'`

1. 儲存 `Podfile` 檔案，然後從指令行執行 `pod install`。<br/>Cocoapods 會安裝新增的相依關係，並顯示新增的元件。<br/>

	**重要事項**：CocoaPods 會產生 `xcworkspace` 檔案。您必須開啟此檔案，才能繼續處理專案。

1. 開啟 iOS 專案工作區。開啟 CocoaPods 所產生的 `xcworkspace` 檔案。例如：`{your-project-name}.xcworkspace`。執行 `open {your-project-name}.xcworkspace`。

## 起始設定 {{site.data.keyword.amashort}} 用戶端 SDK
{: #init-mca-sdk-ios}

1. 新增下列標頭，在您要使用 {{site.data.keyword.amashort}} 用戶端 SDK 的類別中匯入 `IMFCore` 架構：

	####Objective-C
	{: #imfcore-objc}

	```Objective-C
	  #import <IMFCore/IMFCore.h>
	
	```

	####Swift
	{: #sdk-swift}

	{{site.data.keyword.amashort}} 用戶端 SDK 是使用 Objective-C 進行實作。您可能需要將橋接標頭新增至 Swift 專案：
	1. 在 Xcode 中的專案上按一下滑鼠右鍵，然後選取 **New File**。
	1. 在 **iOS Source** 種類中，按一下 **Header file**。將檔案命名為 `BridgingHeader.h`。
	1. 將下行新增至橋接標頭：`#import <IMFCore/IMFCore.h>`。
	1. 在 Xcode 中按一下您的專案，然後選取 **Build Settings** 標籤。
	1. 搜尋 `Objective-C Bridging Header`。
	1. 將值設為 `BridgingHeader.h` 檔案的位置（例如 `$(SRCROOT)/MyApp/BridgingHeader.h`）。
	1. 建置專案，以確定 Xcode 取得橋接標頭。您應該不會看到任何失敗訊息。

1. 使用下列程式碼來起始設定 {{site.data.keyword.amashort}} 用戶端 SDK。放置起始設定碼的一般（但非強制）位置是在應用程式委派的 `application:didFinishLaunchingWithOptions` 方法。<br/>
如需取得 `applicationRoute` 和 `applicationGUID` 的相關資訊，請參閱[開始之前](#before-you-begin)。 

	####Objective-C
	{: #sharedinstance-objc}

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	####Swift
	{: #sharedinstance-swift}
	```Swift
 		MFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",backendGUID: "applicationGUID")
	```

## 起始設定 AuthorizationManager
傳遞 {{site.data.keyword.amashort}} 服務 `tenantId` 參數，以起始設定 `AuthorizationManager`。如需取得這些值的相關資訊，請參閱[開始之前](#before-you-begin)。 

####Objective-C

```Objective-C
[[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"<tenantId>"];
```

####Swift

```Swift
IMFAuthorizationManager.sharedInstance().initializeWithTenantId("<tenantId>")
```

	
## 對行動後端應用程式提出要求
{: #request}

起始設定 {{site.data.keyword.amashort}} 用戶端 SDK 之後，即可開始對行動後端應用程式提出要求。

1. 嘗試在瀏覽器中將要求傳送給行動後端應用程式上的受保護端點。開啟下列 URL：`{applicationRoute}/protected`。例如：`http://my-mobile-backend.mybluemix.net/protected`。
<br/>使用 MobileFirst Services Starter 樣板所建立之行動後端應用程式的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護。在瀏覽器中會傳回 `Unauthorized` 訊息，因為只有使用 {{site.data.keyword.amashort}} 用戶端 SDK 所檢測的行動應用程式才能存取這個端點。

1. 使用 iOS 應用程式以對相同的端點提出要求。起始設定 `IMFClient` 之後，請新增下列程式碼：

	####Objective-C
	{: #nsstring-objc}

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
		}
	}];
	```

	####Swift
	{: #imfclientrequestpath-swift}

	```Swift
	let requestPath = IMFClient.sharedInstance().backendRoute + "/protected"

	let request = IMFResourceRequest(path: requestPath, method: "GET");
	request.sendWithCompletionHandler { (response, error) -> Void in
		if (nil != error){
			NSLog("Error :: %@", error.description)
		} else {
			NSLog("Response :: %@", response.responseText)
		}
	};

	```

1.  當要求成功時，您會在 Xcode 主控台中看到下列輸出：

	![影像](images/getting-started-ios-success.png)

## 後續步驟
{: #next-steps}
當您連接至受保護端點時，不需要任何認證。若需要使用者登入應用程式，您必須配置 Facebook、Google 或自訂鑑別。
  * [Facebook](facebook-auth-ios.html)
  * [Google](google-auth-ios.html)
  * [自訂](custom-auth-ios.html)
