---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 開始使用 {{site.data.keyword.amashort}}
{: #gettingstarted}

使用 {{site.data.keyword.amafull}} 服務，將安全新增至您的行動應用程式。您可以配置用戶端授權，以存取在 {{site.data.keyword.Bluemix}} 上執行的受保護後端資源。使用身分提供者（Google 及 Facebook）或自訂身分來鑑別使用者，以及授與受保護後端資源和 Web 應用程式的存取權。
{:shortdesc}

**附註：**{{site.data.keyword.amashort}} 服務先前稱為 Advanced Mobile Access。


若要開始進行 {{site.data.keyword.amashort}} 服務，請執行下列動作：

1. 使用下列其中一個選項來建立連結或取消連結的服務：
 * 使用型錄中的 **MobileFirst Services Starter** 樣板來建立 {{site.data.keyword.Bluemix_notm}} 應用程式。這會建立連結至 {{site.data.keyword.Bluemix_notm}} 後端應用程式的 {{site.data.keyword.amashort}} 服務。
 * 使用 {{site.data.keyword.amashort}} 主控台來建立 {{site.data.keyword.amashort}} 服務。您可以將服務連結至現有的後端應用程式，並且在 {{site.data.keyword.amashort}} 主控台中加以配置。

   當您使用 MobileFirst Services Starter 時，會取得在 IBM {{site.data.keyword.Bluemix_notm}} 上執行的 Node.js 運行環境實例來實作自訂後端邏輯。會將一組提供安全、資料、推送及監視功能的核心行動服務連結至該 Node.js 應用程式。建立 {{site.data.keyword.Bluemix_notm}} Node.js 應用程式之後，即可設定開發環境，並開始使用 {{site.data.keyword.Bluemix_notm}} Mobile Services SDK。您可以使用 SDK，透過簡單的 API 呼叫來存取連結至雲端應用程式的服務。

	如需如何建立及使用專案、應用程式及服務的相關資訊，請參閱 [IBM Bluemix 行動儀表板](https://console.{DomainName}/docs/mobile/index.html)。

2. 保護伺服器端資源的安全。

   使用已啟用行動功能的 OAuth 安全，來保護 Node.js 或 Liberty for Java&trade; 運行環境上執行的行動後端資源。如需相關資訊，請參閱[保護資源](protecting-resources.html)。若要進一步瞭解預設行動後端應用程式，請參閱 [bms-hellotodo-strongloop ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop "外部鏈結圖示"){: new_window} 範例應用程式。

3. 設定您的核心 {{site.data.keyword.amashort}} 開發環境。

  ####用戶端開發
  {: #client-development}

	您可以將 {{site.data.keyword.amashort}} SDK 新增至現有的 Android、iOS 或 Cordova 應用程式，如下所示：
   * Android：（[設定 Android SDK](getting-started-android.html)）[範例 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication "外部鏈結圖示"){: new_window}
    * iOS (Swift SDK)：（[設定 iOS Swift SDK](getting-started-ios-swift-sdk.html)）[範例 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "外部鏈結圖示"){: new_window}    
   * Cordova：（[設定 Cordova 外掛程式](getting-started-cordova.html)）[範例 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication "外部鏈結圖示"){: new_window}


 ####Web 開發
 {: #web-development}

   {{site.data.keyword.amashort}} 服務可以保護您的 Web 應用程式，而不需要特殊的 SDK。除了 {{site.data.keyword.amashort}} 服務提供的保護外，您還可以運用不同的身分提供者。{{site.data.keyword.amashort}} 整合可讓任何 Web 應用程式（不論其實作何種技術）充分運用 OAuth2 通訊協定。如需將 {{site.data.keyword.amashort}} Web 應用程式設定為使用不同身分提供者來存取 {{site.data.keyword.amashort}} 服務的相關資訊，請參閱：

   * [啟用 Web 應用程式的 Facebook 鑑別](facebook-auth-web.html)
   * [啟用 Web 應用程式的 Google 鑑別](google-auth-web.html)
   * [啟用 Web 應用程式的自訂鑑別](custom-auth-web.html)

**選用項目：**配置應用程式的身分提供者。您可以為每個應用程式配置一個身分提供者。配置身分提供者可讓行動應用程式使用者利用其現有 Facebook 或 Google+ 帳戶進行登入。或者，您可以建立自訂鑑別來定義使用者的登入方式。
   * [使用 Facebook 認證鑑別使用者](facebook-auth-overview.html)
   * [使用 Google 認證鑑別使用者](google-auth-overview.html)
   * [使用自訂身分提供者鑑別使用者](custom-auth.html)

## 指導教學及範例
{: #samples}

* [android-helloauthentication 範例 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication "外部鏈結圖示"){: new_window}
* [ios-helloauthentication 範例 (Swift SDK) ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "外部鏈結圖示"){: new_window}

## SDK
{: #sdk}

* [核心 SDK (Android) ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core "外部鏈結圖示"){: new_window}

* [ios-helloauthentication 範例 (Swift SDK) ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "外部鏈結圖示"){: new_window}

* [自訂鑑別 - 簡式範例 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "外部鏈結圖示"){: new_window}

* [自訂鑑別 - 進階範例 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management "外部鏈結圖示"){: new_window}


