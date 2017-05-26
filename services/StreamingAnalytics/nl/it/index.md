---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Introduzione a {{site.data.keyword.streaminganalyticsshort}}
{: #gettingstarted}

{{site.data.keyword.streaminganalyticsshort}} è fornito da
{{site.data.keyword.streamsshort}}, una piattaforma di analisi avanzata
che puoi utilizzare per inserire, analizzare e correlare le informazioni come arrivano da diversi tipi
di origini dati in tempo reale. Quando crei un'istanza del servizio {{site.data.keyword.streaminganalyticsshort}},
ottieni la tua propria istanza {{site.data.keyword.streamsshort}} in esecuzione nel cloud
{{site.data.keyword.Bluemix_short}}, pronta per eseguire le tue applicazioni
{{site.data.keyword.streamsshort}}.
{:shortdesc}

Inizia a utilizzare subito {{site.data.keyword.streaminganalyticsshort}} eseguendo le [applicazioni starter](/docs/services/StreamingAnalytics/c_starterapps.html){:new_window}.

Per iniziare a utilizzare {{site.data.keyword.streaminganalyticsshort}}, usa uno dei seguenti metodi per inviare il bundle dell'applicazione (file .sab) associato alla tua applicazione SPL, Java™, Python o Scala Streams:
* Usa il pulsante **Invia lavoro** nella console {{site.data.keyword.streaminganalyticsshort}}.
* Sviluppa un'applicazione {{site.data.keyword.Bluemix_short}} e aggiungi l'applicazione
{{site.data.keyword.streamsshort}} ad essa. Controllala utilizzando l'[API REST {{site.data.keyword.streaminganalyticsshort}}](https://console.ng.bluemix.net/apidocs/220).


Usa {{site.data.keyword.streaminganalyticsshort}} con altri servizi {{site.data.keyword.Bluemix_short}}, compresi {{site.data.keyword.cloudant}} e {{site.data.keyword.messagehub}}. Consulta le [Esercitazioni per l'integrazione con altri servizi {{site.data.keyword.Bluemix_short}}](/docs/services/StreamingAnalytics/r_integrating_cloudant_rest.html){:new_window} per gli esempi che ti renderanno subito operativo.

Se vuoi fare ancora di più con le tue applicazioni, puoi ottenere un ambiente di sviluppo {{site.data.keyword.streamsshort}} e devi preparare la tua applicazione per il cloud. Se non disponi di un ambiente {{site.data.keyword.streamsshort}}, puoi scaricare {{site.data.keyword.streamsshort}} Quick Start Edition, dalla pagina del prodotto [{{site.data.keyword.streamsshort}}](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products) gratuitamente

Se non hai familiarità con la distribuzione dell'applicazione {{site.data.keyword.streamsshort}}, sono presenti delle risorse per aiutarti nell'apprendimento. Per ulteriori informazioni, vedi [{{site.data.keyword.streamsshort}} Knowledge Center.](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}

Se già disponi di un'applicazione SPL che esegui in loco, devi [preparare la tua applicazione per il cloud.](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud/){:new_window}

**Nota:** devi compilare le applicazioni in RHEL (Red Hat Enterprise Linux) 6.5 o una versione CentOS equivalente utilizzando processori Intel.

## {{site.data.keyword.streamsshort}} Applicazioni Python per {{site.data.keyword.streaminganalyticsshort}}
{: #gettingstarted_py notoc}

Puoi ora creare delle applicazioni Streams in un ambiente Python, come IBM DSX (Data Science Experience), e inviare queste applicazioni all'istanza {{site.data.keyword.streaminganalyticsshort}} da distribuire nel cloud Bluemix. Non hai più bisogno di installare {{site.data.keyword.streamsshort}} in locale per compilare e distribuire un'applicazione Streams Python.

Inizia creando delle applicazioni Streams Python di esempio utilizzando i notebook Jupyter in DSX e invia queste applicazioni all'istanza del servizio direttamente da DSX. Per ulteriori informazioni, vedi [Sviluppo di applicazioni Streams Python in DSX](/docs/services/StreamingAnalytics/t_develop_apps_python.html#t_develop_python_dsx).

{{site.data.keyword.streaminganalyticsshort}} supporta anche la distribuzione di applicazioni Streams dal tuo ambiente Python locale . Devi utilizzare la [API dell'applicazione {{site.data.keyword.streamsshort}} Python](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features), che è inclusa nel pacchetto streamsx, per sviluppare le tue applicazioni Streams Python in locale e inviarle all'istanza del servizio. Per iniziare, attieniti alla procedura nell'esercitazione [Developing for the {{site.data.keyword.streaminganalyticsshort}} service](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html).
