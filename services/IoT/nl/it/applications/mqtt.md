---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Connettività MQTT per le applicazioni
{: #mqtt}

MQTT è il protocollo primario che i dispositivi e le applicazioni utilizzano per comunicare con {{site.data.keyword.iot_full}}. Le librerie client, le informazioni e gli esempi sono forniti per aiutarti nel collegarti e integrare le tue applicazioni {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Connessioni client
{: #client_connections}

Per informazioni sulla sicurezza client e su come collegare i client MQTT alle applicazioni in {{site.data.keyword.iot_short_notm}}, consulta [Connecting applications, devices, and gateways to {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).

## Autenticazione MQTT
{: #mqtt_authentication}

Le applicazioni {{site.data.keyword.iot_short_notm}} richiedono una chiave API per collegarsi a un'organizzazione. Quando viene registrata una chiave API, viene generato un token di autenticazione, che deve essere utilizzato con tale chiave API.

Il seguente esempio mostra una chiave API tipica:

<pre class="pre">a-<var class="keyword varname">orgId</var>-a84ps90Ajs</pre>
{: codeblock}


Il seguente esempio mostra un token di autenticazione tipico:

```
MP$08VKz!8rXwnR-Q*
```

Quando effettui una connessione MQTT utilizzando una chiave API, assicurati che siano applicate le seguenti linee guida:

- L'ID client MQTT deve essere nel formato: a:*orgId*:*appId*
- Il nome utente MQTT è la chiave API (ad esempio, a-*orgId*-a84ps90Ajs)
- La password MQTT è il token di autenticazione (ad esempio, MP$08VKz!8rXwnR-Q*)


## Pubblicazione eventi dispositivo
{: #publishing_device_events}

Un'applicazione può pubblicare eventi come se provenissero da un qualsiasi dispositivo registrato, ad esempio:

-  Pubblica nell'argomento iot-2/type/*device_type*/id/*device_id*/evt/*event_id*/fmt/*format_string*

Per inviare i dati esistenti da un dispositivo a {{site.data.keyword.iot_short_notm}}, puoi creare un'applicazione per elaborare i dati e pubblicarli in {{site.data.keyword.iot_short_notm}}.

**Importante:** il payload dei messaggi è limitato ad un massimo di 131072 byte.  I messaggi che superano il limite vengono rifiutati.

### Messaggi conservati
Le organizzazioni {{site.data.keyword.iot_short_notm}} non sono autorizzate a pubblicare i messaggi MQTT conservati. Se un'applicazione, un gateway o un dispositivo invia un messaggio conservato, il servizio {{site.data.keyword.iot_short_notm}} sovrascrive l'indicatore del messaggio conservato quando viene impostato su true ed elabora il messaggio come se l'indicatore fosse impostato su false.

## Pubblicazione comandi dispositivo
{: #publishing_device_commands}

Un'applicazione può pubblicare un comando per qualsiasi dispositivo, ad esempio:

-  Pubblica nell'argomento iot-2/type/*device_type*/id/*device_id*/cmd/*command_id*/fmt/*format_string*

## Sottoscrizione agli eventi del dispositivo
{: #subscribe_device_events}

Un'applicazione può sottoscriversi agli eventi da uno o più dispositivi, ad esempio:

-  Sottoscrizione all'argomento iot-2/type/*device_type*/id/*device_id*/evt/*event_id*/fmt/*format_string*

**Nota:**  per la sottoscrizione a più di un tipo di evento o agli eventi da più di un dispositivo, utilizza il carattere jolly "any" MQTT (+) per tutti i seguenti componenti:

- device_type
- device_id
- event_id
- format_string

## Sottoscrizione ai comandi del dispositivo
{: #subscribe_device_commands}

Un'applicazione può sottoscriversi ai comandi che stanno venendo inviati a uno o più dispositivi, ad esempio:

-  Sottoscrizione all'argomento iot-2/type/*device_type*/id/*device_id*/cmd/*command_id*/fmt/*format_string*

**Nota:**  per la sottoscrizione a più di un tipo di evento o agli eventi da più di un dispositivo, utilizza il carattere jolly "any" MQTT (+) per tutti i seguenti componenti:

-  device_type
-  device_id
-  cmd_id
-  format_string

## Sottoscrizione ai messaggi di stato del dispositivo
{: #subscribe_device_status}

Un'applicazione può sottoscriversi per monitorare lo stato di uno o più dispositivi, ad esempio:

-  Sottoscrizione all'argomento iot-2/type/*device_type*/id/*device_id*/mon

**Nota:** per la sottoscrizione agli aggiornamenti da più di un dispositivo, utilizza il carattere jolly "any" MQTT (+) per tutti i seguenti componenti:

- device_type
- device_id

## Sottoscrizione ai messaggi di stato dell'applicazione
{: #subscribe_app_status}

Un'applicazione può sottoscriversi per monitorare lo stato di una o più applicazioni, ad esempio:

- Sottoscrizione all'argomento iot-2/app/*appId*/mon

**Nota:** per la sottoscrizione agli aggiornamenti di tutte le applicazioni, utilizza il carattere jolly "any" MQTT (+) per il componente *appId*.


## Restrizioni Quickstart
{: #quickstart_restrictions}
Se stai pianificando di creare un codice dell'applicazione da utilizzare con il servizio Quickstart, le seguenti funzioni non sono supportate in Quickstart:

- Pubblicazione dei comandi
- Sottoscrizione ai comandi
- Utilizzo del carattere jolly "any" MQTT (+) nei componenti **deviceType** o **appId**
- La connessione MQTT tramite TLS (Transport Layer Security)
- Applicazioni scalabili

## Applicazioni scalabili
{: #scalable_apps}

Modificando il modo con cui si collegano le tue applicazioni, puoi rendere le tue applicazioni {{site.data.keyword.iot_short_notm}} più scalabili bilanciando la gestione del carico tra più istanze di un'applicazione.

Il numero di client necessari per una scalabilità e un bilanciamento del carico ottimali varia a secondo della distribuzione. Per identificare il numero di client ottimale, devi eseguire un test di stress del tuo sistema.

Le applicazioni scalabili sono definite come sottoscrizioni non durevoli o come sottoscrizioni condivise a durata mista (Beta).

### Sottoscrizioni non durevoli
{: #shared_sub_non_durable}

Per abilitare il bilanciamento del carico, verifica che la sottoscrizione dell'applicazione non sia durevole e che l'ID client nella sottoscrizione corrisponda al seguente formato:

<pre class="pre">A:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
{: codeblock}

Dove:
-  Il carattere **A** indica che il client è un applicazione scalabile.
-  *orgId* è l'ID dell'organizzazione a sei caratteri univoco generato quando hai registrato il servizio.
-  *appId* è un identificativo stringa univoco definito dall'utente per il client. La stringa può contenere solo caratteri alfanumerici (a-z, A-Z, 0-9) e i caratteri speciali trattino (-), carattere di sottolineatura (_), e punto (.).


**Importante:**
- L'ID client deve iniziare con un carattere maiuscolo **A** per essere correttamente creato come un'applicazione scalabile da {{site.data.keyword.iot_short_notm}}.
- Gli altri client che fanno parte dell'applicazione scalabile devono utilizzare lo stesso ID client.
- Il valore della sessione di pulizia deve essere impostato su false (0) per le sottoscrizioni non durevoli.

### Sottoscrizioni condivise a durata mista (Beta)
{: #shared_sub_mixed}

Il servizio {{site.data.keyword.iot_short_notm}} estende la specifica del protocollo di messaggistica MQTT V3.1.1 per supportare la versione di prova beta delle sottoscrizioni condivise a durata mista. Le sottoscrizioni condivise forniscono le funzionalità di bilanciamento del carico alle applicazioni. Può essere necessaria una sottoscrizione condivisa se un'applicazione aziendale di backend non può elaborare il volume di messaggi che stanno venendo pubblicati per spazio dell'argomento specifico. Ad esempio, quando molti dispositivi pubblicano i messaggi che stanno venendo elaborati da una sola applicazione, può essere necessario utilizzare la funzionalità di bilanciamento del carico di una sottoscrizione condivisa.

Per le sottoscrizioni condivise a durata mista, assicurati che l'ID client nella sottoscrizione corrisponda al seguente formato:

<pre class="pre">A:<var class="keyword varname">org</var>:<var class="keyword varname">appId</var>:<var class="keyword varname">instanceId</var></pre>
{: codeblock}

Dove:
- La lettera **A**, il *orgId* e il *appId* nell'ID client sono definiti nello stesso modo delle [sottoscrizioni non durevoli](#shared_sub_non_durable).
- *instanceID* è una stringa che non deve essere più lunga di 36 caratteri e può contenere solo i seguenti caratteri:
   - Caratteri alfanumerici (a-z, A-Z, 0-9)
   - Trattini ( - )
   - Caratteri di sottolineatura ( _ )
   - Punti ( . )

**Importante:**
- Il supporto per le sottoscrizioni condivise a durata mista è disponibile soltanto come una funzione beta. Non implementare le funzioni beta nelle applicazioni di produzione.
- Il valore della sessione di pulizia può essere impostato su true (1) o false (0) nelle sottoscrizioni condivise a durata mista.
- I client che si collegano tramite il instanceId utilizzano sottoscrizioni differenti rispetto ai client che si collegano senza il instanceId. Pertanto, se vuoi che più client si colleghino a una sottoscrizione condivisa a durata mista, devi specificare il instanceID in tutte le sottoscrizioni.

**Scenario di esempio**

Il seguente scenario è un esempio di come funziona un'applicazione scalabile non durevole in {{site.data.keyword.iot_short_notm}}:

- Il client uno si collega come **A:abc123:myApplication** e si sottoscrive a tutti gli eventi del dispositivo, il che significa che il client uno riceve il 100% degli eventi del dispositivo che vengono pubblicati.
- Il client due di collega come **A:abc123:myApplication** e si sottoscrive anche a tutti gli eventi del dispositivo, il che significa che il client uno e il client due condividono tutti gli eventi che vengono pubblicati. Il carico di elaborazione viene condiviso tra il client uno e due.
- Il client tre si collega come **A:abc123:myApplication** e si sottoscrive anche a tutti gli eventi del dispositivo, il che significa che il client uno, il client due e il client tre condividono il carico di elaborazione degli eventi.
- I client due e tre annullano la sottoscrizione da tutti gli eventi del dispositivo, il che significa che solo il client uno riceve tutti gli eventi del dispositivo che vengono pubblicati. Mentre i client due e tre sono ancora collegati al servizio, il client uno riceve il 100% degli eventi del dispositivo che vengono pubblicati.
- Quando due o più applicazioni condividono una sottoscrizione, i messaggi possono non arrivare nell'ordine nel quale vengono inviati. Ad esempio il messaggio B può arrivare al client uno prima che il messaggio A arrivi al client due, anche se il messaggio A è stato inviato prima.
