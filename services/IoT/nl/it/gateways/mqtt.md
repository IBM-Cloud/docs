---

copyright:
  years: 2015, 2017
lastupdated: "2016-11-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Connettività MQTT per i gateway
{: #mqtt}

MQTT è il protocollo primario che i dispositivi e le applicazioni utilizzano per comunicare con {{site.data.keyword.iot_full}}. Le librerie client, le informazioni e gli esempi sono forniti per aiutarti ad utilizzare i client MQTT come gateway per collegare i tuoi dispositivi a {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Connessioni client
{: #client_connections}

Per informazioni sulla sicurezza client e su come collegare i client MQTT come gateway, consulta [Connecting applications, devices, and gateways to {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).

## Autenticazione MQTT
{: #authentication}
Per i gateway e i dispositivi, {{site.data.keyword.iot_short_notm}} utilizza l'autenticazione basata sul token MQTT.

Per abilitare l'autenticazione MQTT, invia una password e un nome utente quando esegui una connessione MQTT.

### Nome utente
{: #username}

Il nome utente è lo stesso valore per tutti i gateway: `use-token-auth`. Questo valore obbliga {{site.data.keyword.iot_short_notm}} ad utilizzare il token di autenticazione del gateway, specificato come la password.

### Password
{: #password}

La password per ogni gateway è un token di autenticazione univoco che è stato generato quando è stato registrato il gateway con {{site.data.keyword.iot_short_notm}}.

## Pubblicazione eventi
{: #pub_events}

Un gateway può pubblicare gli eventi per se stesso o per conto di qualsiasi dispositivo collegato attraverso di esso. Per pubblicare gli eventi, utilizza il seguente argomento e sostituisci i valori `typeId` e `deviceId` appropriati in base all'origine voluta dell'evento:

<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/evt/<var class="keyword varname">eventId</var>/fmt/<var class="keyword varname">formatString</var></pre>
{: codeblock}


**Esempio**


|    |'typeID'|'deviceID'|
|:---|:---|:---|
|Gateway 1 |mygateway |gateway1 |
|Device 1 |mydevice |device1 |

-   Il Gateway 1 può pubblicare i propri eventi di stato:
      
    `iot-2/type/mygateway/id/gateway1/evt/status/fmt/json`
-   Il Gateway 1 può pubblicare gli eventi di stato al posto del Device 1:
      
    `iot-2/type/mydevice/id/device1/evt/status/fmt/json`

**Importante:** il payload dei messaggi è limitato ad un massimo di 131072 byte. I messaggi che superano questo limite vengono rifiutati.

### Messaggi conservati
Le organizzazioni {{site.data.keyword.iot_short_notm}} non sono autorizzate a pubblicare i messaggi MQTT conservati. Se un gateway invia un messaggio conservato, il servizio {{site.data.keyword.iot_short_notm}} sovrascrive l'indicatore del messaggio conservato quando viene impostato su true ed elabora il messaggio come se l'indicatore fosse impostato su false.

## Sottoscrizione ai comandi
{: #subscribing_cmds}

Un gateway può sottoscriversi ai comandi indirizzati al gateway stesso o a qualsiasi dispositivo nell'organizzazione, inclusi altri gateway. Per la sottoscrizione ai comandi, utilizza il seguente argomento e sostituisci i valori `typeId` e `deviceId` appropriati.

<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/cmd/<var class="keyword varname">commandId</var>/fmt/<var class="keyword varname">formatString</var></pre>
{: codeblock}

Il carattere jolly `+` MQTT può essere utilizzato per `typeId`, `deviceId`, `commandId` e `formatString` per la sottoscrizione a più origini del comando.

**Esempio:**

|Dispositivo |`typeId`|`deviceId`|
|:---|:---|
|Gateway 1| mygateway   | gateway1   |
|Device 1 | mydevice    | device1    |


-   Il Gateway 1 può sottoscriversi ai comandi diretti al gateway:
      
    `iot-2/type/mygateway/id/gateway1/cmd/+/fmt/+`
-   Il Gateway 1 può sottoscriversi ai comandi inviati al Device 1:
      
    `iot-2/type/mydevice/id/device1/cmd/+/fmt/+`
-   Il Gateway 1 può sottoscriversi a qualsiasi comando inviato ai dispositivi del tipo `mydevice`:
       
     `iot-2/type/mydevice/id/+/cmd/+/fmt/+`

**Importante:** le sessioni persistenti MQTT specificate come `cleansession=false`, non ricercano i dispositivi collegati ai gateway. Se un dispositivo si collega al gateway A e successivamente al gateway B, non riceve i messaggi che sono stati pubblicati nel gateway A per tale dispositivo mentre era scollegato. Un gateway gestisce la sottoscrizione e il client MQTT ma non i dispositivi collegati al gateway.

## Registrazione automatica dei gateway
{: #auto-reg}

I dispositivi gateway possono automaticamente registrare i dispositivi a loro collegati. Quando un gateway pubblica un messaggio o si sottoscrive ad un argomento per conto di un dispositivo non registrato, tale dispositivo viene registrato automaticamente.

Le richieste di registrazione dai dispositivi gateway sono limitate a 128 richieste in attesa alla volta. Il tentativo di collegare molti nuovi dispositivi può causare un ritardo nella registrazione dei dispositivi tramite il gateway.

**Avvertenza**

Se il gateway non riesce a registrare un dispositivo automatico, non tenta di registrare di nuovo tale dispositivo per un breve periodo di tempo. Tutti i messaggi o le sottoscrizioni dai dispositivi in errore vengono eliminati durante tale periodo.

## Notifiche gateway
{: #notification}

Quando si verificano degli errori durante la convalida della pubblicazione e della sottoscrizione a un argomento o durante la registrazione automatica, viene inviata una notifica al dispositivo gateway. Un gateway può ricevere tali notifiche tramite la sottoscrizione al seguente argomento, sostituendo i valori `typeId` e `deviceId`:

```
iot-2/type/**typeId**/id/**deviceId**/notify
```
<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/notify</pre>
{: codeblock}

I messaggi ricevuti nell'argomento di notifica utilizzano il seguente formato:

```   
{
   "Request": "<Request_Type>",
   "Time": "<Timestamp>",
   "Topic": "<Topic>",
   "Type": "<Device_Type>",
   "Id": "<Device_Id>",
   "Client": "<Client_ID>",
   "RC": "<Return_Code>",
   "Message": "<Message>"
}
```
Dove
-   `Request_Type` i valori sono `publish` o `subscribe`
-   `Timestamp` è l'ora nel formato ISO 8601
-   `Topic` è l'argomento richiesto dal gateway
-   `Device_Type` è il tipo dispositivo dall'argomento
-   `Device_Id` è l'ID del dispositivo dall'argomento
-   `Client_ID` è l'ID client della richiesta
-   `Return_Code` è il codice di ritorno
-   `Message` è il messaggio di errore

Un gateway può ricevere le seguenti notifiche:

-   L'argomento non corrisponde ad alcuna regola dell'argomento consentita.
-   Il tipo dispositivo non è valido.
-   L'ID del dispositivo non è valido.
-   È stato raggiunto il numero massimo di dispositivi per gateway.
-   È stato raggiunto il numero massimo di dispositivi per organizzazione.
-   Impossibile creare il dispositivo a causa di errori interni.

## Gateway gestiti
{: #managed_gateways}

Il supporto per la gestione del ciclo di vita del dispositivo è facoltativo. Il protocollo di gestione del dispositivo utilizzato da {{site.data.keyword.iot_short_notm}} utilizza la stessa connessione MQTT che utilizza il gateway per il controllo del comando e degli eventi.

### Livelli di QOS (quality of service) e sessione di pulizia
{: #quality_service}

I gateway gestiti possono pubblicare i messaggi con un livello di QOS (quality of service) di 0 o 1.

I messaggi con QoS=0 possono essere scartati e non sono conservati dopo il riavvio del server di messaggistica. I messaggi con QoS=1 possono essere accodati e sono conservati dopo il riavvio del server di messaggistica. La durata della sottoscrizione determina se una richiesta viene accodata. Il parametro `cleansession` della connessione che effettua la sottoscrizione determina la durata della sottoscrizione.  

{{site.data.keyword.iot_short_notm}} pubblica le richieste che hanno un livello QoS di 1 per supportare l'accodamento dei messaggi. Per accodare i messaggi inviati mentre un gateway gestito non è collegato, configura il dispositivo per non utilizzare le sessioni di pulitura impostando il parametro `cleansession` su false.

**Avvertenza**

Quando un gateway gestito utilizza una sottoscrizione durevole, i comandi di gestione del dispositivo che vengono inviati al gateway mentre è offline sono riportati come operazioni non riuscite se il gateway non si ricollega al servizio prima del timeout della richiesta. Quando il gateway si ricollega, queste richieste vengono elaborate dal gateway. Le sottoscrizioni durevoli sono specificate dal parametro `cleansession=false`.

I gateway gestiscono la sessione MQTT, indipendentemente dai dispositivi in essa. Quando un dispositivo invia una richiesta di sottoscrizione a un gateway, la richiesta non viene inoltrata ad altri gateway anche se sono impostate le opzioni `cleansession=false`.

### Argomenti
{: #topics}

Un gateway gestito deve sottoscriversi ai seguenti argomenti per gestire le richieste e le risposte da {{site.data.keyword.iot_short_notm}}:

-   Il gateway gestito si sottoscrive alle risposte di gestione del dispositivo in:  
<pre class="pre">iotdm-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/response/+</pre>
{: codeblock}
-   Il gateway gestito si sottoscrive alle richieste di gestione del dispositivo in:  
<pre class="pre">iotdm-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/+</pre>
{: codeblock}

Un gateway pubblica le seguenti risposte e richieste:

- Le risposte di gestione del dispositivo sono pubblicate in:  
<pre class="pre">iotdevice-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/response/</pre>
{: codeblock}
- Le richieste di gestione del dispositivo sono pubblicate in:  
<pre class="pre">iotdevice-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/</pre>
{: codeblock}

Il gateway può elaborare i messaggi del protocollo di gestione del dispositivo per se stesso o per conto dei dispositivi collegati utilizzando i valori **typeId** e **deviceId** rilevanti.

### Formato del messaggio
{: #msg_format}

Tutti i messaggi sono inviati nel formato JSON.

**Richieste**

Le richieste sono formattate come mostrato nel seguente esempio di codice:

```   
    {  "d": {...}, "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056" }
```

-   `d` contiene tutti i dati rilevanti per la richiesta
-   `reqId` è un identificativo della richiesta e deve essere copiato in una risposta. Se non è richiesta una risposta, il campo non viene utilizzato.

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
-   `rc` è un codice risultato della richiesta originale.
-   `message` è un elemento facoltativo con una descrizione di testo del codice di risposta.
-   `d` è un elemento di dati facoltativo che accompagna la risposta.
-   `reqId` è l'ID della richiesta della richiesta originale. L'ID della richiesta viene utilizzato per collegare le risposte alle richieste e il dispositivo deve assicurarsi che tutti gli ID della richiesta siano univoci. Le risposte alle richieste {{site.data.keyword.iot_short_notm}} devono contenere il valore `reqId` corretto.
