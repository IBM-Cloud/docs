---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Abilitazione delle applicazioni web alla ricezione di {{site.data.keyword.mobilepushshort}}
{: #web_notifications}
Ultimo aggiornamento: 16 febbraio 2017
{: .last-updated}

Puoi abilitare le applicazioni web Google Chrome, Mozilla Firefox e Safari a ricevere {{site.data.keyword.mobilepushshort}}. Assicurati di aver consultato [Configurazione delle credenziali per un provider di notifica](t__main_push_config_provider.html) prima di continuare con la procedura.

## Installazione dell'SDK client del browser web per {{site.data.keyword.mobilepushshort}}
{: #web_install}

Questo argomento descrive come installare e utilizzare il JavaScript Push SDK client per sviluppare ulteriormente le tue applicazioni Web.

### Inizializzazione nell'applicazione web

Per l'installazione dell'SDK Javascript nell'applicazione web Google Chrome completa la seguente procedura:

Scarica i file `BMSPushSDK.js`, `BMSPushServiceWorker.js` e `manifest_Website.json` dalla [SDK di push web di Bluemix](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master){: new_window}.

1. Modifica il file `manifest_Website.json`.
	- Per il browser Google Chrome, modifica `name` con il nome del tuo sito. Ad esempio, `www.dailynewsupdates.com`. Modifica `gcm_sender_id` con il tuo sender_ID FCM (Firebase Cloud Messaging) o GCM (Google Cloud Messaging). Per ulteriori informazioni, consulta [Come ottenere il tuo ID mittente e la chiave API](t_push_provider_android.html). Il valore gcm_sender_id contiene solo numeri.

		```
			{
	"name": "YOUR_WEBSITE_NAME",
  			"gcm_sender_id": "GCM_Sender_Id"
			 }
		```
    		{: codeblock}
 
	- Per il browser Mozilla Firefox, aggiungi i seguenti valori nel file `manifest_Website.json`. Fornisci un `name` appropriato. Questo sarà il nome del tuo sito web.

		```
			{ 
	"name": "YOUR_WEBSITE_NAME"
			 }
		```
    		{: codeblock}

2. Modifica il nome del file `manifest_Website.json` con `manifest.json`.
3. Aggiungi `BMSPushSDK.js`, `BMSPushServiceWorker.js` e `manifest.json` alla directory root del tuo sito web.
3. Includi `manifest.json` nella tag `<head>` del tuo file html.
	```
		<link rel="manifest" href="manifest.json">
	```
    	{: codeblock}
4. Includi l'SDK di push web Bluemix nella tua applicazione web.
	```
		<script src="BMSPushSDK.js" async></script>
	```
    	{: codeblock}

**Nota**: assicurati che il codice venga distribuito e che si acceda al link di esempio utilizzando `https` e non `http`. 

## Inizializzazione della SDK di push web di Bluemix 
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
   "websitePushIDSafari": "Optional parameter for Safari Push Notifications only. The value should match the website Push ID provided during the server side configuration."
  }
  	bmsPush.initialize(initParams, callback)
```
	{: codeblock}

**Nota**: se le tue credenziali FCM sono state modificate per l'SDK push Web, la ricezione dei messaggi potrebbe non riuscire per il browser Chrome. Assicurati di richiamare `bmsPush.unRegisterDevice` per evitare errori.

Se fornisci un parametro errato potresti visualizzare degli errori di configurazione. Per ulteriori informazioni, vedi [Risoluzione degli errori di configurazione push web](troubleshooting_config_errors.html).

## Registrazione dell'applicazione web
{: #web_register}

Utilizza l'API **register()** per registrare il dispositivo con il servizio {{site.data.keyword.mobilepushshort}}. Utilizza una delle seguenti opzioni, in base al tuo browser.

- Per la registrazione da Google Chrome, aggiungi l'URL del sito web e la chiave API di FCM (Firebase Cloud Messaging) o GCM (Google Cloud Messaging) nel dashboard di configurazione web del servizio {{site.data.keyword.mobilepushshort}} di Bluemix. Per ulteriori informazioni, consulta [Configurazione delle credenziali per GCM (Google Cloud Messaging)](t_push_provider_android.html) nelle impostazioni di Chrome.

- Per la registrazione da Mozilla Firefox, aggiungi l'URL del sito web nel dashboard di configurazione web del servizio {{site.data.keyword.mobilepushshort}} di Bluemix nelle impostazioni di Firefox.

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
  "websitePushIDSafari": "Optional parameter for Safari Push Notifications only. The value should match the website Push ID provided during the server side configuration."
  }
  bmsPush.initialize(params, callback)
    bmsPush.register(function(response) {
    alert(response.response)
  })
```
    {: codeblock}






