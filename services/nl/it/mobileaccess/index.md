---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introduzione a {{site.data.keyword.amashort}}
{: #gettingstarted}
*Ultimo aggiornamento: 21 marzo 2016*

Aggiungi funzionalità di sicurezza e monitoraggio alla tua applicazione mobile con il servizio {{site.data.keyword.amafull}}. Puoi configurare l'autenticazione client e i provider di identità in modo che gli utenti possano accedere all'applicazione con i loro account Google o Facebook esistenti. Puoi anche aggiungere una funzione di monitoraggio alla tua applicazione che abilita
sia le statistiche di utilizzo che quelle di registrazione client.
{:shortdesc}

**Nota:** il servizio {{site.data.keyword.amashort}} era precedentemente noto come Advanced Mobile Access.


Per essere operativo in tempi brevi con il servizio {{site.data.keyword.amashort}}, attieniti alla seguente procedura:

1. Configura il tuo ambiente di sviluppo lato client.
Puoi aggiungere l'SDK {{site.data.keyword.amashort}} alla tua applicazione Android, Cordova o iOS esistente. Puoi anche scaricare l'applicazione di esempio HelloAuthentication.
   * **Android**: ([SDK](getting-started-android.html)) ([Esempio](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication))
   * **Cordova**: ([SDK](getting-started-cordova.html)) ([Esempio](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication))
   * **iOS (Swift-C SDK)**: ([SDK](getting-started-ios-swift-sdk.html)) ([Esempio](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication))
   * **iOS (Objective-C SDK)**: ([SDK](getting-started-ios.html)) ([Esempio](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication))

1. Risorse lato server sicure. Proteggi le tue risorse di backend mobile in esecuzione su runtime Node.js o Liberty for Java&trade; con la sicurezza OAuth abilitata ai dispositivi mobili. Per ulteriori informazioni, vedi [Protezione delle risorse](protecting-resources.html).

1. Facoltativo: configura un provider di identità per la tua applicazione. Puoi configurare un singolo provider di identità per applicazione. La configurazione di un provider di identità abilita gli utenti della tua applicazione mobile ad accedere con il loro             account Facebook o Google+ esistente. In alternativa, puoi definire il modo in cui gli utenti eseguono l'accesso creando
             un'autenticazione personalizzata.
   * [Facebook](facebook-auth-overview.html)
   * [Google](google-auth-overview.html)
   * [Personalizzata](custom-auth.html)

1. Configura il monitoraggio e la registrazione in log delle applicazioni.  Per ulteriori informazioni, vedi [Monitoraggio applicazioni](app-monitoring.html).

# Link correlati
{: #rellinks}

## Esercitazioni ed esempi
{: #samples}
* [Esempio android-helloauthentication](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication){: new_window}
* [Esempio ios-helloauthentication (SDK Swift)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication){: new_window}
* [Esempio ios-helloauthentication (SDK Objective-C)](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication){: new_window}

## SDK
{: #sdk}
* [SDK Core (Android)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [SDK Core (plugin Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
* [SDK Core (iOS - Swift) ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [SDK Core (iOS - Objective-C) ](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}
* [Autenticazione personalizzata - esempio semplice](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
* [Autenticazione personalizzata - esempio avanzato](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## Guida di riferimento API
{: api}
* [Android](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html){: new_window}
* [iOS (SDK Objective-C)](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html){: new_window}


## Link correlati
{: #general}
* [Panoramica](overview.html){: new_window}
