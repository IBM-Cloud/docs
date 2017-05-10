---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Registrazione per le applicazioni CF in un ambiente dedicato e locale
{: #hybrid_apps_logs_ov}

In {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm}}, le applicazioni Cloud Foundry sono fornite con la registrazione integrata. Puoi rivedere i dati raccolti dalle tue applicazioni nella console {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Le applicazioni Cloud Foundry utilizzano il  Loggregator per monitorare e inoltrare i log dall'esterno dell'applicazione. Non devi installare gli agent nell'applicazione.

## Requisiti hardware


| **Requisito** |    **1 nodo**     | **3 nodi per l'alta disponibilità** |
|-----------------|-------------------|-------------------|
| vCPU | 19 | 57 |
| Memoria | 80 GB | 240 GB |
| Memoria locale | 2.98 TB | 8.94 TB |
{: caption="Tabella 2. Registrazione dei requisiti hardware per {{site.data.keyword.Bluemix_local_notm}}" caption-side="top"}

## Configurazione

In {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm}}, i log sono attivi per tutte le applicazioni per impostazione predefinita. Per visualizzare le informazioni sulla lettura dei log standard, consulta [Registrazione per le applicazioni in esecuzione su Cloud Foundry](../logging_cf_apps.html#logging_bluemix_cf_apps). In aggiunta, può essere abilitata la registrazione avanzata negli ambienti {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm}}.

* Per confermare che la registrazione avanzata è abilitata nei tuoi ambienti {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm}}, segui le istruzioni in [Visualizzazione dei log](#hybrid_apps_logs_dash). Se non visualizzi il pulsante **Vista avanzata**, questa funzione non è abilitata.

* Per aggiungere la registrazione avanzata al tuo ambiente, segui le istruzioni nella documentazione [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) o [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local).

## Conservazione log

Nelle applicazioni Cloud Foundry {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm}}, i dati dei log vengono memorizzati per 30 giorni per impostazione predefinita.

## Visualizzazione dei log per le applicazioni Cloud Foundry in un ambiente dedicato e locale
{: #hybrid_apps_logs_dash}

Puoi rivedere i log per le applicazioni che stai eseguendo in {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm}}.
{:shortdesc}

Per visualizzare i tuoi log delle applicazioni, segui queste istruzioni.
1. Seleziona un'applicazione in esecuzione.
2. Fai clic su **Log**. Nella vista **Log**, puoi visualizzare i log dalla tua applicazione in esecuzione.
4. Fai clic sul pulsante **Vista avanzata**. **Vista avanzata** mostra una vista più dettagliata dei log utilizzando Kibana, uno strumento di visualizzazione che utilizza i log e i dati con data/ora per creare le visualizzazioni personalizzate. Per ulteriori informazioni sull'utilizzo della vista avanzata, consulta la documentazione di [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html).

Successivamente, puoi personalizzare un dashboard Kibana. Per ulteriori informazioni, vedi [Analisi dei log in Kibana](../logging_view_kibana3.html#analyzing_logs_Kibana3).
