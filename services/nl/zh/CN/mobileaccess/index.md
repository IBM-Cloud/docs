---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# {{site.data.keyword.amashort}} 入门
{: #gettingstarted}
*上次更新时间：2016 年 6 月 15 日*
{: .last-updated}

使用 {{site.data.keyword.amafull}} 服务，将安全功能添加到移动应用程序。您可以配置客户端认证和身份提供者，以便用户可使用其现有 Google 或 Facebook 帐户登录应用程序。
{:shortdesc}

**注：**{{site.data.keyword.amashort}} 服务先前称为 Advanced Mobile Access。


要启动和运行 {{site.data.keyword.amashort}} 服务，请执行以下步骤：

1.  使用 {{site.data.keyword.Bluemix_notm}}“仪表板”，创建移动后端应用程序，或者配置现有的移动后端应用程序。
  - 您可以从 Bluemix 目录中选择 MobileFirst Services Starter。
  - 或者，您可以将服务与现有应用程序绑定，并对其进行配置。

   使用 MobileFirst Services Starter 时，您会获得在 IBM {{site.data.keyword.Bluemix_notm}} 上运行的 Node.js 运行时的实例，以实现定制后端逻辑。此外，还会将一组提供了安全性、数据、推送和监视功能的核心移动服务绑定到该 Node.js 应用程序。创建 {{site.data.keyword.Bluemix_notm}} Node.js 应用程序后，可设置开发环境，并开始使用 {{site.data.keyword.Bluemix_notm}} Mobile Services SDK。您可以使用 SDK 通过简单的 API 调用来访问绑定到云应用程序的服务。
   
  
1. 保护服务器端资源。

   通过支持移动的 OAuth 安全性，保护正在 Node.js 或 Liberty for Java&trade; 运行时上运行的移动后端资源。有关更多信息，请参阅[保护资源](protecting-resources.html)。要了解有关缺省移动后端应用程序的更多信息，请参阅 [bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop)。

1. 设置核心 {{site.data.keyword.amashort}} 客户端开发环境。

   您可以将 {{site.data.keyword.amashort}} SDK 添加到现有 Android、Cordova 或 iOS 应用程序。您还可以下载 HelloAuthentication 样本应用程序。
   * **Android**：（[设置 Android SDK](getting-started-android.html)）（[样本](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication)）
  
   * **Cordova**：（[设置 Cordova 插件](getting-started-cordova.html)）（[样本](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication)）
  
   * **iOS (Swift SDK)**：（[设置 iOSSwift SDK](getting-started-ios-swift-sdk.html)）（[样本](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication)）
  
   * **iOS (Objective-C SDK)**：（[设置 iOS Object-C SDK](getting-started-ios.html)）（[样本](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication)）
   
   **注：**虽然 Objective-C SDK 仍受到完全支持，且仍视为 Bluemix Mobile Services 的主 SDK，但是有计划要在今年晚些时候停止使用此 SDK，以支持新的 Swift SDK。如果您在创建应用程序，我们强烈建议您使用 Swift SDK（请参阅[设置 iOS Swift SDK](getting-started-ios-swift-sdk.html)）。

1. **可选：**为应用程序配置身份提供者。可以每个应用程序配置一个身份提供者。配置身份提供者使移动应用程序的用户能够使用其现有 Facebook 或 Google+ 帐户登录。或者，您可以定义用户如何通过创建定制认证来登录。
   * [使用 Facebook 凭证认证用户](facebook-auth-overview.html)
   * [使用 Google 凭证认证用户](google-auth-overview.html)
   * [使用定制身份提供者认证用户](custom-auth.html)

1. 配置应用程序监视和日志记录。

    有关更多信息，请参阅[监视应用程序](app-monitoring.html)。

# 相关链接
{: #rellinks}

## 教程和样本
{: #samples}
* [android-helloauthentication 样本](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication){: new_window}
* [ios-helloauthentication 样本 (Swift SDK)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication){: new_window}
* [ios-helloauthentication 样本 (Objective-C SDK)](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication){: new_window}

## SDK
{: #sdk}
* [核心 SDK (Android)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [核心 SDK（Cordova 插件）](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
* [核心 SDK (iOS - Swift)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [核心 SDK（iOS - Objective-C - 不推荐）](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}
* [定制认证 - 简单样本](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
* [定制认证 - 高级样本](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## API 参考
{: api}
* [Android](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html){: new_window}
* [iOS (Objective-C SDK) - 不推荐](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html){: new_window}


## 相关链接
{: #general}
* [概述](overview.html){: new_window}
