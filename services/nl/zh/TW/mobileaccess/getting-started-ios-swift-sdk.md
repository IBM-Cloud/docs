---

copyright:
  years: 2016

---
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# 設定 iOS Swift SDK
{: #getting-started-ios}

*前次更新：2016 年 6 月 14 日*
{: .last-updated}

Mobile Client Access 已發行新的 Swift SDK，可新增至現有 Mobile Client Access Objective-C SDK 所提供的功能並加以改善，更輕鬆地鑑別應用程式並為後端資源提供更好的保護。請使用 {{site.data.keyword.amashort}} SDK 檢測 iOS Swift 應用程式、起始設定 SDK，以及對受保護資源及未受保護資源提出要求。
{:shortdesc}

**附註：**Objective-C SDK 會向 Mobile Client Access 服務的「監視主控台」報告監視資料。如果您是依賴 Mobile Client Access 服務的「監視」功能，則需要繼續使用 Objective-C SDK。

**附註：**雖然仍然完全支援 Objective-C SDK 且將它視為 {{site.data.keyword.Bluemix_notm}} Mobile Services 的主要 SDK，不過預計在今年稍晚中斷使用 Objective-C SDK，改用這個新的 Swift SDK。 






## 開始之前
{: #before-you-begin}
您必須具有：
* {{site.data.keyword.amashort}} 服務所保護的 {{site.data.keyword.Bluemix_notm}} 應用程式實例。如需如何建立 {{site.data.keyword.Bluemix_notm}} 後端的相關資訊，請參閱[開始使用](index.html)。
* Xcode 專案。如需如何設定 iOS 開發環境的相關資訊，請參閱 [Apple Developer 網站](https://developer.apple.com/support/xcode/)。


## 安裝 {{site.data.keyword.amashort}} 用戶端 SDK
{: #install-mca-sdk-ios}
{{site.data.keyword.amashort}} SDK 是使用 CocoaPods（iOS 專案的相依關係管理程式）進行配送。CocoaPods 會從儲存庫中自動下載構件，並使它們可供 iOS 應用程式使用。


### 安裝 CocoaPods
{: #install-cocoapods}
1. 開啟「終端機」，並執行 **pod --version** 指令。如果您已經安裝 CocoaPods，則會顯示版本號碼。您可以跳到下一節來安裝 SDK。

1. 如果您未安裝 CocoaPods，請執行：

```
sudo gem install cocoapods
```
如需相關資訊，請參閱 [CocoaPods 網站](https://cocoapods.org/)。

### 使用 CocoaPods 安裝 {{site.data.keyword.amashort}} 用戶端 SDK
{: #install-sdk-cocoapods}

1. 在終端機視窗中，導覽至您 iOS 專案的根目錄。

1. 如果您尚未起始設定 CocoaPods 的工作區，請執行 `pod init` 指令。<br/>CocoaPods 會為您建立 `Podfile` 檔案，其中定義 iOS 專案的相依關係。

1. 編輯 `Podfile` 檔案，並將下行新增至必要目標：

	```
  use_frameworks!
  pod 'BMSSecurity'
	```
  **提示：**您可以將 `use_frameworks!` 新增至 Xcode 目標，而不是將它置於 Podfile。

1. 儲存 `Podfile` 檔案，並從指令行執行 `pod install`。<br/>Cocoapods 會安裝相關的相依關係，並顯示新增的相依關係及 Pod。<br/>
**重要事項**：CocoaPods 會產生 `xcworkspace` 檔案。您必須開啟此檔案，才能繼續處理專案。

1. 開啟 iOS 專案工作區。開啟 CocoaPods 所產生的 `xcworkspace` 檔案。例如：`{your-project-name}.xcworkspace`。執行 `open {your-project-name}.xcworkspace`。

## 起始設定 {{site.data.keyword.amashort}} 用戶端 SDK
{: #init-mca-sdk-ios}

 透過傳遞 `applicationRoute` 及 `applicationGUID` 參數來起始設定 SDK。放置起始設定碼的一般（但非強制）位置是在應用程式委派的 `application:didFinishLaunchingWithOptions` 方法。

1. 取得應用程式參數值。在 {{site.data.keyword.Bluemix_notm}} 儀表板中開啟應用程式。按一下**行動選項**。`applicationRoute` 及 `applicationGUID` 值即會顯示在**路徑**及**應用程式 GUID** 欄位中。

1. 在您要使用 {{site.data.keyword.amashort}} 用戶端 SDK 的類別中，匯入必要架構。

 ```Swift
 import BMSCore
 import BMSSecurity
 ```  

1. 起始設定 {{site.data.keyword.amashort}} 用戶端 SDK。將 `<applicationRoute>` 及 `<applicationGUID>` 取代為您取自 {{site.data.keyword.Bluemix_notm}} 儀表板中**行動選項**的**路徑**及**應用程式 GUID** 值。將 `<applicationBluemixRegion>` 取代為管理您 {{site.data.keyword.Bluemix_notm}} 應用程式的地區。若要檢視您的 {{site.data.keyword.Bluemix_notm}} 地區，請按一下儀表板左上角的樣式圖示 (![樣式](/face.png "樣式"))。 


 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 // Initialize the client SDK.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<applicationBluemixRegion>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 return true
 }
 ```

## 對行動後端提出要求
{: #request}

起始設定 {{site.data.keyword.amashort}} 用戶端 SDK 之後，即可開始對行動後端提出要求。

1. 嘗試在瀏覽器中將要求傳送給行動後端上的受保護端點。開啟下列 URL：`{applicationRoute}/protected`。例如：`http://my-mobile-backend.mybluemix.net/protected`。
<br/>使用 MobileFirst Services Starter 樣板所建立之行動後端的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護。在瀏覽器中會傳回 `Unauthorized` 訊息，因為只有使用 {{site.data.keyword.amashort}} 用戶端 SDK 所檢測的行動應用程式才能存取這個端點。

1. 使用 iOS 應用程式以對相同的端點提出要求。起始設定 `BMSClient` 之後，請新增下列程式碼：

 ```Swift
 let customResourceURL = "<your protected resource's path>"
 let request = Request(url: customResourceURL, method: HttpMethod.GET)
 let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) in
     if error == nil {
         print ("response:\(response?.responseText), no error")
     } else {
         print ("error: \(error)")
     }
 }

 request.sendWithCompletionHandler(callBack)
 ```

1.  當要求成功時，您會在 Xcode 主控台中看到下列輸出：

 ```
 response:Optional("Hello, this is a protected resouce of the mobile backend application!"), no error
 ```
{: screen}
 
## 後續步驟
{: #next-steps}
當您連接至受保護端點時，不需要任何認證。若需要使用者登入應用程式，您必須配置 Facebook、Google 或自訂鑑別。
  * [Facebook](facebook-auth-ios-swift-sdk.html)
  * [Google](google-auth-ios-swift-sdk.html)
  * [自訂](custom-auth-ios-swift-sdk.html)
