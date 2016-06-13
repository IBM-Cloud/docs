---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobilepushshort}} 入门

{: #gettingstartedtemplate}


{:shortdesc}

Push Notification Service 提供一个统一平台来发送和管理针对 iOS 和 Android 平台的移动推送通知。此服务可管理应用程序用户到设备的映射、管理设备平台以及处理向用户分派推送通知。使用此服务，您可以向移动应用程序用户发送广播、单点广播（基于 deviceID），以及基于标记（或基于主题）的推送通知。还可以使用 SDK 和 [REST API](https://mobile.{DomainName}/imfpushrestapidocs/) 来进一步开发您的客户机应用程序。

本部分描述了如何设置基本推送通知。使用基本通知时，通知为广播，而不是使用标记发送给一组特定用户。

1. [配置通知提供者凭证](t__main_push_config_provider.html)
2. [使移动应用程序能够接收通知](c_enable_push.html)
3. [发送基本通知](t_send_push_notifications.html)

# 相关链接
{: #rellinks}

* [概述](c_overview_push.md){: new_window}

## 教程和样本 {:id="samples"}
{: #samples}
* [Android helloPush 样本应用程序](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/){: new_window}
- [Cordova 样本应用程序](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-hellopush){: new_window}
* [iOS helloPush 样本应用程序](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-hellopush/){: new_window}

## SDK
{: #sdk}
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-push){: new_window}
* [Cordova SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window}
* [iOS SDK](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}

## API 参考
{: #api}
* [Push API 参考 (Android)](https://classicdocs.ng.bluemix.net/docs/api/content/api/mobilefirst/android/push-api-doc/overview-summary.html){: new_window}
* [IMFPush API 参考 (iOS)](https://classicdocs.ng.bluemix.net/docs/api/content/api/mobilefirst/ios/IMFPush_api-doc/html/index.html){: new_window}
* [REST API 参考](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window}
