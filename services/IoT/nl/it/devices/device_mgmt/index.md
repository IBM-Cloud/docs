---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Protocollo di gestione dispositivo
{: #index}

## Introduzione
{: #introduction}

{{site.data.keyword.iot_full}} riconosce due classi di dispositivo: **dispositivi gestiti** e **dispositivi non gestiti**.

**Dispositivi gestiti** sono definiti come dispositivi che contengono un agent di gestione del dispositivo. Un agent di gestione del dispositivo è un insieme di logica che consente al dispositivo di interagire con il servizio di gestione del dispositivo {{site.data.keyword.iot_short_notm}} utilizzando il protocollo di gestione del dispositivo. I dispositivi gestiti possono eseguire operazioni di gestione del dispositivo inclusi gli aggiornamenti dell'ubicazione, gli scaricamenti e gli aggiornamenti del firmware, i riavvi e le reimpostazioni dei valori predefiniti.

Il protocollo di gestione del dispositivo definisce un insieme di operazioni supportate. Un agent di gestione del dispositivo può supportare un insieme secondario di operazioni, ma devono essere supportate le operazioni **dispositivi gestiti** e **dispositivi non gestiti**. Un dispositivo che supporta le operazioni di azione firmware deve supportare anche l'osservazione.

Il protocollo di gestione del dispositivo è creato con il protocollo di messaggistica MQTT. Per ulteriori informazioni su come il protocollo di gestione del dispositivo interagisce con MQTT, consulta [Connettività MQTT per i dispositivi](../mqtt.html).


### Il ciclo di vita di gestione del dispositivo

1. Un dispositivo e il suo tipo di dispositivo associato vengono creati in {{site.data.keyword.iot_short_notm}} utilizzando il dashboard o l'API REST.
2. Un dispositivo si collega a {{site.data.keyword.iot_short_notm}} e utilizza l'operazione **dispositivi gestiti** per diventare un dispositivo gestito.
3. Puoi visualizzare e modificare i metadati per un dispositivo utilizzando le operazioni del dispositivo. Queste operazioni - ad esempio le operazioni di aggiornamento firmware e riavvio dispositivo - sono descritte nella documentazione 'Modello dispositivo'. Per ulteriori informazioni sul modello di dispositivo, consulta [Modello dispositivo](https://console.ng.bluemix.net/docs/services/IoT/reference/device_model.html).
4. Un dispositivo può comunicare gli aggiornamenti sulla sua ubicazione, le informazioni di diagnostica e i codici di errore utilizzando il protocollo di gestione del dispositivo.
5. Per gestire i dispositivi inattivi in un grande gruppo di dispositivi, la richiesta dell'operazione **dispositivi gestiti** include un parametro sul ciclo di vita facoltativo. Un parametro del ciclo di vita è il numero di secondi in cui il dispositivo deve effettuare un'altra richiesta **dispositivi gestiti** per evitare di essere classificato come inattivo e diventare un dispositivo non gestito.
6. Quando un dispositivo viene ritirato, puoi rimuoverlo da {{site.data.keyword.iot_short_notm}} utilizzando il dashboard o l'API REST.

Fai riferimento alla ricetta [Connect Raspberry Pi as Managed Device to IBM Watson IoT Platform](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-managed-device-to-ibm-iot-foundation/).

### Riepilogo codice di ritorno


La seguente tabella mostra i codici di ritorno generati in varie fasi durante il ciclo di vita di gestione del dispositivo.

|Codice di ritorno |Messaggio |
|:---|:---|
|200   |Operazione riuscita|
|202   |Accettato (per avviare i comandi)|
|204   |Modificato (per gli aggiornamenti dell'attributo)|
|400   |Richiesta non valida (ad esempio, se un dispositivo non si trova nello stato appropriato per questo comando)|
|404   |L'attributo non è stato trovato (utilizzato anche se l'operazione è stata pubblicata su un argomento non valido)|
|409   |Impossibile aggiornare la risorsa a causa di un conflitto (ad esempio, se la risorsa sta venendo aggiornata da due richieste contemporaneamente, per cui l'aggiornamento può essere richiamato successivamente)|
|500   |Errore dispositivo non previsto|
|501   |Operazione non implementata|


## Richieste di gestione del dispositivo
{: #manage_device_request}

Un dispositivo utilizza la richiesta di gestione del dispositivo per diventare un dispositivo gestito. La richiesta di gestione del dispositivo deve essere la prima richiesta inviata dal dispositivo dopo il collegamento a {{site.data.keyword.iot_short_notm}}. Un agent di gestione del dispositivo normalmente invia questo tipo di richiesta se viene avviato o riavviato.

**Importante:** il supporto per questa operazione è obbligatorio per ogni dispositivo gestito.


### Argomento per una richiesta di gestione del dispositivo

Un dispositivo pubblica una richiesta di gestione del dispositivo nel seguente argomento:

```
iotdevice-1/mgmt/manage
```

Il server risponde alla richiesta di gestione del dispositivo nel seguente argomento:

```
iotdm-1/response
```




### Il formato del messaggio per una richiesta di gestione del dispositivo


In una richiesta di gestione del dispositivo, il campo `d` e tutti i campi secondari relativi sono facoltativi. I valori del campo `metadata` e `deviceInfo` sostituiscono gli attributi corrispondenti per l'invio del dispositivo se sono stati inviati.

Il campo `lifetime` facoltativo specifica l'arco di tempo in secondi in cui il dispositivo deve inviare un'altra richiesta di gestione del dispositivo per evitare di essere classificato come inattivo e diventare un dispositivo non gestito. Se il campo `lifetime` viene omesso o impostato su `0`, il dispositivo gestito non diventa inattivo. L'impostazione supportata minima per il campo `lifetime` è `3600` secondi, che corrisponde a 1 ora.

I campi facoltativi `supports.deviceActions` e `supports.firmwareActions` indicano le funzionalità dell'agent di gestione del dispositivo. Se `supports.deviceActions` è impostato, l'agent supporta le azioni di reimpostazione dei valori predefiniti e di riavvio. Per un dispositivo che non distingue un riavvio da una reimpostazione dei valori predefiniti, è accettabile utilizzare lo stesso comportamento per entrambe le azioni. Se `supports.firmwareActions` è impostato, l'agent supporta le azioni di aggiornamento e scaricamento firmware.

Il seguente esempio mostra il formato della richiesta:

```
Outgoing message from the device:

Topic: iotdevice-1/mgmt/manage
	{
    "d": {
        "metadata":{},
        "lifetime": number,
        "supports": {
            "deviceActions": boolean,
            "firmwareActions": boolean
        },
        "deviceInfo": {
            "serialNumber": "string",
            "manufacturer": "string",
            "model": "string",
            "deviceClass": "string",
            "description" :"string",
            "fwVersion": "string",
            "hwVersion": "string",
            "descriptiveLocation": "string"
        }
    },
    "reqId": "string"
}
```

Il seguente esempio mostra il formato della risposta:

```
Incoming message from the server:

Topic: iotdm-1/response
	{
    "rc": 200,
    "reqId": "string"
}
```


### Codici di risposta per una richiesta di gestione del dispositivo

|Codice di risposta |Messaggio |
|:---|:---|
|200   |L'operazione è riuscita.|
|400   |Il messaggio di input non corrisponde al formato previsto o uno dei valori è fuori dall'intervallo valido.|
|404   |Il nome dell'argomento non è corretto o il dispositivo non è nel database|
|409   |Si è verificato un conflitto durante l'aggiornamento del database del dispositivo. Per risolvere questo conflitto, semplifica l'operazione se necessario.|


## Richieste di annullamento della gestione del dispositivo
{: #manage-unmanage}


Un dispositivo utilizza una richiesta di annullamento della gestione del dispositivo quando non è più necessario che sia un dispositivo gestito. Quando un dispositivo divine non gestito, {{site.data.keyword.iot_short_notm}} non invia più nuove richieste di gestione del dispositivo al dispositivo. I dispositivi non gestiti continuano a pubblicare i codici di errore, i messaggi di log e i messaggi di ubicazione.
**Importante:** il supporto per questa operazione è obbligatorio per ogni dispositivo gestito.

### Argomento per una richiesta di annullamento della gestione del dispositivo


Un dispositivo pubblica una richiesta di annullamento della gestione del dispositivo nel seguente argomento:

```
iotdevice-1/mgmt/unmanage
```

Il server risponde alla richiesta di annullamento della gestione del dispositivo nel seguente argomento:

```
iotdm-1/response
```

### Il formato del messaggio per una richiesta di annullamento della gestione del dispositivo

Formato richiesta:

```
Outgoing message from the device:

Topic: iotdevice-1/mgmt/unmanage
{
    "reqId": "string"
}
```

Formato risposta:

```
Incoming message from the server:

Topic: iotdm-1/response
	{
    "rc": 200,
    "reqId": "string"
}
```

### Codici di risposta per una richiesta di annullamento della gestione del dispositivo

|Codice di risposta |Messaggio |
|:---|:---|
|200   |L'operazione è riuscita.|
|400   |Il messaggio di input non corrisponde al formato previsto o uno dei valori è fuori dall'intervallo valido.|
|404   |Il nome dell'argomento non è corretto o il dispositivo non è nel database|
|409   |Si è verificato un conflitto durante l'aggiornamento del database del dispositivo. Per risolvere questo conflitto, semplifica l'operazione se necessario.|


## Richieste di aggiornamento dell'ubicazione
{: #update-location}

Un dispositivo utilizza una richiesta di aggiornamento dell'ubicazione per gestire i dati di ubicazione di un dispositivo. I metadati di ubicazione di un dispositivo possono essere aggiornati in {{site.data.keyword.iot_short_notm}} nei seguenti modi:

#### Aggiornamenti dell'ubicazione del dispositivo automatici
- Il dispositivo invia notifiche a {{site.data.keyword.iot_short_notm}} sull'aggiornamento dell'ubicazione. Il dispositivo richiama la propria ubicazione da un ricevitore GPS e invia un messaggio di gestione del dispositivo all'istanza {{site.data.keyword.iot_short_notm}} per aggiornare la propria ubicazione. La data/ora acquisisce l'ora in cui è stata richiamata l'ubicazione dal ricevitore GPS. La data/ora è valida anche se è presente un ritardo nell'invio del messaggio di aggiornamento dell'ubicazione. Se la data/ora viene omessa dal messaggio di aggiornamento del dispositivo, vengono utilizzate la data e l'ora del messaggio ricevuto per aggiornare i metadati dell'ubicazione.

#### Aggiornamenti dell'ubciazione del dispositivo manuali utilizzando l'API REST
- Puoi impostare i metadati dell'ubicazione manualmente per un dispositivo statico utilizzando l'API REST {{site.data.keyword.iot_short_notm}} quando viene registrato il dispositivo. Puoi anche modificare l'ubicazione successivamente. L'impostazione di data/ora è facoltativa, ma quando omessa, vengono impostate la data e l'ora correnti nei metadati del dispositivo.

### Aggiornamenti dell'ubicazione attivati dai dispositivi

I dispositivi che determinano la loro ubicazione possono scegliere di inviare notifiche al server di gestione del dispositivo {{site.data.keyword.iot_short_notm}} sulle modifiche dell'ubicazione.

### Argomento per una richiesta di aggiornamento dell'ubicazione attivata dal dispositivo:


Un dispositivo pubblica una richiesta di aggiornamento dell'ubicazione nel seguente argomento:

```
iotdevice-1/device/update/location
```

Il server risponde alla richiesta di aggiornamento dell'ubicazione nel seguente argomento:

```
iotdm-1/response
```

### Aggiornamento dell'ubicazione attivato dagli utenti o dalle applicazioni


Quando un utente o un'applicazione aggiorna l'ubicazione di un dispositivo gestito attivo, il dispositivo richiama un messaggio di aggiornamento.




### Argomento per una richiesta di aggiornamento dell'ubicazione attivata dagli utenti o dalle applicazioni


Il server pubblica una richiesta di aggiornamento dell'ubicazione nel seguente argomento:

```
iotdm-1/device/update
```

### Il formato del messaggio per una richiesta di aggiornamento dell'ubicazione


Il campo `measuredDateTime` è la data della misurazione dell'ubicazione. Il campo `updatedDateTime` è la data dell'aggiornamento delle informazioni del dispositivo. Per motivi di efficacia, {{site.data.keyword.iot_short_notm}} alcune volte raggruppa gli aggiornamenti delle informazioni di ubicazione in modo che gli aggiornamenti siano leggermente differiti. La latitudine e la longitudine devono essere specificate in gradi decimali utilizzando il World Geodetic System 1984 (WGS84).

Se viene aggiornata l'ubicazione, i valori forniti per latitudine, longitudine, altitudine e incertezza sono considerati un solo aggiornamento con più valori. La latitudine e la longitudine sono obbligatorie e devono essere entrambe fornite con ogni aggiornamento.  L'altitudine e l'incertezza sono facoltative e possono essere omesse.

Se un valore facoltativo viene fornito su un aggiornamento e poi omesso in un aggiornamento successivo, il valore precedente viene cancellato dall'aggiornamento successivo. Ogni aggiornamento viene considerato un insieme completo con più valori.

### Aggiornamenti dell'ubicazione attivati dal dispositivo


Formato richiesta:

```
Outgoing message from the device:

Topic: iotdevice-1/device/update/location
{
    "d": {
        "longitude": number,
        "latitude": number,

        "elevation": number,
        "measuredDateTime": "string in ISO8601 format",
        "updatedDateTime": "string in ISO8601 format",
        "accuracy": number
    },
    "reqId": "string"
}
```

Formato risposta:

```
Incoming message from the server:

Topic: iotdm-1/response
	{
    "rc": 200,
    "reqId": "string"
}
```

### Codici di risposta per una richiesta di aggiornamento dell'ubicazione

|Codice di risposta |Messaggio |
|:---|:---|
|200   |L'operazione è riuscita.|
|400   |Il messaggio di input non corrisponde al formato previsto o uno dei valori è fuori dall'intervallo valido.|
|404   |Il nome dell'argomento non è corretto o il dispositivo non è nel database|
|409   |Si è verificato un conflitto durante l'aggiornamento del database del dispositivo. Per risolvere questo conflitto, semplifica l'operazione se necessario.|


### Aggiornamenti dell'ubicazione attivati dagli utenti o dalle applicazioni


Il seguente esempio illustra il formato del payload:

```
Incoming message from the server:

Topic: iotdm-1/device/update
{
    "d": {
        "fields": [
				{
                "field": "location",
                "value": {
                    "latitude": number,
                    "longitude": number,
                    "elevation": number,
                    "accuracy": number,
                    "measuredDateTime": "string in ISO8601 format"
                }
            }
        ]
    }
}
```

**Nota:** il parametro `reqID` non viene utilizzato perché il dispositivo non è richiesto nella risposta.

## Richieste di aggiornamento dell'attributo del dispositivo
{: #update-attributes}

Utilizzando l'API REST, {{site.data.keyword.iot_short_notm}} può inviare una richiesta a un dispositivo di aggiornare il valore di uno o più dei seguenti attributi del dispositivo:


|Attributo | Ulteriori informazioni|
|:---|:---|
|location  | Consulta [Aggiornamento ubicazione](index.html#update-location)|
|metadata  | Facoltativo|
|deviceInfo | Facoltativo|
|mgmt.firmware | Consulta [Processo di aggiornamento firmware](requests.html#firmware-actions-update)|

### Argomento per una richiesta di aggiornamento degli attributi del dispositivo


Il server pubblica una richiesta di aggiornamento degli attributi del dispositivo nel seguente argomento:

```
iotdm-1/device/update
```


### Il formato del messaggio per una richiesta di aggiornamento degli attributi del dispositivo


Il seguente esempio illustra il formato del payload per la richiesta:

```
Incoming message from the server:

Topic: iotdm-1/device/update
{
    "d": {
        "fields": [
				{
                "field": "location",
                "value": ""
            }
        ]
    }
}
```


## Richieste di aggiunta dei codici di errore
{: #diag-add-error-code}

I dispositivi possono scegliere di inviare notifiche al server di gestione del dispositivo {{site.data.keyword.iot_short_notm}} sulle modifiche dei loro stati di errore utilizzando il tipo di richiesta di aggiunta dei codice di errore.

### Argomento per una richiesta di aggiunta dei codici di errore


Un dispositivo pubblica una richiesta di aggiunta dei codici di errore nel seguente argomento:

```
iotdevice-1/add/diag/errorCodes
```

### Il formato del messaggio per una richiesta di aggiunta dei codici di errore


Il valore associato a `errorCode` è il codice di errore del dispositivo corrente e deve essere aggiunto a {{site.data.keyword.iot_short_notm}}.

Formato richiesta:

```
Outgoing message from the device:

Topic: iotdevice-1/add/diag/errorCodes
{
    "d": {
        "errorCode": number
    },
    "reqId": "string"
}
```

Formato risposta:

```
Incoming message from the server:

Topic: iotdm-1/response
	{
    "rc": 200,
    "reqId": "string"
}
```

### Codici di risposta per una richiesta di aggiunta dei codici di errore

|Codice di risposta |Messaggio |
|:---|:---|
|200   |L'operazione è riuscita.|
|400   |Il messaggio di input non corrisponde al formato previsto o uno dei valori è fuori dall'intervallo valido.|
|404   |Il nome dell'argomento non è corretto o il dispositivo non è nel database|
|409   |Si è verificato un conflitto durante l'aggiornamento del database del dispositivo. Per risolvere questo conflitto, semplifica l'operazione se necessario.|


## Richieste di eliminazione dei codici di errore
{: #diag-clear-error-codes}

I dispositivi possono richiedere che {{site.data.keyword.iot_short_notm}} elimini tutti i codici di errore per il dispositivo utilizzando il tipo di richiesta di eliminazione dei codici di errore

### Argomento per una richiesta di eliminazione dei codici di errore


Un dispositivo pubblica questa richiesta nel seguente argomento:

```
iotdevice-1/clear/diag/errorCodes
```

### Il formato del messaggio per una richiesta di eliminazione dei codici di errore


Formato richiesta:

```
Outgoing message from the device:

Topic: iotdevice-1/clear/diag/errorCodes
{
    "reqId": "string"
}
```

Formato risposta:

```
Incoming message from the server:

Topic: iotdm-1/response
	{
    "rc": 200,
    "reqId": "string"
}
```

### Codici di risposta per una richiesta di eliminazione dei codici di errore

|Codice di risposta |Messaggio |
|:---|:---|
|200   |L'operazione è riuscita.|
|400   |Il messaggio di input non corrisponde al formato previsto o uno dei valori è fuori dall'intervallo valido.|
|404   |Il nome dell'argomento non è corretto o il dispositivo non è nel database|
|409   |Si è verificato un conflitto durante l'aggiornamento del database del dispositivo. Per risolvere questo conflitto, semplifica l'operazione se necessario.|


## Richieste di aggiunta dei log
{: #diag-add-log}

I dispositivi possono scegliere se inviare notifiche al supporto di gestione del dispositivo {{site.data.keyword.iot_short_notm}} sulle modifiche aggiungendo una nuova voce di log. Le voci di log includono un messaggio di log, la data/ora, la severità e i dati diagnostici codificati base64 facoltativi.

### Argomento per una richiesta di aggiunta dei log
Un dispositivo pubblica questa richiesta nel seguente argomento:

```
iotdevice-1/add/diag/log
```


### Il formato del messaggio per una richiesta di aggiunta dei log

La seguente tabella descrive il formato degli attributi del messaggio in uscita:

|Attributo |Descrizione |
|:---|:---|
|`message`|Specifica un messaggio di diagnostica che deve essere aggiunto a {{site.data.keyword.iot_short_notm}}|
|`timestamp`|Specifica la data e l'ora della voce di log nel formato ISO8601 |
|`data`|Specifica i dati di diagnostica codificati base64 facoltativi|
|`severity`|Specifica la severità del messaggio (0: informativo, 1: avvertenza, 2: errore)|


Formato richiesta:

```
Outgoing message from the device:

Topic: iotdevice-1/add/diag/log
{
    "d": {
        "message": string,
        "timestamp": string,
        "data": string,
        "severity": number
    },
    "reqId": "string"
}
```

Formato risposta:

```
Incoming message from the server:

Topic: iotdm-1/response
	{
    "rc": 200,
    "reqId": "string"
}
```


### Codici di risposta per una richiesta di aggiunta dei log

|Codice di risposta |Messaggio |
|:---|:---|
|200   |L'operazione è riuscita.|
|400   |Il messaggio di input non corrisponde al formato previsto o uno dei valori è fuori dall'intervallo valido.|
|404   |Il nome dell'argomento non è corretto o il dispositivo non è nel database|
|409   |Si è verificato un conflitto durante l'aggiornamento del database del dispositivo. Per risolvere questo conflitto, semplifica l'operazione se necessario.|

## Richieste di eliminazione dei log
{: #diag-clear-logs}

I dispositivi possono richiedere che {{site.data.keyword.iot_short_notm}} elimini tutte le voci di log utilizzando il tipo di richiesta di eliminazione dei log.

### Argomento per una richiesta di eliminazione dei log


Un dispositivo pubblica una richiesta di eliminazione dei log nel seguente argomento:

```
iotdevice-1/clear/diag/log
```

### Il formato del messaggio per una richiesta di eliminazione dei log


Formato richiesta:

```
Outgoing message from the device:

Topic: iotdevice-1/clear/diag/log
{
    "reqId": "string"
}
```

Formato risposta:

```
Incoming message from the device:

Topic: iotdm-1/response
	{
    "rc": 200,
    "reqId": "string"
}
```

### Codici di risposta per una richiesta di eliminazione dei log

|Codice di risposta |Messaggio |
|:---|:---|
|200   |L'operazione è riuscita.|
|400   |Il messaggio di input non corrisponde al formato previsto o uno dei valori è fuori dall'intervallo valido.|
|404   |Il nome dell'argomento non è corretto o il dispositivo non è nel database|
|409   |Si è verificato un conflitto durante l'aggiornamento del database del dispositivo. Per risolvere questo conflitto, semplifica l'operazione se necessario.|

## Richieste di osservazione delle modifiche dell'attributo
{: #observations-observe}

{{site.data.keyword.iot_short_notm}} può inviare una richiesta di osservazione delle modifiche dell'attributo a un dispositivo per osservare le modifiche ad uno o più attributi utilizzando il tipo di richiesta di osservazione delle modifiche dell'attributo. Quando il dispositivo riceve la richiesta, deve inviare una richiesta di notifica a {{site.data.keyword.iot_short_notm}} ogni volta che i valori degli attributi osservati vengono modificati.

**Importante:** i dispositivi devono implementare, osservare, inviare notifiche e annullare le operazioni per supportare i tipi di richiesta [Azioni firmware - Aggiornamento](requests.html#firmware-actions-update).

### Argomento per una richiesta di osservazione delle modifiche dell'attributo


Il server pubblica una richiesta di osservazione delle modifiche dell'attributo nel seguente argomento:

```
iotdm-1/observe
```

### Il formato del messaggio per una richiesta di osservazione delle modifiche dell'attributo


L'array `fields` è un array degli attributi del dispositivo dal modello del dispositivo. Se viene specificato un campo complesso, come ad esempio `mgmt.firmware`, è previsto che i relativi campi sottostanti siano aggiornati nello stesso momento in modo che sia generato un solo messaggio di notifica.

Il parametro `message` utilizzato nella risposta può essere specificato nella risposta se il valore del parametro `rc` non è `200`. Se non è possibile richiamare il valore del parametro specificato, il valore del parametro `rc` deve essere impostato su `404` se non è stato trovato il dispositivo o su `500` per qualsiasi altro motivo. Quando non possibile trovare i valori dei parametri, l'array `fields` deve contenere gli elementi con `field` impostato sul nome di ogni parametro che non può essere letto. Il parametro `value` deve essere omesso. Per il parametro del codice di risposta da impostare su `200`, devono essere specificati `field` e `value`, dove `value` è il valore corrente di un attributo identificato dal valore del parametro `field`.

Formato richiesta:

```
Incoming message from the server:

Topic: iotdm-1/observe
{
    "d": {
        "fields": [
            "string"
        ]
    },
    "reqId": "string"
}
```

Formato risposta:

```
Outgoing message from the device:

Topic: iotdevice-1/response
	{
    "rc": number,
    "message": "string",
    "d": {
        "fields": [
				{
                "field": "field_name",
                "value": "field_value"
            }
        ]
    },
    "reqId": "string"
}
```


## Richieste di annullamento dell'osservazione dell'attributo
{: #observations-cancel}

{{site.data.keyword.iot_short_notm}} può inviare una richiesta a un dispositivo per annullare l'osservazione corrente di uno o più attributi del dispositivo utilizzando il tipo di richiesta di annullamento dell'osservazione dell'attributo. La parte `fields` della richiesta è un array dei nomi attributo del dispositivo dal modello del dispositivo, ad esempio i parametri `location`, `mgmt.firmware` o `mgmt.firmware.state`.

Il parametro `message` deve essere specificato nella risposta se il valore del parametro `rc` non è `200`.

**Importante:** i dispositivi devono implementare, osservare, inviare notifiche e annullare le operazioni per supportare i tipi di richiesta [Azioni firmware - Aggiornamento](requests.html#firmware-actions-update).

### Argomento per una richiesta di annullamento dell'osservazione dell'attributo


Il server pubblica una richiesta di annullamento dell'osservazione dell'attributo nel seguente argomento:

```
iotdm-1/cancel
```


### Il formato del messaggio per una richiesta di annullamento dell'osservazione dell'attributo


Formato richiesta:

```
Incoming message from the server:

Topic: iotdm-1/cancel
{
    "d": {
        "fields": [
            "string"
        ]
    },
    "reqId": "string"
}
```

Formato risposta:

```
Outgoing message from the device:

Topic: iotdevice-1/response
	{
    "rc": number,
    "message": "string",
    "reqId": "string"
}
```



## Richieste di notifica delle modifiche dell'attributo
{: #observations-notify}

{{site.data.keyword.iot_short_notm}} può effettuare una richiesta di osservazione per un attributo specifico o impostare un insieme di valori utilizzando il tipo di richiesta di notifica delle modifiche dell'attributo. Quando il valore dell'attributo o degli attributi viene modificato, il dispositivo deve inviare una notifica che contiene il valore più recente.

Il valore del parametro `field_name` è il nome dell'attributo modificato e `field_value` è il valore corrente dell'attributo. L'attributo può essere un campo complesso. Se vengono aggiornati più valori in un campo complesso come risultato di una sola operazione, viene inviato solo un messaggio di notifica.

Quando la richiesta di notifica viene elaborata positivamente, il valore del parametro `rc` viene impostato su `200`. Se la richiesta non è corretta, il valore del parametro `rc` viene impostato su `400`. Se il parametro specificato nella richiesta di notifica non è osservato, il valore del parametro `rc` viene impostato su `404`.

**Importante:** i dispositivi devono implementare, osservare, inviare notifiche e annullare le operazioni per supportare i tipi di richiesta [Azioni firmware - Aggiornamento](requests.html#firmware-actions-update).


### Argomento per una richiesta di notifica delle modifiche dell'attributo


Un dispositivo pubblica una richiesta di notifica delle modifiche dell'attributo nel seguente argomento:

```
iotdevice-1/notify
```


### Il formato del messaggio per una richiesta di notifica delle modifiche dell'attributo


Formato richiesta:

```
Outgoing message from the device:

Topic: iotdevice-1/notify
{
    "d": {
        "field": "field_name",
        "value": "field_value"
    }
    "reqId": "string"
}
```

Formato risposta:

```
Incoming message from the server:

Topic: iotdm-1/response
	{
    "rc": number,
    "reqId": "string"
}
```

### Codici di risposta per una richiesta di notifica delle modifiche dell'attributo

|Codice di risposta |Messaggio |
|:---|:---|
|200   |L'operazione è riuscita.|
|400   |Il messaggio di input non corrisponde al formato previsto o uno dei valori è fuori dall'intervallo valido.|
|404   |Il nome dell'argomento non è corretto o il dispositivo non è nel database oppure non esiste un'osservazione per il campo che è stato riportato|
|409   |Si è verificato un conflitto durante l'aggiornamento del database del dispositivo. Per risolvere questo conflitto, semplifica l'operazione se necessario.|
|500   |Si è verificato un errore interno|
