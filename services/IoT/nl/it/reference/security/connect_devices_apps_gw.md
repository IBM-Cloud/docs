---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-05"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Connessione di applicazioni, dispositivi e gateway utilizzando l'API
{: #connect_devices_apps_gw}

Puoi collegare le applicazioni, i dispositivi e i gateway a {{site.data.keyword.iot_full}} tramite il protocollo MQTT. Puoi anche utilizzare l'API REST HTTP per collegare i dispositivi a {{site.data.keyword.iot_short_notm}}.
{: shortdesc}


## URL di connessione client
{: #client_connect_url}

Per collegare i client dispositivo, applicazione e gateway alla tua stanza {{site.data.keyword.iot_short_notm}}, utilizza le seguenti connessioni URL:

### Indirizzo di messaggistica

<pre class="pre"><var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com</pre>
{: codeblock}

### API REST HTTP per l'URL di connessione

<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.internetofthings.ibmcloud.com/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>
{: codeblock}

**Note
**
- Dove *orgId* è l'ID dell'organizzazione univoco generato quando hai registrato l'istanza del servizio.
- Se stai collegando un dispositivo o un'applicazione al servizio Quickstart, specifica 'quickstart' per il valore *orgId*.

## Porta di sicurezza
{: #client_port_security}

Assicurati che le porte richieste siano aperte e abilitate per la comunicazione. Le porte 8883 e 443 supportano le connessioni sicure utilizzando TLS con il protocollo MQTT e HTTP. La porta 1883 supporta le connessioni non sicure con il protocollo MQTT e HTTP. Le informazioni sul tipo di connessione associata ai numeri di porta viene riepilogata nella seguente tabella:   

|Tipo di connessione |Numero di porta|
|:---|:---|
|Non sicura|1883|
|Sicura|8883|
|Sicura|443|

MQTT è supportato per TCP e i socket web. I client MQTT si collegano utilizzando le credenziali appropriate, come i token di autenticazione del dispositivo per i dispositivi e i token e le chiavi API per le applicazioni. Poiché la messaggistica MQTT nella porta non sicura 1883 invia tali credenziali in testo semplice, utilizza invece sempre le alternative sicure 8883 o 443. Le credenziali TLS sono sempre crittografate quando inviate su porte sicure. Tieni presente che devi abilitare TLS nell'applicazione utilizzando il metodo tls_set() nella libreria MQTT Python. Altrimenti, i dati potrebbero essere inviati in modo non sicuro.

Quando utilizzi la messaggistica MQTT sicura sulle porte 8883 o 443, le librerie client più recenti verificano automaticamente il certificato presentato da {{site.data.keyword.iot_short_notm}}. Se non è questo il caso del tuo ambiente client, puoi scaricare e utilizzare la catena di certificati completa da [messaging.pem](https://github.com/ibm-messaging/iot-python/blob/master/src/ibmiotf/messaging.pem).


## Requisiti TLS
{: #tls_requirements}

Alcune librerie client TLS (Transport Layer Security) non supportano i domini che includono un carattere jolly. Se non puoi modificare correttamente le librerie, disabilita il controllo del certificato.

I tuoi requisiti TLS dipendono se ti stai collegando a {{site.data.keyword.iot_short_notm}} con il protocollo MQTT o HTTP. Le seguenti sezioni mostrano le suite di cifratura supportate se viene utilizzato il certificato server predefinito. Se stai utilizzando il tuo proprio certificato,
le suite di cifratura supportate dipendono dal certificato utilizzato.

### Requisiti TLS per le connessioni MQTT

{{site.data.keyword.iot_short_notm}} richiede TLS v1.2 e le seguenti suite di cifratura:


- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384

### Requisiti TLS per le connessioni HTTP

Se stai utilizzando il certificato server predefinito, {{site.data.keyword.iot_short_notm}} richiede TLS v1, TLS v1.1 o TLS v1.2 e le seguenti suite di cifratura:


- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_256_GCM_SHA384


## Autenticazione client MQTT
{: #mqtt_authentication}

**Importante:** ogni client MQTT richiede un ID client univoco. Se tenti di collegare un client alla tua organizzazione utilizzando un ID client che è già collegato, la prima connessione viene scollegata.

I dispositivi e i gateway collegati direttamente a {{site.data.keyword.iot_short_notm}} visualizzano un'icona di stato sul dashboard che indica che sono collegati. I dispositivi che sono collegati indirettamente tramite un gateway vengono mostrati come scollegati perché il dashboard non è a conoscenza dei dispositivi collegati tramite un gateway.

### Identificativi client MQTT

Per i dispositivi, le applicazioni e i gateway correttamente autenticati, definisci ogni client MQTT utilizzando il seguente formato e identificativi client:

|Tipo di client |ID|Formato ID MQTT|
|:---|:---|:---|
|Applicazioni|a|<pre class="pre">a:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
|Applicazioni scalabili|A|<pre class="pre">A:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
|Dispositivi|d|<pre class="pre">d:<var class="keyword varname">orgId</var>:<var class="keyword varname">deviceType</var>:<var class="keyword varname">deviceId</var></pre>|
|Gateway|g|<pre class="pre">g:<var class="keyword varname">orgId</var>:<var class="keyword varname">typeId</var>:<var class="keyword varname">deviceId</var></pre>|

Dove
- *orgId* è l'ID dell'organizzazione a sei caratteri univoco generato quando hai registrato il servizio.
- *appId* è un identificativo stringa univoco definito dall'utente per il client.
- *deviceId* identifica univocamente un dispositivo o un gateway tra tutti i tipi ed è simile a un numero di serie.
- *device_type* è l'identificativo del tipo dispositivo collegato ed è simile al numero di modello.
- *typeId* è un identificativo del tipo di gateway collegato ed è simile al numero di modello.

I valori *appId*, *type_id*, *device_type* e *device_id* non devono essere maggiori di 36 caratteri e possono contenere solo:
- Caratteri alfanumerici (a-z, A-Z, 0-9)
- Trattini ( - )
- Caratteri di sottolineatura ( _ )
- Punti ( . )

**Note:**
- Quando ti colleghi al servizio Quickstart, l'autenticazione non è richiesta.
- Non hai bisogno di registrare un'applicazione prima del collegamento.


### Connessione delle applicazioni utilizzando MQTT

Le applicazioni {{site.data.keyword.iot_short_notm}} richiedono una chiave API per collegarsi in un'organizzazione. Quando viene registrata una chiave API, viene generato un token, che deve essere utilizzato con tale chiave API.

Il seguente codice fornisce un esempio di una chiave API:

<pre class="pre">a-<var class="keyword varname">orgId</var>-a84ps90Ajs</pre>
{: codeblock}

Il seguente esempio mostra un token di autenticazione tipico:

```
 MP$08VKz!8rXwnR-Q*
```

Quando effettui una connessione MQTT utilizzando una chiave API, assicurati di rispettare i seguenti requisiti:

- L'ID client MQTT deve essere nel seguente formato: a:*orgId*:*appId*
- Il nome utente MQTT è la chiave API, ad esempio, a-*orgId*-a84ps90Ajs
- La password MQTT è il token di autenticazione, ad esempio, *MP$08VKz!8rXwnR-Q*

Per ulteriori informazioni, consulta [Connettività MQTT per le applicazioni](../../applications/mqtt.html).

### Autenticazione del dispositivo

#### Nomi utente
Il servizio {{site.data.keyword.iot_short_notm}} supporta solo le autenticazioni basate sui token per i dispositivi; quindi, ogni dispositivo ha solo un nome utente valido.
Un valore di `use-token-auth` indica al servizio che viene utilizzato il token di autenticazione per il gateway o per il dispositivo come password per la connessione MQTT.

Per ulteriori informazioni, consulta [Connettività MQTT per i dispositivi](../../devices/mqtt.html).

#### Password
Se il client sta utilizzando l'autenticazione basata sul token, invia il token di autenticazione del dispositivo come password per le connessioni MQTT.
