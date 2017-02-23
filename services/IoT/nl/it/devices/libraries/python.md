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


# Python per gli sviluppatori dei dispositivi
{: #python}

Puoi utilizzare Python per creare e sviluppare il codice del dispositivo per interagire con la tua organizzazione su {{site.data.keyword.iot_full}}. Il client Python per {{site.data.keyword.iot_short_notm}} fornisce un'API per facilitare la facile interazione con le funzioni {{site.data.keyword.iot_short_notm}} astraendole dai protocolli sottostanti come MQTT e HTTP.
{:shortdesc}

Utilizza le informazioni e gli esempi forniti per iniziare a sviluppare i tuoi dispositivi utilizzando Python.

## Scaricamento delle risorse e del client Python
{: #python_client_download}

Per accedere al client Node.js per {{site.data.keyword.iot_short_notm}} e ad altre risorse disponibili, vai al repository [iot-python](https://github.com/ibm-watson-iot/iot-python) in GitHub e completa le istruzioni di installazione.

## Constructor
{: #constructor}

Il dizionario delle opzioni crea le definizioni utilizzate per interagire con il modulo {{site.data.keyword.iot_short_notm}}. Il constructor crea l'istanza client e accetta un dizionario delle opzioni che contiene le seguenti definizioni:

|Definizione|Descrizione |
|:---|:---|
|`orgId`|Il tuo ID dell'organizzazione.|
|`type`|Il tipo del dispositivo. Il tipo del dispositivo è un raggruppamento di dispositivi che esegue un'attività specifica, ad esempio "weatherballoon".|
|`id`|Un ID univoco per identificare un dispositivo. Generalmente, per determinato tipo di dispositivo, l'ID del dispositivo è un identificativo univoco di tale dispositivo, ad esempio un numero seriale o un indirizzo MAC.|
|`auth-method`|Il metodo di autenticazione. L'unico metodo supportato è `apikey`.|
|`auth-token`|Un token chiave API, che è inoltre obbligatorio quando imposti il valore di auth-method su `apikey`.|
|`clean-session`|Un valore true o false obbligatorio solo se desideri collegarti all'applicazione con il metodo di sottoscrizione durevole. Per impostazione predefinita, `clean-session` è impostato su true.|

Se non viene fornito un dizionario delle opzioni, il client si collega al servizio {{site.data.keyword.iot_short_notm}} come un dispositivo non registrato.

```python

import ibmiotf.device
try:
  options = {
    "org": orgId,
    "type": deviceType,
    "id": deviceId,
    "auth-method": authMethod,
    "auth-token": authToken,
    "clean-session": true
  }
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

### Utilizzo di un file di configurazione

Invece di definire direttamente un dizionario delle opzioni, puoi anche definire un dizionario delle opzioni separatamente in un file di configurazione, come descritto nel seguente esempio di codice:

```python

import ibmiotf.device
try:
  options = ibmiotf.device.ParseConfigFile(configFilePath)
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

Il file di configurazione che contiene il dizionario delle opzioni deve essere nel seguente formato:

```python

[device]
org=orgID
type=deviceType
id=deviceId
auth-method=token
auth-token=token
clean-session=true/false
```

## Pubblicazione eventi
{: #publishing_events}

Gli eventi sono meccanismi con cui i dispositivi pubblicano i dati in {{site.data.keyword.iot_short_notm}}. Il dispositivo controlla il contenuto dell'evento e assegna un nome ad ogni evento che invia.

Quando viene ricevuto un evento dall'istanza {{site.data.keyword.iot_short_notm}}, le credenziali dell'evento ricevuto identificano il dispositivo di invio, il che significa che un dispositivo non può impersonare un altro dispositivo.

Gli eventi possono essere pubblicati in uno dei tre livelli di QoS (quality of service) definiti dal protocollo MQTT.  Per impostazione predefinita, gli eventi vengono pubblicati al livello QoS `0`.

### Pubblica un evento utilizzando il QOS (quality of service) predefinito

```
client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData)
```

### Aumento del livello QoS per un evento

Puoi aumentare il [livello di QoS (quality of service)](../../reference/mqtt/index.html#qos-levels) per gli eventi pubblicati. Gli eventi con un livello QoS maggiore di `0` possono impiegare più tempo per la pubblicazione, perché sono incluse ulteriori informazioni di ricezione della conferma.

**Nota:** la modalità del flusso Quickstart supporta solo un livello QoS di `0`.

```
client.connect()
myQosLevel=2
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData, myQosLevel)
```
## Gestione dei comandi
{: #handling_commands}

Quando il client del dispositivo si connette, effettua automaticamente la sottoscrizione a qualsiasi comando specificato per questo dispositivo. Per elaborare comandi specifici è necessario registrare un metodo di callback del comando. I messaggi vengono restituiti come un'istanza della classe comando, che contiene le seguenti proprietà:

|Proprietà|Tipo di dati|Descrizione|
|:---|:---|
|`command`|Stringa|Identifica il comando.|
|`format`|Stringa|Il formato può essere qualsiasi stringa, ad esempio JSON.|
|`data`|Dizionario|I dati per il payload. La lunghezza massima è di 131072 byte.|
|`timestamp`|Data e ora|La data e l'ora dell'evento.|


```python

def myCommandCallback(cmd):
  print("Command received: %s" % cmd.data)
  if cmd.command == "setInterval":
    if 'interval' not in cmd.data:
      print("Error - command is missing required information: 'interval'")
    else:
      interval = cmd.data['interval']
  elif cmd.command == "print":
    if 'message' not in cmd.data:
      print("Error - command is missing required information: 'message'")
    else:
      print(cmd.data['message'])

...
client.connect()
client.commandCallback = myCommandCallback
```

## Supporto formato messaggio personalizzato
{: #custom_message_format}

Per impostazione predefinita, il formato del messaggio è impostato su `json`, che significa che la libreria supporta la codifica e la decodifica degli oggetti del dizionario Python nel formato JSON. Quando il formato del messaggio è impostato su `json-iotf`, il messaggio viene codificato in base alla specifica del payload JSON di {{site.data.keyword.iot_short_notm}}. Per aggiungere il supporto ai tuoi propri formati del messaggio personalizzati, consulta l'esempio [Custom Message Format](https://github.com/ibm-watson-iot/iot-python/tree/master/samples/customMessageFormat) in GitHub.

Quando crei un modulo di codifica personalizzato, devi registrarlo nel client del dispositivo come descritto nel seguente esempio:

```python

import myCustomCodec

client.setMessageEncoderModule("custom", myCustomCodec)
client.publishEvent("status", "custom", myData)
```
Se viene inviato un evento in un formato sconosciuto o se un dispositivo non riconosce il formato, la libreria del dispositivo restituisce una condizione `MissingMessageDecoderException`.
