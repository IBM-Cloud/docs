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


{:shortdesc}

The Push Notifications service provides a unified platform to send and manage mobile push notifications that are targeted to iOS and Android platforms. This service manages the mapping of your application users to their devices, device platform, and handles dispatching push notifications to them. With this service, you can send broadcasts, unicasts, (based on deviceID), and also tags (or topics) push notifications to your mobile application users. You can also use an SDK and [REST APIs](https://mobile.{DomainName}/imfpushrestapidocs/) to further develop your client applications.

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
* [iOS helloPush sample application](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-hellopush/){: new_window}

## SDK
{: #sdk}
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-push){: new_window}
* [Cordova SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window}
* [iOS SDK](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}

## API Reference
{: #api}
* [Push API Reference (Android)](https://classicdocs.ng.bluemix.net/docs/api/content/api/mobilefirst/android/push-api-doc/overview-summary.html){: new_window}
* [IMFPush API reference iOS](https://classicdocs.ng.bluemix.net/docs/api/content/api/mobilefirst/ios/IMFPush_api-doc/html/index.html){: new_window}
* [REST API Reference](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window}
