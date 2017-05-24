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


# ﻿C# per gli sviluppatori dell'applicazionee
{: #c_sharp}


Puoi utilizzare C# per creare e personalizzare le applicazioni che interagiscono con la tua organizzazione su {{site.data.keyword.iot_full}}. Utilizza le informazioni e gli esempi forniti per iniziare a sviluppare le tue applicazioni utilizzando C#.
{:shortdesc}

## Scaricare le risorse e il client C#
{: #csharp_client_download}

Per accedere agli esempi e alle librerie client C# per {{site.data.keyword.iot_short_notm}}, vai al repository [iot-csharp ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-watson-iot/iot-csharp){: new_window} in GitHub e completa le istruzioni di installazione.


## Constructor
{: #constructor}

Il constructor crea l'istanza client e accetta gli argomenti che contengono le seguenti definizioni:

|Definizione |Descrizione |
|:---|:---|
|`orgId`   |Il tuo ID dell'organizzazione.|
|`appId`   |L'ID univoco di un'applicazione nella tua organizzazione.|
|`auth-key`   |Una chiave API per la connessione sicura alla tua applicazione su Watson IoT Platform|
|`auth-token`   |Un token chiave API per la connessione sicura alla tua applicazione su Watson IoT Platform.|

Se `appId` è l'unico argomento fornito, il client si collega al servizio Quickstart di {{site.data.keyword.iot_short_notm}} come un dispositivo non registrato. L'elenco degli argomenti definisce come il client si collega al modulo {{site.data.keyword.iot_short_notm}}.

```
ApplicationClient applicationClient = new ApplicationClient(orgId, appId, apiKey, authToken);  
applicationClient.connect();
```


## Sottoscrizione agli eventi del dispositivo
{: #subscribe_device_events}

I dispositivi utilizzano gli eventi per pubblicare i dati all'istanza {{site.data.keyword.iot_short_notm}}. Il dispositivo controlla il contenuto dell'evento e assegna un nome ad ogni evento che invia.

Quando viene ricevuto un evento dall'istanza {{site.data.keyword.iot_short_notm}}, le credenziali dell'evento ricevuto identificano il dispositivo di invio, il che significa che un dispositivo non può impersonare un altro dispositivo.

Per impostazione predefinita, le applicazioni si sottoscrivono a tutti gli eventi da tutti i dispositivi collegati. Utilizza i parametri di tipo dispositivo, ID dispositivo e formato del messaggio per controllare l'ambito della sottoscrizione. I seguenti esempi di codice mostrano come è possibile definire l'ambito di una sottoscrizione utilizzando questi parametri:

### Sottoscrizione a tutti gli eventi provenienti da tutti i dispositivi

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents();
```

### Sottoscrizione a tutti gli eventi provenienti da tutti i dispositivi di un tipo specifico

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType);
```

### Sottoscrizione di un evento specifico da tutti i dispositivi

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(evt);
```

###  Sottoscrizione di un evento specifico da due o più dispositivi differenti:

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt);
```

### Sottoscrizione a tutti gli eventi che vengono pubblicati in formato JSON

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt, "json", 0);
```

**Nota**: un'istanza del singolo client può supportare più sottoscrizioni.

### Gestione degli eventi dai dispositivi

Per elaborare gli eventi ricevuti dalle tue sottoscrizioni, registra un metodo di callback dell'evento come mostrato nel seguente esempio:

```
public static void processEvent(String eventName, string eventFormat, string eventData) {
// Fai qualcosa
}
applicationClient.connect();
applicationClient.eventCallback += processEvent;
applicationClient.subscribeToDeviceEvents();
```
La seguente tabella descrive i parametri del metodo di callback dell'evento:

|Parametro|Tipo di dati|Descrizione|
|:---|:---|
|`eventName`|Stringa|Identifica l'evento. |
|`eventFormat`|Stringa| Il formato può essere qualsiasi stringa, ad esempio JSON.|
|`eventData`|Dizionario| I dati per il payload del messaggio. La lunghezza massima è di 131072 byte.|


## Sottoscrizione agli stati del dispositivo
{: #subscribe_device_status}

Per impostazione predefinita, la richiesta viene impostata per ricevere gli aggiornamenti dello stato da tutti i dispositivi collegati. Utilizza i parametri di tipo dispositivo e ID dispositivo per controllare l'ambito della sottoscrizione. I seguenti esempi di codice mostrano come è possibile definire l'ambito di una sottoscrizione utilizzando questi parametri:

### Sottoscrizione agli aggiornamenti dello stato per tutti i dispositivi

```
applicationClient.connect();
applicationClient.subscribeToDeviceStatus += processDeviceStatus;
applicationClient.subscribeToDeviceStatus();
```

### Sottoscrizione agli aggiornamenti dello stato per due dispositivi differenti

```
applicationClient.connect();
applicationClient.subscribeToDeviceStatus += processDeviceStatus;
applicationClient.subscribeToDeviceStatus(deviceType, deviceId);
```

**Nota**: un'istanza del singolo client può supportare più sottoscrizioni.

### Gestione degli stati dai dispositivi

Per elaborare gli aggiornamenti dello stato ricevuti dalle tue sottoscrizioni, registra un metodo di callback dell'evento come mostrato nel seguente esempio:

```
public static void processDeviceStatus(String deviceType, string deviceId, string data)
        {
           //
        }
applicationClient.connect();
applicationClient.appStatusCallback += processAppStatus;
applicationClient.subscribeToApplicationStatus();
```

## Pubblicazione degli eventi dai dispositivi
{: #publish_events_devices}

Le applicazioni possono pubblicare gli eventi come se fossero originati da un dispositivo.

```
applicationClient.connect();
applicationClient.publishEvent(deviceType, deviceId, evt, data, 0);

```

La seguente tabella descrive i parametri specificati nel metodo `publishEvent()`:

|Parametro|Tipo di dati|Descrizione|
|:---|:---|
|`deviceType`|Stringa| Il tipo dispositivo. Generalmente, il deviceType è un raggruppamento di dispositivi che esegue un'attività specifica, ad esempio "weatherballoon".|
|`deviceId`|Stringa| L'ID del dispositivo. Generalmente, per determinato tipo dispositivo, il deviceId è un identificativo univoco di tale dispositivo, ad esempio un numero seriale o un indirizzo MAC.|
|`evt`|Stringa| Il nome dell'evento.|
|`format`|Stringa| Il formato può essere qualsiasi stringa, ad esempio JSON.|
|`data`|Dizionario| I dati per il payload del messaggio. La lunghezza massima è di 131072 byte.|
|`QoS`|Numero intero| QOS (quality of service). I valori validi sono `0`, `1`, `2`. |


## Pubblicazione dei comandi ai dispositivi
{: #publish_commands_devices}

Le applicazioni possono pubblicare i comandi sui dispositivi connessi.

```
applicationClient.connect();
applicationClient.publishCommand(deviceType, deviceId, "testcmd", "json", data, 0);
```
La seguente tabella descrive i parametri specificati nel metodo `publishCommand()`:

|Parametro|Tipo di dati|Descrizione|
|:---|:---|
|`deviceType`|Stringa| Il tipo dispositivo. Generalmente, il deviceType è un raggruppamento di dispositivi che esegue un'attività specifica, ad esempio "weatherballoon".|
|`deviceId`|Stringa| L'ID del dispositivo. Generalmente, per determinato di tipo dispositivo, il deviceId è un identificativo univoco di tale dispositivo, ad esempio un numero seriale o un indirizzo MAC.|
|`command`|Stringa| Il nome del comando.|
|`format`|Stringa| Il formato può essere qualsiasi stringa, ad esempio JSON.|
|`data`|Dizionario| I dati per il payload del messaggio. La lunghezza massima è di 131072 byte.|
|`QoS`|Numero intero| QOS (quality of service). I valori validi sono `0`, `1`, `2`. |
