---

copyright:
  years: 2015, 2016
  
---

{:shortdesc: .shortdesc}

# 開始使用 {{site.data.keyword.amashort}}
{: #getting-started}

{{site.data.keyword.amafull}} 服務為您的行動式應用程式提供了安全和監視功能。您可以配置用戶端鑑別和身分提供者。此外，還可以將監視功能新增至應用程式，以同時啟用用戶端記載和使用情形統計資料。

附註：Mobile Client Access 服務先前稱為 Advanced Mobile Access。
{: shortdesc}

1. 在 Bluemix 中設定行動式後端，以及在行動式應用程式中配置 SDK。如需相關資訊，請參閱[開始使用](getting-started.html)。
1. 保護伺服器端資源的安全。使用已啟用行動式功能的 OAuth 安全，來保護 Node.js 或 Liberty for Java&trade; 執行時期上執行的行動式後端資源。如需相關資訊，請參閱[保護資源](protecting-resources.html)。
1. 選用項目：配置應用程式的身分提供者。您可以為每個應用程式配置一個身分提供者。配置身分提供者可讓行動式應用程式使用者利用其現有 Facebook 或 Google+ 帳戶進行登入。或者，您可以建立自訂鑑別來定義使用者的登入方式。
   * [Facebook](facebook-auth-overview.html)
   * [Google](google-auth-overview.html)
   * [自訂](custom-auth.html)
1. 配置應用程式監視及記載。如需相關資訊，請參閱[應用程式監視](app-monitoring.html)。


># 相關鏈結
{:class="linklist"}
>## 指導教學及範例
{:id="samples"}
>* [android-helloauthentication](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication)
>* [ios-helloauthentication](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication)
>
># 相關鏈結
{:class="linklist"}
>## API 參考資料
{:id="api"}
>* [核心 API 參考資料 (Android)](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
>* [核心 API 參考資料 (iOS)](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)
>
># 相關鏈結
{:class="linklist"}
>## SDK
{:id="sdk"}
>* [Core SDK (iOS)](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master)  
>* [bms-clientsdk-android-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)
>* [bms-clientsdk-cordova-plugin-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)
>
>{:elementKind="article" id="rellinks"}
