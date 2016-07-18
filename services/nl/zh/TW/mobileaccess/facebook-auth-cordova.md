---

copyright:
  years: 2015, 2016

---
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# 啟用 Cordova 應用程式的 Facebook 鑑別
{: #facebook-auth-cordova}

*前次更新：2016 年 6 月 15 日*
{: .last-updated}


若要配置 Cordova 應用程式進行 Facebook 鑑別整合，您必須以 Cordova 應用程式的原生程式碼（以 Java、Objective-C 或 Swift）進行變更。分別配置每一個平台。此 Cordova 應用程式必須已使用 {{site.data.keyword.amashort}} SDK 進行檢測。 


使用原生開發環境，以原生程式碼進行變更（例如，在 Android Studio 或 Xcode 中）。
{:shortdesc}

## 開始之前
{: #facebook-auth-before}
您必須具有：
* 使用 {{site.data.keyword.amashort}} 用戶端 SDK 進行檢測的 Cordova 專案，請參閱[設定 Cordova 外掛程式](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)。
* {{site.data.keyword.amashort}} 服務所保護的 {{site.data.keyword.Bluemix_notm}} 應用程式實例。如需如何建立 {{site.data.keyword.Bluemix_notm}} 後端的相關資訊，請參閱[開始使用](index.html)。
* Facebook 應用程式 ID。如需相關資訊，請參閱[從 Facebook 開發人員入口網站取得 Facebook 應用程式 ID](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)。



## 配置 Android 平台
{: #facebook-auth-cordova-android}

配置 Cordova 應用程式的 Android 平台進行 Facebook 鑑別整合所需的步驟，與原生 Android 應用程式所需的步驟極為類似。如需相關資訊，請參閱[在 Android 應用程式中啟用 Facebook 鑑別](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html)。請完成下列步驟：

* 配置 Android 平台的 Facebook 應用程式
* 配置 {{site.data.keyword.amashort}} 進行 Facebook 鑑別
* 配置適用於 Android 的 {{site.data.keyword.amashort}} 用戶端 SDK

配置 Cordova 應用程式時的唯一差異是您必須以 JavaScript 程式碼（而非以 Java 程式碼）來起始設定 {{site.data.keyword.amashort}} 用戶端 SDK（請參閱[測試鑑別](#facebook-auth-cordova-test)）。仍然必須以原生程式碼登錄 `FacebookAuthenticationManager` API。

## 配置 iOS 平台
{: #facebook-auth-cordova-ios}

配置 Cordova 應用程式的 iOS 平台進行 Facebook 鑑別整合所需的步驟，與原生 iOS 應用程式所需的步驟類似。主要差異是 Cordova CLI 目前不支援 CocoaPods 相依關係管理程式。您必須手動新增與 Facebook 鑑別整合所需的檔案。如需相關資訊，請參閱[在 iOS 應用程式中啟用 Facebook 鑑別](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html)。請完成下列步驟：

* 配置 iOS 平台的 Facebook 應用程式
* 配置 {{site.data.keyword.amashort}} 進行 Facebook 鑑別

### 手動安裝用於 Facebook 鑑別的 {{site.data.keyword.amashort}} SDK 及 Facebook SDK
{: #facebook-auth-cordova-ios-sdk}
1. 下載包含 [{{site.data.keyword.Bluemix_notm}} Mobile Services SDK for iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master) 的保存檔。

1. 移至 `Sources/Authenticators/IMFFacebookAuthentication` 目錄，並將所有檔案複製（拖放）到 Xcode 中的 iOS 專案。複製下列檔案：
  * IMFDefaultFacebookAuthenticationDelegate.h
  * IMFDefaultFacebookAuthenticationDelegate.m
  * IMFFacebookAuthenticationDelegate.h
  * IMFFacebookAuthenticationHandler.h
  * IMFFacebookAuthenticationHandler.m

	Xcode 提示時，選取**複製檔案...**。

1. 下載並安裝 [Facebook SDK 3.19 版](https://developers.facebook.com/resources/facebook-ios-sdk-3.19.pkg)。

1. Facebook SDK 將安裝至 `~/Documents/FacebookSDK` 目錄。導覽至該目錄，並將 `FacebookSDK.framework` 檔案複製（拖放）到 Xcode 中的 iOS 專案。

1. 	在 Xcode 左窗格中按一下專案根目錄，然後選取**建置階段**。

1. 將 `FacebookSDK.framework` 檔案新增至**鏈結二進位檔與檔案庫**中的已鏈結檔案庫清單。

 請參閱[配置 iOS Platform for Facebook 鑑別](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html)。以原生程式碼登錄 `IMFFacebookAuthenticationHandler` API（如**起始設定 {{site.data.keyword.amashort}} 用戶端 SDK** 小節中所述）。請不要以原生程式碼起始設定 `IMFClient`。

將下行新增至應用程式委派的 `application:openURL:sourceApplication:annotation` 方法。此程式碼確保所有 Cordova 外掛程式都會收到個別事件的通知。

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```

## 起始設定 {{site.data.keyword.amashort}} 用戶端 SDK
{: #facebook-auth-cordova-init}

在 Cordova 應用程式中使用下列 JavaScript 程式碼，以起始設定 {{site.data.keyword.amashort}} 用戶端 SDK。

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```

將 *applicationRoute* 及 *applicationGUID* 取代為取自**行動選項**的**路徑**及**應用程式 GUID** 值。

## 測試鑑別
{: #facebook-auth-cordova-test}
在起始設定用戶端 SDK 並登錄 Facebook 鑑別管理程式之後，即可開始對行動後端提出要求。

### 開始之前
您必須使用 {{site.data.keyword.mobilefirstbp}} 樣板，並且在 `/protected` 端點已具有 {{site.data.keyword.amashort}} 所保護的資源。如需相關資訊，請參閱[保護資源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。

1. 嘗試在瀏覽器中將要求傳送給新建行動後端的受保護端點。開啟下列 URL：`{applicationRoute}/protected`。例如：`http://my-mobile-backend.mybluemix.net/protected`。
<br/>使用 MobileFirst Services Starter 樣板所建立之行動後端的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護。瀏覽器中會傳回 `Unauthorized` 訊息。傳回此訊息的原因是只有使用 {{site.data.keyword.amashort}} 用戶端 SDK 所檢測的行動應用程式才能存取這個端點。

1. 使用 Cordova 應用程式以對相同的端點提出要求。起始設定 `BMSClient` 之後，請新增下列程式碼：

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error){
    	console.log("failure", error);
    }
	var request = new MFPRequest("/protected", MFPRequest.GET);
	request.send(success, failure);
	```

1. 執行您的應用程式。即會蹦現「Facebook 登入」畫面：

	![影像](images/android-facebook-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![影像](images/ios-facebook-login.png)

	> 如果您未在裝置上安裝 Facebook 應用程式，或目前未登入 Facebook，則此畫面可能會稍微不同。

1. 按一下**確定**，以授權 {{site.data.keyword.amashort}} 使用 Facebook 使用者身分來進行鑑別。

1. 	當要求成功時，在 LogCat 公用程式或 Xcode 主控台中會有下列輸出：

	![Android 的 Facebook 鑑別成功訊息](images/android-facebook-login-success.png)

	![iOS 的 Facebook 鑑別成功訊息](images/ios-facebook-login-success.png)
