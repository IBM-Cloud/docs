---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"
---
{:screen: .screen}
{:shortdesc: .shortdesc}

# 啟用 Cordova 應用程式的 Google 鑑別
{: #google-auth-cordova}


若要配置 {{site.data.keyword.amafull}} Cordova 應用程式進行 Google 鑑別整合，您必須以 Cordova 應用程式的原生程式碼（Java、Objective-C 或 Swift）進行變更。每一個平台都必須分別進行配置。使用原生開發環境，以原生程式碼進行變更（例如，在 Android Studio 或 Xcode 中）。

## 開始之前
{: #before-you-begin}
您必須具有：
* 使用 {{site.data.keyword.amashort}} 用戶端 SDK 進行檢測的 Cordova 專案。如需相關資訊，請參閱[設定 Cordova 外掛程式](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)。  
* {{site.data.keyword.amashort}} 服務所保護的 {{site.data.keyword.Bluemix_notm}} 應用程式實例。如需如何建立 {{site.data.keyword.Bluemix_notm}} 後端應用程式的相關資訊，請參閱[開始使用](index.html)。
* （選用）熟悉下列各節：
   * [啟用 Android 應用程式的 Google 鑑別](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)
   * [啟用 iOS 應用程式的 Google 鑑別](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html)


## 配置 Android 平台
{: #google-auth-cordova-android}

配置 Cordova 應用程式的 Android 平台進行 Google 鑑別整合所需的步驟，與原生應用程式所需的步驟極為類似。請參閱[在 Android 應用程式中啟用 Google 鑑別](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)，並設定下列項目：

* 配置 Android 平台的 Google 專案
* 配置 {{site.data.keyword.amashort}} 進行 Google 鑑別

### 配置適用於 Android Cordova 的 {{site.data.keyword.amashort}} 用戶端 SDK


2. 在 Android 專案資料夾中，開啟應用程式模組的 `build.gradle` 檔案（**不是**專案 `build.gradle` 檔案）。
尋找 dependencies 區段，並新增用戶端 SDK 的編譯相依關係：

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'googleauthentication',
        version: '1.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```

2. 按一下**工具 > Android > 將專案與 Gradle 檔案同步化**，以將專案與 Gradle 同步化。

3. 若為 Cordova 應用程式，請以 JavaScript 程式碼（而不是 Java 程式碼）起始設定 {{site.data.keyword.amashort}} 用戶端 SDK。仍然必須以原生程式碼登錄 `GoogleAuthenticationManager` API。將此程式碼新增至主要活動 `onCreate` 方法： 

	```Java
	GoogleAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
	```

1. 將下列程式碼新增至您的活動中：
 
 	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		GoogleAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
```

## 配置 iOS 平台
{: #google-auth-cordova-ios}

配置 Cordova 應用程式的 iOS 平台進行 Google 鑑別整合所需的步驟，與原生應用程式的步驟類似。主要差異是 Cordova CLI 目前不支援 CocoaPods 相依關係管理程式。您必須手動新增與 Google 鑑別整合所需的檔案。如需相關資訊，請參閱[在 iOS 應用程式中啟用 Google 鑑別](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html)。請完成下列步驟：

* 配置 iOS 平台的 Google 專案
* 配置 {{site.data.keyword.amashort}} 進行 Google 鑑別

### 手動安裝用於 Google 鑑別的 {{site.data.keyword.amashort}} SDK 及 Google SDK
{: #google-auth-cordova-ios-sdk}
1. 下載包含 [{{site.data.keyword.Bluemix}} Mobile Services SDK for iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master) 的保存檔。

1. 移至 `Sources/Authenticators/IMFGoogleAuthentication` 目錄，並將所有檔案複製（拖放）到 Xcode 中的 iOS 專案。您需要複製的檔案為：

	* IMFDefaultGoogleAuthenticationDelegate.h
	* IMFDefaultGoogleAuthenticationDelegate.m
	* IMFGoogleAuthenticationDelegate.h
	* IMFGoogleAuthenticationHandler.h
	* IMFGoogleAuthenticationHandler.m

	選取**複製檔案...** 勾選框。

1. 下載並安裝 [Google+ iOS SDK](http://goo.gl/9cTqyZ)。

1. 遵循[開始將 Google+ 整合至 iOS 應用程式](https://developers.google.com/+/mobile/ios/getting-started)指導教學的步驟 2，以將 Google+ iOS SDK 整合至 Xcode 專案。

繼續[配置 iOS 平台進行 Google 鑑別](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html)的**配置 iOS 專案進行 Google 鑑別**小節。以原生程式碼登錄 `IMFGoogleAuthenticationHandler`（如`起始設定 {{site.data.keyword.amashort}} 用戶端 SDK` 小節中所述）。請不要以原生程式碼起始設定 `IMFClient`（在下節中，是以 JavaScript 起始設定用戶端）。

將此行增至應用程式委派的 `application:openURL:sourceApplication:annotation` 方法。如此可確保所有 Cordova 外掛程式都會收到個別事件的通知。

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];
```
{: codeblock}

## 起始設定 {{site.data.keyword.amashort}} 用戶端 SDK
{: #google-auth-cordova-initialize}

在 Cordova 應用程式中使用下列 JavaScript 程式碼，以起始設定 {{site.data.keyword.amashort}} 用戶端 SDK。

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```
{: codeblock}

將 `applicationRoute` 及 `applicationGUID` 值取代為應用程式**路徑**及**應用程式 Guid** 值。您可以從儀表板上的應用程式頁面內按一下**行動選項**按鈕，來尋找這些值。
	



##起始設定 {{site.data.keyword.amashort}} AuthorizationManager
在 Cordova 應用程式中使用下列 JavaScript 程式碼，以起始設定 {{site.data.keyword.amashort}} AuthorizationManager。

```JavaScript
  MFPAuthorizationManager.initialize("tenantId");
  ```
{: codeblock}

將 `tenantId` 值取代為 {{site.data.keyword.amashort}} 服務 `tenantId`。按一下 {{site.data.keyword.amashort}} 服務磚上的**顯示認證**按鈕，即可找到此值。





## 測試鑑別
{: #google-auth-cordova-test}
起始設定用戶端 SDK 之後，即可開始對行動後端應用程式提出要求。

### 開始之前
{: #google-auth-cordova-testing-before}
您必須在 `/protected` 端點具有 {{site.data.keyword.amashort}} 所保護的後端應用程式。如果您需要設定 `/protected` 端點，請參閱[保護資源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。


1. 開啟 `{applicationRoute}/protected`（例如 `http://my-mobile-backend.mybluemix.net/protected`），嘗試在桌面瀏覽器中將要求傳送給行動後端應用程式的受保護端點。

1. 使用「MobileFirst Services 樣板」所建立之行動後端應用程式的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護，因此只有使用 {{site.data.keyword.amashort}} Client SDK 所檢測的行動應用程式才能存取它。因此，您會在桌面瀏覽器中看到 `Unauthorized`。

1. 使用 Cordova 應用程式以對相同的端點提出要求。起始設定 `BMSClient` 之後，請新增下列程式碼。

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
{: codeblock}

1. 執行您的應用程式。即會顯示 Google 登入畫面。

	![Google 登入畫面](images/android-google-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![Google 登入畫面](images/ios-google-login.png)
	
	如果您未在裝置上安裝 Facebook 應用程式，或目前未登入 Facebook，則此畫面可能會稍微不同。

1. 按一下**確定**，即會授權 {{site.data.keyword.amashort}} 使用 Google 使用者身分來進行鑑別。

1. 您的要求應該會成功。視使用的平台而定，您會在 LogCat/Xcode 主控台中看到下列輸出：

	![Android 上的程式碼 Snippet](images/android-google-login-success.png)

	![iOS 上的程式碼 Snippet](images/ios-google-login-success.png)
