---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Introduzione a {{site.data.keyword.amashort}}
{: #gettingstarted}
*Ultimo aggiornamento: 15 giugno 2016*
{: .last-updated}

Aggiungi funzionalità di sicurezza alla tua applicazione mobile con il servizio {{site.data.keyword.amafull}}. Puoi configurare l'autenticazione client e i provider di identità in modo che gli utenti possano accedere all'applicazione con i loro account Google o Facebook esistenti.
{:shortdesc}

**Nota:** il servizio {{site.data.keyword.amashort}} era precedentemente noto come Advanced Mobile Access.


Per essere operativo in tempi brevi con il servizio {{site.data.keyword.amashort}}, attieniti alla seguente procedura:

1.  Utilizza il dashboard {{site.data.keyword.Bluemix_notm}} per creare un'applicazione di back-end mobile o per configurarne una esistente.
  - Puoi selezionare MobileFirst Services Starter dal catalogo Bluemix.
  - Oppure puoi eseguire il bind del servizio a un'applicazione esistente e configurarla.

   Quando utilizzi MobileFirst Services Starter, ottieni un'istanza di un runtime Node.js che viene eseguito su IBM {{site.data.keyword.Bluemix_notm}} per implementare la tua logica di back-end personalizzata. A tale applicazione Node.js viene associata mediante bind una serie di servizi mobili di base che forniscono funzioni di sicurezza, dati, push e monitoraggio. Dopo che l'applicazione {{site.data.keyword.Bluemix_notm}} Node.js è stata creata, puoi configurare il tuo ambiente di sviluppo e iniziare a utilizzare
gli SDK {{site.data.keyword.Bluemix_notm}} Mobile Services. Puoi utilizzare gli SDK per accedere ai servizi associati mediante bind alla tua applicazione cloud con delle semplici chiamate API.
   
  
1. Risorse lato server sicure.

   Proteggi le tue risorse di back-end mobile in esecuzione su runtime Node.js o Liberty for Java&trade; con la sicurezza OAuth abilitata ai dispositivi mobili. Per ulteriori informazioni, vedi [Protezione delle risorse](protecting-resources.html).
   Per ulteriori informazioni sull'applicazione di back-end mobile predefinita, vedi  [bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop).

1. Configura il tuo ambiente di sviluppo lato client {{site.data.keyword.amashort}} core.

   Puoi aggiungere l'SDK {{site.data.keyword.amashort}} alla tua applicazione Android, Cordova o iOS esistente. Puoi anche scaricare l'applicazione di esempio HelloAuthentication.
   * **Android**: ([Configurazione dell'SDK Android](getting-started-android.html)) ([Esempio](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication))
  
   * **Cordova**: ([Configurazione del plug-in Cordova](getting-started-cordova.html)) ([Esempio](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication))
  
   * **iOS (Swift SDK)**: ([Configurazione dell'SDK Swift iOS](getting-started-ios-swift-sdk.html))
      ([Esempio](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication))
  
   * **iOS (Objective-C SDK)**: ([Configurazione dell'SDK Object-C iOS](getting-started-ios.html)) ([Esempio](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication))
   
   **Nota:** mentre la SDK Objective-C SDK rimane completamente supportata ed è ancora considerata la SDK primaria per i servizi mobili Bluemix, è pianificato di abbandonarla più avanti questo anno in favore della nuova SDK Swift. Se stai creando un'applicazione, ti consigliamo caldamente di utilizzare l'SDK Swift (consulta [Configurazione dell'SDK Swift iOS](getting-started-ios-swift-sdk.html)).

1. **Facoltativo:** configura un provider di identità per la tua applicazione. Puoi configurare un singolo provider di identità per applicazione. La configurazione di un provider di identità abilita gli utenti della tua applicazione mobile ad accedere con il loro             account Facebook o Google+ esistente. In alternativa, puoi definire il modo in cui gli utenti eseguono l'accesso creando
             un'autenticazione personalizzata.
   * [Autenticazione degli utenti con le credenziali Facebook](facebook-auth-overview.html)
   * [Autenticazione degli utenti con le credenziali Google](google-auth-overview.html)
   * [Autenticazione utenti con un provider di identità personalizzato](custom-auth.html)

1. Configura il monitoraggio e la registrazione in log delle applicazioni.

    Per ulteriori informazioni, vedi [Monitoraggio applicazioni](app-monitoring.html).

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
* [SDK Core (iOS - Objective-C - obsoleto) ](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}
* [Autenticazione personalizzata - esempio semplice](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
* [Autenticazione personalizzata - esempio avanzato](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## Guida di riferimento API
{: api}
* [Android](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html){: new_window}
* [iOS (SDK Objective-C) - obsoleto](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html){: new_window}


## Link correlati
{: #general}
* [Panoramica](overview.html){: new_window}
