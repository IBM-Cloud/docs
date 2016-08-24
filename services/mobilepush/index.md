	---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Getting started with {{site.data.keyword.mobilepushshort}}
{: #gettingstartedtemplate}
<<<<<<< HEAD
Last updated: 21 August 2016
=======
Last updated: 16 August 2016
>>>>>>> 659bec289ef614725483fb60c244d9f26cadce1f
{: .last-updated}

{:shortdesc}

<<<<<<< HEAD
The {{site.data.keyword.mobilepushshort}} service provides a unified platform to send and manage mobile and web {{site.data.keyword.mobilepushshort}} that are targeted to iOS, Android mobile platforms, Google Chrome and Mozilla Firefox web browsers. The {{site.data.keyword.mobilepushshort}} service manages the mapping of your application users to their devices, device platform, web browsers and handles dispatching push notifications to them. With this service, you can send broadcasts, unicasts, (based on deviceID), and also tags (or topics) as push notifications to your mobile and web browser application users. You can also use an SDK and [REST APIs](https://mobile.{DomainName}/imfpushrestapidocs/) to further develop your client applications.
=======
The {{site.data.keyword.mobilepushshort}} service provides a unified platform to send and manage mobile {{site.data.keyword.mobilepushshort}} that are targeted to iOS and Android platforms. The {{site.data.keyword.mobilepushshort}} service manages the mapping of your application users to their devices, device platform, and handles dispatching push notifications to them. With this service, you can send broadcasts, unicasts, (based on deviceID), and also tags (or topics) as push notifications to your mobile application users. You can also use an SDK and [REST APIs](https://mobile.{DomainName}/imfpushrestapidocs/) to further develop your client applications.
>>>>>>> 659bec289ef614725483fb60c244d9f26cadce1f

This section describes how to set up basic push notifications. When you use a basic notification, the notifications are broadcast instead of reaching a specific set of users using tags.

1. [Configure credentials for a notification provider](t__main_push_config_provider.html)
2. [Enable mobile app to receive notifications](c_enable_push.html)
3. [Send basic notifications](t_send_push_notifications.html)

# Related Links
{: #rellinks}

* [Overview](c_overview_push.md){: new_window}

## Tutorials and samples {:id="samples"}
{: #samples}
* [Android helloPush sample application](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/){: new_window}
- [Cordova sample application](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-hellopush){: new_window}
* [iOS helloPush sample application (Obj-C)](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-hellopush/){: new_window}
* [iOS helloPush sample application (Swift)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellopush){: new_window}

## SDK
{: #sdk}
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-push){: new_window}
* [Cordova SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window}
* [iOS SDK (Obj-C)](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}
* [iOS SDK (Swift)](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/zip/master){: new_window}

## API Reference
{: #api}
* [Push API Reference (Android)](https://classicdocs.ng.bluemix.net/docs/api/content/api/mobilefirst/android/push-api-doc/overview-summary.html){: new_window}
* [IMFPush API reference iOS](https://classicdocs.ng.bluemix.net/docs/api/content/api/mobilefirst/ios/IMFPush_api-doc/html/index.html){: new_window}
* [BMSPush API reference iOS (Swift)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/blob/development/Apple Docs/index.html){: new_window}
* [REST API Reference](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window}
