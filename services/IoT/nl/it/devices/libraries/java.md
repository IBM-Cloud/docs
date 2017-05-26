---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-21"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Java per gli sviluppatori dei dispositivi
{: #java}

Puoi utilizzare Java™ per creare e personalizzare i dispositivi che interagiscono con la tua organizzazione su {{site.data.keyword.iot_full}}. Una libreria client Java per {{site.data.keyword.iot_short_notm}}, la documentazione e gli esempi ti vengono forniti per iniziare ad utilizzare lo sviluppo del dispositivo.
{:shortdesc}

## Scaricare le risorse e il client Java
{: #java_client_download}

Per accedere agli esempi e alle librerie client Java per {{site.data.keyword.iot_short_notm}}, vai al repository [iot-java ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-watson-iot/iot-java){: new_window} in GitHub e completa le istruzioni di installazione.

## Constructor
{: #constructor}

Il constructor crea l'istanza client e accetta l'oggetto `Properties` che contiene le seguenti definizioni:

|Definizione |Descrizione |
|:----|:----|
|`org` |Un valore obbligatorio che deve essere impostato nel tuo ID dell'organizzazione. Se stai utilizzando un flusso Quickstart, specifica `quickstart`.|
|`type`  |Un valore obbligatorio che specifica il tipo del dispositivo.|
|`id`  |Un valore obbligatorio che specifica l'ID univoco del dispositivo.|
|`auth-method`  |Il metodo di autenticazione da utilizzare. L'unico metodo supportato è `token`.|
|`auth-token`   |Un token di autenticazione per la connessione sicura al tuo dispositivo a {{site.data.keyword.iot_short_notm}}.|
|`clean-session`|Un valore true o false obbligatorio solo se desideri collegarti all'applicazione con il metodo di sottoscrizione durevole. Per impostazione predefinita, `clean-session` è impostato su true.|
|`Porta`|Il numero di porta a cui collegarsi. Specifica 8883 o 443. Se non specifichi un numero di porta, il client si collega a {{site.data.keyword.iot_short_notm}} nel numero di porta 8883 per impostazione predefinita.|
|`MaxInflightMessages`  |Imposta il numero massimo di messaggi in elaborazione per la connessione. Il valore predefinito è 100.|
|`Automatic-Reconnect`  |Un valore true o false obbligatorio quando desideri ricollegare automaticamente il dispositivo a {{site.data.keyword.iot_short_notm}} mentre è in uno stato disconnesso. Il valore predefinito è false.|
|`Disconnected-Buffer-Size`|Il numero massimo di messaggi che possono essere archiviati nella memoria mentre il client è disconnesso. Il valore predefinito è 5000.|
|`WebSocket`|Un valore true o false obbligatorio quando desideri utilizzare le connessioni websocket con {{site.data.keyword.iot_short_notm}}. Il valore predefinito è false.|

**Nota:** per collegare il dispositivo con il metodo di sottoscrizione durevole, imposta `clean-session` su `false`. Per ulteriori informazioni sulla session di ripulitura, consulta la sezione 'Sottoscrizione buffer e ripulitura sessione' della [Documentazione MQTT](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

L'oggetto `Properties` crea le definizioni utilizzate per interagire con il modulo {{site.data.keyword.iot_short_notm}}.

Il seguente esempio di codice mostra come i dispositivi possono pubblicare gli eventi nella modalità Quickstart.

```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class QuickstartDeviceEventPublish {

    public static void main(String[] args) {

        //Fornisci i dati specifici del dispositivo utilizzando la classe delle proprietà
        Properties options = new Properties();
        options.setProperty("org", "quickstart");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");

        DeviceClient myClient = null;
        try {
            //Istanzia la classe trasmettendo il file delle proprietà
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Collega a {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Genera un oggetto JSON dell'evento da pubblicare
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Il flusso Quickstart consente solo QoS = 0
        myClient.publishEvent("status", event, 0);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

Il seguente esempio di codice mostra come i dispositivi possono pubblicare gli eventi in un flusso registrato.


```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class RegisteredDeviceEventPublish {

    public static void main(String[] args) {

        //Fornisce i dati specifici del dispositivo, così come una Auth-key e un token utilizzando la classe delle proprietà
        Properties options = new Properties();

        options.setProperty("org", "uguhsp");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");
        options.setProperty("auth-method", "token");
        options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");

        DeviceClient myClient = null;
        try {
            //Istanzia la classe trasmettendo il file delle proprietà
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Collega a {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Genera un oggetto JSON dell'evento da pubblicare
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Il flusso registrato consente solo 0, 1 e 2 QoS
        myClient.publishEvent("status", event);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

### Utilizzo di un file di configurazione

Invece di utilizzare direttamente un oggetto `Properties`, puoi anche utilizzare un file di configurazione che contiene le coppie nome-valore per le proprietà. Se stai utilizzando un file delle proprietà che contiene un oggetto `Properties`, utilizza il seguente formato del codice:

```
package com.ibm.iotf.sample.client.device;

import java.io.File;
import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class RegisteredDeviceEventPublishPropertiesFile {

    public static void main(String[] args) {
        //Fornisce i dati specifici del dispositivo, così come una Auth-key e un token utilizzando la classe delle proprietà
        Properties options = DeviceClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));

        DeviceClient myClient = null;
        try {
            //Istanzia la classe trasmettendo il file delle proprietà
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Collega a {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Genera un oggetto JSON dell'evento da pubblicare
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Il flusso registrato consente solo 0, 1 e 2 QoS
        myClient.publishEvent("status", event, 1);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

Il contenuto del file di configurazione deve essere nel seguente formato:

```
    [device]
    org=$orgId
    typ=$myDeviceType
    id=$myDeviceId
    auth-method=token
    auth-token=$token
```

## Connessione a {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}


Per collegarti a {{site.data.keyword.iot_short_notm}}, utilizza la funzione `connect()`. La funzione `connect()` include un parametro booleano facoltativo denominato `autoRetry` che determina se la libreria tenta di ricollegarsi nel caso di un errore di connessione MqttException. Per impostazione predefinita, `autoRetry` è impostato su true. Se una connessione MqttSecurityException ha esito negativo perché vengono trasmessi i dettagli di registrazione del dispositivo non corretti, la libreria non tenta di ricollegarsi, anche se `autoRetry` è impostato su true.

Per impostare l'intervallo 'keepalive' per MQTT, puoi facoltativamente utilizzare il metodo `setKeepAliveInterval(int)` prima di richiamare la funzione `connect()`. Il valore `setKeepAliveInterval(int)` viene misurato in secondi e definisce l'intervallo di tempo massimo tra i messaggi inviati o ricevuti. Quando utilizzato, il client può rilevare quando il server non è più disponibile senza attendere che venga raggiunta la fine del periodo di timeout TCP/IP. Il client assicura che almeno un messaggio sia trasmesso in rete in ogni periodo di intervallo 'keepalive'. Se i messaggi correlati a zero dati vengono ricevuti durante il periodo di timeout, il client invia un piccolo messaggio `ping`, che il server riconosce. `setKeepAliveInterval(int)` è impostato su 60 secondi per impostazione predefinita. Per disabilitare la funzione di elaborazione 'keepalive' sul client, impostata il valore `setKeepAliveInterval(int)` su 0.


```
DeviceClient myClient = new DeviceClient(options);
myClient.setKeepAliveInterval(120);
myClient.connect(true);
```

Per controllare il numero di tentativi che si verificano quando c'è un errore di connessione, utilizza la funzione connect(int numberOfTimesToRetry) sovrascritta.


```
DeviceClient myClient = new DeviceClient(options);
    myClient.setKeepAliveInterval(120);
    myClient.connect(10);
```

Dopo aver collegato correttamente i tuoi dispositivi a {{site.data.keyword.iot_short_notm}}, possono pubblicare eventi e sottoscriversi ai comandi del dispositivo da un'applicazione.


## Pubblicazione eventi
{: #publishing_events}

Gli eventi sono meccanismi con cui i dispositivi pubblicano i dati in {{site.data.keyword.iot_short_notm}}. Il dispositivo controlla il contenuto dell'evento e assegna un nome ad ogni evento che invia.

Quando viene ricevuto un evento dall'istanza {{site.data.keyword.iot_short_notm}}, le credenziali dell'evento ricevuto identificano il dispositivo di invio, il che significa che un dispositivo non può impersonare un altro dispositivo.

Gli eventi possono essere pubblicati in uno dei tre [livelli di QoS (quality of service)](../../reference/mqtt/index.html#qos-levels), definiti dal protocollo MQTT.  Per impostazione predefinita, gli eventi vengono pubblicati al livello QoS=0.

### Pubblica gli eventi al livello QoS predefinito

```
myClient.connect();

JsonObject event = new JsonObject();
    	event.addProperty("name", "foo");
    	event.addProperty("cpu",  90);
    	event.addProperty("mem",  70);

myClient.publishEvent("status", event);
```


### Aumento del livello QoS per un evento

Puoi aumentare i [livelli QoS](../../reference/mqtt/index.html#qos-levels) per gli eventi che sono stati pubblicati. Gli eventi con un livello QoS maggiore di zero possono impiegare più tempo per la pubblicazione, perché sono incluse ulteriori informazioni di ricezione della conferma.

```
myClient.connect();

JsonObject event = new JsonObject();
    	event.addProperty("name", "foo");
    	event.addProperty("cpu",  90);
    	event.addProperty("mem",  70);

//Il flusso di lavoro registrato consente 0, 1 e 2 QoS
myClient.publishEvent("status", event, 2);
```

### Pubblicazione di eventi nei formati personalizzati.

Gli eventi possono essere pubblicati in diversi formati, ad esempio, JSON, stringa, binario e altro. Per impostazione predefinita, la libreria pubblica gli eventi nel formato JSON, ma puoi specificare i dati in formati differenti se preferisci. Ad esempio, per pubblicare i dati nel formato stringa utilizza il seguente frammento di codice:

```
myClient.connect();

String data = "cpu:"+getProcessCpuLoad();
status = myClient.publishEvent("load", data, "text", 2);
```

**Nota:** nel precedente esempio di codice, il payload dell'evento deve essere nel formato stringa:

Tutti i dati XML possono essere convertiti nel formato stringa e pubblicati nel seguente modo,

```
status = myClient.publishEvent("load", xmlConvertedString, "xml", 2);
```

In modo simile, per pubblicare gli eventi nel formato binario, utilizza un array di byte descritto nel seguente esempio:

```
myClient.connect();

byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = myClient.publishEvent("blink", cpuLoad , "binary", 1);
```

### Pubblica gli eventi utilizzando l'HTTP
{: #publishing_events_http}


In aggiunta all'utilizzo di MQTT, puoi anche configurare i tuoi dispositivi in modo che pubblichino gli eventi in {{site.data.keyword.iot_short_notm}} tramite HTTP. La seguente procedura descrive la sequenza per la pubblicazione degli eventi tramite HTTP:

1. Crea un'istanza `DeviceClient` utilizzando il file delle proprietà.
2. Crea un evento che deve essere pubblicato.
3. Specifica il nome dell'evento e quindi pubblicalo utilizzando il metodo `publishEventOverHTTP()`, come mostrato nel seguente esempio di codice:

``` 
DeviceClient myClient = new DeviceClient(deviceProps);

JsonObject event = new JsonObject();
    	event.addProperty("name", "foo");
    	event.addProperty("cpu",  90);
    	event.addProperty("mem",  70);

boolean response  = myClient.api().publishDeviceEventOverHTTP("blink", event, ContentType.json);
```

Per visualizzare il codice completo, consulta l'esempio del dispositivo [HttpDeviceEventPublish ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")].{: new_window}

In base alle impostazioni nel file delle proprietà, il metodo `publishEventOverHTTP()` pubblica l'evento in modalità Quickstart o nella modalità del flusso registrato. Quando l'ID dell'organizzazione nel file delle proprietà è impostato su `quickstart`, il metodo `publishEventOverHTTP()` pubblica l'evento nel servizio quickstart di esempio del dispositivo e lo pubblica nel formato HTTP semplice. Quando viene specificata un'organizzazione registrata valida nel file delle proprietà, gli eventi sono pubblicati in modo sicuro tramite HTTPS.

Il protocollo HTTP fornisce la distribuzione 'at most once', che è simile al livello di QOS (quality of service) 'at most once' del protocollo MQTT. Quando utilizzi la distribuzione 'at most once' per pubblicare gli eventi, l'applicazione deve implementare la logica del nuovo tentativo se si verifica un errore.

[HttpDeviceEventPublish]: https://github.com/ibm-messaging/iot-device-samples/blob/master/java/device-samples/src/main/java/com/ibm/iotf/sample/client/device/HttpDeviceEventPublish.java

## Gestione dei comandi
{: #handling_commands}

Quando il client del dispositivo si connette, effettua automaticamente la sottoscrizione a qualsiasi comando per questo dispositivo. Per elaborare comandi specifici è necessario registrare un metodo di callback del comando.
I messaggi vengono restituiti come un'istanza della classe `Command`, che contiene le seguenti proprietà:

| Proprietà     |Tipo di dati     | Descrizione|
|----------------|----------------|
|`payload` |java.lang.String| I dati per il payload del messaggio.|
|`format`  |java.lang.String| Il formato può essere qualsiasi stringa, ad esempio JSON.|
|`command`   |java.lang.String|Identifica il comando.|
|`timestamp`   |org.joda.time.DateTime|La data e l'ora dell'evento.|


```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.LinkedBlockingQueue;


import com.ibm.iotf.client.device.Command;
import com.ibm.iotf.client.device.CommandCallback;
import com.ibm.iotf.client.device.DeviceClient;


//Implementa la classe CommandCallback per fornire il metodo con cui si desidera il comando sia gestito
class MyNewCommandCallback implements CommandCallback, Runnable {

    // Una coda che ospita e elabora i comandi per la gestione uniforme dei messaggi MQTT
    private BlockingQueue<Command> queue = new LinkedBlockingQueue<Command>();

    /**
    * Questo metodo viene richiamato dalla libreria se è presente un comando che corrisponda ai criteri della sottoscrizione
    */
    @Override
    public void processCommand(Command cmd) {
        try {
            queue.put(cmd);
            } catch (InterruptedException e) {
        }
    }

    @Override
	public void run() {
        while(true) {
            Command cmd = null;
            try {
                //In questo esempio, visualizziamo solo il comando
                cmd = queue.take();
                System.out.println("COMMAND RECEIVED = '" + cmd.getCommand() + "'\twith Payload = '" + cmd.getPayload() + "'");
            } catch (InterruptedException e) {}
        }
    }
}

public class RegisteredDeviceCommandSubscribe {


    public static void main(String[] args) {

        //Fornisce i dati specifici del dispositivo, così come una Auth-key e un token utilizzando la classe delle proprietà
        Properties options = new Properties();

        options.setProperty("org", "uguhsp");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");
        options.setProperty("auth-method", "token");
        options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");

        DeviceClient myClient = null;
        try {
            //Istanzia la classe trasmettendo il file delle proprietà
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Trasmette il seguente CommandCallback implementato come un argomento a questo client del dispositivo
        myClient.setCommandCallback(new MyNewCommandCallback());

        //Collega a {{site.data.keyword.iot_short_notm}}
        myClient.connect();
    }
}
```

## Esempi
{: #samples}

Per un elenco di dispositivi e di esempi di gestione del dispositivo sviluppati utilizzando la libreria Java client {{site.data.keyword.iot_short_notm}}, consulta il repository [iot-device-samples GitHub ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-messaging/iot-device-samples/tree/master/java){: new_window}.
