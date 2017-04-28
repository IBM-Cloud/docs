---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Abilitazione delle notifiche basate sull'utente
{: #user_based_notifications}
Ultimo aggiornamento: 28 febbraio 2017
{: .last-updated}

Le {{site.data.keyword.mobilepushshort}} basate su ID utente sono destinate agli utenti dell'applicazione mobile con messaggi personalizzati. Con le notifiche basate sull'utente, puoi scegliere di inviare la notifica a delle persone specifiche in base alle rispettive preferenze.

## Registrazione del dispositivo con l'ID utente
{: #register_device_wh_userid}

Per abilitare le notifiche di push indirizzate dall'ID utente, assicurati di aver registrato il dispositivo con un campo ID utente impostato.     

L'ID utente può essere una qualsiasi stringa fornita dall'applicazione all'API di registrazione del dispositivo. Normalmente, un'applicazione mobile prima eseguirà un ciclo di autenticazione in cui l'utente dell'applicazione mobile viene autenticato in un servizio di autenticazione come [{{site.data.keyword.amafull}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html){: new_window}. Dopo la corretta autenticazione, l'ID dell'utente autenticato viene trasmesso all'API Push Device Registration. 

Per registrare la notifica basate sull'ID utente, completa la seguente procedura:

### Android
{: #android-register}

Inizializza la classe MFPPush con le chiavi `AppGUID` e `clientSecret` del servizio {{site.data.keyword.mobilepushshort}}.
```
// Initialize the Push Notifications service
push = MFPPush.getInstance();
push.initialize(getApplicationContext(),"AppGUID", "clientSecret");
```
	{: codeblock}


- **AppGUID**: questa è la chiave AppGUID del servizio {{site.data.keyword.mobilepushshort}}.
- **clientSecret**: questa è la chiave clientSecret del servizio {{site.data.keyword.mobilepushshort}}.

  Utilizza l'API **registerDeviceWithUserId** per registrare il dispositivo per {{site.data.keyword.mobilepushshort}}.

```
// Register the device to Push Notifications
push.registerDeviceWithUserId("userId",new MFPPushResponseListener<String>() {
		@Override
		public void onSuccess(String response) {
		Log.d("Device is registered with Push Service.");}
		@Override
    public void onFailure(MFPPushException ex) {
		  Log.d("Error registering with Push Service...\n"
        + "Push notifications will not be received.");
		}
		});
```
	{: codeblock}

- **userId**: passa il valore ID utente univoco per la registrazione per {{site.data.keyword.mobilepushshort}}.

**Nota:** per abilitare le {{site.data.keyword.mobilepushshort}} indirizzate dall'ID utente, assicurati di aver registrato il dispositivo con un ID utente e inoltre di passare il 'clientSecret' assegnato quando viene eseguito il provisioning dei servizi {{site.data.keyword.mobilepushshort}}. La registrazione del dispositivo avrà esito negativo senza un clientSecret valido.

### Cordova
{: #cordova_register}

Utilizza le seguenti API per registrare le {{site.data.keyword.mobilepushshort}} basate sull'ID utente.

```
// Register device for Push Notification with UserId
var options = {"userId": "Your User Id value"};
BMSPush.registerDevice(options,success, failure); 
```
	{: codeblock}


- **userId**: passa il valore ID utente univoco per la registrazione per {{site.data.keyword.mobilepushshort}}.


### Swift
{: #swift-register}

```
// Inizializza BMSPushClient
let push =  BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


- **AppGUID**: questa è la chiave AppGUID del servizio {{site.data.keyword.mobilepushshort}}.
- **clientSecret**: questa è la chiave clientSecret del servizio {{site.data.keyword.mobilepushshort}}.

Utilizza l'API **registerWithUserId** per registrare il dispositivo per {{site.data.keyword.mobilepushshort}}.

```
// Register the device to Push Notifications service
push.registerWithDeviceToken("deviceToken", WithUserId: "userId")  { (response, statusCode, error) -> Void in
if error.isEmpty {
  print( "Response during device registration : \(response)")
        print( "status code during device registration : \(statusCode)")
    } else {
  print( "Error during device registration \(error) ")
    }
  }
```
	{: codeblock}

- **userId**: passa il valore ID utente univoco per la registrazione per {{site.data.keyword.mobilepushshort}}.

### Google Chrome, Safari e Mozilla Firefox
{: #web-register}

Utilizza le seguenti API per registrare le notifiche basate sull'ID utente. Inizializza l'SDK con `app GUID`, `app Region` e `Client Secret`.

```
var bmsPush = new BMSPush();
var params = {
    "appGUID":"push app GUID",
    "appRegion":"App Region",
    "clientSecret":"Push Client Secret" 
    }
  bmsPush.initialize(params, function(response){
          alert(response.response)
    })
```
	{: codeblock}
  
Dopo aver correttamente eseguito l'inizializzazione registra l'applicazione web con l'ID utente.

```
bmsPush.registerWithUserId("UserId", function(response) {
 alert(response.response)
  })
```
	{: codeblock}

### Estensioni e applicazioni Google Chrome
{: #web-register-new}

Utilizza le seguenti API per registrare le notifiche basate sull'ID utente. Inizializza l'SDK con `app GUID`, `app Region` e `Client Secret`.

```
var bmsPush = new BMSPush();
var params = {
    "appGUID":"push app GUID",
    "appRegion":"App Region",
    "clientSecret":"Push Client Secret" 
    }
  bmsPush.initialize(params, function(response){
          alert(response.response)
    })
```
	{: codeblock}
  
Dopo l'inizializzazione, devi registrare l'applicazione web con l'ID utente.

```
bmsPush.registerWithUserId("UserId", function(response) {
 alert(response.response)
  })
```
	{: codeblock}

## Utilizzo delle notifiche basate sull'ID utente
{: #using_userid}

Le notifiche basate sull'ID utente sono messaggi di notifica destinati a uno specifico utente. Possono essere registrati con un utente molti dispositivi. I seguenti passi descrivono come inviare le notifiche basate sull'ID utente.

1. Dal dashboard **Push Notification**, seleziona l'opzione **Send Notifications**.
1. Seleziona **UserId** nell'elenco delle opzioni **Send to**.
1. Nel campo **User Id**, cerca gli ID utente che vuoi utilizzare e fai quindi clic su **+Add**.![Schermata notifiche](images/user_notification.jpg)
1. Nel campo **Message**, immetti il testo che vuoi inviare nella tua notifica.
1. Fai clic su **Send**.


## Sincronizzazione di accesso/disconnessione dell'utente 
{: #sync_login_logout}

Puoi scegliere di inviare le notifiche solo se l'utente ha effettuato l'accesso. 

Ad esempio, prendi in considerazione un dispositivo condiviso dai membri di una famiglia o un team di lavoro e che ci sia bisogno di indirizzare utenti specifici. In questo caso di utilizzo, dovrebbe esserci una sequenza di accesso e disconnessione utente. Questo meccanismo di autenticazione consente alll'applicazione di tracciare l'identità dell'utente presente dell'applicazione. Questo assicura che le notifiche destinate a un'utente specifico siano sempre ricevute solo da tale utente. Dopo un accesso corretto, richiama l'API di registrazione del dispositivo trasmettendo l'ID utente dell'utente che ha eseguito l'accesso. Allo stesso modo, prima della disconnessione, richiama l'API di annullamento della registrazione del dispositivo. La sequenza di queste API push con accesso e disconnessione ti assicurerà che le notifiche pensate per un utente specifico siano inviate solo a tale utente.
