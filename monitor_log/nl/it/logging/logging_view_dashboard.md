---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-27"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analisi dei log dalla console Bluemix
{: #analyzing_logs_bmx_ui}

In {{site.data.keyword.Bluemix}}, puoi visualizzare, filtrare e analizzare i log attraverso la scheda log disponibile per ogni applicazione Cloud Foundry o contenitore Docker.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} pubblico offre funzionalità di registrazione integrate. Ad esempio, quando esegui le tue applicazioni in Cloud Foundry (CF), i dati di log vengono acquisiti dai componenti del sistema che interagiscono con la tua applicazione, relativi all'applicazione e anche i dati di log dall'interno dell'applicazione quando utilizzi stdout e stderr.

Tieni conto delle seguenti informazioni sulla disponibilità dei dati di log per l'analisi e sulla conservazione del log:

* In {{site.data.keyword.Bluemix_notm}} pubblico, i dati dei log vengono memorizzati per 7 giorni per impostazione predefinita. 
* Puoi archiviare fino a 1 GB di dati al giorno. 
* Per impostazione predefinita, i log disponibili per l'analisi dalla console {{site.data.keyword.Bluemix_notm}} includono i dati delle ultime 24 ore.

**Suggerimento:** per analizzare i dati per un periodo personalizzato precedente alle ultime 24 ore, consulta [Analisi log avanzata con Kibana](logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana). 

##  Passaggio ai log di un'applicazione Cloud Foundry
{: #launch_logs_tab_bmx_ui_cf}

Per visualizzare i log di distribuzione o di runtime di un'applicazione Cloud Foundry, completa la seguente procedura:

1. Dal dashboard Applicazioni, fai clic sul nome della tua applicazione Cloud Foundry. 
    
2. Dalla pagina dei dettagli dell'applicazione, fai clic su **Log**.
    
    Dalla scheda **Log**, puoi visualizzare in tempo reale i log recenti riguardanti la tua applicazione o le parti finali dei log. Inoltre, puoi filtrare i log in base al componente (tipo di log), all'ID istanza dell'applicazione e all'errore.
    

##  Passaggio ai log di un contenitore Docker
{: #launch_logs_tab_bmx_ui_containers}

Per visualizzare i log di distribuzione o di runtime di un contenitore Docker, completa la seguente procedura:

1. Dal dashboard Applicazioni, fai clic sul singolo contenitore o sul gruppo di contenitori 
    
2. Dalla pagina dei dettagli dell'applicazione, fai clic su **Monitoraggio e log**.

3. Seleziona la scheda **Registrazione**.
    
    Dalla scheda **Registrazione**, puoi visualizzare in tempo reale i log recenti riguardanti il tuo contenitore o le parti finali dei log. 

## Formato dei log dell'applicazione CF
{: #log_format_cf}

I log per le applicazioni Cloud Foundry {{site.data.keyword.Bluemix_notm}} vengono visualizzati in un formato fisso, simile al seguente modello:

<code><var class="keyword varname">Component</var>/<var class="keyword varname">instanceID</var>/<var class="keyword varname">message</var>/<var class="keyword varname">timestamp</var></code>

Ogni voce di log contiene i seguenti campi:

| Campo | Descrizione |
|-------|-------------|
| Data/ora | L'ora dell'istruzione di log. La data e ora è definita fino al millisecondo. |
| Componente | Il componente che produce il log. Per l'elenco dei diversi componenti, consulta [Origini del log per le applicazioni CF](logging_cf_apps.html#logging_bluemix_cf_apps_log_sources). <br> Ogni tipo di componente è seguito da una barra e da un numero che indica l'istanza dell'applicazione. 0 è il numero assegnato alla prima istanza, 1 è il numero assegnato alla seconda e così via. |
| Messaggio | Il messaggio che viene emesso dal componente. Il messaggio varia a seconda dal contesto. |
{: caption="Tabella 1. Campi per le voci di log dell'applicazione CF" caption-side="top"}


## Formato dei log dei log del contenitore
{: #log_format_containers}

I log per i contenitori vengono visualizzati in un formato fisso, simile al seguente modello:

<code><var class="keyword varname">timestamp</var>/<var class="keyword varname">machine</var>/<var class="keyword varname">message</var>  </code>

Ogni voce di log contiene i seguenti campi:

| Campo | Descrizione |
|-------|-------------|
| Data/Ora | L'ora dell'istruzione di log. La data e ora è definita fino al millisecondo. |
| Macchina | Il nome host in cui il contenitore è in esecuzione. |
| Messaggio | Il messaggio che viene emesso. Il messaggio varia a seconda dal contesto. |
{: caption="Tabella 2. Campi per le voci di log del contenitore Docker" caption-side="top"}

