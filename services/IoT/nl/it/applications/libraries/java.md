---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Java per gli sviluppatori dell'applicazione
{: #java}


Puoi utilizzare Java™ per creare e personalizzare le applicazioni che interagiscono con la tua organizzazione su {{site.data.keyword.iot_full}}. Una libreria client Java per {{site.data.keyword.iot_short_notm}}, la documentazione e gli esempi ti vengono forniti per iniziare ad utilizzare lo sviluppo dell'applicazione.

{:shortdesc}

## Scaricare le risorse e il client Java
{: #java_client_download}

Ultimo aggiornamento: 25 ottobre 2016
{: .last-updated}

Per accedere agli esempi e alle librerie client Java per {{site.data.keyword.iot_short_notm}}, vai al repository [iot-java](https://github.com/ibm-watson-iot/iot-java) in GitHub e completa le istruzioni di installazione.


## Constructor
{: #constructor}

Il constructor crea l'istanza client e accetta l'oggetto `Properties` che contiene le seguenti definizioni:

| Definizione     |Descrizione     |
|----------------|----------------|
|`org` |Un valore obbligatorio che deve essere impostato nel tuo ID dell'organizzazione. Se stai utilizzando un flusso Quickstart, specifica `quickstart`.|
|`id` |L'ID univoco dell'applicazione nella tua organizzazione.|
|`auth-method`  |Il metodo di autenticazione. L'unico metodo supportato è `apikey`.|
|`auth-key`   |Una chiave API facoltativa, che devi specificare quando imposti il valore di auth-method su `apikey`.|
|`auth-token`   |Un token chiave API, che è inoltre obbligatorio quando imposti il valore di auth-method su `apikey`. |
|`clean-session`|Un valore true o false obbligatorio solo se desideri collegarti all'applicazione con il metodo di sottoscrizione durevole. Per impostazione predefinita, `clean-session` è impostato su `true`.|
|`Porta`|Il numero di porta a cui collegarsi. Specifica 8883 o 443. Se non specifichi un numero di porta, il client si collega a {{site.data.keyword.iot_short_notm}} nel numero di porta 8883 per impostazione predefinita.|
|`MaxInflightMessages`  |Imposta il numero massimo di messaggi in elaborazione per la connessione. Il valore predefinito è 100.|
|`Automatic-Reconnect`  |Un valore true o false obbligatorio quando desideri ricollegare automaticamente il dispositivo a {{site.data.keyword.iot_short_notm}} mentre è in uno stato disconnesso. Il valore predefinito è false.|
|`Disconnected-Buffer-Size`|Il numero massimo di messaggi che possono essere archiviati nella memoria mentre il client è disconnesso. Il valore predefinito è 5000.|
|`shared-subscription`|Un valore booleano che deve essere impostato su true se desideri creare applicazioni scalabili che bilanciano il carico dei messaggi tra più istanze dell'applicazione. Per ulteriori informazioni, consulta [Applicazioni scalabili](../mqtt.html#scalable_apps).

L'oggetto `Properties` crea le definizioni utilizzate per interagire con il modulo {{site.data.keyword.iot_short_notm}}. Se non specifichi le proprietà per questo oggetto o se specifichi `quickstart`, il client si collega al servizio Quickstart di {{site.data.keyword.iot_short_notm}} come un dispositivo non registrato.

Il seguente esempio di codice mostra come puoi creare l'istanza (`ApplicationClient`) client dell'applicazione nella modalità `quickstart`:

```
    import com.ibm.iotf.client.app.ApplicationClient;
    import java.util.Properties;

    Properties options = new Properties();
    options.put("org", "quickstart");

    ApplicationClient myClient = new ApplicationClient(options);
```

Il seguente esempio di codice mostra come puoi creare l'istanza (`ApplicationClient`) client dell'applicazione nella modalità del flusso registrato:

```
    Properties options = new Properties();
    options.put("org", "uguhsp");
    options.put("id", "app" + (Math.random() * 10000));
    options.put("Authentication-Method","apikey");
    options.put("API-Key", "<API-Key>");
    options.put("Authentication-Token", "<Authentication-Token>");

    ApplicationClient myClient = new ApplicationClient(options);
```

### Utilizzo di un file di configurazione

Invece di includere direttamente l'oggetto `Properties`, puoi utilizzare un file di configurazione che contiene una coppia nome-valore per l'oggetto `Properties`, come descritto nel seguente esempio di codice:

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    ...
```
Il file di configurazione dell'applicazione specificata deve essere nel seguente formato:

```
    [application]
    org=$orgId
    id=$myApplication
    auth-method=apikey
    auth-key=$key
    auth-token=$token
    enable-shared-subscription=true|false
```

## Connessione a {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

Per collegarti a {{site.data.keyword.iot_short_notm}}, utilizza la funzione `connect()`. La funzione `connect()` include un parametro booleano facoltativo denominato `autoRetry` che determina se la libreria tenta di ricollegarsi nel caso di un errore di connessione MqttException. Per impostazione predefinita, `autoRetry` è impostato su true. Se una connessione MqttSecurityException ha esito negativo perché vengono trasmessi i dettagli di registrazione del dispositivo non corretti, la libreria non tenta di ricollegarsi, anche se `autoRetry` è impostato su true.

Per impostare l'intervallo 'keepalive' per MQTT, puoi facoltativamente utilizzare il metodo `setKeepAliveInterval(int)` prima di richiamare la funzione `connect()`. Il valore `setKeepAliveInterval(int)` viene misurato in secondi e definisce l'intervallo di tempo massimo tra i messaggi inviati o ricevuti. Quando utilizzato, il client può rilevare quando il server non è più disponibile senza attendere che venga raggiunta la fine del periodo di timeout TCP/IP. Il client assicura che almeno un messaggio sia trasmesso in rete in ogni periodo di intervallo 'keepalive'. Se i messaggi correlati a zero dati vengono ricevuti durante il periodo di timeout, il client invia un piccolo messaggio `ping`, che il server riconosce. `setKeepAliveInterval(int)` è impostato su 60 secondi per impostazione predefinita. Per disabilitare la funzione di elaborazione 'keepalive' sul client, impostata il valore `setKeepAliveInterval(int)` su 0.

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    myClient.setKeepAliveInterval(120);
    myClient.connect();
```

Per controllare il numero di tentativi che si verificano quando c'è un errore di connessione, specifica un numero intero nella funzione myClient.connect(), come descritto nel seguente frammento di codice:

```
    DeviceClient myClient = new DeviceClient(options);
    myClient.setKeepAliveInterval(120);
    myClient.connect(10);
```

Dopo che i tuoi client dell'applicazione si sono collegati correttamente al servizio {{site.data.keyword.iot_short_notm}}, possono sottoscriversi agli eventi e agli stati del dispositivo e possono inoltre pubblicare gli eventi e i comandi del dispositivo.

## Sottoscrizione agli eventi del dispositivo
{: #subscribing_device_events}

Gli eventi sono meccanismi con cui i dispositivi pubblicano i dati in {{site.data.keyword.iot_short_notm}}. Il dispositivo controlla il contenuto dell'evento e assegna un nome ad ogni evento che invia.

Quando viene ricevuto un evento dall'istanza {{site.data.keyword.iot_short_notm}}, le credenziali dell'evento ricevuto identificano il dispositivo di invio, il che significa che un dispositivo non può impersonare un altro dispositivo.


Per impostazione predefinita, le applicazioni si sottoscrivono a tutti gli eventi da tutti i dispositivi collegati. Utilizza i parametri tipo di dispositivo, ID dispositivo e formato del messaggio per controllare l'ambito della sottoscrizione. I seguenti esempi di codice mostrano come puoi utilizzare questi parametri per definire l'ambito di una sottoscrizione:

### Sottoscrizione a tutti gli eventi provenienti da tutti i dispositivi


```
    myClient.connect();
    myClient.subscribeToDeviceEvents();
```
### Sottoscrizione a tutti gli eventi provenienti da tutti i dispositivi di un tipo specifico


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino");
```

### Sottoscrizione a tutti gli eventi da un dispositivo specifico


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee");
```
### Sottoscrizione di un evento specifico da due o più dispositivi differenti

```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee", "myEvent");
    myClient.subscribeToDeviceEvents("iotsample-arduino", "10aabbccddee", "myEvent");
```
### Sottoscrizione agli eventi che vengono pubblicati in formato JSON


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee", "myEvent", "json", 0);
```

**Nota**: un singolo client può supportare più sottoscrizioni.

## Gestione degli eventi dai dispositivi
{: #handling_device_events}

Per elaborare gli eventi ricevuti dalle tue sottoscrizioni, registra un metodo di callback dell'evento. I messaggi vengono restituiti come un'istanza della classe evento, che dispone dei seguenti parametri:

|Parametro|Tipo di dati|Descrizione|
|:---|:---|
|`event.device`|Stringa|Identifica univocamente il dispositivo tra tutti i tipi di dispositivi nell'organizzazione.|
|`event.deviceType`|Stringa|Identifica il tipo di dispositivo. Generalmente, il deviceType è un raggruppamento di dispositivi che esegue un'attività specifica, ad esempio, "weatherballoon" può essere un tipo di dispositivo.|
|`event.deviceId`|Stringa|Rappresenta l'ID del dispositivo. Generalmente, per un tipo di dispositivo specifico, il deviceId è un identificativo univoco di tale dispositivo, ad esempio un numero seriale o un indirizzo MAC.|
|`event.event`|Stringa|Solitamente viene utilizzato per raggruppare gli eventi specifici, ad esempio "status", "warning" e "data".|
|`event.format`|Stringa|Il formato può essere qualsiasi stringa, ad esempio JSON.  |
|`event.data`|Dizionario|I dati per il payload del messaggio. La lunghezza massima è di 131072 byte.|
|`event.timestamp`|Data e ora|La data e l'ora dell'evento|


Il seguente codice fornisce un'implementazione di esempio del callback dell'evento:

```
  import com.ibm.iotf.client.app.Event;
  import com.ibm.iotf.client.app.EventCallback;
  import com.ibm.iotf.client.app.Command;

  import java.util.concurrent.BlockingQueue;
  import java.util.concurrent.LinkedBlockingQueue;

  /**
    * A sample Event callback class that processes the device events in a separate thread.
    *
    */
   class MyEventCallback implements EventCallback, Runnable {

	// Una coda che ospita e elabora gli eventi per la gestione uniforme dei messaggi MQTT
	private BlockingQueue<Event> evtQueue = new LinkedBlockingQueue<Event>();

	public void processEvent(Event e) {
		try {
			evtQueue.put(e);
		} catch (InterruptedException e1) {
			e1.printStackTrace();
		}
	}

	@Override
	public void processCommand(Command cmd) {
		System.out.println("Command received:: " + cmd);
	}

	@Override
	public void run() {
		while(true) {
			Event e = null;
			try {
				e = evtQueue.take();
				// In questo esempio, l'unico output è l'evento
				System.out.println("Event:: " + e.getDeviceId() + ":" + e.getEvent() + ":" + e.getPayload());
			} catch (InterruptedException e1) {
				// Ignora l'eccezione interrotta, ritenta
				continue;
			}
		}
	}
    }
```

Quando il callback dell'evento viene aggiunto a ApplicationClient, viene richiamato il metodo `processEvent()` se viene pubblicato un evento che corrisponde alla sottoscrizione. Il seguente frammento mostra come aggiungere il callback dell'evento in un'istanza ApplicationClient:



```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToDeviceEvents();
```

In modo simile alla sottoscrizione agli eventi del dispositivo, l'applicazione può effettuare la sottoscrizione ai comandi inviati ai dispositivi. Il seguente esempio di codice mostra come effettuare una sottoscrizione a tutti i comandi per tutti i dispositivi nell'organizzazione:

```

    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToDeviceCommands();
```

I metodi overloaded sono disponibili per controllare la sottoscrizione ai comandi. Il metodo `processCommand()` viene richiamato quando al dispositivo viene inviato un comando che corrisponde alla sottoscrizione al comando.


## Sottoscrizione agli stati del dispositivo
{: #subscribing_device_status}

In modo simile alla sottoscrizione agli eventi del dispositivo, le applicazioni possono sottoscriversi allo stato del dispositivo, come ad esempio una connessione e disconnessione a {{site.data.keyword.iot_short_notm}}. Per impostazione predefinita, questa è una sottoscrizione agli aggiornamenti dello stato per tutti i dispositivi collegati. Utilizza i parametri tipo di dispositivo e ID dispositivo per controllare l'ambito della sottoscrizione. I seguenti esempi di codice mostrano come puoi utilizzare questi parametri per definire l'ambito di una sottoscrizione:

### Sottoscrizione agli aggiornamenti dello stato per tutti i dispositivi

```
    myClient.connect();
    myClient.subscribeToDeviceStatus();
```

### Sottoscrizione agli aggiornamenti dello stato per tutti i dispositivi di un tipo specifico


```

    myClient.connect();
    myClient.subscribeToDeviceStatus("iotsample-arduino");
```

### Sottoscrizione agli aggiornamenti dello stato per due dispositivi differenti


```

    myClient.connect();
    myClient.subscribeToDeviceStatus("iotsample-arduino", "00aabbccddee");
    myClient.subscribeToDeviceStatus("iotsample-arduino", "10aabbccddee");
```

**Nota**: un singolo client può supportare più sottoscrizioni.

## Gestione degli stati dai dispositivi
{: #handling_device_status_updates}

Per elaborare gli aggiornamenti dello stato ricevuti dalle tue sottoscrizioni, devi registrare un metodo di callback dell'evento dello stato. Per gli stati `Connect` e `Disconnect`, i messaggi vengono restituiti come un'istanza della classe dello stato, che contiene i seguenti parametri:


| Parametro     |Tipo di dati     |
|----------------|----------------|
|`status.clientAddr` |stringa|
|`status.protocol`  |stringa|
|`status.clientId`   |stringa|
|`status.user`   |stringa|
|`status.time`   |java.util.Date|
|`status.action` |stringa|
|`status.connectTime`   |java.util.Date|
|`status.port`|numero intero|

Le seguenti proprietà vengono impostate solo quando l'evento dello stato è `Disconnect`:

| Proprietà     |Tipo di dati     |
|----------------|----------------|
|`status.writeMsg` |numero intero|
|`status.readMsg`  |numero intero|
|`status.reason`   |stringa|
|`status.readBytes`   |numero intero|
|`status.writeBytes`   |numero intero|


Il seguente esempio di codice fornisce un'implementazione di esempio del callback dello stato:

```

  private static class MyStatusCallback implements StatusCallback {

      public void processApplicationStatus(ApplicationStatus status) {
          System.out.println("Application Status = " + status.getPayload());
      }

      public void processDeviceStatus(DeviceStatus status) {
          if(status.getAction() == "Disconnect") {
              System.out.println("device: "+status.getDeviceId()
                                  + "  time: "+ status.getTime()
                                  + "  action: " + status.getAction()
                                  + "  reason: " + status.getReason());
          } else {
              System.out.println("device: "+status.getDeviceId()
                                  + "  time: "+ status.getTime()
                                  + "  action: " + status.getAction());
          }
      }
  }
```

Quando il callback dello stato viene aggiunto al client dell'applicazione, viene richiamato il metodo `processDeviceStatus()` se viene collegato o scollegato un dispositivo che corrisponde ai criteri da {{site.data.keyword.iot_short_notm}}. Il seguente esempio di codice mostra come puoi aggiungere l'istanza di callback dello stato al client dell'applicazione:

```

    myClient.connect()
    myClient.setStatusCallback(new MyStatusCallback());
    myClient.subscribeToDeviceStatus();
```
Le applicazioni possono sottoscriversi a qualsiasi altro stato dell'applicazione, come ad esempio la connessione o disconnessione dell'applicazione da {{site.data.keyword.iot_short_notm}}. Il seguente frammento di codice mostra come effettuare una sottoscrizione allo stato dell'applicazione di un'organizzazione {{site.data.keyword.iot_short_notm}}:

```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToApplicationStatus();
```
Il metodo overloaded è disponibile per controllare la sottoscrizione dello stato a un'applicazione in particolare. Il metodo `processApplicationStatus()` è richiamato se viene collegata o scollegata un'applicazione che corrisponde ai criteri da {{site.data.keyword.iot_short_notm}}.


## Pubblicazione degli eventi dai dispositivi
{: #publishing_events_devices}

Il seguente esempio di codice mostra come le applicazione possono pubblicare gli eventi come se fossero originati da un dispositivo.

```

    myClient.connect()

    //Genera l'evento da pubblicare
    JsonObject event = new JsonObject();
    event.addProperty("name", "foo");
    event.addProperty("cpu",  60);
    event.addProperty("mem",  40);

    // pubblica l'evento al posto del dispositivo
    myClient.publishEvent(deviceType, deviceId, "blink", event);
```


Gli eventi possono essere pubblicati in diversi formati, ad esempio, JSON, stringa, binario e altro. Per impostazione predefinita, la libreria pubblica gli eventi nel formato JSON, ma puoi specificare i dati in formati differenti se preferisci. Ad esempio, per pubblicare i dati nel formato stringa utilizza il seguente frammento di codice:

```
    myClient.connect();
    String data = "cpu:"+60;
    status = myClient.publishEvent("load", data, "text", 2);
```
**Nota:** nel precedente esempio di codice, il payload dell'evento deve essere nel formato stringa:

Tutti i dati XML possono essere convertiti nel formato stringa e pubblicati nel seguente modo:

```
    status = myClient.publishEvent("load", xmlConvertedString, "xml", 2);
```

In modo simile, per pubblicare gli eventi nel formato binario, utilizza un array di byte, come descritto nel seguente esempio:

```
    myClient.connect();
    byte[] cpuLoad = new byte[] {60, 35, 30, 25};
    status = myClient.publishEvent("blink", cpuLoad , "binary", 1);
```

### Pubblica gli eventi utilizzando l'HTTP
{: #publishing_events_http}

In aggiunta all'utilizzo di MQTT, puoi anche configurare le tue applicazioni in modo che pubblichino gli eventi del dispositivo in {{site.data.keyword.iot_short_notm}} tramite HTTP. La seguente procedura descrive la sequenza per la pubblicazione degli eventi del dispositivo tramite HTTP:

1. Crea l'istanza ApplicationClient utilizzando il file delle proprietà.
2. Crea l'evento che deve essere pubblicato.
3. Specifica il nome dell'evento, il tipo di dispositivo e l'ID del dispositivo.
4. Pubblica l'evento utilizzando il metodo `publishEventOverHTTP`(), come mostrato nel seguente esempio di codice:

```
    	ApplicationClient myClient = new ApplicationClient(props);

    	JsonObject event = new JsonObject();
    	event.addProperty("name", "foo");
    	event.addProperty("cpu",  90);
    	event.addProperty("mem",  70);

    	boolean status = myClient.publishApplicationEventforDeviceOverHTTP(deviceId, deviceType, "blink", event, ContentType.json);
```

Per l'esempio di codice completo, consulta l'applicazione di esempio [HttpApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpApplicationDeviceEventPublish.java).

In base alle impostazioni nel file delle proprietà, il metodo `publishEventOverHTTP()` pubblica l'evento nel flusso registrato o in  Quickstart. Quando `quickstart` viene specificato come ID dell'organizzazione nel file delle proprietà, il metodo `publishEventOverHTTP()` pubblica l'evento al servizio Quickstart {{site.data.keyword.iot_short_notm}} nel formato HTTP semplice. Quando viene specificata un'organizzazione registrata valida nel file delle proprietà, l'evento viene sempre pubblicato utilizzando HTTPS in modo che tutte le comunicazioni siano sicure.

Il protocollo HTTP fornisce la distribuzione 'at most once', che è simile al livello di QOS (quality of service) 'at most once' del protocollo MQTT. Quando utilizzi la distribuzione 'at most once' per pubblicare gli eventi, l'applicazione deve implementare la logica del nuovo tentativo quando si verifica un errore.


## Pubblicazione dei comandi ai dispositivi
{: #publishing_commands_devices}

Le applicazioni possono pubblicare i comandi sui dispositivi connessi, come mostrato nel seguente esempio:

```

    myClient.connect()

    //Genera l'evento da pubblicare
    JsonObject data = new JsonObject();
    data.addProperty("name", "stop-rotation");
    data.addProperty("delay",  0);

    //Il flusso di lavoro registrato consente 0, 1 e 2 QoS
    myAppClient.publishCommand(deviceType, deviceId, "stop", data);
```

### Pubblica i comandi utilizzando l'HTTP
{: #publishing_commands_http}

In aggiunta all'utilizzo di MQTT, puoi anche configurare le tue applicazioni in modo che pubblichino i comandi al dispositivo collegato tramite HTTP. La seguente procedura descrive la sequenza per la pubblicazione degli eventi del dispositivo utilizzando HTTP:

1. Crea l'istanza ApplicationClient utilizzando il file delle proprietà
2. Crea il comando che deve essere pubblicato
3. Specifica il nome del comando, il tipo di dispositivo e l'ID del dispositivo
4. Pubblica il comando utilizzando il metodo `publishCommandOverHTTP`(), come mostrato nel seguente codice:

```

    	ApplicationClient myClient = new ApplicationClient(props);

    	// Genera un oggetto JSON dell'evento da pubblicare
	JsonObject event = new JsonObject();
	event.addProperty("reboot", 5);

	boolean response = myClient.publishCommandOverHTTP("execute", event);
```

Per visualizzare l'esempio di codice completo, consulta l'applicazione di esempio [HttpCommandPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpCommandPublish.java).

Il protocollo HTTP fornisce la distribuzione 'at most once', che è simile al livello di QOS (quality of service) 'at most once' del protocollo MQTT. Quando utilizzi la distribuzione 'at most once' per pubblicare i comandi, l'applicazione deve implementare la logica del nuovo tentativo quando si verifica un errore. Per ulteriori informazioni, consulta [API REST HTTP per le applicazioni](../api.html).


## Esempi
{: #samples}

-  [MQTTApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/MQTTApplicationDeviceEventPublish.java) - Un'applicazione di esempio che mostra come puoi pubblicare gli eventi del dispositivo.
-   [RegisteredApplicationCommandPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationCommandPublish.java) - Un'applicazione di esempio che mostra come puoi pubblicare un comando in un dispositivo.
-  [RegisteredApplicationSubscribeSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationSubscribeSample.java) - Un'applicazione di esempio che mostra come puoi sottoscriverti a eventi differenti come gli eventi, i comandi e lo stato del dispositivo e dell'applicazione.
-   [SharedSubscriptionSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/SharedSubscriptionSample.java) - Un'applicazione di esempio che mostra come puoi creare un'applicazione scalabile che bilancia il carico dei messaggi tra più istanze dell'applicazione.
-  [Esempio di backup e ripristino](https://github.com/ibm-messaging/iot-backup-restore-sample) - Un esempio che mostra come puoi eseguire il backup e il ripristino della configurazione del dispositivo in {{site.data.keyword.cloudant}}.
