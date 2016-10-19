---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# API REST HTTP per i dispositivi
{: #api}
Ultimo aggiornamento: 09 settembre 2016
{: .last-updated}

**Importante:** l'API REST HTTP {{site.data.keyword.iot_full}} per la funzione dei dispositivi è disponibile solo come parte di un programma beta limitato. Futuri aggiornamenti possono includere modifiche incompatibili con la versione corrente di questa funzione. Provala e [facci sapere cosa ne pensi](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html).

## Accesso all'API REST HTTP
{: #api_link}

Per accedere all'API REST HTTP {{site.data.keyword.iot_short_notm}} e ottenere ulteriori informazioni su come integrare i dispositivi nella tua organizzazione, vai all'indirizzo  https://docs.internetofthings.ibmcloud.com/swagger/v0002.html.

L'unica versione dell'API REST HTTP {{site.data.keyword.iot_short_notm}} supportata è la versione 2. Assicurati che le tue soluzioni {{site.data.keyword.iot_short_notm}} utilizzino la versione 2.

# API di messaggistica REST HTTP per i dispositivi 
{: #rest_messaging_api}

## Pubblicazione eventi
{: #event_publication}

In aggiunta all'utilizzo del protocollo di messaggistica MQTT, puoi anche configurare i tuoi dispositivi a pubblicare eventi {{site.data.keyword.iot_short_notm}} in HTTP utilizzando i comandi API REST HTTP.

Utilizza uno dei seguenti URL per inviare una richiesta `POST` da un dispositivo collegato a {{site.data.keyword.iot_short_notm}}:

### Richiesta POST non sicura 
<pre class="pre">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### Richiesta POST sicura 
<pre class="pre">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

Se stai collegando un dispositivo o un'applicazione al servizio Quickstart, invece utilizza uno dei seguenti URL:

### Richiesta POST non sicura a Quickstart
<pre class="pre">http://quickstart.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### Richiesta POST sicura a Quickstart
<pre class="pre">https://quickstart.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

**Note importanti:**
- Nella versione dell'API REST HTTP corrente, puoi inviare gli eventi del dispositivo solo utilizzando la messaggistica HTTP. Utilizza il protocollo di messaggistica MQTT per inviare richieste per la gestione di un altro dispositivo o per le funzioni di controllo.
- Le connessioni HTTP possono essere riutilizzate per pubblicare eventi solo per lo stesso dispositivo poiché l'intestazione HTTP non può essere modificata.

### Autenticazione

Tutte le richieste devono includere un'intestazione di autorizzazione. L'autenticazione di base è l'unico metodo supportato. Quando un dispositivo effettua una richiesta HTTP tramite l'API REST HTTP {{site.data.keyword.iot_short_notm}}, sono necessarie le seguenti credenziali:

```
username = "use-token-auth"
password = Authentication token
```

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
