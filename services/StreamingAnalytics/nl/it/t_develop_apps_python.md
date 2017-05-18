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

# Sviluppo di applicazioni Python per {{site.data.keyword.streaminganalyticsshort}}
{: #t_develop_apps_python}

Puoi ora sviluppare applicazioni Python in IBM DSX (Data Science Experience) o nel tuo ambiente di sviluppo Python locale e distribuire queste applicazioni in {{site.data.keyword.streaminganalyticsshort}}.
{:shortdesc}

Sviluppa e distribuisci le tue applicazioni Python al cloud {{site.data.keyword.Bluemix_short}} utilizzando il servizio {{site.data.keyword.streaminganalyticsshort}} ricorrendo a uno di questi metodi:


## Sviluppo di applicazioni Streams Python in DSX
{: #t_develop_python_dsx}

Se non hai un ambiente di sviluppo Python, il modo più facile per iniziare è utilizzare i nostri notebook in DSX e creare delle applicazioni Python di esempio per il servizio {{site.data.keyword.streaminganalyticsshort}}. Questi notebook forniscono la procedura e gli esempi di codice per creare e distribuire delle semplici applicazioni Python per il servizio {{site.data.keyword.streaminganalyticsshort}} nell'ambiente Python DSX:

* [Hello World!](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039ca9c6e8): Crea una semplice applicazione Hello World! per iniziare e distribuisci quindi l'applicazione a un'istanza del servizio {{site.data.keyword.streaminganalyticsshort}}.

* [Healthcare Demo](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039cad29a6): crea un'applicazione che integra e analizza i dati di gestione flussi da un feed e visualizza quindi i dati nel notebook. Invii infine questa applicazione all'istanza del servizio {{site.data.keyword.streaminganalyticsshort}}.

* [Neural Net Demo](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039ca60bb7): crea un dataset di esempio, crea un modello per i dati di esempio, utilizza tale modello in un'applicazione di gestione flussi, visualizzare i dati di gestione flussi e, infine, invia l'applicazione di gestione flussi al servizio {{site.data.keyword.streaminganalyticsshort}}-

## Sviluppo di applicazioni nel tuo ambiente Python locale
 {: #t_develop_python_api}

 La [API dell'applicazione {{site.data.keyword.streamsshort}} Python](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features), che è inclusa nel pacchetto streamsx, consente di creare delle applicazioni di elaborazione della gestione flussi utilizzando le funzioni o le classi richiamabili Python . Puoi utilizzare l'API dell'applicazione Python per definire, e quindi inviare, l'applicazione al servizio.

Inizia attenendoti alla procedura nell'esercitazione [Developing for the {{site.data.keyword.streaminganalyticsshort}} service](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html) per creare un'applicazione di esempio nel tuo ambiente Python locale e distribuirla al servizio {{site.data.keyword.streaminganalyticsshort}}.
