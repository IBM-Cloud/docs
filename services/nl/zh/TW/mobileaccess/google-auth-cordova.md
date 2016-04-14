---

copyright:
  years: 2015, 2016

---

# 在 Cordova 應用程式中啟用 Google 鑑別
{: #google-auth-cordova}
若要配置 Cordova 應用程式進行 Google 鑑別整合，您必須以 Cordova 應用程式的原生程式碼（例如，以 Java、Objective-C、Swift）進行變更。每一個平台都必須分別進行配置。使用原生開發環境，以原生程式碼進行變更（例如，在 Android Studio 或 Xcode 中）。

## 開始之前
{: #before-you-begin}
* 您必須具有 {{site.data.keyword.amashort}} 所保護的資源，以及使用 {{site.data.keyword.amashort}} Client SDK 所檢測的 Cordova 專案。如需相關資訊，請參閱[開始使用 {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) 及[設定 Cordova 外掛程式](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)。  
* 使用 {{site.data.keyword.amashort}} Server SDK，手動保護後端應用程式。如需相關資訊，請參閱[保護資源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。
* （選用）熟悉下列各節：
   * [在 Android 應用程式中啟用 Google 鑑別](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)
   * [在 iOS 應用程式中啟用 Google 鑑別](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html)


## 配置 Android 平台
{: #google-auth-cordova-android}

配置 Cordova 應用程式的 Android 平台進行 Google 鑑別整合所需的步驟，與原生應用程式所需的步驟極為類似。如需相關資訊，請參閱[在 Android 應用程式中啟用 Google 鑑別](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)。設定下列部分：

* 配置 Android 平台的 Google 專案
* 配置 {{site.data.keyword.amashort}} 進行 Google 鑑別
* 配置 {{site.data.keyword.amashort}} Client SDK for Android

配置 Cordova 應用程式時的唯一差異是您必須以 JavaScript 程式碼（而非以 Java 程式碼）來起始設定 {{site.data.keyword.amashort}} Client SDK。仍然必須以原生程式碼登錄 `GoogleAuthenticationManager` API。

## 配置 iOS 平台
{: #google-auth-cordova-ios}

配置 Cordova 應用程式的 iOS 平台進行 Google 鑑別整合所需的步驟，與原生應用程式的步驟類似。主要差異是 Cordova CLI 目前不支援 CocoaPods 相依關係管理程式。您必須手動新增與 Google 鑑別整合所需的檔案。如需相關資訊，請參閱[在 iOS 應用程式中啟用 Google 鑑別](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html)。請完成下列步驟：

* 配置 iOS 平台的 Google 專案
* 配置 {{site.data.keyword.amashort}} 進行 Google 鑑別

### 手動安裝用於 Google 鑑別的 {{site.data.keyword.amashort}} SDK 及 Google SDK
{: #google-auth-cordova-ios-sdk}
1. 下載包含 [{{site.data.keyword.Bluemix}} Mobile Services SDK for iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master) 的保存檔

1. 移至 `Sources/Authenticators/IMFGoogleAuthentication` 目錄，並將所有檔案複製（拖放）到 Xcode 中的 iOS 專案。您需要複製的檔案為：

	> * IMFDefaultGoogleAuthenticationDelegate.h
	> * IMFDefaultGoogleAuthenticationDelegate.m
	> * IMFGoogleAuthenticationDelegate.h
	> * IMFGoogleAuthenticationHandler.h
	> * IMFGoogleAuthenticationHandler.m

選取**複製檔案...** 勾選框。

1. 下載並安裝 [Google+ iOS SDK](http://goo.gl/9cTqyZ)。

1. 遵循[開始將 Google+ 整合至 iOS 應用程式](https://developers.google.com/+/mobile/ios/getting-started)指導教學的步驟 2，以將 Google+ iOS SDK 整合至 Xcode 專案。

繼續[配置 iOS 平台進行 Google 鑑別](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html)的**配置 iOS 專案進行 Google 鑑別**小節。以原生程式碼登錄 `IMFGoogleAuthenticationHandler`（如`起始設定 {{site.data.keyword.amashort}} Client SDK` 小節中所述）。您不需要以原生程式碼起始設定 `IMFClient`，這在不久後將以 JavaScript 程式碼完成。

將下行新增至應用程式委派的 `application:openURL:sourceApplication:annotation` 方法。這行確保所有 Cordova 外掛程式都會收到個別事件的通知。

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```

## 起始設定 {{site.data.keyword.amashort}} Client SDK
{: #google-auth-cordova-initialize}

在 Cordova 應用程式中使用下列 JavaScript 程式碼，以起始設定 {{site.data.keyword.amashort}} Client SDK。

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```

將 *applicationRoute* 及 *applicationGUID* 值取代為您取自儀表板上應用程式之**行動式選項**區段的**路徑**及**應用程式 GUID** 值。

## 測試鑑別
{: #google-auth-cordova-test}
起始設定 Client SDK 之後，即可開始對行動式後端提出要求。

### 開始之前
{: #google-auth-cordova-testing-before}
您必須使用 {{site.data.keyword.mobilefirstbp}} 樣板，並且在 `/protected` 端點已具有 {{site.data.keyword.amashort}} 所保護的資源。如果您需要設定 `/protected` 端點，請參閱[保護資源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。


1. 開啟 `{applicationRoute}/protected`（例如 `http://my-mobile-backend.mybluemix.net/protected`），嘗試在桌面瀏覽器中將要求傳送給行動式後端的受保護端點

1. 使用「MobileFirst Services 樣板」所建立之行動式後端的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護，所以只有使用 {{site.data.keyword.amashort}} Client SDK 所檢測的行動式應用程式才能存取它。因此，您會在桌面瀏覽器中看到 `Unauthorized`。

1. 使用 Cordova 應用程式以對相同的端點提出要求。起始設定 `BMSClient` 之後，請新增下列程式碼：

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new MFPRequest("/protected", MFPRequest.GET);
	request.send(success, failure);
	```


1. 執行您的應用程式。即會蹦現「Google 登入」畫面。

	![影像](images/android-google-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![影像](images/ios-google-login.png)
	如果您未在裝置上安裝 Facebook 應用程式，或目前未登入 Facebook，則此畫面可能會稍微不同。
1. 按一下**確定**，即會授權 {{site.data.keyword.amashort}} 使用 Google 使用者身分來進行鑑別。

1. 	您的要求應該會成功。根據使用的平台，您應該會在 LogCat/Xcode 主控台中看到下列輸出：

	![影像](images/android-google-login-success.png)

	![影像](images/ios-google-login-success.png)
