---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 開始使用 {{site.data.keyword.amashort}}
{: #gettingstarted}
*前次更新：2016 年 3 月 21 日*

利用 {{site.data.keyword.amafull}} 服務，將安全及監視功能新增至您的行動式應用程式。您可以配置用戶端鑑別和身分提供者，讓使用者可以利用其現有的 Google 或 Facebook 帳戶登入應用程式。此外，還可以將監視功能新增至應用程式，以同時啟用用戶端記載和使用情形統計資料。
{:shortdesc}

**附註：**{{site.data.keyword.amashort}} 服務先前稱為 Advanced Mobile Access。


若要開始進行 {{site.data.keyword.amashort}} 服務，請遵循下列步驟：

1. 設定您的用戶端開發環境。
您可以將 {{site.data.keyword.amashort}} SDK 新增至現有的 Android、Cordova 或 iOS 應用程式。您也可以下載 HelloAuthentication 範例應用程式。
   * **Android**：([SDK](getting-started-android.html))（[範例](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication)）
   * **Cordova**：([SDK](getting-started-cordova.html))（[範例](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication)）
   * **iOS (Swift-C SDK)**：([SDK](getting-started-ios-swift-sdk.html))（[範例](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication)）
   * **iOS (Objective-C SDK)**：([SDK](getting-started-ios.html))（[範例](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication)）

1. 保護伺服器端資源的安全。使用已啟用行動式功能的 OAuth 安全，來保護 Node.js 或 Liberty for Java&trade; 執行時期上執行的行動式後端資源。如需相關資訊，請參閱[保護資源](protecting-resources.html)。

1. 選用項目：配置應用程式的身分提供者。您可以為每個應用程式配置一個身分提供者。配置身分提供者可讓行動式應用程式使用者利用其現有 Facebook 或 Google+ 帳戶進行登入。或者，您可以建立自訂鑑別來定義使用者的登入方式。
   * [Facebook](facebook-auth-overview.html)
   * [Google](google-auth-overview.html)
   * [自訂](custom-auth.html)

1. 配置應用程式監視及記載。如需相關資訊，請參閱[應用程式監視](app-monitoring.html)。

# 相關鏈結
{: #rellinks}

## 指導教學與範例
{: #samples}
* [android-helloauthentication 範例](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication){: new_window}
* [ios-helloauthentication 範例 (Swift SDK)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication){: new_window}
* [ios-helloauthentication 範例 (Objective-C SDK)](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication){: new_window}

## SDK
{: #sdk}
* [Core SDK (Android)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [Core SDK（Cordova 外掛程式）](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
* [Core SDK (iOS - Swift) ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [Core SDK (iOS - Objective-C) ](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}
* [自訂鑑別 - 簡式範例](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
* [自訂鑑別 - 進階範例](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## API 參考資料
{: api}
* [Android](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html){: new_window}
* [iOS (Objective-C SDK)](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html){: new_window}


## 相關鏈結
{: #general}
* [概觀](overview.html){: new_window}
