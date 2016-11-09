---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"
---


# Introduzione a {{site.data.keyword.amashort}}
{: #gettingstarted}


Aggiungi sicurezza alla tua applicazione mobile con il servizio {{site.data.keyword.amafull}}. Puoi configurare l'autorizzazione client per accedere alle risorse di backend protette in esecuzione su {{site.data.keyword.Bluemix_notm}}. Utilizza i provider di identità (Google e Facebook) o le identità personalizzate per autenticare gli utenti e concedere l'accesso alle applicazioni web e alle risorse di backend protette.
{:shortdesc}

**Nota:** il servizio {{site.data.keyword.amashort}} era precedentemente noto come Advanced Mobile Access.


Per essere operativo in tempi brevi con il servizio {{site.data.keyword.amashort}}:

1. Utilizza il dashboard {{site.data.keyword.Bluemix_notm}} per creare un'applicazione di back-end mobile o per configurarne una esistente.
  - Puoi selezionare il contenitore tipo **MobileFirst Services Starter** dal catalogo {{site.data.keyword.Bluemix_notm}}.
  - Inoltre puoi eseguire il bind del servizio a un'applicazione esistente e configurarla.

   Quando utilizzi MobileFirst Services Starter, ottieni un'istanza di un runtime Node.js che viene eseguito su IBM {{site.data.keyword.Bluemix_notm}} per implementare la tua logica di back-end personalizzata. A tale applicazione Node.js viene associata mediante bind una serie di servizi mobili di base che forniscono funzioni di sicurezza, dati, push e monitoraggio. Dopo che l'applicazione {{site.data.keyword.Bluemix_notm}} Node.js è stata creata, puoi configurare il tuo ambiente di sviluppo e iniziare a utilizzare
gli SDK {{site.data.keyword.Bluemix_notm}} Mobile Services. Puoi utilizzare gli SDK per accedere ai servizi associati mediante bind alla tua applicazione cloud con delle semplici chiamate API.
  
2. Risorse lato server sicure.

   Proteggi le tue risorse di backend mobile in esecuzione su runtime Node.js o Liberty for Java&trade; con la sicurezza OAuth abilitata ai dispositivi mobili. Per ulteriori informazioni, vedi [Protezione delle risorse](protecting-resources.html).
   Per ulteriori informazioni sull'applicazione di back-end mobile predefinita, vedi l'applicazione di esempio [bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop).

3. Configura il tuo ambiente di sviluppo {{site.data.keyword.amashort}} core.
   
	####Sviluppo dei client
   {: #client-development}
   
	Puoi aggiungere l'SDK {{site.data.keyword.amashort}} alla tua applicazione Android, iOS o Cordova esistente, nel seguente modo: 
   * Android: ([Configurazione dell'SDK Android](getting-started-android.html)) ([Esempio](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication))
  
   * iOS (Swift SDK): ([Configurazione dell'SDK Swift iOS](getting-started-ios-swift-sdk.html))
      ([Esempio](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication))
  
   * iOS (Objective-C SDK): ([Configurazione dell'SDK Object-C iOS](getting-started-ios.html)) ([Esempio](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication))

   * Cordova: ([Configurazione del plug-in Cordova](getting-started-cordova.html)) ([Esempio](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication))
   
   **Nota:** mentre la SDK Objective-C SDK rimane completamente supportata ed è ancora considerata la SDK primaria per i servizi mobili {{site.data.keyword.amashort}}, è pianificato di abbandonarla più avanti questo anno in favore della nuova SDK Swift. Se stai creando un'applicazione, ti consigliamo caldamente di utilizzare l'SDK Swift (consulta [Configurazione dell'SDK Swift iOS](getting-started-ios-swift-sdk.html)).

	####Sviluppo Web
   {: #web-development}

   Il servizio {{site.data.keyword.amashort}} può proteggere la tua applicazione web, senza richiedere un SDK speciale. Puoi sfruttare diversi provider di identità, in aggiunta alla protezione fornita dal servizio {{site.data.keyword.amashort}}. L'integrazione {{site.data.keyword.amashort}} abilita tutte le applicazioni web, a prescindere dalla tecnologia che le implementa, per usufruire dei vantaggi del protocollo OAuth2. Per informazioni sulla configurazione della tua applicazione web per l'accesso al servizio {{site.data.keyword.amashort}} utilizzando altri provider di identità, consulta:

    * [Abilitazione dell'autenticazione Facebook per le applicazioni web ](facebook-auth-web.html)
              
    * [Abilitazione dell'autenticazione Google per le applicazioni web ](google-auth-web.html)
              
    * [Abilitazione dell'autenticazione personalizzata per le applicazioni web ](custom-auth-web.html)
              
4. **Facoltativo:** configura un provider di identità per la tua applicazione. Puoi configurare un singolo provider di identità per applicazione. La configurazione di un provider di identità abilita gli utenti della tua applicazione mobile ad accedere con il loro             account Facebook o Google+ esistente. In alternativa, puoi definire il modo in cui gli utenti eseguono l'accesso creando
             un'autenticazione personalizzata.
   * [Autenticazione degli utenti con le credenziali Facebook](facebook-auth-overview.html)
   * [Autenticazione degli utenti con le credenziali Google](google-auth-overview.html)
   * [Autenticazione utenti con un provider di identità personalizzato](custom-auth.html)

5. Configura il monitoraggio e la registrazione in log della tua applicazione.

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
