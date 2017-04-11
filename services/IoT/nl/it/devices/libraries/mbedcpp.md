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


# mBed C++ per gli sviluppatori dei dispositivi
{: #mbedcpp}

Utilizza la libreria client [mBed C++ ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/){: new_window} per collegare facilmente i dispositivi [mBed ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://www.mbed.com/en/){: new_window}, come [LPC1768](https://developer.mbed.org/platforms/mbed-LPC1768/) o [FRDM-K64F ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://developer.mbed.org/platforms/FRDM-K64F/){: new_window}, al servizio {{site.data.keyword.iot_full}}.
{:shortdesc}

Per ulteriori informazioni, consulta [ibmiotf ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/){: new_window} in [developer.mbed.org ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://developer.mbed.org/){: new_window}.

Anche se la libreria utilizza C++, ancora evita le allocazioni di memoria dinamica e l'utilizzo delle funzioni STL, perché i dispositivi mBed alcune volte hanno dei modelli di memoria peculiari che portano delle difficoltà. In ogni caso, la libreria ti consente di rendere l'utilizzo della memoria il più prevedibile possibile.

## Dipendenze
{: #dependencies}

|Dipendenza |Descrizione|
|:---|:---|
|[Eclipse Paho MQTT library ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://developer.mbed.org/teams/mqtt/code/MQTT/){: new_window}|Fornisce un libreria client MQTT per i dispositivi mBed. Per ulteriori informazioni, consulta [Embedded MQTT C/C++ client libraries ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](http://www.eclipse.org/paho/clients/c/embedded/){: new_window}|
|[EthernetInterface library ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://developer.mbed.org/users/mbed_official/code/EthernetInterface/){: new_window}|Una libreria mBed IP su Ethernet.|

## Come utilizzare la libreria
{: #library_use}

Utilizza [mBed compiler ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://developer.mbed.org/compiler/){: new_window} per creare le tue applicazioni quando utilizzi la libreria client C++ IBMIoTF. mBed compiler fornisce un'IDE C/C++ online leggera configurata per la scrittura, la compilazione e lo scaricamento di programmi da eseguire sul tuo minicontroller mBed.

**Nota:** non devi installare o configurare nulla per l'esecuzione con mBed.

er informazioni su come collegare un microcontroller ARM mBed NXP LPC 1768 {{site.data.keyword.iot_short_notm}}, consulta la ricetta [mBed C++ client library for IBM Watson IoT Platform ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/recipes/tutorials/mbed-c-client-library-for-ibm-iot-foundation/){: new_window}.

## Constructor
{: #constructor}

Il constructor crea l'istanza client e accetta i seguenti parametri:

|Parametro |Descrizione |
|:---|:---|
|`org` |Il tuo ID dell'organizzazione. Questo valore è obbligatorio. Se stai utilizzando un flusso Quickstart, specifica `quickstart`.|
|`type`   |Il tipo del tuo dispositivo. Questo campo è obbligatorio.|
|`id`   |L'ID del tuo dispositivo. Questo campo è obbligatorio.|
|`auth-method`   |Il metodo di autenticazione, che è un campo facoltativo necessario solo per un flusso registrato. L'unico valore al momento supportato è `token`.|
|`auth-token`   |Un token di autenticazione per la connessione sicura al tuo dispositivo su Watson IoT Platform. Questo è un campo facoltativo necessario solo per un flusso registrato.|

Questi parametri creano le definizioni utilizzate per interagire con il servizio {{site.data.keyword.iot_short_notm}}.

Il seguente codice di esempio descrive come un'istanza DeviceClient può interagire con il servizio Quickstart {{site.data.keyword.iot_short_notm}}:

```
  #include "DeviceClient.h"
  ....
  ....

  // Imposta i parametri di connessione {{site.data.keyword.iot_short_notm}}
  char organization[11] = "quickstart";     // Per una connessione registrata sostituisci con la tua organizzazione
  char deviceType[8] = "LPC1768";           // Per una connessione registrata sostituisci con il tuo tipo di dispositivo
  char deviceId[3] = "01";                  // Per una connessione registrata sostituisci con il tuo ID del dispositivo

  // Crea DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId);

  // Ottieni il DeviceID(MAC Address) se sei nella modalità quickstart e l'ID del dispositivo non è specificato
  if((strcmp(organization, QUICKSTART) == 0) && (strcmp("", deviceId) == 0))
  {
  	char tmpBuf[50];
  	client.getDeviceId(tmpBuf, sizeof(tmpBuf));
  }
  ....
```

Come nell'esempio di codice precedente, se l'ID del dispositivo non viene specificato, DeviceClient utilizza l'indirizzo MAC del dispositivo come ID del dispositivo per collegarsi a {{site.data.keyword.iot_short_notm}}. Il codice del dispositivo può utilizzare il metodo `getDeviceId()` per richiamare l'ID del dispositivo dall'istanza DeviceClient.

Il seguente blocco di codice mostra come creare un'istanza DeviceClient per interagire con l'organizzazione registrata {{site.data.keyword.iot_short_notm}}.

```
  #include "DeviceClient.h"
  ....
  ....

  // Imposta i parametri di connessione {{site.data.keyword.iot_short_notm}}
  char organization[11] = "hrcl78";
  char deviceType[8] = "LPC1768";
  char deviceId[3] = "LPC176801";
  char method[6] = "token";
  char token[9] = "password";

  // Crea DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId, method, token);
  ....
```

## Connessione a {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

Il dispositivo può collegarsi a {{site.data.keyword.iot_short_notm}} richiamando la funzione di collegamento nell'istanza DeviceClient.

```
  #include "DeviceClient.h"
  ....
  ....

  // Crea DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId, method, token);

  bool status = client.connect();

```
Dopo che la connessione ha avuto esito positivo, il dispositivo può pubblicare gli eventi in {{site.data.keyword.iot_short_notm}} e può elencare i comandi.

Inoltre, il dispositivo può eseguire la query dello stato della connessione utilizzando il metodo `isConnected()`, come mostrato nel seguente esempio:

```
  #include "DeviceClient.h"
  ....
  ....

  client.isConnected();

```


## Pubblicazione eventi
{: #publishing_events}

Gli eventi sono meccanismi con cui i dispositivi pubblicano i dati in {{site.data.keyword.iot_short_notm}}. Il dispositivo controlla il contenuto dell'evento e assegna un nome ad ogni evento che invia.

Quando viene ricevuto un evento dall'istanza {{site.data.keyword.iot_short_notm}}, le credenziali dell'evento ricevuto identificano il dispositivo di invio, il che significa che un dispositivo non può impersonare un altro dispositivo.

Gli eventi possono essere pubblicati in uno dei tre [livelli di QoS (quality of service)](../../reference/mqtt/index.html#qos-levels), definiti dal protocollo MQTT. Per impostazione predefinita, gli eventi vengono pubblicati al livello QoS 0.

### Pubblica l'evento utilizzando il QOS (quality of service) predefinito

L'esempio seguente mostra come pubblicare i seguenti punti dati in {{site.data.keyword.iot_short_notm}} nel formato JSON:

- LPC1768, come assi x, y e z
- Posizione Joystick
- Lettura temperatura corrente

```
	boolean status = client.connect();

	// Crea un buffer per ospitare l'evento
	char buf[250];

	// Crea un messaggio dell'evento con i punti dati desiderati nel formato JSON
	sprintf(buf,
            "{\"d\":{\"myName\":\"IoT mbed\",\"accelX\":%0.4f,\"accelY\":%0.4f,\"accelZ\":%0.4f,
            \"temp\":%0.4f,\"joystick\":\"%s\",\"potentiometer1\":%0.4f,\"potentiometer2\":%0.4f}}",
            MMA.x(), MMA.y(), MMA.z(), sensor.temp(), joystickPos, ain1.read(), ain2.read());

        status = client.publishEvent("blink", buf);
	....
```
Per l'esempio completo, consulta [ IBMIoTClientLibrarySample ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/file/e58533b6bc6b/src/Main.cpp){: new_window}.

### Aumento del livello QoS per un evento

Puoi aumentare i [livelli QoS](../../reference/mqtt/index.html#qos-levels) per gli eventi che sono stati pubblicati. Gli eventi con un livello QoS maggiore di `0` possono impiegare più tempo per la pubblicazione, perché sono incluse ulteriori informazioni di ricezione della conferma.

**Nota:** la modalità del flusso Quickstart supporta solo QoS 0.

```
	#include "MQTTClient.h"

	boolean status = client.connect();

	// Crea un buffer per ospitare l'evento
	char buf[250];

	// Crea un messaggio dell'evento con i punti dati desiderati nel formato JSON
	sprintf(buf,
            "{\"d\":{\"myName\":\"IoT mbed\",\"accelX\":%0.4f,\"accelY\":%0.4f,\"accelZ\":%0.4f,
            \"temp\":%0.4f,\"joystick\":\"%s\",\"potentiometer1\":%0.4f,\"potentiometer2\":%0.4f}}",
            MMA.x(), MMA.y(), MMA.z(), sensor.temp(), joystickPos, ain1.read(), ain2.read());

        status = client.publishEvent("blink", buf, MQTT::QOS2);
	....
```

### Gestione dell'errore di perdita della connessione durante la pubblicazione dell'evento


Quando il metodo `publishEvent()` restituisce il valore false, puoi controllare lo stato della connessione e richiamare `reConnect()` se la connessione viene persa.

```
	#include "MQTTClient.h"

	status = client.publishEvent("blink", buf, MQTT::QOS2);

	if(status == false) {
	    // Controlla se la connessione è stata persa e ritenta
	    while(!client.isConnected())
	    {
	        client.reConnect();
	        wait(5.0);
	    }
	}
	....
```
La libreria non archivia gli eventi pubblicati durante lo stato non connesso, per cui il dispositivo deve nuovamente richiamare il metodo `publishEvent()` per inviare questi eventi dopo che è stata ristabilita la connessione.


## Gestione dei comandi
{: #handling_commands}

Quando il client del dispositivo si connette, effettua automaticamente la sottoscrizione a qualsiasi comando per questo dispositivo. Per elaborare comandi specifici è necessario registrare un metodo di callback del comando.
I messaggi vengono restituiti come un'istanza della classe comando, che dispone delle seguenti proprietà:

|Proprietà |Descrizione|
|:---|:---|
|`command` | Il nome del comando che è stato richiamato.|  
|`format`  |Il formato dell'evento. Il formato può essere qualsiasi stringa, ad esempio JSON. |
|`payload`  |I dati per il payload del comando. La lunghezza massima è di 131072 byte. |


Il seguente codice definisce una funzione di callback di comando di esempio che elabora il comando dell'intervallo di intermittenza LED dall'applicazione e imposta la gestione della funzione sull'istanza DeviceClient in modo che il metodo callback sia in esecuzione se il dispositivo riceve il comando blink.

```
    #include "DeviceClient.h"
    #include "Command.h"

    // Elabora il comando e imposta l'intervallo di intermittenza LED
    void processCommand(IoTF::Command &cmd)
    {
        if (strcmp(cmd.getCommand(), "blink") == 0)
    	{
    	    char *payload = cmd.getPayload();
    	    char* pos = strchr(payload, '}');
    	    if (pos != NULL) {
    	        *pos = '\0';
    	        char* ratepos = strstr(payload, "rate");
    	        if(ratepos == NULL)
    	            return;
    	        if ((pos = strchr(ratepos, ':')) != NULL)
    	        {
    	            int blink_rate = atoi(pos + 1);
    	            blink_interval = (blink_rate <= 0) ? 0 : (blink_rate > 50 ? 1 : 50/blink_rate);
    	        }
    	    }
    	} else {
            WARN("Unsupported command: %s\n", cmd.getCommand());
        }
    }

    client.setCommandCallback(processCommand);

    client.yield(1000);  // consente al client MQTT di ricevere i messaggi
    ....
```
Per l'esempio completo, consulta [ IBMIoTClientLibrarySample ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/file/e58533b6bc6b/src/Main.cpp){: new_window}.

**Nota:** la funzione `client.yield()` deve essere richiamata periodicamente per ricevere i comandi.
La funzione `client.yield()` abilita il dispositivo a ricevere i comandi da Watson IoT Platform e a mantenere la connessione attiva. Se la funzione `client.yield()` non è richiamata nell'intervallo di tempo specificato nell'intervallo keepAlive, tutti i comandi inviati dalla piattaforma non saranno ricevuti dal dispositivo. Il valore assegnato alla funzione `client.yield()` specifica la durata (in millisecondi) in cui i dati possono essere letti dal socket prima che il controllo sia restituito all'applicazione.

## Disconnessione del client
{: #disconnect_client}

Per scollegare il client e rilasciare le connessioni, esegui il seguente frammento di codice:

```
	...
	client.disconnect();
	....
```
## Esempi
{: #samples}

[IBMIoTClientLibrarySample ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/){: new_window} è un codice di esempio che mostra come utilizzare la libreria client {{site.data.keyword.iot_short_notm}} per collegare i dispositivi mbed LPC1768 o FRDM-K64F all'istanza del servizio.
