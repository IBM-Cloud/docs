---

copyright:
 years: 2015 2016

---


# Abilitazione delle applicazioni web alla ricezione di {{site.data.keyword.mobilepushshort}}
{: #web_notifications}
Ultimo aggiornamento: 17 ottobre 2016
{: .last-updated}

Puoi ora abilitare le applicazioni web Google Chrome e Mozilla Firefox a ricevere   {{site.data.keyword.mobilepushshort}}.

## Installazione dell'SDK client del browser web per {{site.data.keyword.mobilepushshort}}
{: #web_install}

Questo argomento descrive come installare e utilizzare il JavaScript Push SDK client per sviluppare ulteriormente le tue applicazioni Web.

### Inizializzazione nell'applicazione web Google Chrome 

Per l'installazione dell'applicazione web Javascript SDK in Chrome completa la seguente procedura:

Scarica `BMSPushSDK.js`, `BMSPushServiceWorker.js` e `manifest_Website.json` dalla [SDK di push web di Bluemix](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master).

1. Modifica il file `manifest_Website.json`. 

Per il browser Google Chrome, modifica `name` con il nome del tuo sito. Modifica `gcm_sender_id` con il tuo sender_ID FCM (Firebase Cloud Messaging) o GCM (Google Cloud Messaging). Per ulteriori informazioni, vedi la [Documentazione Google](https://developers.google.com/web/fundamentals/getting-started/codelabs/push-notifications/#make_a_project_on_the_google_developer_console). Il valore gcm_sender_id contiene solo numeri.

```
 {
  "name": "YOUR_WEBSITE_NAME",
      "gcm_sender_id": "GCM_Sender_Id"
 }
```
    {: codeblock}
 
Per il browser Mozilla Firefox, aggiungi i seguenti valori nel file `manifest.json`.     Modifica `name` con il nome del tuo sito. 

```
{
  "name": "YOUR_WEBSITE_NAME"
 }
```
    {: codeblock}

2. Modifica il nome del file `manifest_Website.json` con `manifest.json`.
3. Aggiungi `BMSPushSDK.js`, `BMSPushServiceWorker.js` e `manifest.json` alla tua directory root.
3. Includi `manifest.json` nella tag `<head>` del tuo file html.
```
 <link rel="manifest" href="manifest.json">
```
    {: codeblock}
4. Includi l'SDK di push web di Bluemix nell'applicazione web dal GitHub.
```
 <script src="BMSPushSDK.js" async></script>
```
    {: codeblock}

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
    }
  bmsPush.initialize(params, callback)
```
	{: codeblock}

## Registrazione dell'applicazione web
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

## Invio di {{site.data.keyword.mobilepushshort}} di base
  {: #send}

Dopo che hai sviluppato le tue applicazioni, puoi inviare una notifica push. 

1. Seleziona **Send Notifications** e componi un messaggio scegliendo **Web Notifications** come l'opzione **Send To**. 
2. Immetti il messaggio che deve essere consegnato nel campo **Message**.
3. Puoi scegliere di fornire delle impostazioni facoltative:
  - **Titolo della notifica**: questo è il testo che deve essere visualizzato nell'intestazione dell'avviso del messaggio.
  - **URL dell'icona di notifica**: se il tuo messaggio deve essere consegnato con un'icona di notifica dell'applicazione, fornisci il link alla tua icona nel campo.
  - **Payload addizionale**: specifica i valori di payload personalizzati per le tue notifiche.

La seguente immagine mostra l'opzione delle notifiche web nel dashboard.

  ![Schermata notifiche](images/DashboardWebpush.jpg)
  
## Fasi successive
  {: #next_steps_tags}

Dopo che hai correttamente configurato le notifiche di base, puoi configurare le notifiche
        basate sulle tag e le opzioni avanzate.

Aggiungi queste funzioni del servizio {{site.data.keyword.mobilepushshort}} alla tua applicazione. Per utilizzare le notifiche basate sulle tag, vedi [Notifiche basate sulle tag](c_tag_basednotifications.html). Per utilizzare le opzioni di notifica avanzate, vedi [Notifiche avanzate](t_advance_badge_sound_payload.html). 



