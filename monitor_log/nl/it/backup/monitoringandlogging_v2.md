---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-14"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Monitoraggio e registrazione
{: #monitoringandlogging}

{{site.data.keyword.Bluemix}} è una piattaforma di elaborazione cloud di {{site.data.keyword.IBM_notm}} progettata per la creazione, esecuzione e gestione di applicazioni e servizi.  {{site.data.keyword.Bluemix_notm}} combina la soluzione PaaS (platform as a service ) con la soluzione IaaS (infrastructure as a service). Inoltre, {{site.data.keyword.Bluemix_notm}} fornisce un ricco catalogo di servizi facilmente integrabili con PaaS e IaaS per creare rapidamente delle applicazioni di business. {{site.data.keyword.Bluemix_notm}} include servizi integrati di registrazione e monitoraggio in tutta la piattaforma.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} offre servizi di registrazione e di monitoraggio tra i diversi servizi di elaborazione, come Cloud Foundry e {{site.data.keyword.containershort}}. Puoi sviluppare, eseguire e gestire le applicazioni in qualsiasi runtime di elaborazione senza la complessità della creazione e manutenzione dell'infrastruttura che è tipicamente associata allo sviluppo e al lancio di un applicazione.  

**Nota:** le funzionalità di monitoraggio e di registrazione sono disponibili nelle regioni Stati Uniti Sud e Regno Unito. 

Puoi utilizzare le funzionalità di monitoraggio in {{site.data.keyword.Bluemix_notm}} per raccogliere e misurare automaticamente le metriche chiave dal tuo ambiente e dalle tue applicazioni. Non è richiesta alcuna strumentazione speciale per raccogliere le metriche. Ad esempio, puoi utilizzare le informazioni fornite dalle metriche delle prestazioni per monitorare in che modo un servizio viene eseguito nel cloud, per individuare colli di bottiglia delle risorse e per controllare lo SLA (service level agreement). Ad esempio, quando analizzi i dati delle prestazioni di un servizio, puoi rilevare delle situazioni che possono causare un collo di bottiglia delle risorse e di conseguenza influire sullo SLA del servizio per i tuoi clienti. Adottando delle azioni tempestive, puoi prevenire situazioni che possono compromettere il tuo business.  

Puoi utilizzare le funzionalità di registrazione in {{site.data.keyword.Bluemix_notm}} per comprendere il funzionamento della piattaforma cloud e delle risorse eseguite al suo interno. Non è richiesta alcuna strumentazione speciale per raccogliere i log di output standard e di errore standard. Ad esempio, puoi utilizzare i log per fornire un audit trail per un'applicazione, rilevare problemi nel tuo servizio, identificare vulnerabilità, risolvere problemi relativi alle distribuzioni delle applicazioni e al funzionamento del runtime, rilevare problemi nell'infrastruttura in cui è in esecuzione l'applicazione, tracciare la tua applicazione tra i componenti della piattaforma cloud e individuare dei modelli da utilizzare per prevenire azioni che potrebbero compromettere il tuo servizio SLA.

## Monitoraggio delle risorse dell'infrastruttura di elaborazione
{: #monitoring_sl_ov}

Ogni server {{site.data.keyword.Bluemix_notm}} include dei report sul monitoraggio di facile lettura che sono sempre disponibili. Per ulteriori informazioni, vedi [Infrastructure Monitoring & Reporting ![icona link esterno](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud-computing/bluemix/infrastructure-monitoring){: new_window}.


## Monitoraggio in {{site.data.keyword.Bluemix}} per i servizi di elaborazione
{: #monitoring_bmx_ov}

Per impostazione predefinita {{site.data.keyword.Bluemix_notm}} raccoglie e visualizza le metriche delle prestazioni per l'utilizzo della CPU, l'utilizzo della memoria e l'I/O di rete. Queste metriche forniscono informazioni relative alle prestazioni delle singole risorse cloud. Puoi monitorare le prestazioni di queste risorse nel tuo ambiente cloud tramite l'IU di {{site.data.keyword.Bluemix_notm}}. Puoi inoltre visualizzare i dati in tempo reale e i dati cronologici. 

Puoi anche configurare e monitorare altre metriche delle prestazioni. Puoi visualizzare e analizzare queste metriche esternamente a {{site.data.keyword.Bluemix_notm}}. Ad esempio, puoi utilizzare Grafana per monitorare altre metriche quando esegui la tua applicazione in {{site.data.keyword.containershort}}. Puoi personalizzare i dashboard per ogni istanza di contenitore o per ogni spazio in cui visualizzi e analizzi i dati delle prestazioni.

![Visualizzazione del monitoraggio Grafana di un contenitore in esecuzione in {{site.data.keyword.Bluemix_notm}}](images/monitoring_default_container_grafana_view.jpg)

Puoi utilizzare il monitoraggio della piattaforma {{site.data.keyword.Bluemix_notm}} per:

* Acquisire informazioni approfondite sulle operazioni dell'applicazione, ad esempio, individuare i potenziali colli di bottiglia o se sono necessari degli aggiornamenti.
* Definire le tendenze che puoi utilizzare per pianificare futuri requisiti di applicazione nella tua piattaforma cloud.

Per ulteriori informazioni sul monitoraggio delle applicazioni eseguite in Cloud Foundry, vedi [Monitoraggio delle applicazioni eseguite in Cloud Foundry](monitoring_cf_apps.html#monitoring_bluemix_apps).

Per ulteriori informazioni sul monitoraggio in {{site.data.keyword.containershort}}, vedi [Monitoraggio in {{site.data.keyword.containershort}}](/docs/containers/monitoringandlogging/container_ml_monitor.html#container_ml_monitor).   

## Registrazione in {{site.data.keyword.Bluemix}}
{: #logging_bmx_ov}

Le funzionalità di registrazione {{site.data.keyword.Bluemix_notm}} sono integrate nella piattaforma e la raccolta dei dati è abilitata automaticamente per le risorse cloud. Per impostazione predefinita, {{site.data.keyword.Bluemix_notm}}, raccoglie e visualizza i log per le tue applicazioni, i runtime delle applicazioni e i runtime di calcolo in cui queste applicazioni vengono eseguite. 

Quando esegui le tue applicazioni nel cloud, potresti non riuscire a stabilire un tunnel SSH o FTP nell'infrastruttura in cui sono in esecuzione le tue applicazioni per accedere ai log, ad esempio se l'applicazione è eseguita in Cloud Foundry. D'altra parte, puoi eseguire la tua applicazione in {{site.data.keyword.containershort}}, un altro runtime di calcolo disponibile in {{site.data.keyword.Bluemix_notm}}, in cui puoi stabilire un tunnel SSH e accedere ai log. Indipendentemente dal runtime di calcolo, l'accesso ai log è critico e {{site.data.keyword.Bluemix_notm}} fornisce un'esperienza comune per visualizzare e analizzare i log nella tua piattaforma cloud.

{{site.data.keyword.Bluemix_notm}} registra i dati di log generati dalla piattaforma Cloud Foundry e dalle applicazioni Cloud Foundry. Nei log, puoi visualizzare gli errori, le avvertenze e i messaggi informativi che vengono generati per la tua applicazione. Per ulteriori informazioni sulla registrazione in Cloud Foundry, vedi [Registrazione per le applicazioni Cloud Foundry in {{site.data.keyword.Bluemix}}](logging_cf_apps.html#logging_bluemix_cf_apps).

{{site.data.keyword.Bluemix_notm}} registra i dati di log generati da {{site.data.keyword.containershort}}. Per ulteriori informazioni sulla registrazione in {{site.data.keyword.containershort}}, vedi [Registrazione in {{site.data.keyword.containershort}}](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_logs).   


Mediante la funzionalità di registrazione offerta da {{site.data.keyword.Bluemix_notm}}, puoi:

* Visualizzare le tue risorse cloud e il modo in cui vengono eseguite.
* Definire le tendenze che ti aiutano a identificare gli scenari che richiedono il tuo intervento.
* Definire i tracciati dei dati per un'applicazione che puoi utilizzare, ad esempio, per il controllo.
* Ridurre il tempo e lo sforzo richiesti per individuare e correggere un problema nell'applicazione. 
* Monitorare la distribuzione delle tue applicazioni nella piattaforma cloud.
* Rilevare l'inattività o l'arresto anomalo di un servizio o un'applicazione.
* Seguire l'esecuzione dell'applicazione e il flusso di dati.
* Identificare vulnerabilità nella tua applicazione.
* Rilevare problemi nell'infrastruttura.
* Rilevare problemi nel runtime dell'applicazione.


