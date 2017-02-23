---

copyright:
years: 2016, 2017
lastupdated: "2017-01-17"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Utilizzo delle interfacce per associare i dati del dispositivo (Beta)
{: #im_index}

Utilizza la funzione di associazione dell'interfaccia di {{site.data.keyword.iot_full}} per organizzare e integrare i dati del dispositivo in entrata e in uscita.
{:shortdesc}

**Importante:** la funzione di associazione dell'interfaccia è disponibile al momento solo come una funzione beta. Prima della release finale, gli aggiornamenti beta dovranno probabilmente includere le modifiche che non sono compatibili con la versione corrente. È fortemente raccomandato che le funzioni beta non siano utilizzate nelle applicazioni di produzione fino alla release finale. Per ricevere ulteriori informazioni e fornire il feedback per questa beta, [registrati al programma beta di IBM](https://www.ibm.com/software/support/trial/cst/forms/nomination.wss?id=7050) e lasciaci sapere cosa ne pensi.

## Panoramica
{: #overview}

Puoi utilizzare la funzione di associazione dell'interfaccia per sviluppare le interfacce per le tue applicazioni. Potresti avere diversi tipi, marche e modelli del dispositivo o del sensore che desideri collegare {{site.data.keyword.iot_short_notm}} e tali dispositivi potrebbero pubblicare i dati in formati differenti. Utilizza la funzione di associazione dell'interfaccia per normalizzare i dati in entrata e per semplificare le tue applicazioni separandole dalle complessità su come i tuoi dispositivi specifici si collegano.

Ad esempio, potresti avere due sensori per la temperatura. Un sensore misura la temperatura in gradi Celsius e uno in gradi Fahrenheit.

![Associazione tra i dispositivi del sensore della temperatura e un applicazione su {{site.data.keyword.iot_short_notm}}.](images/Information "Associazione tra i dispositivi del sensore della temperatura e un applicazione su {{site.data.keyword.iot_short_notm}}")

Il sensore della temperatura 1 pubblica una lettura della temperatura di `{ "t" : 34.5 }` su {{site.data.keyword.iot_short_notm}}. Questa è una lettura della temperatura con un valore in Celsius. Il sensore della temperatura 2 pubblica una lettura della temperatura di `{ "temp" : 72.55 }` su {{site.data.keyword.iot_short_notm}}. Questo è un tipo differente di sensore della temperatura con una lettura con un valore in Fahrenheit. Le letture della temperatura sono pubblicate come eventi separati in {{site.data.keyword.iot_short_notm}}.

Utilizzando la funzione di associazione dell'interfaccia, puoi normalizzare queste letture in un formato congruente per l'elaborazione. Non hai bisogno di scrivere la tua applicazione in modo che comprenda o converta scale di temperatura diverse. L'applicazione riceve una sola vista normalizzata e può collegarsi a **temperature** invece di collegarsi a **t** e **temp**.

## Flusso di dati tra i dispositivi e le applicazioni
{: #mapping}

Il seguente diagramma del flusso mostra come vengono utilizzate risorse differenti nella funzione di associazione dell'interfaccia:

![Il flusso tra un dispositivo e un'applicazione su {{site.data.keyword.iot_short_notm}}.](images/Information "Il flusso tra un dispositivo e un'applicazione su {{site.data.keyword.iot_short_notm}}")

Il seguente diagramma illustra come gli schemi sono utilizzati in questo flusso:

![Il flusso tra un dispositivo e un'applicazione su {{site.data.keyword.iot_short_notm}}.](images/Information "Il flusso tra un dispositivo e un'applicazione su {{site.data.keyword.iot_short_notm}}")

Gli schemi JSON sono utilizzati per definire e convalidare il formato degli eventi in entrata e lo [stato del dispositivo](#key_concepts). Per ulteriori informazioni su questi schemi, consulta [Schemi](#resources).

## Concetti chiave
{: #key_concepts}

La funzione di associazione dell'interfaccia estende il concetto corrente di [tipo di dispositivo](#resources) aggiungendo una risorsa dell'interfaccia fisica e una risorsa dell'interfaccia dell'applicazione per un controllo più accurato dei dati trasmessi tramite {{site.data.keyword.iot_short_notm}}.

Il seguente diagramma illustra l'associazione logica tra i dispositivi e le applicazioni su {{site.data.keyword.iot_short_notm}} utilizzando le [risorse](#resources):

![Associazione logica tra un dispositivo e un'applicazione su {{site.data.keyword.iot_short_notm}}.](images/im_mapping.svg "Associazione logica tra un dispositivo e un'applicazione su {{site.data.keyword.iot_short_notm}}")

L'associazione dell'interfaccia fa riferimento al concetto di stato del dispositivo. Lo stato del dispositivo è composto da una serie di proprietà definite dall'interfaccia dell'applicazione. Il valori più recenti di queste proprietà sono archiviati in {{site.data.keyword.iot_short_notm}} e resi disponibili all'applicazione su richiesta utilizzando un'API HTTP.

Per elaborare i dati dagli eventi in entrata e associare le proprietà nell'evento in entrata alle proprietà nell'interfaccia dell'applicazione, devono essere configurate le seguenti informazioni:

- La struttura di uno o più eventi in entrata. Lo schema dell'evento definisce queste informazioni.  Ogni schema dell'evento definisce la struttura di un evento in entrata e viene associato con un tipo di evento. L'interfaccia fisica raggruppa uno o più tipi di evento.

    La struttura e il formato dei dati contenuti in un evento del dispositivo in entrata sono definiti da un file dello schema evento che è nel formato schema JSON. Puoi caricare il file dello schema evento in {{site.data.keyword.iot_short_notm}} utilizzando un metodo POST per creare una risorsa dello schema denominata. Per la beta, tutti gli eventi in entrata devono essere nel formato JSON.

- La struttura dello stato del dispositivo desiderato. Lo schema dell'interfaccia dell'applicazione definisce queste informazioni. 

    Lo stato del dispositivo è una rappresentazione della struttura dei dati e i dati che la tua applicazione è configurata a ricevere come dati dal dispositivo. Il valori della proprietà che sono archiviati nello stato del dispositivo, vengono aggiornati in risposta a un evento del dispositivo in entrata. Gli ultimi valori dello stato del dispositivo vengono forniti all'applicazione su richiesta utilizzando un'API HTTP.

- Le informazioni su come associare gli eventi in entrata allo stato del dispositivo preferito. Le associazioni definiscono queste informazioni.

    Per associare i dati contenuti nelle proprietà di un evento in entrata alle proprietà appropriate nell'interfaccia dell'applicazione, devi creare un'associazione. L'associazione descrive come aggiornare le proprietà definite da un'interfaccia dell'applicazione specifica in risposta a un evento in entrata da un dispositivo.


## Risorse
{: #resources}

Puoi gestire le risorse illustrate nei precedenti diagrammi utilizzando le API REST. Per informazioni sulle API REST, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html).

Risorsa                         | Descrizione       
------------- | ------------- | -------------  
Schemi                         | Gli schemi JSON sono utilizzati per definire la struttura degli eventi in entrata pubblicati in {{site.data.keyword.iot_short_notm}} dai dispositivi e lo stato del dispositivo desiderato. Per ulteriori informazioni sullo schema JSON, consulta [Schema JSON](http://json-schema.org/). Nell'associazione dell'interfaccia, si fa riferimento a due schemi JSON - gli schemi dell'evento e gli schemi dell'interfaccia dell'applicazione. Gli schemi dell'evento sono utilizzati per definire la struttura degli eventi pubblicati in {{site.data.keyword.iot_short_notm}} da un dispositivo. Viene fatto riferimento agli schemi dell'interfaccia dell'applicazione dall'interfaccia dell'applicazione e sono utilizzati per definire la struttura dello [stato del dispositivo](#key_concepts) archiviato in {{site.data.keyword.iot_short_notm}}.
Tipo di evento                          | Devi creare un tipo di evento nella tua organizzazione in modo che {{site.data.keyword.iot_short_notm}} possa elaborare i dati contenuti in un evento specifico. Tutti i tipi di evento devono far riferimento a uno schema dell'evento. Per la beta, tutti gli eventi in entrata devono essere nel formato JSON.    
Interfaccia fisica                          | L'interfaccia fisica può essere associata con uno o più tipi di evento e definisce quali tipi di evento sono associati a un tipo di dispositivo.  
Tipo dispositivo                         | Ogni dispositivo collegato a Watson IoT Platform è associato a un tipo di dispositivo. I tipi di dispositivo sono gruppi di dispositivi che condividono le caratteristiche o i comportamenti. Nell'associazione dell'interfaccia, il tipo di evento viene esteso per includere un'interfaccia fisica per un dispositivo e un'interfaccia dell'applicazione che può essere utilizzata per richiamare lo stato del dispositivo. Un tipo di dispositivo può essere configurato con più interfacce dell'applicazione. Per ulteriori informazioni sui tipi di dispositivo, consulta la sezione "Tipi di dispositivo e identificativi" in [Modello del dispositivo](../reference/device_model.html#id_and_device_types).
Interfaccia applicazione                         | L'interfaccia dell'applicazione deve far riferimento a uno schema dell'interfaccia dell'applicazione. Nella tua interfaccia dell'applicazione, puoi definire la struttura dei dati archiviati come lo stato del dispositivo. Lo stato del dispositivo è una rappresentazione della struttura dei dati e i dati che un'applicazione è configurata a ricevere come dati dal dispositivo. Deve essere associata almeno un'interfaccia con un tipo di dispositivo prima che possa essere definita un'associazione.
Associazioni                         | Le associazione definiscono come le proprietà associate negli eventi in entrata vengono associate alle proprietà definite in un'interfaccia dell'applicazione specifica. Un'associazione deve specificare l'identificativo dell'interfaccia dell'applicazione a cui viene applicata e tale interfaccia dell'applicazione deve essere associata al tipo di dispositivo a cui l'associazione sta venendo aggiunta.


## Flusso di lavoro di elevato livello
{: #workflow}



### Informazioni su quest'attività

Utilizza la seguente procedura come supporto per la configurazione delle risorse di cui hai bisogno per iniziare l'associazione dei tuo i dati del dispositivo utilizzando le interfacce.

Per i dettagli sull'API, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html).
Per ulteriori informazioni dettagliate su ognuno di questi passi, consulta lo [Scenario di esempio](#scenario) o utilizza i link per andare direttamente a un passo specifico nello scenario di esempio.

### Configura il tuo ambiente per iniziare ad utilizzare le interfacce per associare i dati del dispositivo.

1.  Se necessario, aggiungi un tipo di dispositivo e un dispositivo.

  1. Crea un tipo di dispositivo utilizzando il metodo POST dell'API REST utilizzando il seguente URI:
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types
      ```
  2.  Aggiungi un dispositivo se necessario.  
Per ulteriori informazioni sull'aggiunta di un tipo di dispositivo e un dispositivo, consulta [Connessione dispositivi](../iotplatform_task.html#devices)

2. Crea un'interfaccia fisica

  1. [Crea un file dello schema evento](#step1). Il file dello schema evento è un file .JSON locale che definisce la struttura e il formato di un evento in entrata.

  2. [Crea una risorsa dello schema evento per il tuo tipo di evento](#step2) utilizzando il metodo POST dell'API REST utilizzando il seguente URI:
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/schemas
      ```  

  3. [Crea un tipo di evento che fa riferimento allo schema evento](#step3) utilizzando il metodo POST dell'API REST utilizzando il seguente URI:
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/event/types
      ```
      Aggiungi il tipo di evento al tuo schema evento utilizzando l'identificativo dello schema restituito dal metodo POST utilizzato per creare la risorsa dello schema evento.

  4. [Crea un'interfaccia fisica](#step7) utilizzando il metodo POST dell'API REST utilizzando il seguente URI:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces
        ```

   5. [Aggiungi il tipo di evento all'interfaccia fisica](#step8) utilizzando il metodo POST dell'API REST utilizzando il seguente URI:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/{physicalInterfaceId}/events
        ```

       Aggiungi il tipo di evento alla tua interfaccia fisica utilizzando il *eventId* dall'argomento e dal tipo di evento *eventTypeId* restituito dal metodo POST utilizzato per creare il tipo di evento.       

3. Aggiungi la tua interfaccia fisica al tuo tipo di dispositivo       

      [Aggiorna il tipo di dispositivo per il collegamento dell'interfaccia fisica](#step9) utilizzando il metodo PUT dell'API REST utilizzando il seguente URI:
     ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}
     ```

4. Crea un'interfaccia dell'applicazione

  1. [Crea un file dello schema dell'interfaccia dell'applicazione](#step4). Un file dello schema dell'interfaccia dell'applicazione è un file .JSON locale che definisce che definisce lo stato del dispositivo.

  2. [Crea una risorsa dello schema dell'interfaccia dell'applicazione](#step5) utilizzando il metodo POST dell'API REST utilizzando il seguente URI:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/schemas
        ```     

  3. [Crea un'interfaccia dell'applicazione che fa riferimento a uno schema dell'interfaccia dell'applicazione](#step6) utilizzando il metodo POST dell'API REST utilizzando il seguente URI:
         ```
         https://**orgId**.internetofthings.ibmcloud.com/api/v0002/applicationinterfaces
         ```  

        L'interfaccia dell'applicazione fa riferimento allo schema dell'interfaccia dell'applicazione utilizzando l'identificativo dello schema restituito dal metodo POST utilizzato per creare la risorsa dello schema dell'interfaccia dell'applicazione.

  4. [Aggiungi l'interfaccia dell'applicazione a un tipo di dispositivo](#step10) utilizzando il metodo POST dell'API REST utilizzando il seguente URI:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/types/{typeId}/applicationinterfaces
        ```

        Aggiungi la tua interfaccia dell'applicazione al tuo tipo di dispositivo utilizzando la risposta al metodo POST utilizzato per creare l'interfaccia dell'applicazione.

5. Definisci le associazione al tipo di dispositivo

  [Definisci le associazioni per associare le proprietà nell'evento in entrata alle proprietà nell'interfaccia dell'applicazione](#step11) utilizzando il metodo POST dell'API REST utilizzando il seguente URI:       
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}/mappings/{applicationInterfaceId}
      ```

6. Distribuisci la configurazione associata al tuo tipo di dispositivo

  [Distribuisci la configurazione](#step15) a {{site.data.keyword.iot_short_notm}} utilizzando il metodo PATCH dell'API REST utilizzando il seguente URI:
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}
      ```

7. Verifica che gli eventi del dispositivo associati siano pubblicati nell'interfaccia dell'applicazione

  1. [Pubblica un evento del dispositivo in entrata](#step12).

  2. [Controlla che lo stato del dispositivo sia stato modificato](#step13) utilizzando il metodo GET dell'API REST utilizzando il seguente URI:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
        ```

## Scenario di esempio
{: #scenario}

Utilizza le seguenti informazioni per creare uno scenario nel quale due sensori della temperatura pubblicano gli eventi in {{site.data.keyword.iot_short_notm}}. Un sensore misura la temperatura in gradi Celsius. L'altro sensore misura la temperatura in gradi Fahrenheit. Queste letture vengono associate a una sola lettura della temperatura che è in gradi Celsius. Quando viene pubblicata una nuova lettura della temperatura da questi dispositivi, il valore della proprietà associata con lo stato del dispositivo viene modificato.

### Prerequisiti

Devi disporre di un'istanza dell'organizzazione {{site.data.keyword.iot_short_notm}} e un token o una chiave API per tale organizzazione. Per ulteriori informazioni sui token e sulle chiavi API, consulta [API REST HTTP per le applicazioni](../applications/api.html#authentication).

### Informazioni su questo scenario

In questo scenario, vengono configurati due dispositivi.

Un dispositivo viene denominato *TemperatureSensor1*. Questo dispositivo pubblica gli eventi sulla temperatura misurati in gradi Celsius. L'evento sulla temperatura viene pubblicato nell'argomento `iot-2/evt/tevt/fmt/json` e ha il seguente payload di esempio:
```
{
  "t" : 34.5
}
```

**Nota:** l'identificativo dell'evento è *tevt*. Questo identificativo è obbligatorio quando aggiungi un evento sulla temperatura di questo tipo all'interfaccia fisica e quando definisci le associazioni per associare una proprietà associata a un evento in entrata di questo tipo a una proprietà nella tua interfaccia dell'applicazione. In questo scenario, la proprietà definita nell'interfaccia dell'applicazione viene denominata **temperature**.

L'altro dispositivo viene denominato *TemperatureSensor2*. Questo dispositivo pubblica gli eventi sulla temperatura misurati in gradi Fahrenheit. L'evento sulla temperatura viene pubblicato nell'argomento `iot-2/evt/tempevt/fmt/json` e ha il seguente payload di esempio:
```
{
  "temp" : 72.55
}
```

**Nota:** l'identificativo dell'evento è *tempevt*. Questo identificativo è obbligatorio quando aggiungi un evento sulla temperatura di questo tipo all'interfaccia fisica e quando definisci le associazioni per associare una proprietà associata a un evento in entrata di questo tipo a una proprietà nella tua interfaccia dell'applicazione. In questo scenario, la proprietà definita nell'interfaccia dell'applicazione viene denominata **temperature**.

Viene anche configurata un'interfaccia dell'applicazione. Questa interfaccia dell'applicazione rappresenta lo stato per i dispositivi di questo tipo nella seguente struttura:
```
{
  "temperature" : <current temperature value in Celsius>
  }
```
Questa configurazione indica che puoi configurare la tua applicazione per elaborare il valore associato a **temperature**, piuttosto che configurare la tua applicazione per elaborare il valore associato a **t** e per elaborare il valore associato a **temp** dopo aver convertito questo valore in gradi Celsius.

## Passi

Utilizza le seguenti informazioni per configurare lo scenario di esempio utilizzando le interfacce.

### Se necessario, aggiungi un tipo di dispositivo e un dispositivo.
{: #step14}

In questo scenario, vengono prese in considerazione due tipi di dispositivo e due istanze del dispositivo. L'istanza del dispositivo *TemperatureSensor1* è associata con il tipo di dispositivo *EnvSensor1*. L'istanza del dispositivo *TemperatureSensor2* è associata con il tipo di dispositivo *EnvSensor2*. 

Per informazioni sull'utilizzo delle API REST per aggiungere un tipo di dispositivo, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Types).

### Crea un file dello schema evento 
{: #step1}

Per questo scenario, crea due file dello schema evento per definire la struttura di ogni evento sulla temperatura in entrata.

Il seguente esempio mostra come creare un file dello schema denominato *tEventSchema.json*. Questo file definisce la struttura di un evento in entrata da un sensore della temperatura che misura la temperatura in gradi Celsius:

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor1 tEvent Schema",
  "description" : "defines the structure of a temperature event in degrees Celsius",
  "properties" : {
    "t" : {
      "description" : "temperature in degrees Celsius",
      "type" : "number",
      "minimum" : -273.15,
      "default" : 0.0
    }
  },
  "required" : ["t"]
}
  ```

Il nome del file dello schema *tEventSchema* viene utilizzato quando creai una risorsa dello schema evento per il tuo tipo di evento.

Il seguente esempio mostra come creare un file dello schema denominato *tempEventSchema.json*. Questo file definisce la struttura di un evento in entrata da un sensore della temperatura che misura la temperatura in gradi Fahrenheit:

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor2 tempEvent Schema",
  "description" : "defines the structure of a temperature event in degrees Fahrenheit",
  "properties" : {
    "temp" : {
      "description" : "temperature in degrees Fahrenheit",
      "type" : "number",
      "minimum" : −459.67,
      "default" : 0.0
    }
  },
  "required" : ["temp"]
}
  ```
Il nome del file dello schema *tempEventSchema* viene utilizzato quando creai una risorsa dello schema evento per il tuo tipo di evento.   

### Crea una risorsa dello schema evento per il tuo tipo di evento.
{: #step2}

Per creare una risorsa dello schema evento, utilizza la seguente API:

```
POST /schemas
```
Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas).

Il seguente esempio mostra come utilizzare cURL per creare la risorsa dello schema evento *tEventSchema.json*:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: multipart/form-data' \
  --form name=tEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/tEventSchema.json'
```

Il seguente esempio mostra una risposta al metodo POST:

```
{
  "name" : "tEventSchema",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "contentType" : "application/octet-stream",
  "updated" : "2016-12-06T14:38:52Z",
  "schemaFileName" : "tEventSchema.json",
  "created" : "2016-12-06T14:38:52Z",
  "id" : "5846cd7c6522050001db0e0d",
  "refs" : {
      "content" : "/schemas/5846cd7c6522050001db0e0d/content"
  },
  "schemaType" : "json-schema",
  "updatedBy" : "a-8x7nmj-9iqt56kfil"
}
```
L'identificativo dello schema *5846cd7c6522050001db0e0d* restituito nella risposta al metodo POST è obbligatorio quando aggiungi uno schema evento al tuo tipo di evento.

Il seguente esempio mostra come utilizzare cURL per creare la risorsa dello schema evento *tempEventSchema.json*:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: multipart/form-data’ \
  --form name=tempEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/tempEventSchema.json"'
```

Il seguente esempio mostra una risposta al metodo POST:

```
{
  "schemaType" : "json-schema",
  "schemaFileName" : "tempEventSchema.json",
  "updated" : "2016-12-06T14:44:51Z",
  "name" : "tempEventSchema",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "created" : "2016-12-06T14:44:51Z",
  "id" : "5846cee36522050001db0e0e",
  "refs" : {
      "content" : "/schemas/5846cee36522050001db0e0e/content"
  },
  "contentType" : "application/octet-stream",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```
L'identificativo dello schema *5846cee36522050001db0e0e* restituito nella risposta al metodo POST è obbligatorio quando aggiungi uno schema evento al tuo tipo di evento.

### Crea un tipo di evento che fa riferimento allo schema evento
{: #step3}

Ogni tipo di evento fa riferimento allo schema evento pertinente che è stato creato nel precedente esempio utilizzando l'identificativo dello schema restituito nella risposta al metodo POST utilizzato per creare la risorsa dello schema evento.

Per creare un tipo di evento, utilizza la seguente API:

```
POST /event/types
```

Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Event_Types).



Il seguente esempio mostra come utilizzare cURL per creare un tipo di evento per un evento sulla temperatura misurato in gradi Celsius:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tEvent", "schemaId" : "5846cd7c6522050001db0e0d"}'
```

L'identificativo dello schema *5846cd7c6522050001db0e0d* vine utilizzato per aggiungere lo schema evento al tipo di evento. Questo identificativo era stato restituito nella risposta al metodo POST che era stato utilizzato per creare la risorsa dello schema evento *tEventSchema.json*

Il seguente esempio mostra una risposta al metodo POST:

```
{
  "updated" : "2016-12-06T14:53:49Z",
  "schemaId" : "5846cd7c6522050001db0e0d",
  "refs" : {
    "schema" : "/schemas/5846cd7c6522050001db0e0d"
  },
  "name" : "tEvent",
  "created" : "2016-12-06T14:53:49Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "id" : "5846d0fd6522050001db0e0f",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```

L'identificativo del tipo di evento *5846d0fd6522050001db0e0f* restituito nella risposta al metodo POST viene utilizzato per aggiungere un tipo di evento all'interfaccia fisica.

Il seguente esempio mostra come utilizzare cURL per creare un tipo di evento per un evento sulla temperatura misurato in gradi Fahrenheit:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tempEvent", "schemaId" : "5846cee36522050001db0e0e"}'
```
L'identificativo dello schema *5846cee36522050001db0e0e* vine utilizzato per aggiungere lo schema evento al tipo di evento. Questo identificativo era stato restituito nella risposta al metodo POST che era stato utilizzato per creare la risorsa dello schema evento *tempEventSchema.json*

Il seguente esempio mostra una risposta al metodo POST:

```
{
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "schemaId" : "5846cee36522050001db0e0e",
  "created" : "2016-12-06T15:00:20Z",
  "id" : "5846d2846522050001db0e10",
  "updated" : "2016-12-06T15:00:20Z",
  "name" : "tempEvent",
  "refs" : {
    "schema" : "/schemas/5846cee36522050001db0e0e"
  },
  "updatedBy" : "a-8x7nmj-9iqt56kfil"
}
```
L'identificativo del tipo di evento *5846d2846522050001db0e10* restituito nella risposta al metodo POST viene utilizzato per aggiungere un tipo di evento all'interfaccia fisica.
### Crea un'interfaccia fisica 
{: #step7}

Per creare un'interfaccia fisica, utilizza la seguente API:

```
POST /physicalinterfaces
```
Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces).

In questo scenario, abbiamo bisogno di due interfacce fisiche - una per ogni tipo di evento.

Il seguente esempio mostra come utilizzare cURL per creare la prima interfaccia fisica: 

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: application/json’ \
  --data '{"name" : "Env sensor physical interface 1"}'
```

Il seguente esempio mostra una risposta al metodo POST:

```
{
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
    "events" : "/physicalinterfaces/5847d1df6522050001db0e1a/events"
  },
  "id" : "5847d1df6522050001db0e1a",
  "name" : "Env sensor physical interface 1",
  "created" : "2016-12-07T09:09:51Z",
  "updated" : "2016-12-07T09:09:51Z",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```

L'identificativo dell'interfaccia fisica *5847d1df6522050001db0e1a* restituito nella risposta viene utilizzato nell'URL del metodo POST richiamato per aggiungere un evento sulla temperatura misurato in gradi Celsius all'interfaccia fisica.

l seguente esempio mostra come utilizzare cURL per creare la seconda interfaccia fisica: 

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: application/json’ \
  --data '{"name" : "Env sensor physical interface 2"}'
```

Il seguente esempio mostra una risposta al metodo POST:

```
{
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
    "events" : "/physicalinterfaces/5847d1df6522050001db0e1b/events"
  },
  "id" : "5847d1df6522050001db0e1b",
  "name" : "Env sensor physical interface 2",
  "created" : "2016-12-07T09:19:51Z",
  "updated" : "2016-12-07T09:19:51Z",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```

L'identificativo dell'interfaccia fisica *5847d1df6522050001db0e1b* restituito nella risposta viene utilizzato nell'URL del metodo POST richiamato per aggiungere un evento sulla temperatura misurato in gradi Fahrenheit all'interfaccia fisica.   

### Aggiungi il tipo di evento all'interfaccia fisica 
{: #step8}

Per aggiungere un tipo di evento all'interfaccia fisica, utilizza la seguente API:

```
POST /physicalinterfaces/{physicalInterfaceId}/events
```
Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces).

In questo scenario, vengono aggiunti i seguenti tipi di evento alle interfacce fisiche specificate:
- l'evento sulla temperatura Celsius *tevt* viene aggiunto all'interfaccia fisica con l'identificativo *5847d1df6522050001db0e1a* utilizzando il *eventId* dall'argomento e il *eventTypeId* dalla creazione della risorsa dello schema evento.
- l'evento sulla temperatura Fahrenheit *tempevt* viene aggiunto all'interfaccia fisica con l'identificativo *5847d1df6522050001db0e1b* utilizzando il *eventId* dall'argomento e il *eventTypeId* dalla creazione della risorsa dello schema evento.


Il seguente esempio mostra come utilizzare cURL per aggiungere l'evento sulla temperatura *tevt* all'interfaccia fisica con l'identificativo *5847d1df6522050001db0e1a* :

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1a/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : "tevt", "eventTypeId" : "5846d0fd6522050001db0e0f"}'
```

Il seguente esempio mostra una risposta al metodo POST:

```
{
  "eventTypeId" : "5846d0fd6522050001db0e0f",
  "eventId" : "tevt"
}
```

Il seguente esempio mostra come utilizzare cURL per aggiungere l'evento sulla temperatura *tempevt* all'interfaccia fisica con l'identificativo *5847d1df6522050001db0e1b* :

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1b/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : "tempevt", "eventTypeId" : "5846d2846522050001db0e10"}'
```

Il seguente esempio mostra una risposta al metodo POST:

```
{
  "eventTypeId" : "5846d2846522050001db0e10",
  "eventId" : "tempevt"
}
```

### Aggiorna il tipo di dispositivo per il collegamento dell'interfaccia fisica 
{: #step9}

Per aggiornare il tipo di dispositivo, utilizza la seguente API:

```
PUT /device/types/{typeId}
```

Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).


In questo scenario, il tipo di dispositivo *EnvSensor1* per collegarsi all'interfaccia fisica *5847d1df6522050001db0e1a* e il tipo di dispositivo *EnvSensor2* per collegarsi all'interfaccia fisica *5847d1df6522050001db0e1b*.

Il seguente esempio mostra come utilizzare cURL per aggiornare il tipo di dispositivo *EnvSensor1*:

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an environment sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1a"}’
```

Il seguente esempio mostra una risposta al metodo POST:

```
{
  "deviceInfo" : {},
  "physicalInterfaceId" : "5847d1df6522050001db0e1a",
  "updatedDateTime" : "2016-12-07T09:49:52+00:00",
  "refs" : {
    "mappings" : "/device/types/EnvSensor1/mappings",
    "applicationInterfaces" : "/device/types/EnvSensor1/applicationinterfaces",
    "physicalInterface" : "/physicalinterfaces/5847d1df6522050001db0e1a"
   },
  "id" : "EnvironmentSensor",
  "description" : "an environment sensor",
  "metadata" : {},
  "classId" : "Device",
  "createdDateTime" : "2016-12-07T09:49:52+00:00"
}
```
L'identificativo del dispositivo *EnvSensor1* è obbligatorio quando aggiungi la tua interfaccia fisica e la tua interfaccia dell'applicazione.

Il seguente esempio mostra come utilizzare cURL per aggiornare il tipo di dispositivo *EnvSensor2*:

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an env sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1b"}’
```

Il seguente esempio mostra una risposta al metodo POST:

```
{
  "deviceInfo" : {},
  "physicalInterfaceId" : "5847d1df6522050001db0e1b",
  "updatedDateTime" : "2016-12-07T09:59:52+00:00",
  "refs" : {
    "mappings" : "/device/types/EnvSensor2/mappings",
    "applicationInterfaces" : "/device/types/EnvSensor2/applicationinterfaces",
    "physicalInterface" : "/physicalinterfaces/5847d1df6522050001db0e1b"
   },
  "id" : "EnvironmentSensor",
  "description" : "an environment sensor",
  "metadata" : {},
  "classId" : "Device",
  "createdDateTime" : "2016-12-07T09:49:52+00:00"
}
```
L'identificativo del dispositivo *EnvSensor2* è obbligatorio quando aggiungi la tua interfaccia fisica e la tua interfaccia dell'applicazione.



### Crea un file dello schema dell'interfaccia dell'applicazione 
{: #step4}

Il seguente esempio mostra come creare un file dello schema dell'interfaccia dell'applicazione denominato *envSensor.json*.

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
    "type" : "object",
    "title" : "Environment Sensor Schema",
    "description" : "Schema to represent a canonical environment sensor device",
    "properties" : {
        "temperature" : {
            "description" : "temperature in degrees Celsius",
            "type" : "number",
            "minimum" : -273.15,
            "default" : 0.0
        }
    },
    "required" : ["temperature"]
}
```

### Crea una risorsa dello schema dell'interfaccia dell'applicazione 
{: #step5}

Per creare una risorsa dello schema dell'interfaccia dell'applicazione, utilizza la seguente API: 

```
POST /schemas
```
Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas).

Il seguente esempio mostra come utilizzare cURL per creare lo schema dell'interfaccia dell'applicazione: 

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: multipart/form-data' \
  --form name=temperatureEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/envSensor.json"'
```

Il seguente esempio mostra una risposta al metodo POST:

```
{
  "created" : "2016-12-06T16:51:14Z",
  "name" : "temperatureEventSchema",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "updated" : "2016-12-06T16:51:14Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "schemaType" : "json-schema",
  "contentType" : "application/octet-stream",
  "schemaFileName" : "envSensor.json",
  "refs" : {
    "content" : "/schemas/5846ec826522050001db0e11/content"
  },
  "id" : "5846ec826522050001db0e11"
}
```
Utilizza l'identificativo dello schema *5846ec826522050001db0e11* restituito nella risposta al metodo POST per aggiungere lo schema dell'interfaccia dell'applicazione all'interfaccia dell'applicazione.

### Crea un'interfaccia dell'applicazione che fa riferimento a uno schema dell'interfaccia dell'applicazione
{: #step6}

Per creare un'interfaccia dell'applicazione, utilizza la seguente API: 

```
POST /applicationinterfaces
```
Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Application_Interfaces).

In questo scenario, utilizza l'identificativo dello schema *5846ec826522050001db0e11* restituito nella precedente risposta per aggiungere lo schema dell'interfaccia dell'applicazione all'interfaccia dell'applicazione.

Il seguente esempio mostra come utilizzare cURL per creare un'interfaccia dell'applicazione: 

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/applicationinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "environment sensor interface", "schemaId" : "5846ec826522050001db0e11"}'
```

Il seguente esempio mostra una risposta al metodo POST:

```
{
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
  "schemaId" : "5846ec826522050001db0e11",
  "created" : "2016-12-06T16:53:27Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "id" : "5846ed076522050001db0e12",
  "updated" : "2016-12-06T16:53:27Z",
  "name" : "environment sensor interface"
}
```
In questo scenario, utilizza l'identificativo dell'interfaccia dell'applicazione *5846ed076522050001db0e12* restituito nella risposta al metodo POST per aggiungere l'interfaccia dell'applicazione al tuo tipo di dispositivo. Puoi anche utilizzare questo identificativo per associare un evento del dispositivo in entrata a una proprietà definita dall'interfaccia dell'applicazione.

### Aggiungi l'interfaccia dell'applicazione a un tipo di dispositivo
{: #step10}

Per aggiungere un'interfaccia dell'applicazione a un tipo di dispositivo, utilizza la seguente API:

```
POST /device/types/{typeId}/applicationinterfaces
```
Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

In questo scenario, l'interfaccia dell'applicazione viene associata al tipo di dispositivo *EnvSensor1* e al tipo di dispositivo *EnvSensor2*.

Il seguente esempio mostra come utilizzare cURL per aggiungere l'interfaccia dell'applicazione *5846ed076522050001db0e12* che fa riferimento all'identificativo dello schema dell'applicazione *5846ec826522050001db0e11* al tipo di dispositivo *EnvSensor1*:

```
curl --request POST \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/applicationinterfaces \
--header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
--header 'content-type: application/json' \
--data '{"createdBy" : "a-8x7nmj-9iqt56kfil", \
          "refs" : {
              "schema" : "/schemas/5846ec826522050001db0e11"
          },
          "schemaId" : "5846ec826522050001db0e11", "created" : "2016-12-06T16:53:27Z", \
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface"
        }'
```

Il seguente esempio mostra una risposta al metodo POST:

```
{
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
  "updated" : "2016-12-06T16:53:27Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "name" : "environment sensor interface",
  "created" : "2016-12-06T16:53:27Z",
  "id" : "5846ed076522050001db0e12",
  "schemaId" : "5846ec826522050001db0e11"
}
```

Il seguente esempio mostra come utilizzare cURL per aggiungere l'interfaccia dell'applicazione *5846ed076522050001db0e12* associata all'identificativo dello schema dell'applicazione *5846ec826522050001db0e11* al tipo di dispositivo *EnvSensor2*:

```
curl --request POST \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/applicationinterfaces \
--header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
--header 'content-type: application/json' \
--data '{"createdBy" : "a-8x7nmj-9iqt56kfil", \
          "refs" : {
              "schema" : "/schemas/5846ec826522050001db0e11"
          },
          "schemaId" : "5846ec826522050001db0e11", "created" : "2016-12-06T16:53:27Z", \
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface"
        }'
```


Il seguente esempio mostra una risposta al metodo POST:

```
{
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
  "updated" : "2016-12-06T16:53:27Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "name" : "environment sensor interface",
  "created" : "2016-12-06T16:53:27Z",
  "id" : "5846ed076522050001db0e12",
  "schemaId" : "5846ec826522050001db0e11"
}
```

### Definisci le associazioni per associare le proprietà nell'evento in entrata alle proprietà nell'interfaccia dell'applicazione 
{: #step11}

Per associare gli eventi, utilizza la seguente API:

```
POST /device/types/{typeId}/mappings
```
Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

In questo scenario, definiamo le associazioni al tipo di dispositivo *EnvSensor1* per associare la proprietà **t** nell'evento in entrata *tevt* alla proprietà **temperature** nell'interfaccia dell'applicazione. Definiamo inoltre le associazioni al tipo di dispositivo *EnvSensor2* per associare la proprietà **temp** nell'evento in entrata *tempevt* alla proprietà **temperature** nell'interfaccia dell'applicazione.

Il seguente esempio mostra come utilizzare cURL per aggiungere un'associazione al tipo di dispositivo *EnvSensor1*:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/mappings \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"applicationInterfaceId" : "5846ed076522050001db0e12","propertyMappings" : {
              "tevt" : {
                  "temperature" : "$event.t"
              }
            }
          }'
```

Specificare l'identificativo dell'interfaccia dell'applicazione *5846ed076522050001db0e12* restituito nella risposta al metodo POST utilizzato per creare l'interfaccia e il tipo di dispositivo *EnvSensor1*.

Il seguente esempio mostra una risposta al metodo POST:

```
{
  "propertyMappings" : {
      "tevt" : {
       "temperature" : "$event.t"
    }
  },
  "applicationInterfaceId" : "5846ed076522050001db0e12"
}
```
Il seguente esempio mostra come utilizzare cURL per aggiungere un'associazione al tipo di dispositivo *EnvSensor2*:
```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/mappings \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"applicationInterfaceId" : "5846ed076522050001db0e12","propertyMappings" : {
              "tempevt" : {
                  "temperature" : "($event.temp - 32) / 1.8"
              }
            }
          }'
```

Specificare l'identificativo dell'interfaccia dell'applicazione *5846ed076522050001db0e12* restituito nella risposta al metodo POST utilizzato per creare l'interfaccia e il tipo di dispositivo *EnvSensor2*.
Viene applicata una conversione per modificare il valore da una misurazione in gradi Fahrenheit a una in gradi Celsius.


Il seguente esempio mostra una risposta al metodo POST:

```
{
  "propertyMappings" : {
    "tempevt" : {
      "temperature" : "($event.temp - 32) / 1.8"
    }
  },
  "applicationInterfaceId" : "5846ed076522050001db0e12"
}
```

### Distribuisci la configurazione 
{: #step15}

Distribuisci la configurazione collegata all'aggiornamento dello stato del dispositivo per ogni tipo di dispositivo. Questa configurazione include i tuoi schemi, tipi di evento, interfacce fisiche, interfacce dell'applicazione e associazioni.

Per distribuire la tua configurazione del tipo di dispositivo, utilizza la seguente API:

```
PATCH /device/types/{typeId}
```
Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

In questo scenario, abbiamo bisogno di distribuire la configurazione per due tipi di dispositivo.

Il seguente esempio mostra come utilizzare cURL per distribuire la tua configurazione per il tipo di dispositivo *EnvSensor1*:

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy"
          }'
```

Il seguente esempio mostra una risposta al metodo PATCH:

```
{
 "message": "CUDRS0520I: State update configuration for device type 'EnvSensor1' has been successfully submitted for deployment",
  "details": {
    "id": "CUDRS0520I",
    "properties": ["EnvSensor1"]
  },
 "failures": []
}
```

Il seguente esempio mostra come utilizzare cURL per distribuire la tua configurazione per il tipo di dispositivo *EnvSensor2*:

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy"
          }'
```

Il seguente esempio mostra una risposta al metodo PATCH:

```
{
 "message": "CUDRS0520I: State update configuration for device type 'EnvSensor2' has been successfully submitted for deployment",
  "details": {
    "id": "CUDRS0520I",
    "properties": ["EnvSensor2"]
  },
 "failures": []
}
```

### Pubblica un evento del dispositivo in entrata 
{: #step12}

Pubblica un evento sulla temperatura da *TemperatureSensor1* nell'argomento `iot-2/evt/tevt/fmt/json` e un evento sulla temperatura da *TemperatureSensor2* nell'argomento `iot-2/evt/tempevt/fmt/json`.

Per informazioni sulla pubblicazione di un evento in entrata da un dispositivo, consulta [Connettività MQTT per le applicazioni](../applications/mqtt.html#publishing_device_events).


### Controlla che lo stato del dispositivo sia stato modificato 
{: #step13}

Per controllare lo stato del dispositivo, utilizza la seguente API:
```
GET /device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
```
Per ulteriori dettagli, consulta la [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

Il seguente esempio mostra come utilizzare cURL per richiamare lo stato corrente di *TemperatureSensor1* facendo riferimento all'identificativo dell'interfaccia dell'applicazione che è stata creata:
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/devices/TemperatureSensor1/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

L'identificativo dell'interfaccia dell'applicazione *5846ed076522050001db0e12* viene utilizzato nel metodo GET. Questo identificativo viene restituito nella risposta al metodo POST utilizzato per creare l'interfaccia dell'applicazione.
Il seguente esempio mostra una risposta al metodo GET:
```
{
  "temperature":34.5
}
```
Il seguente esempio mostra come utilizzare cURL per richiamare lo stato corrente di *TemperatureSensor2* facendo riferimento all'identificativo dell'interfaccia dell'applicazione che è stata creata:
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/devices/TemperatureSensor2/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

L'identificativo dell'interfaccia dell'applicazione *5846ed076522050001db0e12* viene utilizzato nel metodo GET. Questo identificativo viene restituito nella risposta al metodo POST utilizzato per creare l'interfaccia dell'applicazione.
Il seguente esempio mostra una risposta al metodo GET:
```
{
  "temperature":22.5
}
```
Tieni presente che la lettura sulla temperatura che viene restituita è in gradi Celsius e non in Fahrenheit.

La tua applicazione può elaborare questi dati normalizzati senza richiedere la configurazione per comprendere o convertire le scale di temperatura differenti.
