---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Informazioni su Driving Behavior Analysis
{: #iotdriverinsights_overview}
Ultimo aggiornamento: 16 giugno 2016
{: .last-updated}


Driving Behavior Analysis è un servizio che puoi utilizzare per analizzare il comportamento di un guidatore dai dati di analisi e contestuali degli autoveicoli.

{:shortdesc}


## Architettura
{: #drb}

Puoi identificare e analizzare diversi tipi di comportamento di guida in correlazione a velocità, svolte e altre categorie. Puoi ad esempio determinare delle istanze di brusca accelerazione, eccesso di velocità, svolte strette, frenate frequenti o brusche e altri tipi di comportamento del guidatore.

## Configurazione analitica
{: #configurability}  

I parametri di soglia di analisi determinano come vengono rilevati e analizzati i diversi tipi di comportamento del guidatore dai dati contestuali e di analisi degli autoveicoli che vengono passati al sistema. Puoi configurare alcuni dei parametri di soglia per l'analisi del comportamento di guida dalla console di gestione del servizio {{site.data.keyword.iotdriverinsights_short}}. Puoi ad esempio configurare l'intervallo di velocità per il tipo di strada e l'intervallo di angoli di svolta.

Per ulteriori informazioni su come configurare i parametri di soglia per l'analisi di Driving Behavior Analysis, consulta [Configurazione dei parametri per il servizio](drb_iotdriverinsights_admin.html#configureparameters).

### Categorie e attività del comportamento di guida

Le seguenti tabelle elencano i tipi di comportamento di guida per categoria che possono essere rilevati e analizzati dal servizio

#### Tabella 1: tipi di comportamento di guida correlati alla velocità

|Nome comportamento|ID comportamento|Descrizione|
|--------|:-------:|------|
|Brusca accelerazione|1|Viene impostato internamente un valore di soglia di una brusca accelerazione conformemente alla velocità. Una brusca accelerazione viene riconosciuta se i dati relativi all'accelerazione superano il valore di soglia.|
|Brusca frenata|2|Viene impostato internamente un valore di soglia di una brusca decelerazione conformemente alla velocità. Una brusca frenata viene riconosciuta se i dati relativi alla frenata per un viaggio superano il valore di soglia.|
|Eccesso di velocità|3|Viene impostato un valore di soglia di eccesso di velocità per il tipo di strada. L'eccesso di velocità viene riconosciuto se i dati relativi alla velocità per il viaggio superano il valore di soglia. Puoi configurare la soglia per l'eccesso di velocità. |
|Arresto frequente|4|Un arresto viene rilevato quando il valore di velocità è zero. Degli arresti frequenti vengono riconosciuti se ci sono troppe istanze di arresto in uno specifico arco temporale durante il viaggio.|
|Accelerazione frequente|5|Viene impostato internamente un valore di soglia di accelerazione conformemente alla velocità. Un'accelerazione frequente viene rilevata se il guidatore supera frequentemente il valore di soglia entro uno specifico arco temporale durante il viaggio.|
|Frenata frequente|6|Viene impostato internamente un valore di soglia di decelerazione conformemente alla velocità. Una decelerazione frequente viene riconosciuta se il guidatore supera frequentemente il valore di soglia entro uno specifico arco temporale durante il viaggio.|

#### Tabella 2: comportamento di guida correlato alle svolte

|Nome comportamento|ID comportamento|Descrizione|
|-------|:--------:|-------|
|Svolta stretta (svolta ad alta velocità)|7|Viene impostato un valore di soglia di velocità nella svolta. Una svolta stretta viene riconosciuta se il guidatore supera il valore di soglia. Puoi configurare la soglia per la svolta stretta.
|Accelerazione prima della svolta|8|Viene impostato internamente un valore di soglia di accelerazione conformemente alla velocità. Un'accelerazione prima di una svolta viene riconosciuta se il guidatore supera il valore di soglia.
|Eccesso di frenata prima di uscire da una svolta|9|Viene impostato internamente un valore di soglia di decelerazione conformemente alla velocità. Un eccesso di frenata prima di uscire da una svolta viene riconosciuto se il guidatore supera il valore di soglia.

#### Tabella 3: altri tipi di comportamento di guida

|Nome comportamento|ID comportamento|Descrizione|
|-------|:--------:|-------|
|Guida in condizioni di affaticamento|10|Viene impostato internamente un valore di soglia di decelerazione conformemente alla velocità. L'affaticamento in un guidatore viene riconosciuto se la velocità supera il valore di soglia.|


### Contesto di guida
|Categoria del<br/>contesto|ID categoria<br/>del contesto|Nome contesto|ID contesto|
|-------|:-----:|--------|:-------:|
|**Intervallo di tempo**|**4**|\-|\-|
|Intervallo di tempo|4|Giorno|1|
|Intervallo di tempo|4|Notte|2|
|Intervallo di tempo|4|Ore di picco mattutine|3|
|Intervallo di tempo|4|Ore di picco serali|4|
|**Tipo di strada**|**3**|\-|\-|
|Tipo di strada|3|Autostrada|1|
|Tipo di strada|3|Autostrada urbana|2|
|Tipo di strada|3|Strada primaria urbana|3|
|Tipo di strada|3|Strada urbana|4|
|Tipo di strada|3|Altri|5|
|**Schema di velocità**|**0**|\-|\-|
|Schema di velocità|0|Flusso libero|0|
|Schema di velocità|0|Flusso costante|1|
|Schema di velocità|0|Traffico molto intenso|2|
|Schema di velocità|0|Traffico|3|
|Schema di velocità|0|Condizioni miste|4|


## API REST
{: #rest_api}

La API REST {{site.data.keyword.iotdriverinsights_short}} fornisce le richieste che puoi usare per personalizzare e sviluppare le tue applicazioni {{site.data.keyword.Bluemix_notm}}:

 1. Comandi dei dati degli autoveicoli:
   - `sendCarProbeData` invia i dati di analisi degli autoveicoli da analizzare
   - `getCarProbeDataListAsDate` restituisce l'elenco di dati di analisi degli autoveicoli in base alla data
   - `deleteCarProbeDataListByDate` elimina i dati di analisi degli autoveicoli
 2. Comandi dei lavori di analisi:
   - `sendJobRequest` invia la richiesta di lavoro di analisi del comportamento di guida
   - `getJobInfo` restituisce le informazioni del lavoro specificato
   - `getJobInfoList` restituisce l'elenco di informazioni sul lavoro
 3. Comandi dei risultati dell'analisi:
   - `getAnalyzedTripSummaryList` restituisce l'elenco di informazioni di riepilogo delle traiettorie analizzate
   - `getAnalyzedTripInfo` restituisce le informazioni della traiettoria analizzata specificata
   - `deleteJobResult` elimina tutti i risultati analizzati correlati a un lavoro

Per ulteriori informazioni, consulta la documentazione della [API {{site.data.keyword.iotdriverinsights_short}}](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}.

## Infrastruttura di analisi dei Big Data
{: #big_data_analysis_infrastructure}
{{site.data.keyword.iotdriverinsights_short}} utilizza Hadoop come infrastruttura di back-end. Hadoop fornisce un'elevata scalabilità, consentendo così al
servizio {{site.data.keyword.iotdriverinsights_short}} di richiamare e analizzare grossi volumi di dati contestuali e di analisi relativi agli autoveicoli.
