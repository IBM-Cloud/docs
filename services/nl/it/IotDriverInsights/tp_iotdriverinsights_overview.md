---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Informazioni su Trajectory Pattern Analysis
{: #tp_iotdriverinsights_overview}
Ultimo aggiornamento: 16 giugno 2016
{: .last-updated}

La API Trajectory Pattern Analysis è un servizio fornito da {{site.data.keyword.iotdriverinsights_full}} che puoi utilizzare per analizzare gli schemi O/D (Origine/Destinazione) e di rotta dei viaggi in auto dai dati di analisi degli autoveicoli.

{:shortdesc}

## Analisi degli schemi di traiettoria delle rotte
{: #tpa}

Puoi identificare e analizzare schemi O/D e di rotta per più viaggi in auto.
Il seguente diagramma mostra un semplice esempio degli schemi O/D e di rotta di un veicolo (veicolo-1) presi da più viaggi. In questo esempio, Trajectory Pattern Analysis identifica due schemi O/D:
- Uno schema O/D da Casa (Origine1) a Ufficio (Destinazione1) che ha due schemi di rotta
- Uno schema O/D da Casa (Origine1) a Negozio (Destinazione2) che ha uno schema di rotta.

![esempio di rotta O/D](images/tp_odroute_example.png "Esempio di schema O/D e di rotta")

Trajectory Pattern Analysis calcola anche alcune metriche di diversità nella guida per ciascun veicolo come elencato nella seguente tabella. Puoi utilizzare queste metriche per giudicare le caratteristiche di guida di un guidatore.

|Nome metrica|Descrizione|
|:---|:---|
|Rapporto O/D unico|Il rapporto tra il numero di viaggi che non sono coperti da schemi O/D e il numero totali di viaggi immessi.|
|Rapporto chilometraggio unico|Il rapporto del chilometraggio che non è coperto da schemi di rotta e il chilometraggio totale dei viaggi immessi.|
|Rapporto viaggio unico|Il rapporto del numero di viaggi che non sono coperti dagli schemi di rotta e il numero totale di viaggi immessi.|


## API REST
{: #rest_api}

La API REST Trajectory Pattern Analysis fornisce le richieste che puoi usare per personalizzare e sviluppare le tue applicazioni {{site.data.keyword.Bluemix_notm}}:

 1. Comandi dei dati degli autoveicoli:
   - `sendCarProbeData` invia i dati di analisi degli autoveicoli da analizzare
   - `getCarProbeDataListAsDate` restituisce l'elenco di dati di analisi degli autoveicoli in base alla data
   - `deleteCarProbeDataListByDate` elimina i dati di analisi degli autoveicoli
 2. Comandi dei lavori di analisi:
   - `sendJobRequest` invia la richiesta di lavoro di analisi degli schemi di traiettoria
   - `getJobInfo` restituisce le informazioni del lavoro specificato
   - `getJobInfoList` restituisce l'elenco di informazioni sul lavoro
 3. Comandi dei risultati dell'analisi:
   - `getResultSummary` restituisce le informazioni di riepilogo analizzate dell'analisi degli schemi di traiettoria
   - `getAnalyzedODDetail` restituisce le informazioni dettagliate dello schema O/D analizzato specificato
   - `getRouteGPSList` restituisce l'elenco di informazioni GPS dello schema di rotta analizzata specificato
   - `getODList` restituisce l'elenco di informazioni sugli schemi O/D degli argomenti specificati
   - `deleteJobResult` elimina tutti i risultati analizzati correlati a un lavoro

Per ulteriori informazioni, consulta la documentazione della [API {{site.data.keyword.iotdriverinsights_short}}](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}.
