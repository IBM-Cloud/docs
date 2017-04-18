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


# 設定 iOS Swift SDK
{: #getting-started-ios}

使用 {{site.data.keyword.amashort}} SDK 檢測 iOS Swift 應用程式、起始設定 SDK，以及對受保護資源及未受保護資源提出要求。


{:shortdesc}


## 開始之前
{: #before-you-begin}
您必須具有：

* {{site.data.keyword.Bluemix_notm}} 應用程式的實例。
* {{site.data.keyword.amafull}} 服務的實例。
* **承租戶 ID**。在 {{site.data.keyword.amashort}} 儀表板中，開啟服務。按一下**行動選項**。`tenantId`（也稱為 `appGUID`）值會顯示在**應用程式 GUID/承租戶 ID** 欄位中。您需要此值來起始設定「{{site.data.keyword.amashort}} 授權管理程式」。
* **應用程式路徑**。這是後端應用程式的 URL。在傳送要求至其受保護端點時，將需要此值。
* {{site.data.keyword.Bluemix_notm}} **地區**。您可以在標頭中找到您目前的 {{site.data.keyword.Bluemix_notm}} 地區，就在**虛擬人像**圖示 ![「虛擬人像」圖示](images/face.jpg "「虛擬人像」圖示") 的旁邊。出現的地區值應該是下列其中一項：`美國南部`、`雪梨`或`英國`，並對應至程式碼中所需的 SDK 值：`BMSClient.Region.usSouth`、`BMSClient.Region.unitedKingdom` 或 `BMSClient.Region.sydney`。您需要此值來起始設定 {{site.data.keyword.amashort}} SDK。
* Xcode 專案。如需如何設定 iOS 開發環境的相關資訊，請參閱 [Apple Developer 網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.apple.com/support/xcode/ "External link icon"){: new_window}。


## 安裝 {{site.data.keyword.amashort}} 用戶端 SDK
{: #install-mca-sdk-ios}
{{site.data.keyword.amashort}} SDK 是使用 CocoaPods（iOS 專案的相依關係管理程式）進行配送。CocoaPods 會從儲存庫中自動下載構件，並使它們可供 iOS 應用程式使用。


### 安裝 CocoaPods
{: #install-cocoapods}

1. 在終端機視窗中，執行 **pod --version** 指令。如果您已經安裝 CocoaPods，則會顯示版本號碼，而且可以跳到下一節來安裝 SDK。

1. 如果您未安裝 CocoaPods，請執行：


```
sudo gem install cocoapods
```
{: codeblock}

如需相關資訊，請參閱 [CocoaPods 網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cocoapods.org/ "外部鏈結圖示"){: new_window}。

### 使用 CocoaPods 安裝 {{site.data.keyword.amashort}} 用戶端 SDK
{: #install-sdk-cocoapods}

1. 在終端機視窗中，導覽至您 iOS 專案的根目錄。

1. 如果您尚未起始設定 CocoaPods 的工作區，請執行 `pod init` 指令。<br/>CocoaPods 會為您建立 `Podfile` 檔案，其中定義 iOS 專案的相依關係。

1. 編輯 `Podfile` 檔案，並將下行新增至必要目標：

	```
use_frameworks!
  pod 'BMSSecurity'
	```
	{: codeblock}

  **提示：**您可以將 `use_frameworks!` 新增至 Xcode 目標，而不是將它置於 Podfile。

1. 儲存 `Podfile` 檔案，然後從指令行執行 `pod install`。CocoaPods 會安裝相關的相依關係，並顯示新增的相依關係及 Pod。<br/>

   **重要事項**：CocoaPods 會產生 `xcworkspace` 檔案。您必須開啟此檔案，才能繼續處理專案。

1. 開啟 iOS 專案工作區。開啟 CocoaPods 所產生的 `xcworkspace` 檔案。例如，若為 `{your-project-name}.xcworkspace`，請執行：

	`open {your-project-name}.xcworkspace`

### 針對 iOS 啟用金鑰鏈共用
{: #enable_keychain}

啟用 `Keychain Sharing`。移至 `Capabilities` 標籤，並將 Xcode 專案中的 `Keychain Sharing` 切換為 `On`。

## 起始設定 {{site.data.keyword.amashort}} 用戶端 SDK
{: #init-mca-sdk-ios}

 傳遞 `tenantId` 參數，以起始設定 SDK。放置起始設定碼的一般（但非強制）位置是在應用程式委派的 `application:didFinishLaunchingWithOptions` 方法。

1. 在您要使用 {{site.data.keyword.amashort}} 用戶端 SDK 的類別中，匯入必要架構。

 ```Swift
 import BMSCore
 import BMSSecurity
 ```

1. 起始設定 {{site.data.keyword.amashort}} 用戶端 SDK。

 ```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

	func application(_ application: UIApplication, 
	    didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
	
	 let mcaAuthManager = MCAAuthorizationManager.sharedInstance
    mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
      // possible values for regionName: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, BMSClient.Region.sydney
	BMSClient.sharedInstance.authorizationManager = mcaAuthManager	
	return true
	}
 ```
  {: codeblock}

* 將 `tenantId` 取代為從**行動選項**中取得的值。
* 將 `<applicationBluemixRegion>` 取代為管理您 {{site.data.keyword.Bluemix_notm}} 應用程式的地區。

如需這些值的相關資訊，請參閱[開始之前](#before-you-begin)。


## 對行動後端應用程式提出要求
{: #request}

起始設定 {{site.data.keyword.amashort}} 用戶端 SDK 之後，即可開始對行動後端應用程式提出要求。

1. 嘗試在瀏覽器中將要求傳送給行動後端應用程式上的受保護端點。開啟下列 URL：`{applicationRoute}/protected`，並將 `{applicationRoute}` 取代為從**行動選項**中擷取的 **applicationRoute** 值（請參閱[起始設定 Mobile Client Access 用戶端 SDK](#init-mca-sdk-ios)）。例如：

	`http://my-mobile-backend.mybluemix.net/protected
	`

	在瀏覽器中會傳回 `Unauthorized` 訊息，因為只有使用 {{site.data.keyword.amashort}} 用戶端 SDK 所檢測的行動應用程式才能存取這個端點。



1. 使用 iOS 應用程式以對相同的端點提出要求。起始設定 `BMSClient` 之後，請新增下列程式碼：

 ```Swift
	let customResourceURL = "<your protected resource absolute path>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

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

1.  當要求成功時，下列輸出會出現在 Xcode 主控台中：

 ```
 response:Optional("Hello, this is a protected resource of the mobile backend application!"), no error
 ```
{: screen}

## 後續步驟
{: #next-steps}
當您連接至受保護端點時，不需要任何認證。若需要使用者登入應用程式，您必須配置 Facebook、Google 或自訂鑑別。

  * [Facebook](facebook-auth-ios-swift-sdk.html)
  * [Google](google-auth-ios-swift-sdk.html)
  * [自訂](custom-auth-ios-swift-sdk.html)
