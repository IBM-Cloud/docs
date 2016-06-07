---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Informazioni su {{site.data.keyword.iotdriverinsights_short}}
{: #iotdriverinsights_overview}

Puoi utilizzare {{site.data.keyword.iotdriverinsights_full}} per analizzare il comportamento del conducente dai dati di analisi delle vetture e dai dati di contesto.
{:shortdesc}

## Analisi del comportamento del conducente
{: #driver_behavior_analysis}
Puoi analizzare il comportamento del conducente, come ad esempio delle brusche accelerazioni o frenate, delle frenate frequenti, l'eccesso di velocità, delle svolte strette e altre azioni dai dati di analisi delle vetture e dai dati di contesto.

Sono inclusi le attività e i contesti di seguito indicati:
 - Comportamenti di guida 
    - Correlati alla velocità
       - Brusca accelerazione
       - Brusca frenata
       - Eccesso di velocità
       - Arresti frequenti
       - Accelerazione frequente
       - Frenata frequente
    - Correlati alle svolte
       - Svolta stretta (svolta ad alta velocità)
       - Accelerazione prima della svolta
       - Eccesso di frenata durante una svolta
    - Altri
       - Guida in condizioni di affaticamento
 - Contesto di guida
    - Intervallo di tempo
       - Ore di picco mattutine
       - Ore di picco serali
       - Giorno
       - Notte
    - Tipo di strada
       - Autostrada
       - Autostrada urbana
       - Strada primaria urbana
       - Strada urbana
       - Altre
    - Modello di velocità basato sul tipo di strada
       - Flusso libero
       - Flusso costante
       - Traffico
       - Traffico molto intenso
       - Condizioni miste

## Infrastruttura di analisi dei Big Data
{: #big_data_analysis_infrastructure}
{{site.data.keyword.iotdriverinsights_short}} utilizza Hadoop come infrastruttura di back-end. Hadoop consente a {{site.data.keyword.iotdriverinsights_short}} di realizzare un'elevata scalabilità per l'analisi dei Big Data dai dati di analisi delle vetture e dai dati contesto.

## API REST
{: #rest_api}
Gli sviluppatori possono richiamare i risultati dell'analisi dall'API REST e utilizzarli nell'applicazione {{site.data.keyword.Bluemix_notm}}.
 1. Dati suoi veicoli
   - `sendCarProbeData` invia i dati di analisi delle vetture da analizzare.
   - `getCarProbeDataListAsDate` restituisce l'elenco di dati di analisi delle vetture in base alla data.
   - `deleteCarProbeDataListByDate` elimina i dati di analisi delle vetture.
 2. Lavoro di analisi
   - `sendJobRequest` invia la richiesta di lavoro di analisi del comportamento di guida.
   - `getJobInfo` restituisce le informazioni del lavoro specificato.
   - `getJobInfoList` restituisce l'elenco di informazioni sul lavoro.
 3. Risultati dell'analisi 
   - `getAnalyzedTripSummaryList` restituisce l'elenco di informazioni di riepilogo delle traiettorie analizzate.
   - `getAnalyzedTripInfo` restituisce le informazioni della traiettoria analizzata specificata.
   - `deleteJobResult` elimina tutti i risultati analizzati correlati a un lavoro.

## Configurabilità
{: #configurability}
Alcuni dei parametri di soglia dell'analisi (come l'intervallo di velocità per il tipo di strada, l'intervallo di angoli di svolta e così via) possono essere configurati dall'interfaccia utente (IU).
