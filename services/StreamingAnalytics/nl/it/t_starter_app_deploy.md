---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Distribuzione delle applicazioni starter su {{site.data.keyword.Bluemix_short}}
{: #starterapps_deploy}

Puoi trasmettere e distribuire una delle applicazioni starter di {{site.data.keyword.streaminganalyticsshort}} al cloud
{{site.data.keyword.Bluemix_short}}.
{:shortdesc}

Prima di iniziare, rendi {{site.data.keyword.Bluemix_short}}
pronto per la distribuzione delle applicazioni starter {{site.data.keyword.streaminganalyticsshort}}:

* [Installa lo strumento di riga di comando cf](https://github.com/cloudfoundry/cli/releases).
* Crea un'applicazione in {{site.data.keyword.Bluemix_short}},
aggiungi il servizio {{site.data.keyword.streaminganalyticsshort}} alla tua applicazione
e riprepara l'applicazione:
	* Per distribuire l'applicazione starter Event Detection, crea un'applicazione con il runtime {{site.data.keyword.sdk4node}}.
	* Per distribuire l'applicazione starter NYC Traffic, crea un'applicazione con il runtime Liberty for
Java™.

Ricorda il nome che fornisci per l'applicazione, ti servirà in seguito. 

{{site.data.keyword.streaminganalyticsshort}} fornisce due applicazioni di esempio
per iniziare ad utilizzare il servizio. 

L'applicazione starter Event Detection
analizza i dati correlati al tempo atmosferico in un flusso in tempo reale e visualizza i risultati delle
analisi. L'applicazione è scritta in {{site.data.keyword.sdk4node}}. Per ulteriori informazioni su come utilizzare l'applicazione starter Event
Detection, consulta [Detect complex events in a real-time data stream](https://www.ibm.com/developerworks/library/ba-bluemix-detect-complex-events-from-data-stream-trs/index.html).

L'applicazione starter
NYC Traffic legge e analizza i dati sul traffico da un sito web pubblico. L'applicazione è scritta in
Liberty for Java™. Per ulteriori informazioni su come utilizzare l'applicazione starter NYC Traffic, vedi [{{site.data.keyword.streaminganalyticsfull}} Starter Application](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-starter-application/). 

Per scaricare e distribuire l'applicazione starter a {{site.data.keyword.Bluemix_short}}:

1. Scarica l'applicazione starter [Event Detection](https://hub.jazz.net/project/streamscloud/EventDetection/overview) o [ NYC Traffic](https://hub.jazz.net/project/streamscloud/NYCTraffic/overview).
2. Nella riga di comando, vai alla directory del progetto.
  <pre><code>cd myapp</code></pre>
 
3. Rinomina la directory del progetto in modo che corrisponda al nome fornito alla tua applicazione in {{site.data.keyword.Bluemix_short}}.
4. Connettiti a {{site.data.keyword.Bluemix_short}}:
  <pre><code>cf api https://api.DomainName</code></pre>
   
5. Accedi a {{site.data.keyword.Bluemix_short}} e configura
la tua organizzazione di destinazione quando richiesto:
   <pre><code>cf login</code></pre>
    
6. Distribuisci la tua applicazione:
  <pre><code>cf push myapp</code></pre>
   
7. Vai alla pagina della panoramica dell'applicazione, accessibile dal dashboard
{{site.data.keyword.Bluemix_short}}, per verificare che la tua applicazione
sia stata avviata correttamente.
8. Avvia l'applicazione per visualizzarla nel browser. Puoi trovare l'URL della tua applicazione (o
"rotta") nella pagina della panoramica dell'applicazione.

Ora che la tua applicazione è in esecuzione, puoi andare al dashboard del servizio per visualizzare lo stato della tua istanza {{site.data.keyword.streaminganalyticsshort}} e per ottenere informazioni sulla risoluzione dei problemi. Per accedere al dashboard
del servizio, vai al dashboard
{{site.data.keyword.Bluemix_short}} e fai clic sul tile
{{site.data.keyword.streaminganalyticsshort}} nella tua
pagina della panoramica dell'applicazione.
