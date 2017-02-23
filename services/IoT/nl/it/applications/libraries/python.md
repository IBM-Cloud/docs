---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-10-27"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Python per gli sviluppatori dell'applicazione
{: #python}


Puoi utilizzare Python per creare e sviluppare le applicazioni che interagiscono con la tua organizzazione su {{site.data.keyword.iot_full}}. Il client Python per {{site.data.keyword.iot_short_notm}} fornisce un'API per facilitare la facile interazione con le funzioni {{site.data.keyword.iot_short_notm}} astraendole dai protocolli sottostanti come MQTT e HTTP.

{:shortdesc}

Utilizza le informazioni e gli esempi forniti per iniziare a sviluppare le tue applicazioni utilizzando Python.

## Scaricamento delle risorse e del client Python
{: #python_client_download}

Per accedere al client Node.js per {{site.data.keyword.iot_short_notm}} e ad altre risorse disponibili, vai al repository [iot-python](https://github.com/ibm-messaging/iot-python) in GitHub e completa le istruzioni di installazione.

## Constructor
{: #constructor}

Il dizionario delle opzioni crea le definizioni utilizzate per interagire con il modulo {{site.data.keyword.iot_short_notm}}. Il constructor crea l'istanza client e accetta un dizionario delle opzioni che contiene le seguenti definizioni:

|Definizione|Descrizione |
|:-----|:-----|
|`orgId`|Il tuo ID dell'organizzazione.|
|`appId`|L'ID univoco di un'applicazione nella tua organizzazione.|
|`auth-method`|Il metodo di autenticazione. L'unico metodo supportato è `apikey`.|
|`auth-key`|Una chiave API facoltativa, che devi specificare quando imposti il valore di auth-method su `apikey`.|
|`auth-token`|Un token chiave API, che è inoltre obbligatorio quando imposti il valore di auth-method su `apikey`.|
|`clean-session`|Un valore true o false obbligatorio solo se desideri collegarti all'applicazione con il metodo di sottoscrizione durevole. Per impostazione predefinita, `clean-session` è impostato su true.|


Se non viene fornito un dizionario delle opzioni, il client si collega al servizio {{site.data.keyword.iot_short_notm}} come un dispositivo non registrato.

```python

import ibmiotf.application
try:
  options = {
    "org": organization,
    "id": appId,
    "auth-method": authMethod,
    "auth-key": authKey,
    "auth-token": authToken,
    "clean-session": true
  }
  client = ibmiotf.application.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

### Utilizzo di un file di configurazione


Se non stai utilizzando un dizionario delle opzioni, devi includere un file di configurazione che contiene un dizionario delle opzioni nel seguente formato del codice:

```python

import ibmiotf.application
try:
  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)
except ibmiotf.ConnectionException as e:
...
```
Il file di configurazione dell'applicazione deve essere nel seguente formato:

```python

[application]
org=orgId
id=myApplication
auth-method=apikey
auth-key=key
auth-token=token
clean-session=true/false

```

## Chiamate API
{: #api_calls}

Ogni metodo nel client API risponde con:

- Una risposta JSON o booleana valida se con esito positivo
- Un'eccezione IoTFCReSTException se con esito negativo

Per ulteriori informazioni sul perché una chiamata API ha esito negativo o per controllare se l'azione è parzialmente corretta, un'applicazione può analizzare le proprietà di una risposta dell'eccezione. La risposta dell'eccezione IoTFCReSTException contiene le seguenti proprietà:

|Proprietà|Descrizione|
|:---|:---|
|`httpcode`|Il codice di stato HTTP.|
|`message`|Un messaggio di eccezione che contiene il motivo del malfunzionamento.|
|`response`|L'elemento JSON che contiene la risposta parziale. Se non esiste, questo valore viene impostato su null.|

## Sottoscrizione agli eventi del dispositivo
{: #subscribe_device_events}

Gli eventi sono meccanismi con cui i dispositivi pubblicano i dati nell'istanza {{site.data.keyword.iot_short_notm}}. Il dispositivo controlla il contenuto dell'evento e assegna un nome ad ogni evento che invia.

Quando viene ricevuto un evento dall'istanza {{site.data.keyword.iot_short_notm}}, le credenziali dell'evento ricevuto identificano il dispositivo di invio, il che rende impossibile a un dispositivo di impersonarne un altro.

Per impostazione predefinita, le applicazioni si sottoscrivono a tutti gli eventi da tutti i dispositivi collegati. Utilizza i parametri deviceType, deviceId, event e msgFormat per controllare l'ambito della sottoscrizione. Un singolo client può supportare più sottoscrizioni. I seguenti esempi di codice mostrano come puoi utilizzare i parametri deviceType, deviceId, event e msgFormat per definire l'ambito di una sottoscrizione:


### Sottoscrizione a tutti gli eventi provenienti da tutti i dispositivi


```python

import ibmiotf.application
  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents()
```

### Sottoscrizione a tutti gli eventi provenienti da tutti i dispositivi di un tipo specifico


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType)
```

### Sottoscrizione di un evento specifico da tutti i dispositivi


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(event=myEvent)
```

### Sottoscrizione di un evento specifico da due o più dispositivi differenti

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, event=myEvent)
client.subscribeToDeviceEvents(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId, event=myEvent)
```

### Sottoscrizione a tutti gli eventi che vengono pubblicati in formato JSON

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, msgFormat="json")
```

## Gestione degli eventi dai dispositivi
{: #handling_events_devices}

Per elaborare gli eventi ricevuti dalle tue sottoscrizioni, devi registrare un metodo di callback dell'evento. I messaggi vengono restituiti come un'istanza della classe evento:

|Proprietà|Tipo di dati|Descrizione|
|:---|:---|
|`event.device`|Stringa|Identifica univocamente il dispositivo tra tutti i tipi di dispositivi nell'organizzazione|
|`event.deviceType`|Stringa|Identifica il tipo di dispositivo. Generalmente, il deviceType è un raggruppamento di dispositivi che esegue un'attività specifica, ad esempio "weatherballoon".|
|`event.deviceId`|Stringa|Rappresenta l'ID del dispositivo. Generalmente, per determinato tipo di dispositivo, il deviceId è un identificativo univoco di tale dispositivo, ad esempio un numero seriale o un indirizzo MAC.|
|`event.event`|Stringa|Solitamente viene utilizzato per raggruppare gli eventi specifici, ad esempio "status", "warning" e "data".
|`event.format`|Stringa|Il formato può essere qualsiasi stringa, ad esempio JSON.
|`event.data`|Dizionario|I dati per il payload del messaggio. La lunghezza massima è di 131072 byte.
|`event.timestamp`|Data e ora|La data e l'ora dell'evento|

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  def myEventCallback(event):
      str = "%s event '%s' received from device [%s]: %s"
      print(str % (event.format, event.event, event.device, json.dumps(event.data)))

...
client.connect()
client.deviceEventCallback = myEventCallback
client.subscribeToDeviceEvents()
```


## Sottoscrizione agli stati del dispositivo
{: #subscribe_device_status}


Per impostazione predefinita, quando ti sottoscrivi a uno stato del dispositivo, gli aggiornamenti dello stato sono ricevuti da tutti i dispositivi collegati. Utilizza i parametri tipo e ID per controllare l'ambito della sottoscrizione. Un singolo client può supportare più sottoscrizioni.

### Sottoscrizione agli aggiornamenti dello stato per tutti i dispositivi


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus()
```

### Sottoscrizione agli aggiornamenti dello stato per tutti i dispositivi di un tipo specifico


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus(deviceType=myDeviceType)
```

### Sottoscrizione agli aggiornamenti dello stato per due dispositivi differenti


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus(deviceType=myDeviceType, deviceId=myDeviceId)
client.subscribeToDeviceStatus(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId)
```

## Gestione degli stati dai dispositivi
{: #handling_device_updates}

Eventi di stato

Per elaborare gli aggiornamenti dello stato ricevuti dalle tue sottoscrizioni, devi registrare un metodo di callback dell'evento. I messaggi vengono restituiti come un'istanza della classe stato.

Esistono due tipi di eventi di stato, eventi `Connect` e eventi `Disconnect`. Tutti gli eventi di stato includono le seguenti proprietà:

|Proprietà|Tipo di dati|
|:---|:---|
|`status.clientAddr`|Stringa|
|`status.protocol`|Stringa|
|`status.clientId`|Stringa|
|`status.user`|Stringa|
|`status.time`|Data e ora|
|`status.action`|Stringa|
|`status.connectTime`|Data e ora|
|`status.port`|Numero intero|


La proprietà `status.action` determina se un evento dello stato è del tipo `Connect` o `Disconnect`.

Gli eventi dello stato `Disconnect` includono le seguenti ulteriori proprietà:

|Proprietà|Tipo di dati|
|:---|:---|
|`status.writeMsg`|Numero intero|
|`status.readMsg`|Numero intero|
|`status.reason`|Stringa|
|`status.readBytes`|Numero intero|
|`status.writeBytes`|Numero intero|

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

def myStatusCallback(status):

  if status.action == "Disconnect":
    str = "%s - device %s - %s (%s)"
    print(str % (status.time.isoformat(), status.device, status.action, status.reason))
    else:
      print("%s - %s - %s" % (status.time.isoformat(), status.device, status.action))
  ...
client.connect()
client.deviceStatusCallback = myStatusCallback
client.subscribeToDeviceStstus()
```


## Pubblicazione degli eventi dai dispositivi
{: #publishing_device_events}

Le applicazioni possono pubblicare gli eventi come se fossero originati da un dispositivo.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent(myDeviceType, myDeviceId, "status", "json", myData)
```


## Pubblicazione dei comandi ai dispositivi
{: #publishing_commands_devices}


Le applicazioni possono pubblicare i comandi sui dispositivi connessi.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
commandData={'rebootDelay' : 50}
client.publishCommand(myDeviceType, myDeviceId, "reboot", "json", myData)
```


## Dettagli organizzazione
{: #org_details}

Le applicazioni possono utilizzare il metodo `getOrganizationDetails()` per richiamare i dettagli sulla configurazione dell'organizzazione.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    orgDetail = client.api.getOrganizationDetails()
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```

Per informazioni sul modello della risposta e della richiesta e sui codici di stato HTTP, fai riferimento alla sezione di configurazione dell'organizzazione dell'[API {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html).


## Operazioni dispositivo in blocco
{: #bulk_device_ops}

Le tue applicazioni possono utilizzare operazioni in blocco per ottenere, aggiungere o rimuovere più dispositivi contemporaneamente.

Per informazioni sull'elenco dei parametri di query, il modello della risposta e della richiesta e i codici di stato HTTP, consulta la sezione 'Operazioni in blocco' dell'[API {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Bulk_Operations/).


### Richiamo delle informazioni relative al dispositivo

Le informazioni sul dispositivo in blocco possono essere richiamate utilizzando il metodo `getAllDevices()`. Questo metodo richiama le informazioni su tutti i dispositivi registrati nell'organizzazione. Ogni richiesta può contenere un massimo di 512 KB.

La risposta contiene i parametri richiesti dall'applicazione. Utilizzare i risultati del dizionario dalla risposta per ottenere l'array dei dispositivi restituiti. Sono richiesti altri parametri nella risposta per effettuare ulteriori chiamate, ad esempio, l'elemento `_bookmark` può essere utilizzato per sfogliare i risultati. Invia la prima richiesta senza specificare un segnalibro, quindi prendi il segnalibro restituito nella risposta e forniscilo alla richiesta nella pagina seguente. Ripeti fino al termine della serie di risultati, che viene indicato dall'assenza di un segnalibro. Ogni richiesta deve utilizzare gli stessi valori per gli altri parametri, altrimenti i risultati non saranno definiti.


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    deviceList = client.api.getAllDevices()
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```
### Aggiunta di più dispositivi


Utilizza il metodo `addMultipleDevices()` per aggiungere uno o più dispositivi alla tua organizzazione {{site.data.keyword.iot_short_notm}}. Una richiesta non può essere maggiore di 512 KB. La risposta contiene i token di autenticazione che sono stati generati per ogni dispositivo. Assicurati di effettuare una copia dei token di autenticazione perché se li perdi, non possono essere richiamati.


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  listOfDevicesToAdd = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
  deviceList = client.api.addMultipleDevices(listOfDevicesToAdd)
except IoTFCReSTException as e:
  print("ERROR [" + e.httpcode + "] " + e.message)
```

### Eliminazione di più dispositivi


Utilizza il metodo `deleteMultipleDevices()` per eliminare più dispositivi da un'organizzazione
{{site.data.keyword.iot_short_notm}}. Una richiesta non può essere maggiore di 512 KB.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  listOfDevicesToDelete = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
      deviceList = client.api.deleteMultipleDevices(listOfDevicesToDelete)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```


## Operazioni del tipo di dispositivo
{: #device_type_ops}

I tipi di dispositivo che crei nella tua organizzazione possono essere utilizzati per creare template per l'aggiunta di dispositivi. Utilizzando le funzioni dell'API {{site.data.keyword.iot_short_notm}}, le tue applicazioni possono elencare, creare, eliminare, visualizzare o aggiornare i tipi di dispositivo nella tua organizzazione.

Per informazioni sui parametri di query, il modello della risposta e della richiesta e i codici di stato HTTP, consulta la sezione 'Tipi di dispositivo' della documentazione dell'[API {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html).


### Richiamo di tutti i tipi di dispositivo

Utilizza il metodo `getAllDeviceTypes()` per richiamare tutti i tipi di dispositivo presenti nella tua organizzazione {{site.data.keyword.iot_short_notm}}.
Utilizzare i risultati del dizionario dalla risposta per ottenere l'array dei dispositivi restituiti. Sono richiesti altri parametri nella risposta per effettuare ulteriori chiamate, ad esempio, l'elemento `_bookmark` può essere utilizzato per sfogliare i risultati. Invia la prima richiesta senza specificare un segnalibro, quindi prendi il segnalibro restituito nella risposta e forniscilo alla richiesta nella pagina seguente. Ripeti questo processo fino al termine della serie di risultati, che viene indicato dall'assenza di un segnalibro. Ogni richiesta deve utilizzare gli stessi valori per gli altri parametri, altrimenti i risultati non saranno definiti.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

 listOfDevicesToAdd = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
   options = {'_limit' : 2}
   deviceTypeList = client.api.getAllDeviceTypes(options)
except IoTFCReSTException as e:
   print("ERROR [" + e.httpcode + "] " + e.message)

```

### Aggiunta di un tipo di dispositivo

Utilizza il metodo `addDeviceType()` per registrare un tipo di dispositivo per la tua istanza {{site.data.keyword.iot_short_notm}}. In ogni istanza, devi prima definire gli elementi delle informazioni e dei metadati del dispositivo che desideri siano applicati a tutti i dispositivi di questo tipo. L'elemento delle informazioni sul dispositivo è costituito da molte variabili, inclusi serial number, manufacturer, model, class, description, firmware, hardware versions e descriptive location. L'elemento dei metadati è costituito da valori e variabili personalizzati, che sono definite dall'utente.


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  info = {
      "serialNumber": "100087",
      "manufacturer": "ACME Co.",
      "model": "7865",
      "deviceClass": "A",
      "description": "My shiny device",
      "fwVersion": "1.0.0",
      "hwVersion": "1.0",
      "descriptiveLocation": "Office 5, D Block"
  }
  meta = {
      "customField1": "customValue1",
      "customField2": "customValue2"
  }

try:
      deviceType = client.api.addDeviceType(deviceType = "myDeviceType", description = "My first device type", deviceInfo = info, metadata = meta)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```

### Eliminazione di un tipo di dispositivo


Utilizza il metodo `deleteDeviceType()` per eliminare un tipo di dispositivo dalla tua organizzazione {{site.data.keyword.iot_short_notm}}.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
      success = client.api.deleteDeviceType("myDeviceType")
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```

### Richiamo delle informazioni sui tipi di dispositivo specifici


Utilizza il metodo `getDeviceType()` per richiamare le informazioni su un tipo di dispositivo specifico. Il `typeId` del tipo di dispositivo che desideri richiamare deve essere specificato come un parametro.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    deviceTypeInfo = client.api.getDeviceType("myDeviceType")
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```

### Aggiornamento di un tipo di dispositivo


Utilizza il metodo `updateDeviceType()` per modificare le proprietà di un tipo di dispositivo. Quando utilizzi il metodo `updateDeviceType()`, specifica prima il `typeId` del tipo di dispositivo da aggiornare e quindi specifica i seguenti elementi:

- `description`
- `deviceInfo`
- `metadata`

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  info = {
      "serialNumber": "100087",
      "manufacturer": "ACME Co.",
      "model": "7865",
      "deviceClass": "A",
      "description": "My shiny device",
      "fwVersion": "1.0.0",
      "hwVersion": "1.0",
      "descriptiveLocation": "Office 5, D Block"
  }
  meta = {
      "customField1": "customValue1",
      "customField2": "customValue2",
      "customField3": "customValue3"
  }

try:
      updatedDeviceTypeInfo = client.api.updateDeviceType("myDeviceType", "New description", deviceInfo, metadata)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```


## Operazioni dispositivo
{: #device_ops}

Le operazioni del dispositivo disponibili nell'API inclusi l'elenco, l'aggiunta, la rimozione, la visualizzazione, l'aggiornamento, la visualzizazione dell'ubicazione e la visualizzazione delle informazioni di gestione del dispositivo in un'organizzazione
 {{site.data.keyword.iot_short_notm}}.

Per informazioni sui parametri di query, il modello della risposta e della richiesta e i codici di stato HTTP, consulta la 'Sezione dispositivo' dell'[API {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html).


### Richiamo dei dispositivi di un tipo di dispositivo in particolare

Utilizza il metodo `retrieveDevices()` per richiamare tutti i dispositivi di un tipo di dispositivo in particolare in un'organizzazione in un'istanza {{site.data.keyword.iot_short_notm}}, visualizzata nel seguente esempio:


```python

   print("\nRetrieving All existing devices")
   print("Retrieved Devices = ", apiCli.retrieveDevices(deviceTypeId))
```

Utilizzare i risultati del dizionario dalla risposta per ottenere l'array dei dispositivi restituiti. Sono richiesti altri parametri nella risposta per effettuare ulteriori chiamate, ad esempio, l'elemento *_bookmark* può essere utilizzato per sfogliare i risultati. Invia la prima richiesta senza specificare un segnalibro, quindi prendi il segnalibro restituito nella risposta e forniscilo alla richiesta nella pagina seguente. Ripeti fino al termine della serie di risultati, che viene indicato dall'assenza di un segnalibro. Ogni richiesta deve utilizzare gli stessi valori per gli altri parametri, altrimenti i risultati non saranno definiti.

Per trasmettere *_bookmark* o qualsiasi altra condizione, deve essere utilizzato il metodo overloaded. Il metodo overloaded prende i parametri nel formato del dizionario come mostrato nel seguente esempio:

```python
response = apiClient.retrieveDevices("iotsample-arduino", parameters);
```

Il precedente esempio di codice ordina la risposta in base all'ID del dispositivo e quindi utilizza il segnalibro per sfogliare i risultati.

### Aggiunta di un dispositivo


Per aggiungere un dispositivo a un'organizzazione {{site.data.keyword.iot_short_notm}}, utilizza il metodo `registerDevice()`. Il metodo `registerDevice()` aggiunge un solo dispositivo alla tua organizzazione {{site.data.keyword.iot_short_notm}}. Quando aggiungi un dispositivo, puoi specificare i seguenti parametri:

|Parametro|Requisito|Descrizione
|:---|:---|
|`deviceTypeId`|Facoltativo|Assegna un tipo al dispositivo. Se è presente un conflitto tra le variabili definite dal tipo di dispositivo e le variabili definite dalla variabile `deviceInfo`, le variabili specifiche del dispositivo hanno la precedenza.|
|`deviceId`|Obbligatorio||
|`authToken`|Facoltativo|Se non fornito, viene generato un token di autenticazione e viene incluso nella risposta.|
|`deviceInfo`|Facoltativo|Contiene diverse variabili inclusi serialNumber, manufacturer, model, deviceClass, description, descriptiveLocation, firmware e hardware versions.|
|`metadata`|Facoltativo|Le coppie stringa valore del campo personalizzato, come descritto in [Codice di esempio per l'aggiunta di un tipo di dispositivo](#sample_device_type).|
|`location`|Facoltativo|Contiene le variabili longitude, latitude, elevation, accuracy e measuredDateTime.|

Per ulteriori informazioni su questi parametri e sui codici e sul formato della risposta, consulta la [Documentazione API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Devices/post_device_types_typeId_devices).

Quando utilizzi il metodo `registerDevice()`, definisci il parametro deviceID obbligatorio e i parametri facoltativi necessari per il tuo dispositivo e quindi richiama il metodo utilizzando i parametri selezionati.

### Codice di esempio per l'aggiunta di un tipo di dispositivo
{: #sample_device_type}

Inserisci il seguente codice dopo il codice del constructor in un file di script Python(.py). L'esempio illustra un metodo per l'aggiunta di un tipo di dispositivo definendo i parametri deviceId, authToken, metadata, deviceInfo e location.

```python

deviceId = "200020002000"
authToken = "password"
metadata = {"customField1": "customValue1", "customField2": "customValue2"}
deviceInfo = {"serialNumber": "001", "manufacturer": "Blueberry", "model": "abc1", "deviceClass": "A", "descriptiveLocation" : "Bangalore", "fwVersion" : "1.0.1", "hwVersion" : "12.01"}
location = {"longitude" : "12.78", "latitude" : "45.90", "elevation" : "2000", "accuracy" : "0", "measuredDateTime" : "2015-10-28T08:45:11.662Z"}

apiCli.registerDevice(deviceTypeId, deviceId, metadata, deviceInfo, location)
```
### Eliminazione di un dispositivo

Utilizza il metodo `deleteDevice()` per rimuovere un dispositivo da un'organizzazione nell'organizzazione {{site.data.keyword.iot_short_notm}}. Quando elimini un dispositivo utilizzando il metodo `deleteDevice()`, devi specificare i parametri deviceTypeId e deviceId.

Il seguente esempio di codice illustra il formato richiesto per questo metodo:

```python
apiCli.deleteDevice(deviceTypeId, deviceId)
```

### Ottenimento di un dispositivo

Utilizza il metodo `getDevice()` per richiamare un dispositivo da un'organizzazione in {{site.data.keyword.iot_short_notm}}. Quando richiami i dettagli del dispositivo utilizzando il metodo `getDevice()`, devi specificare i parametri deviceTypeId e deviceId

Il seguente esempio di codice illustra il formato richiesto per questo metodo.

```python
apiCli.getDevice(deviceTypeId, deviceId)
```

### Richiamo di tutti i dispositivi

Utilizza il metodo `getAllDevices()` per richiamare tutti i dispositivi in un'organizzazione in {{site.data.keyword.iot_short_notm}}.

```python
apiCli.getAllDevices({'typeId' : deviceTypeId})
```

### Aggiornamento di un dispositivo

Per modificare una o più proprietà di un dispositivo, utilizza il metodo `updateDevice()`.

Puoi aggiornare qualsiasi proprietà nei parametri deviceInfo o metadata. Per aggiornare una proprietà del dispositivo, definisci il parametro deviceInfo prima di richiamare il metodo `updateDevice()`. Il parametro status deve contenere `alert`: True. La proprietà alert controlla se un dispositivo visualizza dei codici di errore nell'interfaccia utente {{site.data.keyword.iot_short_notm}} e deve essere impostato per impostazione predefinita su `enabled`: True, come illustrato nel seguente esempio di codice:

```python
status = { "alert": { "enabled": True }  }
apiCli.updateDevice(deviceTypeId, deviceId, metadata2, deviceInfo, status)
```

### Codice di esempio per l'aggiornamento delle proprietà deviceInfo

Il seguente esempio di codice identifica un dispositivo specifico e quindi aggiorna molte proprietà del parametro deviceInfo.

```python
status = { "alert": { "enabled": True } }
deviceInfo = {descriptiveLocation: "London", hwVersion: "2.0.1", fwVersion: "2.5.1"}
apiCli.updateDevice("MyDeviceType", "200020002000", deviceInfo, status)
```

### Richiamo delle informazioni sull'ubicazione


Utilizza il metodo `getDeviceLocation()` per richiamare le informazioni sull'ubicazione di un dispositivo. I parametri necessari per il richiamo dei dati di ubicazione sono deviceTypeId e deviceId.

```python
apiClient.getDeviceLocation("iotsample-arduino", "arduino01")
```  

La risposta a questo metodo contiene le proprietà longitude, latitude, elevation, accuracy, measuredTimeStamp e updatedTimeStamp.

### Aggiornamento delle informazioni sull'ubicazione


Utilizza il metodo `updateDeviceLocation()` per modificare le informazioni sull'ubicazione di un dispositivo. Come per l'aggiornamento delle proprietà del dispositivo, deve essere definito il parametro deviceLocation con le modifiche che desideri applicare. Il seguente codice di esempio illustra la modifica dei dati di ubicazione per un dispositivo specifico:

```python
deviceLocation = { "longitude": 0, "latitude": 0, "elevation": 0, "accuracy": 0, "measuredDateTime": "2015-10-28T08:45:11.673Z"}
apiCli.updateDeviceLocation(deviceTypeId, deviceId, deviceLocation)
```

Se non viene fornita una data, viene utilizzata la data corrente.


### Come ottenere le informazioni di gestione


Utilizza il metodo `getDeviceManagementInformation()` per ottenere le informazioni sulla gestione di un dispositivo. La risposta contiene l'ultima data/ora di attività, lo stato inattivo del dispositivo (True/False), il supporto per il dispositivo e le azioni e i dati del firmware. Per un elenco completo del contenuto della risposta, consulta la documentazione API pertinente.

Il seguente codice di esempio restituisce le informazioni sulla gestione del dispositivo per un dispositivo con un deviceId impostato su "00aabbccde03" e un deviceTypeId impostato su "iotsample-arduino":

```
apiCli.getDeviceManagementInformation("iotsample-arduino", "00aabbccde03")
```

## Operazioni di diagnostica del dispositivo
{: #device_diag_ops}

Utilizza le operazioni di diagnostica del dispositivo per implementare le seguenti attività di risoluzione dei problemi e di gestione log:
- Cancellazione dei log
- Richiamo di tutti i log o di log specifici per un dispositivo
- Aggiunta di informazioni del log
- Eliminazione dei log
- Cancellazione dei codici di errore
- Richiamo dei codici di errore del dispositivo
- Aggiunta dei codici di errore

Per ulteriori informazioni sui modelli di risposta e di query, sui codici di risposta e i parametri di query, consulta la [Documentazione API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html)Documentazione API {{site.data.keyword.iot_short_notm}}.

### Come ottenere i log di diagnostica


Utilizza il metodo `getAllDiagnosticLogs()` per richiamare tutti i log di diagnostica per un dispositivo specifico. Il metodo `getAllDiagnosticLogs()` richiede i parametri deviceTypeId e deviceId.

```python
apiCli.getAllDiagnosticLogs(deviceTypeId, deviceId)
```

Il modello di risposta per questo metodo contiene le proprietà log ID, message, severity, data e timestamp.

### Cancellazione dei log di diagnostica di un dispositivo


Utilizza il metodo `clearAllDiagnosticLogs()` per eliminare tutti i log di diagnostica per un dispositivo specifico. I parametri obbligatori sono deviceTypeId e deviceId. Fai attenzione quando elimini i file di log, perché non possono essere ripristinati dopo l'eliminazione.

```python
apiCli.clearAllDiagnosticLogs(deviceTypeId, deviceId)
```

### Aggiunta di un log di diagnostica


Utilizza il metodo `addDiagnosticLog()` per aggiungere una voce nel log di diagnostica di un dispositivo. Il log può essere eliminato quando viene aggiunta la nuova voce. Se non viene fornita una data, vengono aggiunte l'ora e la data corrente alla voce. Per utilizzare questo metodo, devi definire un parametro 'logs' con le seguenti variabili:


|Variabile|Requisito|Descrizione|
|:---|:---|:---|
|`message`|Obbligatorio|Contiene il messaggio diagnostico che desideri aggiungere|
|`severity`|Facoltativo|Corrisponde alla severità del log di diagnostica e può essere impostato su 0, 1 o 2, che corrispondono alle categorie informativo, avvertenza e errore.|
|`data`|Facoltativo|Contiene i dati di diagnostica|
|`timestamp`|Facoltativo|Contiene la data e l'ora della voce del log nel formato ISO8601 ma se non specificato, vengono utilizzate la data e l'ora correnti.|


Gli altri parametri necessari nel metodo sono i valori deviceTypeId e deviceId per il dispositivo.

Il seguente esempio di codice contiene un esempio del metodo `addDiagnosticLog()`:

```python
logs = { "message": "MessageContent", "severity": 0, "data": "LogData"}
apiCli.addDiagnosticLog(deviceTypeId, deviceId, logs)
```

### Richiamo di un log di diagnostica specifico


Utilizza il metodo `getDiagnosticLog()` per richiamare un log di diagnostica specifico per un dispositivo specificato in base all'ID del log. I parametri obbligatori per questo metodo sono deviceTypeId, deviceId e logId.

```python
apiCli.getDiagnosticLog(deviceTypeId, deviceId, logId)
```

### Eliminazione di un log di diagnostica


Utilizza il metodo `deleteDiagnosticLog()` per eliminare un log di diagnostica specifico. Per specificare un log di diagnostica, devi fornire i parametri deviceTypeId, deviceId e logID.

```python
apiCli.deleteDiagnosticLog(deviceTypeId, deviceId, logId)
```

### Richiamo dei codici di errore del dispositivo


Utilizza il metodo `getAllDiagnosticErrorCodes()` per richiamare tutti i codici di errore di diagnostica associati a un dispositivo specifico.

```python
apiCli.getAllDiagnosticErrorCodes(deviceTypeId, deviceId)
```

### Cancellazione i codici di errore di diagnostica


Utilizza il metodo `clearAllErrorCodes()` per cancellare l'elenco dei codici di errore associati al dispositivo. L'elenco viene sostituito da un singolo codice di errore con valore zero.

```python
apiCli.clearAllErrorCodes(deviceTypeId, deviceId)
```

### Aggiunta di un solo codice di errore di diagnostica


Utilizza il metodo `addErrorCode()` per aggiungere un codice di errore all'elenco dei codici di errore associati al dispositivo. L'elenco può essere eliminato quando viene aggiunta la nuova voce. I parametri necessari in questo metodo sono deviceTypeId, deviceId e errorCode. Il parametro errorCode contiene le seguenti variabili:

- errorCode: Questa variabile è obbligatoria e deve essere impostata su un numero intero. Questa variabile imposta il numero di codici di errore creati.
- timestamp: Questa variabile è facoltativa e contiene la data e l'ora della voce del log nel formato ISO8601. Se questa variabile non è inclusa, viene aggiunta automaticamente con la data e l'ora correnti.

```python
errorCode = { "errorCode": 1234, "timestamp": "2015-10-29T05:43:57.112Z" }
apiCli.addErrorCode(deviceTypeId, deviceId, errorCode)
```

## Determinazione del problema di connessione
{: #connection_problem_determination}

Utilizza il metodo `getDeviceConnectionLogs()` per elencare gli eventi di log di connessione per un dispositivo. Gli eventi di log di connessione possono essere utilizzati per aiutare durante la diagnosi dei problemi di connettività tra il dispositivo e il servizio {{site.data.keyword.iot_short_notm}}. Le voci registrano la connessione corretta, i tentativi di connessione non riuscita, la disconnessione intenzionale e gli eventi di disconnessione avviati dal server.

```
apiCli.getDeviceConnectionLogs(deviceTypeId, deviceId)
```

La risposta include un elenco di voci di log, che contengono messaggi di log e date/ore
