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


# Richieste di gestione del dispositivo
{: #requests}


{{site.data.keyword.iot_full}} fornisce azioni che possono essere avviate per uno o più dispositivi. Queste azioni possono essere avviate utilizzando il dashboard o l'API REST. I tipi di azioni disponibili sono **azioni dispositivo** e **azioni firmware**.

## Avviare le richieste di gestione del dispositivo utilizzando il dashboard
{: #initiating-dm-dashboard}

Le richiesta possono essere avviate tramite il dashboard utilizzando la scheda **Actions** della pagina del dispositivo. Fai clic su **Initiate Action** per selezionare un'azione, per selezionare tutti dispositivi e specificare tutti i parametri aggiuntivi che l'azione selezionata supporta.

## Avviare le richieste di gestione del dispositivo utilizzando l'API REST
{: #initiating-dm-api}

Le richieste possono essere avviate utilizzando il seguente esempio API REST:  

`POST https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Per ulteriori informazioni sul corpo di una richiesta di gestione del dispositivo, consulta [API documentation ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.

## Azioni dispositivo
{: #device-actions}

Un dispositivo può specificare di supportare le azioni del dispositivo quando pubblica una richiesta di gestione. Un'azione del dispositivo indica a {{site.data.keyword.iot_short_notm}} che il dispositivo è in grado di rispondere alle azioni di riavvio e di reimpostazione del dispositivo.


## Azioni dispositivo - riavvio
{: #device-actions-reboot}

Puoi avviare l'azione di riavvio del dispositivo utilizzando il dashboard {{site.data.keyword.iot_short_notm}} o utilizzando l'API REST.

Per avviare un riavvio del dispositivo utilizzando l'API REST, immetti una richiesta POST in:

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Fornisci le seguenti informazioni:

- L'azione `device/reboot`
- Un elenco di dispositivi da riavviare, con un massimo di 5000 dispositivi

Esempio di richiesta di riavvio del dispositivo:

```
{
    "action": "device/reboot",
    "devices": [
        {
            "typeId": "someType",
            "deviceId": "someId"
        }
    ]
}
```

Dopo aver avviato la richiesta, viene pubblicato un messaggio MQTT in tutti i dispositivi specificati nel corpo della richiesta di riavvio. Per ogni dispositivo, deve essere restituita una risposta che indica se l'azione di riavvio è stata avviata. Se questa operazione può essere avviata immediatamente, imposta il parametro `rc` su `202`. Se il tentativo di riavvio fallisce, imposta il parametro `rc` su `500` e di conseguenza il parametro `message`. Se il riavvio non è supportato, imposta il parametro `rc` su `501` e di conseguenza il parametro `message`.

L'azione di riavvio termina quando il dispositivo invia una richiesta di gestione del dispositivo dopo il proprio riavvio.

### Argomento per la richiesta di riavvio del dispositivo

Il server pubblica una richiesta di riavvio di un dispositivo nel seguente argomento:

```
iotdm-1/mgmt/initiate/device/reboot
```

### Il formato del messaggio per una richiesta di riavvio del dispositivo


Formato richiesta:

```
Incoming message from the server:

Topic: iotdm-1/mgmt/initiate/device/reboot
{
    "reqId": "string"
}
```

Formato risposta:

```
Outgoing message from the device:

Topic: iotdevice-1/response
	{
    "rc": "response_code",
    "message": "string",
    "reqId": "string"
}
```

## Azioni dispositivo - ripristino impostazioni predefinite
{: #device-actions-factory-reset}

Puoi avviare l'azione di reimpostazione dei valori predefiniti utilizzando il dashboard {{site.data.keyword.iot_short_notm}} o utilizzando l'API REST.

Per avviare una reimpostazione dei valori predefiniti del dispositivo utilizzando l'API REST, immetti una richiesta POST in:

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Vengono fornite le seguenti informazioni:

- L'azione `device/factoryReset`
- Un elenco di dispositivi da reimpostare, con un massimo di 5000 dispositivi

Il seguente esempio fornisce una richiesta di reimpostazione del dispositivo di esempio:

```
{
    "action": "device/factoryReset",
    "devices": [
        {
            "typeId": "someType",
            "deviceId": "someId"
        }
    ]
}
```

Quando viene avviata una richiesta di reimpostazione del dispositivo, viene pubblicato un messaggio MQTT in tutti i dispositivi specificati nel corpo della richiesta. Per ogni dispositivo, deve essere restituita una risposta che indica se l'azione di reimpostazione è stata avviata. Il codice di risposta viene impostato su `202` se questa azione può essere avviata immediatamente. Se il tentativo di reimpostazione dei valori predefiniti fallisce, imposta il parametro `rc` su `500` e di conseguenza il parametro `message`. Se la reimpostazione dei valori predefiniti non è supportata, imposta il parametro `rc` su `501` e di conseguenza il parametro `message`.

L'azione di reimpostazione dei valori predefiniti termina quando il dispositivo invia una richiesta di gestione del dispositivo dopo la reimpostazione.

### Argomento per la richiesta di reimpostazione dei valori predefiniti

Il server pubblica la seguente richiesta al dispositivo:

```
iotdm-1/mgmt/initiate/device/factory_reset
```


### Il formato del messaggio per una richiesta di reimpostazione dei valori predefiniti


Formato richiesta:

```
Il seguente argomento mostra il messaggio in entrata dal server:

Topic: iotdm-1/mgmt/initiate/device/factory_reset
{
    "reqId": "string"
}
```

Formato risposta:

```
Il seguente argomento mostra il messaggio in uscita dal dispositivo:

Topic: iotdevice-1/response
	{
    "rc": "response_code",
    "message": "string",
    "reqId": "string"
}
```


## Azioni firmware
{: #firmware-actions}

Il livello di firmware noto di un dispositivo viene archiviato nell'attributo `deviceInfo.fwVersion`. Gli attributi `mgmt.firmware` sono utilizzati per eseguire l'aggiornamento firmware e osservarne lo stato.

**Importante:** il dispositivo gestito deve supportare l'osservazione dell'attributo `mgmt.firmware` per supportare le azioni firmware. 

Il processo di aggiornamento firmware è diviso in azioni distinte:
- Scaricamento del firmware
- Aggiornamento del firmware

Lo stato di ogni azione firmware viene archiviato in un attributo diverso del dispositivo. L'attributo `mgmt.firmware.state` descrive lo stato dello scaricamento del firmware. La seguente tabella illustra i valori possibili che possono essere configurati per l'attributo `mgmt.firmware.state`:

 |Valore |Stato  | Spiegazione |
 |:---|:---|:---|
 |0  | In sospeso        | Il dispositivo non sta scaricando il firmware.  |  
 |1  | Scaricamento in corso | Il dispositivo sta scaricando il firmware.  |
 |2  | Scaricamento completato  | Il dispositivo ha scaricato correttamente un aggiornamento firmware ed è pronto per installarlo. |


L'attributo `mgmt.firmware.updateStatus` descrive lo stato dell'aggiornamento del firmware. I possibili valori per l'attributo `mgmt.firmware.updateStatus` sono:

|Valore |Stato | Spiegazione |  
|:---|:---|:---|
|0 | Riuscito | Il firmware è stato aggiornato correttamente. |
|1 | In corso | L'aggiornamento del firmware è stato avviato ma non ancora completato.|
|2 | Memoria non sufficiente | È stata rilevata una condizione di memoria non sufficiente durante l'operazione.|
|3 | Connessione persa     | La connessione è stata persa durante lo scaricamento del firmware. |
|4 | Verifica non riuscita | Il firmware non ha superato la verifica. |
|5 | Immagine non supportata   | L'immagine del firmware scaricata non è supportata dal dispositivo. |
|6 | URI non valido         | Il dispositivo non ha potuto scaricare il firmware dall'URI fornito. |

## Azioni firmware - scaricare
{: #firmware-actions-download}

Puoi avviare l'azione di scaricamento del firmware utilizzando il dashboard {{site.data.keyword.iot_short_notm}} o utilizzando l'API REST.

Per avviare uno scaricamento del firmware utilizzando l'API REST, immetti una richiesta POST in:

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Vengono fornite le seguenti informazioni:

- L'azione `firmware/download`
- Un elenco di dispositivi per ricevere l'immagine, con un massimo di 5000 dispositivi
- L'URI per l'immagine del firmware (facoltativo) 
- La stringa di verifica per convalidare l'immagine (facoltativo)
- Nome del firmware (facoltativo)
- Versione del firmware (facoltativo)

Il seguente esempio mostra la richiesta di scaricamento del firmware su cui si basano tutti i seguenti messaggi di esempio:

```
{
   "action" : "firmware/download",
   "parameters" : [{
         "name" : "uri",
         "value" : "some uri for firmware location"
      }, {
         "name" : "name",
         "value" : "some firmware name"
      }, {
         "name" : "verifier",
         "value" : "some validation code"
      }, {
         "name" : "version",
         "value" : "some firmware version"
      }
   ],
   "devices" : [{
         "typeId" : "someType",
         "deviceId" : "someId"
      }
   ]
}
```

Se nessuno dei parametri facoltativi viene specificato, il primo passo nel seguente processo viene saltato.

Il server di gestione del dispositivo in {{site.data.keyword.iot_short_notm}} utilizza il protocollo di gestione del dispositivo per inviare una richiesta ai dispositivi, che avvia lo scaricamento del firmware. Il processo di download è costituito dai seguenti passi:

1. Una richiesta di aggiornamento dei dettagli del firmware viene inviata nell'argomento `iotdm-1/device/update`.
La richiesta di aggiornamento consente la convalida del dispositivo se il firmware richiesto è diverso dal firmware correntemente installato. Se esiste una differenza, imposta il parametro `rc` su `204`, che viene convertito nello stato `Changed`.  
Il seguente esempio mostra quale messaggio attendere dal precedente invio della richiesta di scaricamento del firmware di esempio e quale risposta viene inviata quando viene individuata una differenza: 
```
   Incoming request from the {{site.data.keyword.iot_short_notm}}:

   Topic: iotdm-1/device/update
   Message:
   {
      "reqId" : "f38faafc-53de-47a8-a940-e697552c3194",
      "d" : {
         "fields": [
				{
               "field" : "mgmt.firmware",
               "value" : {
                  "version" : "some firmware version",
                  "name" : "some firmware name",
                  "uri" : "some uri for firmware location",
                  "verifier" : "some validation code",
                  "state" : 0,
                  "updateStatus" : 0,
                  "updatedDateTime" : ""
               }
            }
         ]
      }
   }

   Outgoing response from device:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 204,
      "reqId" : "f38faafc-53de-47a8-a940-e697552c3194"
   }
   ```
   Questa risposta attiva la richiesta successiva.
2. La richiesta di osservazione per lo stato dello scaricamento del firmware `iotdm-1/observe` è stata inviata.
La richiesta di osservazione verifica se il dispositivo è pronto ad avviare lo scaricamento del firmware. Non appena lo scaricamento può essere avviato, imposta il parametro `rc` su `200` (`Ok`), l'attributo `mgmt.firmware.state` su
   `0` (`Idle`) e l'attributo `mgmt.firmware.updateStatus` su `0` (`Idle`). Il seguente codice è un scambio di esempio tra {{site.data.keyword.iot_short_notm}} e il dispositivo:
   ```
   Incoming request from the {{site.data.keyword.iot_short_notm}}:

   Topic: iotdm-1/observe
   Message:
   {
      "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
      "d" : {
         "fields": [
				{
            "field" : "mgmt.firmware"
            }
         ]
      }
   }

   Outgoing response from device:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 200,
      "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8"
   }
   ```
Questo scambio attiva l'ultimo passo.  

3. La richiesta di scaricamento viene inviata all'argomento `iotdm-1/mgmt/initiate/firmware/download`:

   La richiesta di scaricamento indica a un dispositivo di avviare lo scaricamento del firmware. Se l'azione può essere avviata immediatamente, imposta il parametro `rc` su `202`. Il seguente codice fornisce un esempio dell'avvio di una richiesta di scaricamento:

   ```
   Incoming request from the {{site.data.keyword.iot_short_notm}}:

   Topic: iotdm-1/mgmt/initiate/firmware/download
   Message:
   {
      "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
   }

   Outgoing response from device:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 202,
      "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
   }
   ```

Dopo aver avviato lo scaricamento del firmware in questo modo, il dispositivo deve notificare lo stato dello scaricamento a {{site.data.keyword.iot_short_notm}}. Il dispositivo notifica lo stato pubblicando un messaggio in `iotdevice-1/notify`-topic, dove l'attributo `mgmt.firmware.state` è impostato su `1` (`Downloading`) o `2` (`Downloaded`).
I seguenti esempi mostrano un esempio di avvio dello scaricamento del firmware:

```
Outgoing message from device:

Topic: iotdevice-1/notify
Message:
{
   "reqId" : "123456789",
   "d" : {
      "fields": [
				{
         "field" : "mgmt.firmware",
         "value" : {
                 "state" : 1
             }
      } ]
   }
}


Wait some time...


Outgoing message from device:

Topic: iotdevice-1/notify
Message:
{
   "reqId" : "1234567890",
   "d" : {
      "fields": [
				{
         "field" : "mgmt.firmware",
         "value" : {
                 "state" : 2
             }
      } ]
   }
}
```



Dopo la pubblicazione della notifica con l'attributo `mgmt.firmware.state` impostato su `2`, viene attivata una richiesta in `iotdm-1/cancel`-topic. Questa richiesta annulla l'osservazione dell'attributo `mgmt.firmware`.
Dopo l'invio di una risposta con il parametro `rc` impostato su `200`, lo scaricamento del firmware viene completato. Il seguente codice fornisce un esempio:

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/cancel
Message:
{
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f",
   "d" : {
      "fields": [
				{
            "field" : "mgmt.firmware"
         }
      ]
   }
}


Outgoing message from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f"
}
```

Le seguenti informazioni sono utili per la gestione degli errori:

- Se l'attributo `mgmt.firmware.state` non è `0` ("In sospeso"), invia un errore con il codice di risposta `400` e un testo del messaggio facoltativo.
- Se l'attributo `mgmt.firmware.uri` non è impostato o se non è un URI valido, imposta il parametro `rc` su `400`.
- Se il tentativo di scaricamento del firmware fallisce, imposta il parametro `rc` su `500` e facoltativamente di conseguenza il parametro `message`.
- Se lo scaricamento del firmware non è supportato, imposta il parametro `rc` su `500` e facoltativamente di conseguenza il parametro `message`.
- Quando una richiesta di esecuzione viene ricevuta dal dispositivo, modifica l'attributo `mgmt.firmware.state` da `0` (In sospeso) in `1` (Scaricamento in corso).
- Quando lo scaricamento è stato completato correttamente, imposta l'attributo `mgmt.firmware.state` su `2` (Scaricamento completato). 
- Se si verifica un errore durante lo scaricamento, imposta l'attributo `mgmt.firmware.state` su `0` (In sospeso) e l'attributo `mgmt.firmware.updateStatus` su uno dei seguenti valori di stato dell'errore:
  - 2 (Memoria insufficiente)
  - 3 (Connessione persa)
  - 6 (URI non valido)
- Se è stato impostato il verificatore del firmware, il dispositivo tenta di verificare l'immagine del firmware. Se la verifica dell'immagine ha esito negativo, imposta l'attributo `mgmt.firmware.state` su `0` (In sospeso) e l'attributo `mgmt.firmware.updateStatus` sul valore di stato dell'errore `4` (Verifica non riuscita).

## Azioni firmware - Aggiornamento
{: #firmware-actions-update}

L'installazione del firmware scaricato viene avviata mediante l'API REST immettendo una richiesta POST in:

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Vengono fornite le seguenti informazioni:

- L'azione `firmware/update`
- L'elenco di dispositivi per ricevere l'immagine, tutti dello stesso tipo di dispositivo.
- L'URI per l'immagine del firmware (facoltativo) 
- La stringa di verifica per convalidare l'immagine (facoltativo)
- Nome del firmware (facoltativo)
- Versione del firmware (facoltativo)

Il seguente codice è una richiesta di esempio:

```
   {
      "action" : "firmware/update",
      "devices" : [{
            "typeId" : "someType",
            "deviceId" : "someId"
         }
      ]
   }

```

Se nessuno dei parametri facoltativi viene specificato, il primo messaggio ricevuto dal dispositivo è una richiesta di aggiornamento del dispositivo. Questa richiesta di aggiornamento del dispositivo è simile al primo messaggio della richiesta di scaricamento del firmware.

Per monitorare lo stato dell'aggiornamento del firmware, {{site.data.keyword.iot_short_notm}} attiva una richiesta di osservazione nell'argomento `iotdm-1/observe`. Quando il dispositivo è pronto ad avviare il processo di aggiornamento, invia una risposta con il parametro `rc` impostato su `200`, l'attributo `mgmt.firmware.state` impostato su `0` e l'attributo `mgmt.firmware.updateStatus` impostato su `0`.

Il seguente codice fornisce un esempio:

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/observe
Message:
{
   "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
   "d" : {
      "fields": [
				{
            "field": "mgmt.firmware"
         }
      ]
   }
}

Outgoing response from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
   "d" : {
      "fields": [
				{
            "field" : "mgmt.firmware",
            "value" : {
               "state" : 0,
               "updateStatus" : 0
            }
         }
      ]
   }
}
```



Dopo che l'aggiornamento del firmware è stato scaricato correttamente, il server di gestione del dispositivo in {{site.data.keyword.iot_short_notm}} utilizza il protocollo di gestione del dispositivo per richiedere che i dispositivi specificati inizino l'installazione del firmware utilizzando l'argomento `iotdm-1/mgmt/initiate/firmware/update`.
Se questa operazione può essere avviata immediatamente, imposta il parametro `rc` su `202`.
Se il firmware non è stato precedentemente scaricato correttamente, imposta il parametro `rc` su `400`.

Il seguente codice mostra un esempio:

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/mgmt/initiate/firmware/update
Message:
{
   "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
}

Outgoing response from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 202,
   "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
}
```

Per completare la richiesta di aggiornamento del firmware, il dispositivo notifica il suo stato aggiornato a {{site.data.keyword.iot_short_notm}} utilizzando un messaggio di stato pubblicato in `iotdevice-1/notify`-topic.
Quando viene completato un aggiornamento del firmware, l'attributo `mgmt.firmware.updateStatus` viene impostato su `0` (Riuscito), l'attributo `mgmt.firmware.state` viene impostato su `0` (In sospeso). L'immagine del firmware scaricata può quindi essere eliminata dal dispositivo e l'attributo `deviceInfo.fwVersion` viene impostato sul valore dell'attributo `mgmt.firmware.version`.

Il seguente codice fornisce un esempio di un messaggio di notifica:

```
Outgoing message from device:

Topic: iotdevice-1/notify
Message:
{
   "d": {
      "fields": [
				{
            "field" : "mgmt.firmware",
            "value" : {
               "state" : 0,
               "updateStatus" : 0
            }
         }
      ]
   }
}
```

Quando {{site.data.keyword.iot_short_notm}} riceve la notifica di aggiornamento del firmware completato, attiva un'ultima richiesta in `iotdm-1/cancel`-topic per annullare l'osservazione dell'attributo `mgmt.firmware`.


Quando viene inviata una risposta con il parametro `rc` impostato su `200`, la richiesta di aggiornamento del firmware viene completata, come mostrato nel seguente esempio:

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/cancel
Message:
{
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f",
   "d" : {
      "fields": [
				{
            "field" : "mgmt.firmware"
         }
      ]
   }
}


Outgoing message from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f"
}
```

Il seguente elenco fornisce alcune informazioni utili sulla gestione del processo e degli errori:

- Se il tentativo di aggiornamento del firmware fallisce, imposta il parametro `rc` su `500` e facoltativamente il parametro `message` per contenere le informazioni pertinenti.
- Se il tentativo di aggiornamento del firmware non è supportato, imposta il parametro `rc` su `501` e facoltativamente il parametro `message` per contenere le informazioni pertinenti.
- Se l'attributo `mgmt.firmware.state` non è `2` (Scaricato correttamente), invia un errore con il parametro `rc` impostato su `400` e facoltativamente un testo del messaggio.
- In caso contrario, imposta l'attributo `mgmt.firmware.updateStatus` su `1` (In corso) e normalmente l'installazione del firmware viene avviata.
- Se l'installazione del firmware ha esito negativo, imposta l'attributo `mgmt.firmware.updateStatus` su uno dei seguenti valori:
  - `2` (Memoria insufficiente)
  - `5` (Immagine non supportata)


**Importante:** tutti i parametri elencati come parte dell'attributo `mgmt.firmware` devono essere impostati contemporaneamente in modo che se è in corso un'osservazione per `mgmt.firmware`, viene inviato un solo messaggio notifica.

## Ricette sulle azioni dispositivo e firmware

Le seguenti ricette mostrano il flusso completo necessario per eseguire le azioni dispositivo e firmware.

- [Device Management in WIoT Platform – Roll Back & Factory Reset ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-roll-back-factory-reset/){: new_window}

- [Device Initiated Firmware Update ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-device-initiated-firmware-upgrade/){: new_window}

- [Platform Initiated Firmware Update ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-platform-initiated-firmware-upgrade/){: new_window}

- [Platform Initiated Firmware Update with Background Execution ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-platform-initiated-firmware-upgrade/){: new_window}

- [Firmware Roll Back & Factory Reset ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-roll-back-factory-reset/){: new_window}
