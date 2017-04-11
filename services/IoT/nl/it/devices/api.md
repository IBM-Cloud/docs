---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-14"
---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# API REST HTTP per i dispositivi
{: #api}

**Importante:** l'API REST HTTP {{site.data.keyword.iot_full}} per la funzione dei dispositivi è disponibile solo come parte di un programma beta limitato. Futuri aggiornamenti possono includere modifiche incompatibili con la versione corrente di questa funzione. Provala e [facci sapere cosa ne pensi ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html){: new_window}.

## Accesso alla documentazione dell'API REST HTTP
{: #api_link}

Per accedere alla documentazione dell'API REST HTTP {{site.data.keyword.iot_short_notm}} e ottenere ulteriori informazioni su come integrare i dispositivi nella tua organizzazione, consulta [API](../reference/api.html).

L'unica versione dell'API REST HTTP {{site.data.keyword.iot_short_notm}} supportata è la versione 2. Assicurati che le tue soluzioni {{site.data.keyword.iot_short_notm}} utilizzino la versione 2.

## Connessioni client
{: #client_connections}

Per informazioni sulla sicurezza client e su come collegare i client ai dispositivi in {{site.data.keyword.iot_short_notm}}, consulta [Connecting applications, devices, and gateways to {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).

# API di messaggistica REST HTTP per i dispositivi
{: #rest_messaging_api}

Per accedere alla documentazione dell'API di messaggistica HTTP {{site.data.keyword.iot_short_notm}} e trovare più informazioni sulla pubblicazione degli eventi utilizzando HTTP, consulta [API di messaggistica HTTP {{site.data.keyword.iot_short_notm}} ![Icona link esterno](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}.

## Pubblicazione eventi
{: #event_publication}

In aggiunta all'utilizzo del protocollo di messaggistica MQTT, puoi anche configurare i tuoi dispositivi a pubblicare eventi {{site.data.keyword.iot_short_notm}} in HTTP utilizzando i comandi API REST HTTP.

Utilizza uno dei seguenti URL per inviare una richiesta `POST` da un dispositivo collegato a {{site.data.keyword.iot_short_notm}}:

### Richiesta POST non sicura
<pre class="pre"><code class="hljs">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

### Richiesta POST sicura

<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

**Nota: **la porta 443, la porta SSL predefinita, può anche essere specificata per le chiamate API HTTP sicure.

Se stai collegando un dispositivo o un'applicazione al servizio Quickstart, invece utilizza uno dei seguenti URL:

### Richiesta POST non sicura a Quickstart
<pre class="pre"><code class="hljs">http://quickstart.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

### Richiesta POST sicura a Quickstart
<pre class="pre"><code class="hljs">https://quickstart.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

**Note importanti:**
- Nella versione dell'API REST HTTP corrente, puoi inviare gli eventi del dispositivo solo utilizzando la messaggistica HTTP. Utilizza il protocollo di messaggistica MQTT per inviare richieste per la gestione di un altro dispositivo o per le funzioni di controllo.
- Le connessioni HTTP possono essere riutilizzate per pubblicare eventi solo per lo stesso dispositivo poiché l'intestazione HTTP non può essere modificata.
- La porta 443, la porta SSL predefinita, può anche essere specificata per le chiamate API HTTP sicure.

### Autenticazione

Tutte le richieste devono includere un'intestazione di autorizzazione. L'autenticazione di base è l'unico metodo supportato. Quando un dispositivo effettua una richiesta HTTP tramite l'API REST HTTP {{site.data.keyword.iot_short_notm}}, sono necessarie le seguenti credenziali:

|Credenziale|Input richiesto|
|:---|:---|
|Nome utente|`use-token-auth`
|Password| Il token di autenticazione che è stato generato automaticamente o specificato manualmente quando hai registrato il dispositivo.


### Intestazioni richiesta per tipo di contenuto

Deve essere fornita un'intestazione della richiesta `Content-Type` con la richiesta. La seguente tabella mostra come i tipi supportati sono associati ai formati interni di {{site.data.keyword.iot_short_notm}}.

|Intestazione Content-Type|Formato in {{site.data.keyword.iot_short_notm}}|
|:---|:---|
|testo/semplice|"text"
|applicazione/json| "json"
|applicazione/xml | "xml"
|applicazione/octet-stream|"bin"

### QOS (quality of service)

Simile al livello di sicurezza di distribuzione 0 di QOS (quality of service) MQTT "at most once", la messaggistica REST HTTP fornisce la fornitura del messaggio non persistente ma verifica che la richiesta sia corretta e che possa essere distribuita al server prima che invii la risposta HTTP. Un risposta che contiene un codice di stato HTTP di 200 conferma che il messaggio è stato distribuito al server. Quando utilizzi il livello di QOS (quality of service) MQTT "at most once" o l'equivalente HTTP per distribuire i messaggi dell'evento, il dispositivo o l'applicazione deve implementare la logica del nuovo tentativo per garantire la distribuzione.

Per ulteriori informazioni sul protocollo MQTT e sui livelli di QOS (quality of service) per {{site.data.keyword.iot_short_notm}}, consulta [Messaggistica MQTT](../reference/mqtt/index.html).

## Ultimo evento cache
{: #last-event-cache}

Utilizzando l'API Ultima cache evento {{site.data.keyword.iot_short_notm}}, puoi richiamare l'ultimo evento che è stato inviato a un dispositivo. Funziona sia se il dispositivo è online che offline e ti consente di richiamare lo stato del dispositivo indipendentemente dalla sua ubicazione fisica o stato di utilizzo. Puoi richiamare l'ultimo valore registrato di un ID evento per un dispositivo specifico o l'ultimo valore registrato per ogni ID evento che è stato riportato da un dispositivo specifico. Gli ultimi dati evento possono essere richiamati per ogni evento specifico verificatosi negli ultimi 365 giorni.

Per richiedere il valore più recente di un ID evento specifico, utilizza la seguente richiesta API, che restituisce l'ultimo valore registrato per l'ID evento “power”.

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

La risposta includerà tutti gli ID evento che sono stati inviati dal dispositivo. Nel seguente esempio, i valori vengono restituiti per gli eventi “power” e “temperature”.

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
