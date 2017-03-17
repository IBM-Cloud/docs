---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-30"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

#Sviluppo dei gateway su {{site.data.keyword.iot_short_notm}} utilizzando Java
{: #java_cli_gw}

Se i tuoi dispositivi non possono collegarsi direttamente alla tua organizzazione su {{site.data.keyword.iot_full}}, puoi creare e personalizzare dei gateway utilizzando Java™. Vengono forniti una libreria client Java per {{site.data.keyword.iot_short_notm}}, la documentazione e gli esempi per aiutarti ad iniziare a sviluppare i gateway.
{:shortdesc}

## Scaricare le risorse e il client Java
{: #java_client_download}

Per accedere agli esempi e alle librerie client Java per {{site.data.keyword.iot_short_notm}}, vai al repository [iot-java](https://github.com/ibm-watson-iot/iot-java) in GitHub e completa le istruzioni di installazione.

## Constructor
{: #constructor}

Il constructor crea l'istanza client gateway e accetta l'oggetto `Properties` che contiene le seguenti definizioni:

|Definizione |Descrizione |
|:----|:----|
|`org`|Un valore obbligatorio che deve essere impostato nel tuo ID dell'organizzazione. Se stai utilizzando un flusso Quickstart, specifica `quickstart`.|
|`domain`|L'URL dell'endpoint di messaggistica, che è facoltativo. Se non specifichi un valore per un dominio, l'URL predefinito è `internetofthings.ibmcloud.com`, che è il server di produzione {{site.data.keyword.iot_short_notm}}.|
|`type`|Un valore obbligatorio che specifica il tipo di gateway.|
|`id` |Un valore obbligatorio che specifica l'ID univoco del gateway.|
|`auth-method`|Il metodo di autenticazione da utilizzare. L'unico metodo supportato è `token`.|
|`auth-token`|Un token di autenticazione della chiave API per la connessione sicura del tuo gateway a {{site.data.keyword.iot_short_notm}}.|
|`clean-session`|Un valore true o false obbligatorio solo se desideri collegarti al gateway con il metodo di sottoscrizione durevole. Per impostazione predefinita, `clean-session` è impostato su true.|
|`WebSocket`|Un valore true o false obbligatorio solo se desideri collegarti al gateway utilizzando i socket web.|
|`Porta`|Il numero di porta a cui collegarsi. Specifica 8883 o 443. Se non specifichi un numero di porta, il client si collega a {{site.data.keyword.iot_short_notm}} nel numero di porta 8883 per impostazione predefinita.|
|`MaxInflightMessages`|Imposta il numero massimo di messaggi in elaborazione per la connessione. Il valore predefinito è 100.|
|`Automatic-Reconnect`|Un valore true o false obbligatorio quando desideri ricollegare automaticamente il gateway a {{site.data.keyword.iot_short_notm}} mentre è in uno stato disconnesso. Il valore predefinito è false.|
|`Disconnected-Buffer-Size`|Il numero massimo di messaggi che possono essere archiviati nella memoria mentre il client è disconnesso. Il valore predefinito è 5000.|

**Nota:** per collegare il gateway con il metodo di sottoscrizione durevole, imposta `clean-session` su `false`. Per ulteriori informazioni sulla session di ripulitura, consulta la sezione 'Sottoscrizione buffer e ripulitura sessione' della [Documentazione MQTT](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

L'oggetto `Properties` crea le definizioni utilizzate per interagire con il modulo {{site.data.keyword.iot_short_notm}}.

Il seguente esempio di codice mostra come creare un'istanza client gateway:

```java
Properties options = new Properties();
options.setProperty("org", "<Your organization ID>");
options.setProperty("type", "<The gateway device type>");
options.setProperty("id", "The gateway device ID");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "API token");
GatewayClient gwClient = new GatewayClient(options);

```


### Utilizzo di un file di configurazione

Invece di utilizzare direttamente un oggetto `Properties` per creare direttamente un'istanza gateway, puoi anche utilizzare un file di configurazione che contiene le coppie nome-valore per le proprietà del gateway. Per utilizzare un file di configurazione per creare l'oggetto `Properties` per il gateway, utilizza il seguente formato del codice:

```Java
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
...
```

Il contenuto del file di configurazione deve essere nel seguente formato:

```java
[Gateway]
org=$orgId
domain=$domain
typ=$myGatewayDeviceType
id=$myGatewayDeviceId
auth-method=token
auth-token=$token

```

## Connessione a {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

Per collegarti a {{site.data.keyword.iot_short_notm}}, utilizza la funzione `connect()`. La funzione `connect()` include un parametro booleano facoltativo denominato `autoRetry` che determina se la libreria tenta di ricollegarsi nel caso di un errore di connessione dell'eccezione MQTT (MqttException). Per impostazione predefinita, `autoRetry` è impostato su true. Se una connessione MqttSecurityException ha esito negativo perché vengono trasmessi i dettagli di registrazione del dispositivo non corretti, la libreria non tenta di ricollegarsi, anche se `autoRetry` è impostato su true.

Per impostare l'intervallo keepalive per MQTT, puoi facoltativamente utilizzare il metodo `setKeepAliveInterval(int)` prima di richiamare la funzione `connect()`. Il valore `setKeepAliveInterval(int)` viene misurato in secondi e definisce l'intervallo di tempo massimo tra i messaggi inviati o ricevuti. Quando viene specificato un valore `setKeepAliveInterval(int)` il client può rilevare che il server non è più disponibile senza attendere che venga raggiunta la fine del periodo di timeout TCP/IP. Il client assicura che almeno un messaggio sia trasmesso in rete in ogni periodo di intervallo keepalive. Se i messaggi correlati a zero dati vengono ricevuti durante il periodo di timeout, il client invia un piccolo messaggio `ping`, che il server riconosce. `setKeepAliveInterval(int)` è impostato su 60 secondi per impostazione predefinita. Per disabilitare la funzione di elaborazione keepalive sul client, impostata il valore `setKeepAliveInterval(int)` su 0.

```java
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
gwClient.setKeepAliveInterval(80);
gwClient.connect();
```

Per controllare il numero di tentativi che si verificano quando una connessione ha esito negativo, utilizza la funzione connect(int numberOfTimesToRetry) sovrascritta.

```java
GatewayClient gwClient = new GatewayClient(props);
gwClient.setKeepAliveInterval(80);
gwClient .connect(10);
```

Dopo che il client si è correttamente collegato a {{site.data.keyword.iot_short_notm}}, il gateway può pubblicare eventi e sottoscrivere comandi per se stesso e anche al posto dei dispositivi allegati ad esso.

## Registrazione dei dispositivi che sono dietro al gateway
{: #register_device_gateway}

Puoi registrare i dispositivi che sono dietro al gateway collegato alla tua istanza {{site.data.keyword.iot_short_notm}} automaticamente o sviluppando il codice utilizzando l'API.

### Registrazione dispositivo automatica
Puoi registrare i tuoi dispositivi su {{site.data.keyword.iot_short_notm}} automaticamente quando il gateway pubblica un evento o sottoscrive un comando per i dispositivi collegati ad esso.

### Registrazione dispositivo API
Puoi anche utilizzare l'API {{site.data.keyword.iot_short_notm}} per registrare i dispositivi dietro a un gateway per la tua istanza {{site.data.keyword.iot_short_notm}}.

Per semplificare lo sviluppo con l'API {{site.data.keyword.iot_short_notm}}, avviare un'istanza client API richiamando il metodo api(), descritto nel seguente esempio di codice:

```java
import com.ibm.iotf.client.api.APIClient;
....

GatewayClient gwClient = new GatewayClient(props);
gwClient.connect();

APIClient api = gwClient.api();
```
Quando ricevi la gestione del client API, puoi iniziare la registrazione dei dispositivi a un gateway, come descritto nel seguente codice di esempio:

```java
gwClient.connect();

  String deviceToBeAdded = "{\"deviceId\": \"" + DEVICE_ID +
					"\",\"authToken\": \"qwer123\"}";

    JsonParser parser = new JsonParser();
    JsonElement input = parser.parse(deviceToBeAdded);
    JsonObject response = this.gwClient.api().registerDeviceUnderGateway(DEVICE_TYPE, gwDeviceId, gwDeviceType, input);

```

Quando un dispositivo dietro a un gateway viene registrato, il dispositivo viene associato al gateway dai valori degli attributi `gwDeviceId` e `gwDeviceType`.

## Pubblicazione eventi
{: #publish_events}

Gli eventi sono meccanismi con cui i dispositivi e i gateway pubblicano i dati in {{site.data.keyword.iot_short_notm}}. Il dispositivo o il gateway controlla il contenuto dell'evento e assegna un nome ad ogni evento che invia. Un gateway può pubblicare gli eventi per se stesso o per conto di qualsiasi dispositivo collegato attraverso di esso.

Quando viene ricevuto un evento dall'istanza {{site.data.keyword.iot_short_notm}}, le credenziali dell'evento ricevuto identificano il gateway di invio, il che significa che un gateway non può impersonare un altro dispositivo.

Gli eventi possono essere pubblicati in uno dei tre [livelli di QoS (quality of service)](../../reference/mqtt/index.html#qos-levels), definiti dal protocollo MQTT.  Per impostazione predefinita, gli eventi vengono pubblicati al livello QoS=0.

### Codice per la pubblicazione degli eventi gateway al livello QoS predefinito

```java
gwClient.connect();
  JsonObject event = new JsonObject();
  event.addProperty("name", "foo");
  event.addProperty("cpu",  90);
  event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event);
```

### Codice per l'incremento del livello QoS predefinito per un evento

Puoi incrementare i [livelli QoS](../../reference/mqtt/index.html#qos-levels) per gli eventi gateway pubblicati. Gli eventi con un livello QoS maggiore di zero possono impiegare più tempo per la pubblicazione, perché sono incluse ulteriori informazioni di ricezione della conferma.


```java
gwClient.connect();
  JsonObject event = new JsonObject();
  event.addProperty("name", "foo");
  event.addProperty("cpu",  90);
  event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event, 2);
```

### Codice per la pubblicazione di eventi nei formati personalizzati.

Gli eventi possono essere pubblicati in diversi formati, ad esempio, JSON, stringa, binario e altro. Per impostazione predefinita, la libreria pubblica gli eventi nel formato JSON, ma puoi specificare i dati in formati differenti se preferisci. Ad esempio, per pubblicare i dati nel formato stringa utilizza il seguente frammento di codice:

```java
gwClient.connect();
String data = "cpu:80";
boolean status = gwClient.publishGatewayEvent("load", data, "text", 2);
```

**Nota:** nel precedente esempio di codice, il payload dell'evento deve essere nel formato stringa:

I dati XML possono essere convertiti nel formato stringa e pubblicati come descritto nel seguente codice di esempio:

```java
status = gwClient.publishGatewayEvent("load", xmlConvertedString, "xml", 2);
```

In modo simile, per pubblicare gli eventi nel formato binario, utilizza un array di byte descritto nel seguente esempio:

```java
gwClient.connect();
byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = gwClient.publishGatewayEvent("blink", cpuLoad , "binary", 1);
```

### Codice per la pubblicazione di eventi dai dispositivi
{: #publishing_events_devices}

Un gateway può pubblicare gli eventi per conto di qualsiasi dispositivo collegato attraverso di esso trasmettendo i valori dell'ID del tipo appropriato e l'ID del dispositivo dell'evento originale, come descritto nel seguente esempio:

```java

gwClient.connect()

//Genera l'evento da pubblicare
    JsonObject event = new JsonObject();
    event.addProperty("name", "foo");
    event.addProperty("cpu",  60);
    event.addProperty("mem",  40);

// pubblica l'evento al posto del dispositivo
gwClient.publishDeviceEvent(deviceType, deviceId, eventName, event);
```

Utilizza il metodo overloaded `publishDeviceEvent()` per pubblicare l'evento del dispositivo al livello di QOS (quality of service) preferito. Per ulteriori informazioni sulla struttura dell'argomento utilizzata, consulta [Connettività MQTT per i gateway](../mqtt.html).

### Codice per la pubblicazione di eventi del dispositivo che sono in un formato personalizzato

In modo simile agli eventi gateway, anche gli eventi dispositivo possono essere pubblicati in diversi formati. Per impostazione predefinita, la libreria pubblica gli eventi dispositivo nel formato JSON, ma puoi specificare i dati in formati differenti se preferisci. Ad esempio, per pubblicare i dati nel formato stringa utilizza il seguente esempio di codice:

```java
gwClient.connect();
String data = "cpu:80";
boolean status = gwClient.publishDeviceEvent(deviceType, deviceId, "load", data, "text", 2);
```

**Nota:** il payload dell'evento deve essere nel formato stringa.

Tutti i dati XML possono essere convertiti nel formato stringa e pubblicati come mostrato nel seguente esempio di codice:

```java
status = gwClient.publishDeviceEvent(deviceType, deviceId, "load", xmlConvertedString, "xml", 2);
```

In modo simile, per pubblicare gli eventi dispositivo nel formato binario, utilizza un array di byte descritto nel seguente esempio:
```java
gwClient.connect();
byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = gwClient.publishDeviceEvent(deviceType, deviceId, "blink", cpuLoad , "binary", 1);
```

## Gestione dei comandi
{: #handling_commands}

Il gateway può sottoscriversi ai comandi indirizzati al gateway stesso o a qualsiasi dispositivo collegato dietro al gateway. Quando il client del dispositivo si connette, effettua automaticamente la sottoscrizione a qualsiasi comando per questo gateway. Ma per la sottoscrizione a uno qualsiasi dei comandi per i dispositivi collegati tramite il gateway, utilizza il metodo overloaded `subscribeToDeviceCommands()`, che è descritto nel seguente esempio:

```java
gwClient.connect()

// sottoscrizione ai comandi al posto del dispositivo
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

Per elaborare comandi specifici è necessario registrare un metodo di callback `Command`. I messaggi vengono restituiti come un'istanza della classe `Command`, che contiene le seguenti proprietà:


| Proprietà     |Tipo di dati     | Descrizione|
|----------------|----------------|---------------
|`deviceType`|Stringa| Il tipo di dispositivo per cui viene ricevuto il comando.|
|`deviceId`|Stringa| L'ID del dispositivo per cui viene ricevuto il comando, che può essere il gateway o un dispositivo collegato tramite il gateway.|
|`data`|Oggetto| Il payload del comando.|
|`format`|Stringa| Il formato del payload del comando, che può essere qualsiasi stringa, ad esempio, JSON. binario, testo o altro.|
|`command`|Stringa|Il nome del comando.|
|`timestamp`|org.joda.time.DateTime|La data e l'ora del momento in cui è stato inviato il comando.|

Il seguente codice di esempio descrive come puoi implementare il metodo di callback `Command`:

```java
import com.ibm.iotf.client.gateway.Command;
import com.ibm.iotf.client.gateway.GatewayCallback;

public class GatewayCommandCallback implements GatewayCallback, Runnable {
	// Una coda che ospita e elabora i comandi
	private BlockingQueue<Command> queue = new LinkedBlockingQueue<Command>();

	public void processCommand(Command cmd) {
  	    queue.put(cmd);
  	}

  	public void run() {
  	    while(true) {
  	        Command cmd = queue.take();
  	        System.out.println("Command " + cmd.getData());

  	        // codice per elaborare il comando
  	    }
  	}

  	/**
	 * Se un gateway si sottoscrive a un argomento di un dispositivo o invia i dati al posto di un dispositivo
	 * di cui il gateway non dispone dell'autorizzazione per il collegamento, il messaggio o la sottoscrizione viene ignorata.
	 * Questo comportamento è diverso confrontato con il comportamento delle applicazioni, dove la connessione viene terminata.
	 * Al gateway viene notificato nell'argomento di notifica:
	 */
  	@Override
public void processNotification(Notification notification) {

}
  }

```
Quando il callback `Command` viene aggiunto al client gateway, viene richiamato il metodo `processCommand()` ogni volta che per un comando viene pubblicato che dispone di criteri sottoscritti.

Il seguente codice di esempio descrive come aggiungere il metodo di callback `Command` nell'istanza del client gateway.

```java
gwClient.connect()
GatewayCommandCallback callback = new GatewayCommandCallback();
gwClient.setGatewayCallback(callback);
//Sottoscrizione a un dispositivo collegato al gateway
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

I metodi overloaded sono disponibili per controllare la sottoscrizione ai comandi.

### Elenco dei dispositivi collegati tramite un gateway
{: #list_devices_gw}


Per richiamare tutti i dispositivi collegati tramite il gateway specificato (typeId, deviceId) a {{site.data.keyword.iot_short_notm}}, richiama il metodo `getDevicesConnectedThroughGateway()`.

```java
gwClient.connect()
gwClient.api().getDevicesConnectedThroughGateway(gatewayType, gatewayId);
```

## Esempi
{: #samples}

Sono disponibili molti esempi per aiutarti nel collegamento di gateway e dispositivi dietro un gateway alla tua istanza {{site.data.keyword.iot_short_notm}}. Gli esempi utilizzano la libreria client Java {{site.data.keyword.iot_short_notm}} ubicata nel [Gateway Samples GitHub repository](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples).

## Istruzioni specifiche
{: #recipes}

| Ricetta     | Descrizione|
|----------------|----------------
|[Connecting your device as a gateway to {{site.data.keyword.iot_short_notm}}](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-gateway-to-watson-iot-platform/)| Un progetto GitHub e le istruzioni dettagliate che spiegano come collegare un gateway Raspberry Pi e i dispositivi Arduino Uno dietro il gateway a {{site.data.keyword.iot_short_notm}}.
|[Raspberry Pi as a managed gateway in {{site.data.keyword.iot_short_notm}} ](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/)|Un'estensione della precedente ricetta gateway che spiega come collegare il tuo gateway Raspberry Pi come un dispositivo gestito in {{site.data.keyword.iot_short_notm}} e come eseguire le operazioni di gestione.
