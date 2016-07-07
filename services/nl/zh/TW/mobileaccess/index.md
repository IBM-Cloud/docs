---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# 開始使用 {{site.data.keyword.amashort}}
{: #gettingstarted}
*前次更新：2016 年 6 月 15 日*
{: .last-updated}

利用 {{site.data.keyword.amafull}} 服務，將安全功能新增至您的行動應用程式。您可以配置用戶端鑑別和身分提供者，讓使用者可以利用其現有的 Google 或 Facebook 帳戶登入應用程式。{:shortdesc}

**附註：**{{site.data.keyword.amashort}} 服務先前稱為 Advanced Mobile Access。


若要開始進行 {{site.data.keyword.amashort}} 服務，請遵循下列步驟：

1.  使用 {{site.data.keyword.Bluemix_notm}} 儀表板來建立行動後端應用程式，或配置現有的行動後端應用程式。
  - 您可以從 Bluemix 型錄中選取 MobileFirst Services Starter。
  - 或者，您可以將服務連結至現有的應用程式，並對其進行配置。

   當您使用 MobileFirst Services Starter 時，會取得在 IBM {{site.data.keyword.Bluemix_notm}} 上執行的 Node.js 運行環境實例來實作自訂後端邏輯。會將一組提供安全、資料、推送及監視功能的核心行動服務連結至該 Node.js 應用程式。建立 {{site.data.keyword.Bluemix_notm}} Node.js 應用程式之後，即可設定開發環境，並開始使用 {{site.data.keyword.Bluemix_notm}} Mobile Services SDK。您可以使用 SDK，透過簡單的 API 呼叫來存取連結至雲端應用程式的服務。
   
  
1. 保護伺服器端資源的安全。

   使用已啟用行動功能的 OAuth 安全，來保護 Node.js 或 Liberty for Java&trade; 運行環境上執行的行動後端資源。如需相關資訊，請參閱[保護資源](protecting-resources.html)。若要進一步瞭解預設行動後端應用程式，請參閱 [bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop)。

1. 設定您的核心 {{site.data.keyword.amashort}} 用戶端開發環境。

   您可以將 {{site.data.keyword.amashort}} SDK 新增至現有的 Android、Cordova 或 iOS 應用程式。您也可以下載 HelloAuthentication 範例應用程式。
   * **Android**：（[設定 Android SDK](getting-started-android.html)）（[範例](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication)）
  
   * **Cordova**：（[設定 Cordova 外掛程式](getting-started-cordova.html)）（[範例](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication)）
  
   * **iOS (Swift SDK)**：（[設定 iOS Swift SDK](getting-started-ios-swift-sdk.html)）（[範例](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication)）
  
   * **iOS (Objective-C SDK)**：（[設定 iOS Object-C SDK](getting-started-ios.html)）（[範例](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication)）
   
   **附註：**雖然仍然完全支援 Objective-C SDK 且將它視為 Bluemix Mobile Services 的主要 SDK，不過預計在今年稍晚中斷使用此 SDK，改用新的 Swift SDK。如果您要建立應用程式，高度建議您使用 Swift SDK（請參閱[設定 iOS Swift SDK](getting-started-ios-swift-sdk.html)）。

1. **選用項目：**配置應用程式的身分提供者。您可以為每個應用程式配置一個身分提供者。配置身分提供者可讓行動應用程式使用者利用其現有 Facebook 或 Google+ 帳戶進行登入。或者，您可以建立自訂鑑別來定義使用者的登入方式。
   * [使用 Facebook 認證鑑別使用者](facebook-auth-overview.html)
   * [使用 Google 認證鑑別使用者](google-auth-overview.html)
   * [使用自訂身分提供者鑑別使用者](custom-auth.html)

1. 配置應用程式監視及記載。

    如需相關資訊，請參閱[監視應用程式](app-monitoring.html)。

# 相關鏈結
{: #rellinks}

## 指導教學與範例
{: #samples}
* [android-helloauthentication 範例](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication){: new_window}
* [ios-helloauthentication 範例 (Swift SDK)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication){: new_window}
* [ios-helloauthentication 範例 (Objective-C SDK)](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication){: new_window}

## SDK
{: #sdk}
* [核心 SDK (Android)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [核心 SDK（Cordova 外掛程式）](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
* [核心 SDK (iOS - Swift) ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [核心 SDK（iOS - Objective-C - 已淘汰）](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}
* [自訂鑑別 - 簡單範例](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
* [自訂鑑別 - 進階範例](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## API 參考資料
{: api}
* [Android](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html){: new_window}
* [iOS (Objective-C SDK) - 已淘汰](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html){: new_window}


## 相關鏈結
{: #general}
* [概觀](overview.html){: new_window}
