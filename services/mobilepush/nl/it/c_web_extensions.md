---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Abilitazione delle estensioni e delle applicazioni Chrome a ricevere {{site.data.keyword.mobilepushshort}}
{: #web_notifications}
Ultimo aggiornamento: 18 gennaio 2017
{: .last-updated}

Puoi abilitare le estensioni e le applicazioni Google Chrome a ricevere  {{site.data.keyword.mobilepushshort}}. Assicurati di aver consultato [Configurazione delle credenziali per un provider di notifica](t__main_push_config_provider.html) prima di continuare con la procedura.

## Installazione dell'SDK client per {{site.data.keyword.mobilepushshort}}
{: #web_install}

Questo argomento descrive come installare e utilizzare il JavaScript Push SDK client per sviluppare ulteriormente le tue estensioni e applicazioni Chrome.

### Inizializzazione delle estensioni e delle applicazioni Google Chrome

Per l'installazione dell'SDK Javascript SDK nelle estensioni e applicazioni Chrome completa la seguente procedura:

Scarica `BMSPushSDK.js` e `manifest_Chrome_Ext.json` (per le estensioni Chrome) o `manifest_Chrome_App.json` (per le applicazioni Chrome) dalla [SDK di push web di Bluemix ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master "Icona link esterno"){: new_window}.



- Per le applicazioni Chrome, configura il file manifest:
 1. Nel file `manifest_Chrome_App.json`, fornisci il nome, la descrizione e le icone.
 2. Aggiungi `BMSPushSDK.js` in `app.background.scripts`.
 3. Modifica `manifest_Chrome_App.json` in `manifest.json`.

- Per le estensioni Chrome, configura il file manifest:
 1. Nel file `manifest_Chrome_Ext.json` fornisci nome, descrizione e icone.
 2. Aggiungi `BMSPushSDK.js` in `background.scripts`.
 3. Modifica `manifest_Chrome_Ext.json` in `manifest.json`.

Nel file `background.js` aggiungi quanto segue per ricevere le notifiche push 
```
chrome.gcm.onMessage.addListener(BMSPushBackground.onMessageReceived)
chrome.notifications.onClicked.addListener(BMSPushBackground.notification_onClicked);
chrome.notifications.onButtonClicked.addListener(BMSPushBackground.notifiation_buttonClicked); 
```
	{: codeblock}



## Inizializzazione della SDK di push 
{: #web_initialize}

Inizializza la SDK di push con `app GUID` e `app Region` del servizio {{site.data.keyword.mobilepushshort}} di Bluemix.  

Per ottenere il tuo GUID dell'applicazione, seleziona l'opzione **Configurazione** nel pannello di navigazione per i servizi di push inizializzati e fai clic su **Opzioni mobili**. Modifica il frammento di codice per utilizzare il tuo parametro appGUID del servizio di notifiche di push di Bluemix.

`App Region` specifica l'ubicazione in cui è ospitato il servizio {{site.data.keyword.mobilepushshort}}. Puoi utilizzare uno dei seguenti tre valori:

 - Per Dallas Stati Uniti:	 `.ng.bluemix.net`
 - Per il Regno unito:			 `.eu-gb.bluemix.net`
 - Per Sydney:		 `.au-syd.bluemix.net`

```
 var bmsPush = new BMSPush();
    function callback(response) {
 alert(response.response)
    }
  var initParams = {
  "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
   "clientSecret":"clientSecret of your push service"
    }
  bmsPush.initialize(params, callback)
```
	{: codeblock}

## Registrazione delle estensioni e delle applicazioni Chrome
{: #web_register}

Utilizza l'API `register()` per registrare il dispositivo con il servizio {{site.data.keyword.mobilepushshort}}. Per la registrazione da Google Chrome, aggiungi l'URL del sito web e la chiave API di FCM (Firebase Cloud Messaging) o GCM (Google Cloud Messaging) nel dashboard di configurazione web del servizio {{site.data.keyword.mobilepushshort}} di Bluemix. Per ulteriori informazioni, consulta [Configurazione delle credenziali per GCM (Google Cloud Messaging)](t_push_provider_android.html) nelle impostazioni di Chrome.

Per la registrazione da Mozilla Firefox, aggiungi l'URL del sito web nel dashboard di configurazione web del servizio {{site.data.keyword.mobilepushshort}} di Bluemix nelle impostazioni di Firefox.

Utilizza il seguente frammento di codice per registrare il servizio {{site.data.keyword.mobilepushshort}} di Bluemix.
```
var bmsPush = new BMSPush();
    function callback(response) {
     alert(response.response)
    }
  var initParams = {
  "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
  "clientSecret":"clientSecret of your push service"
  }
  bmsPush.initialize(params, callback)
    bmsPush.register(function(response) {
    alert(response.response)
  })
```
    {: codeblock}




