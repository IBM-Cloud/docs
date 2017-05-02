---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Abilitazione delle estensioni e delle applicazioni Chrome alla ricezione di notifiche di push
{: #web_notifications}
Ultimo aggiornamento: 12 aprile 2017
{: .last-updated}

Puoi abilitare le estensioni e le applicazioni Google Chrome a ricevere  {{site.data.keyword.mobilepushshort}}. Assicurati di aver consultato [Configurazione delle credenziali per un provider di notifica](t__main_push_config_provider.html) prima di continuare con la procedura.

## Installazione dell'SDK client per Push Notifications
{: #web_install}

Questo argomento descrive come installare e utilizzare il JavaScript Push SDK client per sviluppare ulteriormente le tue estensioni e applicazioni Chrome.

### Inizializzazione delle estensioni e delle applicazioni Google Chrome
{: #initialize_google_extn_app}

Per l'installazione dell'SDK Javascript SDK nelle estensioni e applicazioni Chrome completa la seguente procedura:

Scarica `BMSPushSDK.js` e `manifest_Chrome_Ext.json` (per le estensioni Chrome) o `manifest_Chrome_App.json` (per le applicazioni Chrome) dall'[SDK di push web Bluemix ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master){: new_window}.



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



### Inizializzazione della SDK di push 
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

### Registrazione delle estensioni e delle applicazioni Chrome
{: #web_register}

Utilizza l'API `register()` per registrare il dispositivo con il servizio {{site.data.keyword.mobilepushshort}}. Per la registrazione da Google Chrome, aggiungi l'URL del sito web e la chiave API di FCM (Firebase Cloud Messaging) nel dashboard di configurazione web del servizio Bluemix {{site.data.keyword.mobilepushshort}}. Per ulteriori informazioni, vedi [Configurazione delle credenziali per un provider di notifica](t__main_push_config_provider.html). 

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


## Inviare le notifiche di base alle estensioni e alle applicazioni Chrome 
{: #web_extensions_notifications}

Dopo che hai sviluppato le tue applicazioni, puoi inviare una notifica push. 

1. Seleziona **Send Notifications** e componi un messaggio scegliendo **Web Notifications** come l'opzione **Send To**. 
2. Immetti il messaggio che deve essere consegnato nel campo **Message**.
3. Puoi scegliere di fornire delle impostazioni facoltative:
  - **Titolo della notifica**: questo è il testo che deve essere visualizzato nell'intestazione dell'avviso del messaggio.
  - **URL dell'icona di notifica**: se il tuo messaggio deve essere consegnato con un'icona di notifica dell'applicazione, fornisci il link alla tua icona nel campo.
  - **Chiave di compressione**:  le chiavi di compressione solo allegate alle notifiche. Se più notifiche arrivano in sequenza con la stessa chiave di compressione quando il dispositivo è offline, esse vengono compresse. Quando un dispositivo va online, riceve le notifiche dal server FCM/GCM e visualizza solo l'ultima notifica rilevando la stessa chiave di compressione. Se la chiave di compressione non viene inviata, sia il nuovo che il vecchio messaggio vengono archiviati per una consegna successiva.
  - **TTL (Time to live)**: questo valore è impostato in secondi. Se questo parametro non viene specificato, il server FCM/GCM archivia il messaggio per quattro settimane e tenterà di consegnarlo. La validità scade dopo quattro settimane. L'intervallo di valori possibile è compreso tra 0 e 2,419,200 secondi.
  - **Ritarda quando inattivo**: impostando questo valore su `true` si danno istruzioni al server FCM/GCM di non consegnare la notifica se il dispositivo è inattivo. Imposta questo valore su `false`, per assicurati di consegnare la notifica anche se il dispositivo è inattivo.
  - **Payload addizionale**: specifica i valori di payload personalizzati per le tue notifiche.

La seguente immagine mostra l'opzione delle notifiche alle estensioni e applicazioni Chrome nel dashboard.

  ![Schermata notifiche](images/push_chrome_extns.jpg)
  
### Fasi successive
{: #next_steps_tags}

Dopo che hai correttamente configurato le notifiche di base, puoi scegliere di configurare le notifiche basate sulle tag e le opzioni avanzate.

Aggiungi queste funzioni del servizio {{site.data.keyword.mobilepushshort}} alla tua applicazione. Per utilizzare le notifiche basate sulle tag, vedi [Notifiche basate sulle tag](c_tag_basednotifications.html). Per utilizzare le opzioni di notifica avanzate, vedi [Notifiche avanzate](t_advance_badge_sound_payload.html).



