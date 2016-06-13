---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 開始使用 {{site.data.keyword.mobilepushshort}}

{: #gettingstartedtemplate}


{:shortdesc}

Push Notifications Service 提供統一的平台，來傳送及管理以 iOS 及 Android 平台為目標的行動式推送通知。此服務可管理應用程式使用者與其裝置的對映、裝置平台，以及處理將推送通知分派給他們的作業。使用此服務，您可以將播送、單點播送（根據 deviceID）以及標籤（或主題）推送通知傳送給您的行動式應用程式使用者。也可以使用 SDK 及 [REST API](https://mobile.{DomainName}/imfpushrestapidocs/) 來進一步開發用戶端應用程式。

本節說明如何設定基本推送通知。當您使用基本通知時，通知會是播送，而不是使用標籤來送達一組特定使用者。

1. [配置通知提供者的認證](t__main_push_config_provider.html)
2. [讓行動式應用程式可接收通知](c_enable_push.html)
3. [傳送基本通知](t_send_push_notifications.html)

# 相關鏈結
{: #rellinks}

* [概觀](c_overview_push.md){: new_window}

## 指導教學及範例{:id="samples"}
{: #samples}
* [Android helloPush 範例應用程式](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/){: new_window}
- [Cordova 範例應用程式](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-hellopush){: new_window}
* [iOS helloPush 範例應用程式](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-hellopush/){: new_window}

## SDK
{: #sdk}
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-push){: new_window}
* [Cordova SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window}
* [iOS SDK](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}

## API 參考資料
{: #api}
* [Push API 參考資料 (Android)](https://classicdocs.ng.bluemix.net/docs/api/content/api/mobilefirst/android/push-api-doc/overview-summary.html){: new_window}
* [IMFPush API 參考資料 iOS](https://classicdocs.ng.bluemix.net/docs/api/content/api/mobilefirst/ios/IMFPush_api-doc/html/index.html){: new_window}
* [REST API 參考資料](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window}
