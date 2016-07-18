---

copyright:
  years: 2016

---

# 配置適用於 iOS 的 {{site.data.keyword.amashort}} 用戶端 SDK (Swift SDK)
{: #custom-ios}

配置 iOS 應用程式，這個應用程式利用自訂鑑別來使用 {{site.data.keyword.amashort}} 用戶端 SDK，並將您的應用程式連接至 {{site.data.keyword.Bluemix}}。新發行的 {{site.data.keyword.amashort}} Swift SDK 會新增至現有 Mobile Client Access Objective-C SDK 所提供的功能並加以改善。

**附註：**雖然仍然完全支援 Objective-C SDK 且將它視為 {{site.data.keyword.Bluemix_notm}} Mobile Services 的主要 SDK，不過預計在今年稍晚中斷使用 Objective-C SDK，改用這個新的 Swift SDK。

## 開始之前
{: #before-you-begin}

您必須具有配置成使用自訂身分提供者的 {{site.data.keyword.amashort}} 服務實例所保護的資源。您的行動應用程式也必須使用 {{site.data.keyword.amashort}} 用戶端 SDK 進行檢測。如需相關資訊，請參閱下列資訊：
 * [開始使用 {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/index.html)
 * [設定 iOS Swift SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html)
 * [使用自訂身分提供者](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [建立自訂身分提供者](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [配置 {{site.data.keyword.amashort}} 進行自訂鑑別](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## 配置 {{site.data.keyword.amashort}} 進行自訂鑑別
 {: #custom-auth-ios-configmca}

 1. 在 {{site.data.keyword.Bluemix_notm}} 儀表板中開啟應用程式。

 1. 按一下**行動選項**，並記下**路徑** (*applicationRoute*) 及 **應用程式 GUID** (*applicationGUID*)。起始設定 SDK 時，您需要這些值。

 1. 按一下 {{site.data.keyword.amashort}} 磚。即會載入 {{site.data.keyword.amashort}} 儀表板。

 1. 按一下**自訂**磚。

 1. 在**領域名稱**中，指定自訂的鑑別領域。

 1. 在 **URL** 中，指定您的 applicationRoute。

 1. 按一下**儲存**。




### 起始設定用戶端 SDK
{: #custom-ios-sdk-initialize}

透過傳遞 `applicationRoute` 及 `applicationGUID` 參數來起始設定 SDK。放置起始設定碼的一般（但非強制）位置是在應用程式委派的 `application:didFinishLaunchingWithOptions` 方法。

1. 取得應用程式參數值。在 {{site.data.keyword.Bluemix_notm}} 儀表板中開啟應用程式。按一下**行動選項**。`applicationRoute` 及 `applicationGUID` 值即會顯示在**路徑**及**應用程式 GUID** 欄位中。

1. 在您要使用 {{site.data.keyword.amashort}} 用戶端 SDK 的類別中，匯入必要架構。

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
```

1. 起始設定 {{site.data.keyword.amashort}} 用戶端 SDK、將授權管理程式變更為 MCAAuthorizationManager，以及定義鑑別委派並予以登錄。將 `<applicationRoute>` 及 `<applicationGUID>` 取代為您取自 {{site.data.keyword.Bluemix_notm}} 儀表板中**行動選項**的**路徑**及**應用程式 GUID** 值。

  將 `<applicationBluemixRegion>` 取代為管理您 {{site.data.keyword.Bluemix_notm}} 應用程式的地區。若要檢視您的 {{site.data.keyword.Bluemix_notm}} 地區，請按一下儀表板左上角的樣式圖示 (![樣式](/face.png "樣式"))。

  對於 `<yourProtectedRealm>`，使用您在 {{site.data.keyword.amashort}} 儀表板的**自訂**磚中定義的**領域名稱**。

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"
 let customRealm = "<yourProtectedRealm>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<applicationBluemixRegion>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

  //Auth delegate for handling custom challenge
 class MyAuthDelegate : AuthenticationDelegate {
      func onAuthenticationChallengeReceived(authContext: AuthenticationContext, challenge: AnyObject){
          print("onAuthenticationChallengeReceived")
              let answer = <An answer to the challenge sent by the backend (Should be of type [String:AnyObject])>
              authContext.submitAuthenticationChallengeAnswer(answer)
      }

      func onAuthenticationSuccess(info: AnyObject?) {
           print("onAuthenticationSuccess info = \(info)")
           print("onAuthenticationSuccess")
      }

      func onAuthenticationFailure(info: AnyObject?){
        print("onAuthenticationFailure info = \(info)")
        print("onAuthenticationFailure")
      }
  }

  let delegate = MyAuthDelegate()
  let mcaAuthManager = MCAAuthorizationManager.sharedInstance

 do {
      try mcaAuthManager.registerAuthenticationDelegate(delegate, realm: customRealm)
  } catch {
      print("error with register: \(error)")
  }
 return true
 }   
 ```

## 測試鑑別
{: #custom-ios-testing}

起始設定用戶端 SDK 並登錄自訂鑑別委派之後，即可開始對行動後端提出要求。

### 開始之前
{: #custom-ios-testing-before}

您必須具有使用 {{site.data.keyword.mobilefirstbp}} 樣板所建立的應用程式，並在 `/protected` 端點具有 {{site.data.keyword.amashort}} 所保護的資源。

1. 開啟 `{applicationRoute}/protected`（例如 `http://my-mobile-backend.mybluemix.net/protected`），以在瀏覽器中將要求傳送給行動後端的受保護端點。
使用 {{site.data.keyword.mobilefirstbp}} 樣板所建立之行動後端的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護。只有使用 {{site.data.keyword.amashort}} 用戶端 SDK 所檢測的行動應用程式才能存取這個端點。因此，會在瀏覽器中顯示 `Unauthorized` 訊息。

1. 使用 iOS 應用程式以對相同的端點提出要求。起始設定 `BMSClient` 並登錄自訂鑑別委派之後，請新增下列程式碼：

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

1. 	當要求成功時，您會在 Xcode 主控台中看到下列輸出：

 ```
 onAuthenticationSuccess info = Optional({
     attributes =     {
     };
     deviceId = don;
     displayName = "Don+Lon";
     isUserAuthenticated = 1;
     userId = don;
 })
 response:Optional("Hello Don Lon"), no error
 ```

1. 您也可以新增下列程式碼，來新增登出功能：

 ```
 MCAAuthorizationManager.sharedInstance.logout(callBack)
 ```  

如果您在使用者登入之後呼叫此程式碼，則會將使用者登出。使用者嘗試再次登入時，必須再次回答接收自伺服器的盤查。
將 `callBack` 傳遞給 logout 函數是選用性的作業。您也可以傳遞 `nil`。
