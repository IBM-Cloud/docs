---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-07"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# API REST HTTP per dispositivi gateway
{: #api_link}


Per accedere alla documentazione dell'API REST HTTP {{site.data.keyword.iot_short_notm}} e trovare ulteriori informazioni sulla creazione, l'aggiornamento, l'eliminazione e l'elenco dei dispositivi, consulta [API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html).

L'unica versione dell'API REST HTTP {{site.data.keyword.iot_short_notm}} supportata è la versione 2. Assicurati che le tue soluzioni {{site.data.keyword.iot_short_notm}} utilizzino la versione 2.

## Connessioni client
{: #client_connections}

Per informazioni sulla sicurezza client e su come collegare i client ai dispositivi client e gateway in {{site.data.keyword.iot_short_notm}}, consulta [Connessione di applicazioni, dispositivi e gateway a {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).


### Autenticazione

Tutte le richieste devono includere un'intestazione di autorizzazione. L'autenticazione di base è l'unico metodo supportato. Quando un dispositivo effettua una richiesta HTTP utilizzando l'API REST HTTP {{site.data.keyword.iot_short_notm}}, sono necessarie le seguenti credenziali:

|Credenziale|Input richiesto|
|:---|:---|
|Nome utente| `g/{orgId}/{gwType}/{gwDevId}`
|Password| Il token di autenticazione che è stato generato automaticamente o specificato manualmente quando hai registrato il dispositivo gateway.

dove:

<dl>
<dt>orgId</dt>  
<dd>Il nome dell'organizzazione, che deve corrispondere al nome specificato nell'intestazione host.</dd>

<p></p>
<dt>gwType</dt>  
<dd>Il tipo del gateway. </dd>
<p></p>
<dt>gwDevId</dt>  
<dd>L'identificativo del dispositivo del gateway. </dd>
</dl>


### Intestazioni richiesta per tipo di contenuto

Deve essere fornita un'intestazione della richiesta `Content-Type` con la richiesta. La seguente tabella mostra come i tipi supportati sono associati ai formati interni di {{site.data.keyword.iot_short_notm}}:

|Intestazione Content-Type|Formato in {{site.data.keyword.iot_short_notm}}|
|:---|:---|
|testo/semplice|"text"
|applicazione/json| "json"
|applicazione/xml | "xml"
|applicazione/octet-stream|"bin"

## Ultimo evento cache
{: #last-event-cache}

Utilizzando l'API Ultima cache evento {{site.data.keyword.iot_short_notm}}, puoi richiamare l'ultimo evento che è stato inviato a un dispositivo. Questa API funziona sia se il dispositivo è online che offline e ti consente di richiamare lo stato del dispositivo indipendentemente dalla sua ubicazione fisica o stato di utilizzo. Puoi richiamare l'ultimo valore registrato di un ID evento per un dispositivo specifico o l'ultimo valore registrato per ogni ID evento che è stato riportato da un dispositivo specifico. Gli ultimi dati evento possono essere richiamati per ogni evento specifico verificatosi negli ultimi 365 giorni.

Per richiedere il valore più recente di un ID evento specifico, utilizza la seguente richiesta API, che restituisce l'ultimo valore registrato per l'ID evento “power”:

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events/power
```

La risposta viene restituita nel seguente formato JSON:

```
{
    "deviceId": "<device-id>",
    "eventId": "power",
    "format": "json",
    "payload": "eyJzdGF0ZSI6Im9uIn0=",
    "timestamp": "2016-03-14T14:12:06.527+0000",
    "typeId": "<device-type>"
}
```

**Nota:** mentre la risposta API è nel formato JSON, i payload dell'evento possono essere scritti in qualsiasi formato. I payload restituiti dall'API Ultima cache evento sono codificati in base64.

Per richiedere il valore più recente di ogni ID evento che è stato riportato da un dispositivo, utilizza la seguente richiesta API:

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events
```

La risposta include tutti gli ID evento che sono stati inviati dal dispositivo. Nel seguente esempio, i valori vengono restituiti per gli eventi “power” e “temperature”.

```
[
    {
        "deviceId": "<device-id>",
        "eventId": "power",
        "format": "json",
        "payload": "eyJzdGF0ZSI6Im9uIn0=",
        "timestamp": "2016-03-14T14:12:06.527+0000",
        "typeId": "<device-type>"
    },
    {
        "deviceId": "<device-id>",
        "eventId": "temperature",
        "format": "json",
        "payload": "eyJpbnRlcm5hbCI6MjIsICJleHRlcm5hbCI6MTZ9",
        "timestamp": "2016-03-14T14:17:44.891+0000",
        "typeId": "<device-type>"
    }
]
```
