---



copyright:

  years: 2016, 2017

lastupdated: "2016-10-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

<!-- audience blue staging only begin -->

# Monitoraggio e registrazione di applicazioni Cloud Foundry in un ambiente dedicato e locale
{: #dedicated_apps_ml_ov}


In {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm:}}, le applicazioni Cloud Foundry sono fornite con la registrazione integrata. Puoi rivedere i dati raccolti dalle tue applicazioni nella console {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Le applicazioni Cloud Foundry utilizzano il  Loggregator per monitorare e inoltrare i log dall'esterno dell'applicazione. Non devi installare gli agent nell'applicazione.

## Requisiti hardware


| **Requisito** |    **1 nodo**     | **3 nodi per l'alta disponibilità** |
|-----------------|-------------------|-------------------|
vCPU | 19 | 57 |
Memoria | 80 GB | 240 GB |
Memoria locale | 2.98 TB | 8.94 TB |
{: caption="Table 1. Logging hardware requirements for {{site.data.keyword.Bluemix_local_notm:}}" caption-side="top"}

## Configurazione

In {{site.data.keyword.Bluemix}} dedicato e {{site.data.keyword.Bluemix}} locale, i log sono attivi per tutte le applicazioni per impostazione predefinita. Per visualizzare le informazioni sulla lettura dei log standard, vedi Registrazione per le applicazioni eseguite su Cloud Foundry. Inoltre, è possibile abilitare la registrazione avanzata negli ambienti {{site.data.keyword.Bluemix}} dedicato e {{site.data.keyword.Bluemix}} locale.

## Conservazione log

Nelle applicazioni Cloud Foundry di {{site.data.keyword.Bluemix}} dedicato e {{site.data.keyword.Bluemix}} locale, i dati dei log vengono memorizzati per 30 giorni per impostazione predefinita.

## Visualizzazione dei log per le applicazioni Cloud Foundry in {{site.data.keyword.Bluemix}} dedicato e {{site.data.keyword.Bluemix}} locale
{: #dedicated_apps_ml_logs_dash}

Puoi riesaminare i log delle applicazioni in esecuzione in {{site.data.keyword.Bluemix_notm}} dedicato e {{site.data.keyword.Bluemix_notm}} locale.
{:shortdesc}

Per visualizzare i tuoi log delle applicazioni, segui queste istruzioni.
1. Seleziona un'applicazione in esecuzione.
2. Fai clic su **Log**. Nella vista **Log**, puoi visualizzare i log dalla tua applicazione in esecuzione.
4. Fai clic sul pulsante **Vista avanzata**. **Vista avanzata** mostra una vista più dettagliata dei log utilizzando Kibana, uno strumento di visualizzazione che utilizza i log e i dati con data/ora per creare le visualizzazioni personalizzate. Per ulteriori informazioni sull'utilizzo della vista avanzata, consulta la documentazione di [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html).

Successivamente, puoi personalizzare un dashboard Kibana. Per ulteriori informazioni, consulta [Personalizzazione della visualizzazione del log nel dashboard Kibana](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_dash_logs_custom).

<!-- audience blue staging only end comment -->
