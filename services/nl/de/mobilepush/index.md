---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Einführung in {{site.data.keyword.mobilepushshort}}

{: #gettingstartedtemplate}


{:shortdesc}

Push Notifications Service bietet eine gemeinsame Plattform zum Senden und Verwalten von mobilen Push-Benachrichtigungen, die als Ziel iOS- und Android-Plattformen haben. Dieser Service verwaltet die Zuordnung Ihrer Anwendungsbenutzer zu den zugehörigen Geräten und zur Geräteplattform und führt das Senden von Push-Benachrichtigungen an die Benutzer aus. Mit diesem Service können Sie Rundsendungen und Unicasts (auf der Basis der 'deviceID') sowie tagbasierte (themenbasierte) Push-Benachrichtigungen an Ihre Benutzer mobiler Anwendungen senden. Sie können auch ein Software Development Kit (SDK) und  [REST-APIs](https://mobile.{DomainName}/imfpushrestapidocs/) verwenden, um Ihre Clientanwendungen weiter zu entwickeln.

In diesem Abschnitt wird beschrieben, wie einfache Push-Benachrichtigungen eingerichtet werden. Wenn Sie eine einfache Benachrichtigung verwenden, wird die Benachrichtigung als Rundsendung versendet und nicht mithilfe von Tags an einen bestimmten Benutzerkreis.

1. [Berechtigungsnachweise für einen Benachrichtigungsprovider konfigurieren](t__main_push_config_provider.html)
2. [Mobile App für den Empfang von Benachrichtungen aktivieren](c_enable_push.html)
3. [Einfache Push-Benachrichtigungen senden](t_send_push_notifications.html)

# Zugehörige Links
{: #rellinks}

* [Übersicht](c_overview_push.md){: new_window}

## Lernprogramme und Beispiele {:id="samples"}
{: #samples}
* [Android helloPush sample application](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/){: new_window}
- [Cordova sample application](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-hellopush){: new_window}
* [iOS helloPush sample application](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-hellopush/){: new_window}

## Software-Development-Kit (SDK)
{: #sdk}
* [Android-SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-push){: new_window}
* [Cordova-SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window}
* [iOS-SDK](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}

## API-Referenz
{: #api}
* [Push-API-Referenz (Android)](https://classicdocs.ng.bluemix.net/docs/api/content/api/mobilefirst/android/push-api-doc/overview-summary.html){: new_window}
* [IMFPush-API-Referenz (iOS)](https://classicdocs.ng.bluemix.net/docs/api/content/api/mobilefirst/ios/IMFPush_api-doc/html/index.html){: new_window}
* [REST-API-Referenz](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window}
