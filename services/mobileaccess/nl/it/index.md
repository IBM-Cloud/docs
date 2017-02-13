---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introduzione a {{site.data.keyword.amashort}}
{: #gettingstarted}

Aggiungi sicurezza alla tua applicazione mobile con il servizio {{site.data.keyword.amafull}}. Puoi configurare l'autorizzazione client per accedere alle risorse di backend protette in esecuzione su {{site.data.keyword.Bluemix}}. Utilizza i provider di identità (Google e Facebook) o le identità personalizzate per autenticare gli utenti e concedere l'accesso alle applicazioni Web e alle risorse di backend protette.
{:shortdesc}

**Nota:** il servizio {{site.data.keyword.amashort}} era precedentemente noto come Advanced Mobile Access.


Per essere operativo in tempi brevi con il servizio {{site.data.keyword.amashort}}:

1. Utilizza una delle seguenti opzioni per creare un servizio di associazione o un servizio di non associazione:
 * Crea un'applicazione {{site.data.keyword.Bluemix_notm}} utilizzando il contenitore tipo **MobileFirst Services Starter** dal catalogo. Viene creato un servizio {{site.data.keyword.amashort}} associato a un'applicazione di back-end {{site.data.keyword.Bluemix_notm}}.
 * Crea un servizio {{site.data.keyword.amashort}} utilizzando la console  {{site.data.keyword.amashort}}.  Puoi eseguire il bind del servizio a un'applicazione di back-end esistente e configurarlo nella console {{site.data.keyword.amashort}}.

   Quando utilizzi MobileFirst Services Starter, ottieni un'istanza di un runtime Node.js che viene eseguito su IBM {{site.data.keyword.Bluemix_notm}} per implementare la tua logica di back-end personalizzata. A tale applicazione Node.js viene associata mediante bind una serie di servizi mobili di base che forniscono funzioni di sicurezza, dati, push e monitoraggio. Dopo che l'applicazione {{site.data.keyword.Bluemix_notm}} Node.js è stata creata, puoi configurare il tuo ambiente di sviluppo e iniziare a utilizzare gli SDK {{site.data.keyword.Bluemix_notm}} Mobile Services. Puoi utilizzare gli SDK per accedere ai servizi associati mediante bind alla tua applicazione cloud con delle semplici chiamate API.

	Per ulteriori informazioni su come creare e lavorare con progetti, applicazioni e servizi, vedi [IBM Bluemix Mobile dashboard](https://console.{DomainName}/docs/mobile/index.html).

2. Risorse lato server sicure.

   Proteggi le tue risorse di backend mobile in esecuzione su runtime Node.js o Liberty for Java&trade; con la sicurezza OAuth abilitata ai dispositivi mobili. Per ulteriori informazioni, vedi [Protezione delle risorse](protecting-resources.html).
   Per ulteriori informazioni sull'applicazione di back-end mobile predefinita, vedi l'applicazione di esempio [bms-hellotodo-strongloop ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop "Icona link esterno"){: new_window}.

3. Configura il tuo ambiente di sviluppo {{site.data.keyword.amashort}} core.

  ####Sviluppo dei client
  {: #client-development}

	Puoi aggiungere l'SDK {{site.data.keyword.amashort}} alla tua applicazione Android, iOS o Cordova esistente, nel seguente modo:
   * Android: ([Configurazione dell'SDK Android](getting-started-android.html)) [Esempio ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication "Icona link esterno"){: new_window}
    * iOS (SDK Swift): ([Configurazione dell'SDK Swift iOS](getting-started-ios-swift-sdk.html)) [Esempio![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "Icona link esterno"){: new_window}    
   * Cordova: ([Configurazione del plugin Cordova](getting-started-cordova.html)) [Esempio ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication "Icona link esterno"){: new_window}


 ####Sviluppo Web
 {: #web-development}

   Il servizio {{site.data.keyword.amashort}} può proteggere la tua applicazione Web, senza richiedere un SDK speciale. Puoi sfruttare diversi provider di identità, in aggiunta alla protezione fornita dal servizio {{site.data.keyword.amashort}}. L'integrazione {{site.data.keyword.amashort}} abilita tutte le applicazioni web, a prescindere dalla tecnologia che le implementa, per usufruire dei vantaggi del protocollo OAuth2. Per informazioni sulla configurazione della tua applicazione web {{site.data.keyword.amashort}} per l'accesso al servizio {{site.data.keyword.amashort}} utilizzando altri provider di identità, consulta:

   * [Abilitazione dell'autenticazione Facebook per le applicazioni Web ](facebook-auth-web.html)
   * [Abilitazione dell'autenticazione Google per le applicazioni Web](google-auth-web.html)
   * [Abilitazione dell'autenticazione personalizzata per le applicazioni Web ](custom-auth-web.html)

**Facoltativo:** configura un provider di identità per la tua applicazione. Puoi configurare un singolo provider di identità per applicazione. La configurazione di un provider di identità abilita gli utenti della tua applicazione mobile ad accedere con il loro             account Facebook o Google+ esistente. In alternativa, puoi definire il modo in cui gli utenti eseguono l'accesso creando
             un'autenticazione personalizzata.
   * [Autenticazione degli utenti con le credenziali Facebook](facebook-auth-overview.html)
   * [Autenticazione degli utenti con le credenziali Google](google-auth-overview.html)
   * [Autenticazione utenti con un provider di identità personalizzato](custom-auth.html)

## Esercitazioni ed esempi
{: #samples}

* [Esempio android-helloauthentication ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication "Icona link esterno"){: new_window}
* [Esempio ios-helloauthentication (SDK Swift) ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "Icona link esterno"){: new_window}

## SDK
{: #sdk}

* [SDK Core (Android) ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core "Icona link esterno"){: new_window}

* [Esempio ios-helloauthentication (SDK Swift) ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "Icona link esterno"){: new_window}

* [Autenticazione personalizzata - esempio semplice ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "Icona link esterno"){: new_window}

* [Autenticazione personalizzata - esempio avanzato ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management "Icona link esterno"){: new_window}


