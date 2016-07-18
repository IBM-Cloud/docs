---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introduzione a {{site.data.keyword.mobilepushshort}}
{: #gettingstartedtemplate}
*Ultimo aggiornamento: 14 giugno 2016*
{: .last-updated}

{:shortdesc}

Il servizio push notifications fornisce una piattaforma unificata per inviare e gestire notifiche di push mobili mirate a piattaforme iOS e Android. Questo servizio gestisce l'associazione dei tuoi utenti dell'applicazione ai loro dispositivi e
        alla loro piattaforma del dispositivo e gestisce l'invio a essi di notifiche di push. Con questo servizio, puoi inviare broadcast, unicast (basati su ID dispositivo) e anche notifiche push di tag (o argomenti) ai tuoi utenti delle applicazioni mobili. Puoi anche utilizzare un SDK e le [API REST](https://mobile.{DomainName}/imfpushrestapidocs/) per sviluppare ulteriormente le tue applicazioni client.

Questa sezione descrive come configurare notifiche di push di base. Quando utilizzi una notifica di base, viene eseguita la trasmissione in broadcast
      delle notifiche invece di raggiungere una specifica serie di utenti utilizzando le tag.

1. [Configura le credenziali per un provider di notifica](t__main_push_config_provider.html)
2. [Abilita l'applicazione mobile a ricevere notifiche](c_enable_push.html)
3. [Invia notifiche di base](t_send_push_notifications.html)

# Link correlati
{: #rellinks}

* [Panoramica](c_overview_push.md){: new_window}

## Esercitazioni ed esempi {:id="samples"}
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

## Guida di riferimento API
{: #api}
* [Push API Reference (Android)](https://classicdocs.ng.bluemix.net/docs/api/content/api/mobilefirst/android/push-api-doc/overview-summary.html){: new_window}
* [IMFPush API reference iOS](https://classicdocs.ng.bluemix.net/docs/api/content/api/mobilefirst/ios/IMFPush_api-doc/html/index.html){: new_window}
* [REST API Reference](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window}
