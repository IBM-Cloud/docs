---

copyright:
  years: 2016, 2017
lastupdated: "2017-3-16"
---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be surrounded by 3 dashes.
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Creazione e distribuzione
{: #deliverypipeline_build_deploy}

Il servizio IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} ti consente di implementare un'integrazione continua ripetibile e un processo di distribuzione continua.
{:shortdesc}

Completa le seguenti attività per creare e configurare una pipeline.

## Aggiunta di una fase
{: #deliverypipeline_add_stage}

1. Nella pagina Pipeline, fai clic su **AGGIUNGI FASE**. Viene aperta la pagina di configurazione della fase.
2. Configura la fase.
  1. Nella scheda **INPUT**, seleziona un input per la fase.
  2. Nella scheda **LAVORI**, aggiungi e configura almeno un lavoro. La prima fase normalmente dispone di almeno un lavoro di creazione.
3. Fai clic su **SALVA**.

## Aggiunta di un lavoro a una fase
{: #deliverypipeline_add_job}

1. Nella fase, fai clic sull'icona **Configurazione fase** e fai quindi clic su **Configura fase**.
2. Fai clic sulla scheda **LAVORI**.
3. Fai clic su **AGGIUNGI LAVORO**. Seleziona il tipo di lavoro da aggiungere.
4. Configura il lavoro.
5. Fai clic su **SALVA**.

![Aggiunta di un lavoro a una fase](images/AddJob2.png)

## Esecuzione di una fase
{: #deliverypipeline_run_stage}

Puoi eseguire manualmente una fase facendo clic sull'icona **Esegui fase** nella pagina Pipeline.

![Fare clic sull'icona Esegui fase su una fase](images/RunStage.png)

Puoi anche richiedere distribuzioni e creazioni on-demand dalla pagina della cronologia di creazione in uno dei seguenti due modi:
* Trascina una creazione nella casella nella fase configurata.
* Accanto alla creazione, fai clic sull'icona **Invia a** e seleziona quindi uno spazio a cui eseguire la distribuzione.
  ![La fase di esecuzione con questa icona di creazione](images/deploy_to.png)

Per annullare una fase in esecuzione, nella fase, fai clic su **Visualizza log e cronologia**. Nell'elenco dei lavori, fai clic sul numero di lavori in esecuzione e quindi fai clic su **ANNULLA**. Puoi anche annullare i lavori individualmente facendo clic su un lavoro e quindi su **ANNULLA** o facendo clic sull'icona **Arresta** accanto a un lavoro nella relativa fase.

## Distribuzione di un'applicazione
{: #deliverypipeline_deploy}

Un lavoro di distribuzione configurato correttamente distribuisce la tua applicazione alla tua destinazione quando il lavoro è in esecuzione. Per eseguire manualmente un lavoro di distribuzione, fai clic sull'icona **Esegui fase** della fase in cui si trova il lavoro.

###Revisioni input
Quando esegui una fase manualmente o se viene eseguita perché la fase precedente è stata completata, la fase in esecuzione seleziona la propria revisione dell'input. Generalmente, la revisione dell'input è un numero di build. Per selezionare la revisione dell'input, la fase segue queste condizioni:

* Se viene selezionata una revisione specifica, la utilizza.
* Se non viene specificata una revisione specifica, ricerca nelle fasi precedenti finché non trova una fase che utilizza lo stesso input. Trova e utilizza l'ultima revisione di esecuzione corretta di tale input.
* Se non viene specificata una revisione specifica e nessun'altra fase utilizza l'origine specificata come input, utilizza l'ultima revisione dell'input.

**Suggerimento:** puoi distribuire una creazione precedente. Nella fase che contiene la generazione, fai clic su **Visualizza log e cronologia**. Nella pagina che viene aperta, fai clic per espandere il numero di esecuzione e quindi fai clic sul lavoro di creazione. Fai clic su **INVIA A** e seleziona una destinazione.

###Aggiunta di servizi alle applicazioni
Puoi aggiungere i servizi alle tue applicazioni e gestirli dal tuo dashboard Bluemix o dalla CLI (command line interface) Cloud Foundry. Puoi anche immettere i comandi della CLI Foundry negli script per i lavori della pipeline. Ad esempio, puoi aggiungere un servizio a un'applicazione nello script di un lavoro di distribuzione. Per ulteriori informazioni sull'aggiunta dei servizi, consulta [Aggiunta di un servizio alla tua applicazione](/docs/services/reqnsi.html#add_service).

## Visualizzazione dei log
{: #deliverypipeline_view_logs}

Puoi visualizzare i log per i lavori e visualizzare le fasi poiché sono in esecuzione nella pagina della cronologia della fase.

Per visualizzare un log del lavoro, fai clic sul lavoro. In alternativa, in una fase, fai clic su **Visualizza log e cronologia**.

Per visualizzare il log di runtime di un'applicazione distribuita, fai clic su **Visualizza log di runtime**.

![Le aree in un tile della fase su cui puoi fare clic per aprire i log pertinenti](images/view_logs_and_history.png)

In aggiunta ai log del lavoro, puoi visualizzare i risultati della verifica dell'unità, le risorse utente generate e le modifiche al codice per ogni lavoro di creazione.

Puoi anche eseguire, annullare, o configurare una fase dalla pagina Cronologia fase. Fai clic su **ESEGUI** per eseguire una fase o su **CONFIGURA** per configurarla. Puoi annullare una fase in esecuzione facendo clic sul numero di esecuzione e quindi su **ANNULLA**.
