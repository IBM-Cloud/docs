---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Connettività MQTT per i dispositivi
{: #mqtt}

MQTT è il protocollo primario che i dispositivi e le applicazioni utilizzano per comunicare con {{site.data.keyword.iot_full}}. Le librerie client, le informazioni e gli esempi sono forniti per aiutarti nel collegarti e integrare i tuoi dispositivi con {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Connessioni client
{: #client_connections}

Per informazioni sulla sicurezza client e su come collegare i client MQTT ai dispositivi in {{site.data.keyword.iot_short_notm}}, consulta [Connecting applications, devices, and gateways to {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).


## Connessione dei dispositivi al servizio Quickstart
{: #connecting_devices}

Il servizio Quickstart è il livello di servizio più veloce. Non offre la conferma di ricezione e non supporta livelli QoS (quality of service) MQTT maggiori di zero. Quando ti colleghi al servizio Quickstart, l'autenticazione o la registrazione non è richiesta, e il `orgId` deve essere impostato su `quickstart`.

Se stai scrivendo il codice del dispositivo per l'utilizzo con Quickstart, presta attenzione che le seguenti funzioni del servizio {{site.data.keyword.iot_short_notm}} non sono supportate nella modalità Quickstart:

-  Sottoscrizione ai comandi
-  Protocollo di gestione dispositivo
-  Sessioni durature o pulite

**Importante:** i messaggi inviati dai dispositivi con una frequenza maggiore di uno al secondo potrebbero venire scartati.


## Autenticazione MQTT
{: #mqtt_authentication}

Per i gateway e i dispositivi, {{site.data.keyword.iot_short_notm}} utilizza l'autenticazione basata sul token MQTT.

Per abilitare l'autenticazione MQTT, invia una password e un nome utente quando esegui una connessione MQTT.

### Nome utente

Il nome utente è lo stesso valore per tutti i dispositivi: `use-token-auth`. Questo valore obbliga {{site.data.keyword.iot_short_notm}} ad utilizzare il token di autenticazione del dispositivo, specificato come la password.

### Password

La password per ogni dispositivo è un token di autenticazione univoco che è stato generato quando è stato registrato il dispositivo con {{site.data.keyword.iot_short_notm}}.

## Pubblicazione eventi
{: #publishing_events}

I dispositivi eseguono la pubblicazione degli argomenti dell'evento nel seguente formato:

<pre class="pre">iot-2/evt/<var class="keyword varname">event_id</var>/fmt/<var class="keyword varname">format_string</var></pre>
{: codeblock}

Dove

-  **event_id** è l'ID dell'evento, ad esempio `status`.  L'ID evento può essere qualsiasi stringa che è valida in MQTT. Se non sono utilizzati i caratteri jolly, le applicazioni del sottoscrittore devono utilizzare questa stringa nel loro argomento di sottoscrizione per ricevere gli eventi che vengono pubblicati nei loro argomenti.
-  **format_string** è una stringa che definisce il tipo di contenuto del payload del messaggio in modo che il ricevente del messaggio possa determinare come analizzare il contenuto. I valori di tipo di contenuto includono ma non sono limitati a "json", "xml", "txt" e "csv". Il valore può essere qualsiasi stringa che è valida in MQTT.

**Importante:** il payload dei messaggi è limitato ad un massimo di 131072 byte. I messaggi che superano questo limite vengono rifiutati.

### Messaggi conservati
Le organizzazioni {{site.data.keyword.iot_short_notm}} non sono autorizzate a pubblicare i messaggi MQTT conservati. Se un dispositivo invia un messaggio conservato, il servizio {{site.data.keyword.iot_short_notm}} sovrascrive l'indicatore del messaggio conservato quando viene impostato su true ed elabora il messaggio come se l'indicatore fosse impostato su false.


## Sottoscrizione ai comandi
{: #subscribing_to_commands}

I dispositivi possono sottoscriversi agli argomenti del comando nel seguente formato:

<pre class="pre">iot-2/cmd/<var class="keyword varname">command_id</var>/fmt/<var class="keyword varname">format_string</var></pre>
{: codeblock}

Dove
 - **command_id** è l'ID del comando, ad esempio, `update`. L'ID comando può essere qualsiasi stringa che è valida nel protocollo MQTT.  Se non sono utilizzati i caratteri jolly, un dispositivo deve utilizzare questa stringa nel proprio argomento di sottoscrizione per ricevere i comandi che vengono pubblicati nel loro argomento.
 - **format_string** è una stringa che definisce il tipo di contenuto del payload del comando in modo che il ricevente del comando possa determinare come analizzare il contenuto. I valori di tipo di contenuto includono ma non sono limitati a "json", "xml", "txt" e "csv". Il valore può essere qualsiasi stringa che è valida in MQTT.

I dispositivi possono sottoscriversi agli eventi da altri dispositivi. Un dispositivo riceve i comandi che vengono pubblicati soltanto per il proprio dispositivo.

## Dispositivi gestiti
{: #managed-devices}

Il supporto per la gestione del ciclo di vita del dispositivo è facoltativo. Il protocollo di gestione del dispositivo utilizza la stessa connessione MQTT che il tuo dispositivo già utilizza per il controllo del comando e degli eventi.

### Livelli di QOS (quality of service) e sessione di pulizia

I dispositivi gestiti possono pubblicare i messaggi con un livello di QOS (quality of service) di 0 o 1.

I messaggi con QoS=0 possono essere scartati e non sono conservati dopo il riavvio del server di messaggistica. I messaggi con QoS=1 possono essere accodati e sono conservati dopo il riavvio del server di messaggistica. La durata della sottoscrizione determina se una richiesta viene accodata. Il parametro `cleansession` della connessione che effettua la sottoscrizione determina la durata della sottoscrizione.  

{{site.data.keyword.iot_short_notm}} pubblica le richieste che hanno un livello QoS di 1 per supportare l'accodamento dei messaggi. Per accodare i messaggi inviati mentre un dispositivo gestito non è collegato, configura il dispositivo per non utilizzare le sessioni di pulitura impostando il parametro `cleansession` su false.

**Avvertenza:**
  Se il tuo dispositivo gestito utilizza una sottoscrizione durevole, tutti i comandi che vengono inviati al tuo dispositivo mentre è offline sono riportati come operazioni non riuscite se il dispositivo non si ricollega al servizio prima del timeout della richiesta. Tuttavia, quando il dispositivo si ricollega, queste richieste vengono elaborate dal dispositivo. Una sottoscrizione durevole viene specificata dal parametro `cleansession=false`.

### Argomenti

A un dispositivo gestito viene richiesto di sottoscriversi al seguente argomento per gestire le richieste e le risposte dal servizio {{site.data.keyword.iot_short_notm}}.

```
iotdm-1/#
```


Un dispositivo gestito pubblica in argomenti specificati dal tipo di richiesta di gestione che sta venendo eseguita:

- Il dispositivo gestito pubblica risposte di gestione del dispositivo in `iotdevice-1/response`.
- Per altri argomenti che un dispositivo gestito può pubblicare, consulta [Protocollo di gestione dispositivo](device_mgmt/index.html) e [Richieste di gestione del dispositivo](device_mgmt/requests.html).



### Formato del messaggio

Tutti i messaggi sono inviati nel formato JSON.

**Richieste**  
Le richieste sono formattate come mostrato nel seguente esempio di codice:

<pre class="pre">{  "d": {...}, "<var class="keyword varname">reqId</var>": "b53eb43e-401c-453c-b8f5-94b73290c056" }</pre>
{: codeblock}

Dove:

 - **d** contiene tutti i dati rilevanti per la richiesta.
 - **reqId** è un identificativo della richiesta e deve essere copiato in una risposta. Se non è richiesta una risposta, puoi omettere il campo *reqId*.

**Risposte**  
Le risposte sono formattate come mostrato nel seguente esempio di codice:
```
        {
            "rc": 0,
            "message": "success",
            "d": {...},
            "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056"
        }
```
Dove:  
 - **rc** è un codice risultato della richiesta originale.
 - **message** è un elemento facoltativo con una descrizione di testo del codice di risposta.
 - **d** è un elemento di dati facoltativo che accompagna la risposta.
 - **reqId** è l'ID della richiesta della richiesta originale, che viene utilizzato per correlare le risposte con le richieste. Il dispositivo si deve assicurare che tutti gli ID della richiesta siano univoci. Le risposte alle richieste {{site.data.keyword.iot_short_notm}} devono includere il valore **reqId** corretto.

Per ulteriori informazioni sui messaggi della risposta e della richiesta specifici, consulta [Protocollo di gestione dispositivo](device_mgmt/index.html) e [Richieste di gestione del dispositivo](device_mgmt/requests.html).
