---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.amashort}} 入门
{: #gettingstarted}
*上次更新时间：2016 年 3 月 21 日*

使用 {{site.data.keyword.amafull}} 服务，将安全和监视功能添加到移动应用程序。您可以配置客户端认证和身份提供者，以便用户可使用其现有 Google 或 Facebook 帐户登录应用程序。此外，还可以向应用程序添加监视功能，以同时支持客户机日志记录和使用情况统计信息。
{:shortdesc}

**注：**{{site.data.keyword.amashort}} 服务先前称为 Advanced Mobile Access。


要启动和运行 {{site.data.keyword.amashort}} 服务，请执行以下步骤：

1. 设置客户端开发环境。您可以将 {{site.data.keyword.amashort}} SDK 添加到现有 Android、Cordova 或 iOS 应用程序。您还可以下载 HelloAuthentication 样本应用程序。
   * **Android**：([SDK](getting-started-android.html))（[样本](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication)）
   * **Cordova**：([SDK](getting-started-cordova.html))（[样本](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication)）
   * **iOS (Swift-C SDK)**：([SDK](getting-started-ios-swift-sdk.html))（[样本](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication)）
   * **iOS (Objective-C SDK)**：([SDK](getting-started-ios.html))（[样本](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication)）

1. 保护服务器端资源。通过支持移动的 OAuth 安全性，保护正在 Node.js 或 Liberty for Java&trade; 运行时上运行的移动后端资源。有关更多信息，请参阅[保护资源](protecting-resources.html)。

1. 可选：为应用程序配置身份提供者。可以每个应用程序配置一个身份提供者。配置身份提供者使移动应用程序的用户能够使用其现有 Facebook 或 Google+ 帐户登录。或者，您可以定义用户如何通过创建定制认证来登录。
   * [Facebook](facebook-auth-overview.html)
   * [Google](google-auth-overview.html)
   * [定制](custom-auth.html)

1. 配置应用程序监视和日志记录。有关更多信息，请参阅[应用程序监视](app-monitoring.html)。

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
* [核心 SDK (iOS - Objective-C)](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}
* [定制认证 - 简单样本](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
* [定制认证 - 高级样本](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## API 参考
{: api}
* [Android](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html){: new_window}
* [iOS (Objective-C SDK)](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html){: new_window}


## 相关链接
{: #general}
* [概述](overview.html){: new_window}
