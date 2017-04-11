---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# Node.js per gli sviluppatori dell'applicazione
{: #nodejs}

Ultimo aggiornamento: 29 luglio 2016
{: .last-updated}

Puoi modificare gli esempi e le librerie client in Node.js per creare e personalizzare le applicazioni che interagiscono con la tua organizzazione su {{site.data.keyword.iot_full}}.
{:shortdesc}

Utilizza le informazioni e gli esempi forniti per iniziare a sviluppare le tue applicazioni utilizzando Node.js.

## Scaricamento delle risorse e del client Node.js
{: #nodejs_client_download}

Per accedere alle librerie client Node.js per {{site.data.keyword.iot_short_notm}} e ad altre risorse disponibili, vai al repository [iot-nodejs ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-watson-iot/iot-nodejs){: new_window} in GitHub e completa le istruzioni di installazione.


Per ulteriori informazioni, consulta le seguenti risorse:
- [Esempi applicazione ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-watson-iot/iot-nodejs/tree/master/samples){: new_window} in GitHub.
- [ibmiotf ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://www.npmjs.com/package/ibmiotf){: new_window} in NPM.
- La sessione [Riferimenti](#reference_nodejs) di questo documento.


## Constructor
{: #constructor}

Il constructor crea l'istanza client dell'applicazione e accetta un file di configurazione JSON che contiene le seguenti proprietà:

| Proprietà     |Descrizione     |
|----------------|----------------|
|`org` |Il tuo ID dell'organizzazione. Questo è un valore obbligatorio.|
|`id`  |L'ID univoco della tua applicazione nella tua organizzazione.|
|`auth-key`   |Una chiave API per la connessione sicura alla tua applicazione su Watson IoT Platform.|
|`auth-token`   |Un token chiave API per la connessione sicura al tuo dispositivo su Watson IoT Platform.|
|`type`  |Il tipo di sottoscrizione. Specifica `shared` per abilitare la sottoscrizione condivisa.|


Per utilizzare Quickstart, sono obbligatorie solo le prime due proprietà.

```
  var Client = require("ibmiotf");
	var appClientConfig = {
		"org" : orgId,
		"id" : appId,
		"auth-key" : apiKey,
		"auth-token" : apiToken
	}

	var appClient = new Client.IotfApplication(appClientConfig);
```


### Utilizzo di un file di configurazione


Invece di trasmettere direttamente le proprietà JSON, puoi anche utilizzare un file di configurazione descritto nel seguente esempio di codice:

```

  var Client = require("ibmiotf");
	var appClientConfig = require("./application.json");
	var appClient = new Client.IotfApplication(appClientConfig);
```

Assicurati che il file di configurazione JSON sia nel seguente formato:

```
    {
	  "org": 'xxxxx',
	  "id": 'myapp',
	  "auth-key": 'a-xxxxxxx-zenkqyfiea',
	  "auth-token": 'xxxxxxxxxx'
    }
```


## Connessione a {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

Per collegarti a {{site.data.keyword.iot_short_notm}}, invia una richiesta *connect*, come segue:

```
  var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

	//Aggiungi qui il tuo codice
	});
```

Dopo una connessione corretta al servizio {{site.data.keyword.iot_short_notm}}, il client dell'applicazione invia un evento `connect`, in modo che ogni logica possa essere implementata in questa funzione di callback.



Il client dell'applicazione tenta automaticamente di ricollegarsi quando perde la connessione. Quando si ricollega correttamente, il client invia un evento `reconnect`.



## Accesso
{: #logging}

Per impostazione predefinita, vengono registrati solo gli eventi di log del tipo `warn`. Se desideri aumentare o diminuire il livello di registrazione, utilizza la funzione `log.setLevel`. Sono supportati i seguenti livelli di registrazione:
- trace
- debug
- info
- warn
- error

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//impostazione del livello di registrazione su 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Aggiungi qui il tuo codice
	});
```

## Sottoscrizioni condivise
{: #shared_subscriptions}

Utilizza la funzione delle sottoscrizioni condivise per creare applicazioni scalabili che bilanciano il carico dei messaggi tra più istanze dell'applicazione. Per abilitare il bilanciamento del carico, imposta il campo `type` su `shared`, come mostrato nel seguente esempio:

```

	var appClientConfig = {
	  org: 'xxxxx',
	  id: 'myapp',
	  "auth-key": 'a-xxxxxx-xxxxxxxxx',
	  "auth-token": 'xxxxx!xxxxxxxx',
	  "type" : "shared" // rendi questa connessione una sottoscrizione condivisa
	};
	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//impostazione del livello di registrazione su 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Aggiungi qui il tuo codice
	});
```

## Gestione degli errori
{: #handling_errors}

Quando il client dell'applicazione riscontra un errore, viene generato un evento `error`.

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//impostazione del livello di registrazione su 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Aggiungi qui il tuo codice
	});
	appClient.on("error", function (err) {
		console.log("Error : "+err);
	});
```

## Sottoscrizione agli eventi del dispositivo
{: #subscribing_device_events}

Gli eventi sono meccanismi con cui i dispositivi pubblicano i dati nell'istanza {{site.data.keyword.iot_short_notm}}. Il dispositivo controlla il contenuto dell'evento e assegna un nome ad ogni evento che invia.

Quando viene ricevuto un evento dall'istanza {{site.data.keyword.iot_short_notm}}, le credenziali dell'evento ricevuto identificano il dispositivo di invio, il che significa che un dispositivo non può impersonare un altro dispositivo.


Per impostazione predefinita, le applicazioni si sottoscrivono a tutti gli eventi da tutti i dispositivi collegati. Utilizza i parametri tipo di dispositivo, ID dispositivo e formato del messaggio per controllare l'ambito della sottoscrizione. I seguenti esempi di codice mostrano come puoi utilizzare questi parametri per definire l'ambito di una sottoscrizione:

### Sottoscrizione a tutti gli eventi provenienti da tutti i dispositivi


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents();
	});
```

### Sottoscrizione a tutti gli eventi provenienti da tutti i dispositivi di un tipo specifico

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("mydeviceType");
	});
```

### Sottoscrizione di un evento specifico da tutti i dispositivi


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("+","+","myevent");
	});
```

### Sottoscrizione di un evento specifico da due o più dispositivi differenti

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","myevent");
		appClient.subscribeToDeviceEvents("myOtherDeviceType","device02","myevent");
	});
```

### Sottoscrizione a tutti gli eventi che vengono pubblicati in formato JSON


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","+","json");

	});
```

**Nota**: un singolo client può supportare più sottoscrizioni.

### Gestione degli eventi dai dispositivi


Per elaborare gli eventi ricevuti dalle tue sottoscrizioni, implementa un metodo di callback dell'evento. Il client dell'applicazione {{site.data.keyword.iot_short_notm}} invia l'evento `deviceEvent`. Questa funzione ha le seguenti proprietà:

- deviceType
- deviceId
- eventType
- format
- payload
- topic

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","+","json");

	});
	appClient.on("deviceEvent", function (deviceType, deviceId, eventType, format, payload) {

		console.log("Device Event from :: "+deviceType+" : "+deviceId+" of event "+eventType+" with payload : "+payload);

	});
```


## Sottoscrizione agli stati del dispositivo
{: #subscribing_device_status}

Per impostazione predefinita, quando ti sottoscrivi a uno stato del dispositivo, gli aggiornamenti dello stato sono ricevuti da tutti i dispositivi collegati. Utilizza i parametri tipo e ID per controllare l'ambito della sottoscrizione. Un singolo client può supportare più sottoscrizioni.

### Sottoscrizione agli aggiornamenti dello stato per tutti i dispositivi

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus();

	});
```

### Sottoscrizione agli aggiornamenti dello stato per tutti i dispositivi di un tipo specifico


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType");

	});
```

### Sottoscrizione agli aggiornamenti dello stato per due dispositivi differenti

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType","device01");
		appClient.subscribeToDeviceStatus("myOtherDeviceType","device02");

	});
```

### Gestione degli stati dai dispositivi

Per elaborare gli aggiornamenti dello stato ricevuti dalle tue sottoscrizioni, implementa un metodo di callback dello stato. Il client dell'applicazione {{site.data.keyword.iot_short_notm}} invia l'evento `deviceStatus`. Questa funzione ha le seguenti proprietà:

-   deviceType
-   deviceId
-   payload
-   topic

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType","device01");
		appClient.subscribeToDeviceStatus("myOtherDeviceType","device02");

	});
	appClient.on("deviceStatus", function (deviceType, deviceId, payload, topic) {

		console.log("Device status from :: "+deviceType+" : "+deviceId+" with payload : "+payload);

	});
```


## Pubblicazione degli eventi dai dispositivi
{: #publishing_device_events}


Le applicazioni possono pubblicare gli eventi come se fossero originati da un dispositivo. La funzione richiede le seguenti proprietà:

-   deviceType
-   deviceId
-   eventType
-   format
-   data


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50};
		myData = JSON.stringify(myData);
		appClient.publishDeviceEvent("myDeviceType","device01", "myEvent", "json", myData);

	});
```


## Pubblicazione dei comandi ai dispositivi
{: #publishing_commands_devices}

Le applicazioni possono pubblicare i comandi sui dispositivi connessi. La funzione richiede le seguenti proprietà:

-   deviceType
-   deviceId
-   eventType
-   format
-   data

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'DelaySeconds' : 10};
		myData = JSON.stringify(myData);
		appClient.publishDeviceCommand("myDeviceType","device01", "reboot", "json", myData);

	});
```


## Disconnessione del client
{: #disconnect_client}

Il seguente esempio scollega il client e rilascia le connessioni:

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'DelaySeconds' : 10}
		appClient.publishDeviceCommand("myDeviceType","device01", "reboot", "json", myData);

		appClient.disconnect();
	});
```


## Riferimenti
{: #reference_nodejs}

La seguente tabella descrive i parametri utilizzati nelle funzioni descritte in questa documentazione Node.js:

|Parametro|Tipo di dati|Descrizione|
|:---|:---|
|`deviceType`|Stringa|Il tipo di dispositivo. Generalmente, il deviceType è un raggruppamento di dispositivi che esegue un'attività specifica, ad esempio "weatherballoon".|
|`deviceId`|Stringa|L'ID del dispositivo. Generalmente, per determinato tipo di dispositivo, il deviceId è un identificativo univoco di tale dispositivo, ad esempio un numero seriale o un indirizzo MAC.|
|`eventType`|Stringa|Un gruppo di eventi specifici, ad esempio "status", "warning" e "data".|
|`format`|Stringa|Il formato può essere qualsiasi stringa, ad esempio JSON.  |
|`data`|Dizionario|I dati per il payload del messaggio. La lunghezza massima è di 131072 byte.|
|`payload`|Stringa|I dati per il payload del messaggio. La lunghezza massima è di 131072 byte.|
|`topic`|Stringa|Quando pubblicato come un dispositivo, la stringa topic non include il tipo o l'ID del dispositivo; vengono presi dall'ID del client.  Ad esempio, `iot-2/evt/event_id/fmt/format_string`.  Quando pubblicato come un'applicazione o un gateway invece di come un dispositivo, la stringa topic deve includere l'ID e il tipo del dispositivo.  Ad esempio `iot-2/type/device_type/id/device_id/evt/event_id/fmt/format_string`.|
