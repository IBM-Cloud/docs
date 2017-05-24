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


# Node.js per gli sviluppatori dei dispositivi
{: #nodejs}

Puoi modificare gli esempi e le librerie client in Node.js per creare e sviluppare il codice del dispositivo che interagisce con la tua organizzazione su {{site.data.keyword.iot_full}}.
{:shortdesc}

Utilizza le informazioni e gli esempi forniti per iniziare a sviluppare i tuoi dispositivi utilizzando Node.js.

## Scaricamento delle risorse e del client Node.js
{: #node.js_client_downloads}

Per accedere alle librerie client Node.js per {{site.data.keyword.iot_short_notm}} e ad altre risorse disponibili, vai al repository [iot-nodejs ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-watson-iot/iot-nodejs){: new_window} in GitHub e completa le istruzioni di installazione.


Per ulteriori informazioni, consulta le seguenti risorse:

- [Esempi per i dispositivi ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-watson-iot/iot-nodejs/tree/master/samples){: new_window} in Github
- Il repository [ibmiotf ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://www.npmjs.com/package/ibmiotf){: new_window} in NPM

## Constructor
{: #constructor}

Il constructor crea l'istanza del client del dispositivo. Accetta una configurazione JSON che contiene le seguenti definizioni:

|Definizione |Descrizione |
|:---|:---|
|`org` |Il tuo ID dell'organizzazione.|
|`type`  |Il tipo del tuo dispositivo. Generalmente, il deviceType è un raggruppamento di dispositivi che esegue un'attività specifica, ad esempio "weatherballoon".|
|`id`  |L'ID del tuo dispositivo. Generalmente, per determinato tipo dispositivo, il deviceId è un identificativo univoco di tale dispositivo, ad esempio un numero seriale o un indirizzo MAC.|
|`auth-method`   |Il metodo di autenticazione da utilizzare. L'unico valore al momento supportato è `token`.|
|`auth-token`   |Un token di autenticazione per la connessione sicura al tuo dispositivo su Watson IoT Platform. Questo campo è obbligatorio se `auth-method` è `token`.|

**Nota:** se vuoi utilizzare il servizio Quickstart, devi inviare solo le prime tre proprietà.

```
    var iotf = require("ibmiotf");
    var config = {
		"org" : "organization",
		"id" : "deviceId",
		"type" : "deviceType",
		"auth-method" : "token",
		"auth-token" : "authToken"
    };


    var deviceClient = new iotf.IotfDevice(config);
```

### Utilizzo di un file di configurazione

Invece di trasmettere direttamente la configurazione, puoi utilizzare un file di configurazione JSON per fornire le proprietà di configurazione richieste, come mostrato nel seguente esempio:


```  
    var iotf = require("ibmiotf");
    var config = require("./device.json");
    var deviceClient = new iotf.IotfDevice(config);  
```
Il file di configurazione `device.json` deve essere nel seguente formato:

```
	{
	  "org": "xxxxx",
	  "type": "raspi",
	  "id": "pi1",
	  "auth-method" : "token",
	  "auth-token" : "xxxxxxxxxxxxxxxx"
	}

```  

## Connessione a {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

Non puoi collegarti a {{site.data.keyword.iot_short_notm}} richiamando la funzione `connect`.

```
	var iotf = require("ibmiotf");
	var config = require("./device.json");

	var deviceClient = new iotf.IotfDevice(config);

	//impostazione del livello di log per eseguire il debug. Per impostazione predefinita è 'warn'
	deviceClient.log.setLevel('debug');

	deviceClient.connect();

	deviceClient.on('connect', function(){
		var i=0;
		console.log("connected");
		setInterval(function function_name () {
			i++;
			deviceClient.publish('myevt', 'json', '{"value":'+i+'}', 2);
		},2000);
	});

```

Dopo avere eseguito correttamente un connessione al servizio {{site.data.keyword.iot_short_notm}}, il client del dispositivo invia un evento `connect`. Questo processo indica che tutta la logica del dispositivo può essere implementata in questa funzione di callback.

Il client del dispositivo tenta automaticamente di ricollegarsi quando perde la connessione. Quando si ricollega correttamente, il client invia un evento `reconnect`.

## Accesso
{: #logging}

Per impostazione predefinita, vengono registrati solo gli eventi di log del tipo *warn*. Se desideri aumentare o diminuire il livello di registrazione, utilizza la funzione log.setLevel. Sono supportati i seguenti livelli di registrazione:
- trace
- debug
- info
- warn
- error

```
	var iotf = require("ibmiotf");
	var config = require("./device.json");

	var deviceClient = new iotf.IotfDevice(config);

	//impostazione del livello di log per eseguire il debug. Per impostazione predefinita è 'warn'
	deviceClient.log.setLevel('debug');

```


## Pubblicazione eventi
{: #publishing_events}

Gli eventi sono meccanismi con cui i dispositivi pubblicano i dati in {{site.data.keyword.iot_short_notm}}. Il dispositivo controlla il contenuto dell'evento e assegna un nome ad ogni evento che invia.

Quando viene ricevuto un evento dall'istanza {{site.data.keyword.iot_short_notm}}, le credenziali dell'evento ricevuto identificano il dispositivo di invio, il che significa che un dispositivo non può impersonare un altro dispositivo.

Puoi aumentare il livello di QoS (quality of service) per gli eventi pubblicati. Gli eventi con un livello QoS maggiore di `0` possono impiegare più tempo per la pubblicazione, perché sono incluse ulteriori informazioni di ricezione della conferma.

**Nota:** la modalità del flusso Quickstart supporta solo un livello QoS di `0`.


Gli eventi possono essere pubblicati con le seguenti proprietà:

|Proprietà |Descrizione|
|:---|:---|
|`eventType`  | Il tipo di evento che deve essere pubblicato, ad esempio stato o GPS. |  
|`eventFormat`  |Il formato dell'evento, ad esempio, JSON. |
|`data`  | Il payload dell'evento, che deve essere una stringa di buffer. |
|`QoS`  | Il QOS (quality of service) di MQTT per la pubblicazione degli eventi. I valori supportati sono 0, 1 e 2.|


```
    var deviceClient = new Client.IotfDevice(config);

    deviceClient.connect();

    deviceClient.on("connect", function () {
       //pubblica un evento con il QOS (quality of service) predefinito
       deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

       //pubblica un evento con il QOS (quality of service) definito dall'utente
       var myQosLevel=2
       deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}', myQosLevel);
  });

```

## Gestione dei comandi
{: #handling_commands}

Quando il client del dispositivo si connette, effettua automaticamente la sottoscrizione a qualsiasi comando per questo dispositivo. Per elaborare comandi specifici devi registrare una funzione di callback del comando. Il client del dispositivo richiama la funzione di callback del comando quando viene ricevuto un comando. La funzione di callback ha le seguenti proprietà:

|Proprietà |Descrizione|
|:---|:---|
|`commandName`  | Una stringa, che specifica il nome del comando che è stato richiamato. |  
|`format`  | Una stringa, che specifica il formato dell'evento, ad esempio, JSON. |
|`payload`  | Una stringa, che specifica i dati per il payload del comando.  |
|`topic`  | Quando pubblicato come un dispositivo, la stringa topic non include il tipo o l'ID del dispositivo; vengono presi dall'ID del client.  Ad esempio, `iot-2/evt/event_id/fmt/format_string`.  Quando pubblicato come un'applicazione o un gateway invece di come un dispositivo, la stringa topic deve includere l'ID e il tipo del dispositivo.  Ad esempio `iot-2/type/device_type/id/device_id/evt/event_id/fmt/format_string`.|


```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	deviceClient.on("connect", function () {
		//pubblica un evento con il QOS (quality of service) predefinito
       deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

	});

	deviceClient.on("command", function (commandName,format,payload,topic) {
		if(commandName === "blink") {
			console.log(blink);
			//la funzione da eseguire per questo comando
			blink(payload);
		} else {
			console.log("Command not supported.. " + commandName);
		}
	});

```

## Gestione degli errori
{: #handling_errors}

Quando il client del dispositivo rileva un errore, invia un evento *errore*.

```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	deviceClient.on("connect", function () {
		//pubblica un evento con il QOS (quality of service) predefinito
       deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

	});

	deviceClient.on("error", function (err) {
		console.log("Error : "+err);
	});
	....

```

## Disconnessione del client
{: #disconnecting_client}

Il seguente esempio mostra come puoi scollegare il client e rilasciare la connessione:

```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	client.on("connect", function () {
		//pubblica un evento con il QOS (quality of service) predefinito
		client.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

		//pubblica un evento con il QOS (quality of service) definito dall'utente
		var myQosLevel=2
		client.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}', myQosLevel);

		//disconnette il client
		client.disconnect();
	});

	....
```
