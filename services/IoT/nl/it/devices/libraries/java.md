---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Java per gli sviluppatori dei dispositivi
{: #java}

Ultimo aggiornamento: 02 agosto 2016
{: .last-updated}


Puoi utilizzare Java per creare e personalizzare i dispositivi che interagiscono con la tua organizzazione su {{site.data.keyword.iot_full}}. Utilizza le informazioni e gli esempi forniti per iniziare a sviluppare i tuoi dispositivi utilizzando Java. {:shortdesc}

## Scaricare le risorse e il client Java
{: #java_client_download}

Per accedere agli esempi e alle librerie client Java per {{site.data.keyword.iot_short_notm}}, vai al repository [iot-java](https://github.com/ibm-watson-iot/iot-java) in GitHub e completa le istruzioni di installazione.


## Constructor
{: #constructor}

Il constructor crea l'istanza client e accetta un oggetto delle proprietà che contiene le seguenti definizioni: 

|Definizione |Descrizione |
|:---|:---|
|`org` |Il tuo ID dell'organizzazione. Questo campo è obbligatorio. Se stai utilizzando un flusso Quickstart, specifica `quickstart`.|
|`type`  |Il tipo del tuo dispositivo. Questo campo è obbligatorio. |
|`id`  |L'ID del tuo dispositivo. Questo campo è obbligatorio. |
|`auth-method`   |Il metodo di autenticazione da utilizzare. L'unico valore al momento supportato è `token`. |
|`auth-token`   |Un token di autenticazione per la connessione sicura al tuo dispositivo su Watson IoT Platform. |
|`clean-session`|Un valore true o false obbligatorio solo se desideri collegarti all'applicazione con il metodo di sottoscrizione durevole. Per impostazione predefinita, `clean-session` è impostato su `true`.|

**Nota:** per collegare il dispositivo con il metodo di sottoscrizione durevole, imposta `clean-session` su `false`. Per ulteriori informazioni sulla session di ripulitura, consulta la sezione 'Sottoscrizione buffer e ripulitura sessione' della [Documentazione MQTT](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

L'oggetto delle proprietà crea le definizioni utilizzate per interagire con il modulo {{site.data.keyword.iot_short_notm}}. 

Il seguente codice mostra un dispositivo che pubblica gli eventi nella modalità Quickstart. 

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

Invece di utilizzare direttamente un oggetto delle proprietà, puoi anche utilizzare un file di configurazione che contiene le coppie nome-valore per le proprietà. Se stai utilizzando un file delle proprietà che contiene un oggetto delle proprietà, utilizza il seguente formato del codice:

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

Collega a {{site.data.keyword.iot_short_notm}} richiamando la funzione di connessione. La funzione di connessione richiede un parametro booleano facoltativo `autoRetry`, che per impostazione predefinita è `true`. Il parametro `autoRetry` consente alla libreria di ricollegarsi quando si verifica un errore MqttException. Tieni presente che la libreria non tenta di ricollegarsi quando sono presenti degli errori MqttSecurityException perché sono stati utilizzati dei dettagli di registrazione del dispositivo non corretti, anche se il parametro `autoRetry` è impostato su `true`.

```
DeviceClient myClient = new DeviceClient(options);

myClient.connect(true);
```

Dopo avere eseguito correttamente un connessione al servizio {{site.data.keyword.iot_short_notm}}, il client del dispositivo può eseguire delle operazioni come la pubblicazione di eventi e la sottoscrizione ai comandi del dispositivo da un'applicazione.


## Pubblicazione eventi
{: #publishing_events}

Gli eventi sono meccanismi con cui i dispositivi pubblicano i dati in {{site.data.keyword.iot_short_notm}}. Il dispositivo controlla il contenuto dell'evento e assegna un nome ad ogni evento che invia.

Quando viene ricevuto un evento dall'istanza {{site.data.keyword.iot_short_notm}}, le credenziali dell'evento ricevuto identificano il dispositivo di invio, il che significa che un dispositivo non può impersonare un altro dispositivo.

Gli eventi possono essere pubblicati in uno dei tre [livelli di QoS (quality of service)](../../reference/mqtt/index.html#qos-levels), definiti dal protocollo MQTT. Per impostazione predefinita, gli eventi vengono pubblicati al livello QoS=0.

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

### Pubblica gli eventi utilizzando l'HTTP 

In aggiunta a MQTT, i dispositivi possono pubblicare gli eventi in {{site.data.keyword.iot_short_notm}} utilizzando l'HTTP con la seguente procedura:

* Crea un'istanza DeviceClient utilizzando il file delle proprietà.
* Creare un evento che deve essere pubblicato. 
* Specifica il nome dell'evento e pubblicalo utilizzando il metodo `publishEventOverHTTP()`, come mostrato nel seguente codice:

``` sourceCode
DeviceClient myClient = new DeviceClient(deviceProps);

JsonObject event = new JsonObject();
    	event.addProperty("name", "foo");
    	event.addProperty("cpu",  90);
    	event.addProperty("mem",  70);

int httpCode = myClient.publishEventOverHTTP("blink", event);
```

Puoi trovare il codice completo nell'esempio del dispositivo [HttpDeviceEventPublish].

In base alle impostazioni nel file delle proprietà, il metodo `publishEventOverHTTP()` pubblica l'evento in modalità Quickstart o nella modalità del flusso registrato . Quando l'ID dell'organizzazione nel file delle proprietà è `quickstart`, il metodo `publishEventOverHTTP()` pubblica l'evento nel servizio quickstart di esempio del dispositivo e lo pubblica nel formato HTTP semplice. Quando viene utilizzata un'organizzazione registrata valida nel file delle proprietà, questo metodo pubblica sempre l'evento in HTTPS, che è HTTP su SSL, in modo che tutte le comunicazioni siano protette.

Il protocollo HTTP fornisce la distribuzione 'at most once', che è simile al livello di QOS (quality of service) 'at most once' del protocollo MQTT. Quando utilizzi la distribuzione 'at most once' per pubblicare gli eventi, l'applicazione deve implementare la logica del nuovo tentativo quando si verifica un errore.

[HttpDeviceEventPublish]: https://github.com/ibm-messaging/iot-device-samples/blob/master/java/device-samples/src/main/java/com/ibm/iotf/sample/client/device/HttpDeviceEventPublish.java

## Gestione dei comandi
{: #handling_commands}

Quando il client del dispositivo si connette, effettua automaticamente la sottoscrizione a qualsiasi comando per questo dispositivo. Per elaborare comandi specifici è necessario registrare un metodo di callback del comando. I messaggi vengono restituiti come un'istanza della classe comando, che dispone delle seguenti proprietà: 

| Proprietà     |Tipo di dati     | Descrizione|
|----------------|----------------|
|`payload` |java.lang.String| I dati per il payload del messaggio.|
|`format`  |java.lang.String| Il formato può essere qualsiasi stringa, ad esempio JSON.|
|`command`   |java.lang.String|Identifica il comando.|
|`timestamp`   |org.joda.time.DateTime|La data e l'ora dell'evento. |


``` sourceCode
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

Per un elenco di dispositivi e di esempi di gestione del dispositivo sviluppati utilizzando la libreria Java Client {{site.data.keyword.iot_short_notm}}, consulta il [repository GitHub](https://github.com/ibm-messaging/iot-device-samples/tree/master/java).
