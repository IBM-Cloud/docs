---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Registrazione per le applicazioni Cloud Foundry in Bluemix
{: #logging_bluemix_cf_apps}

In {{site.data.keyword.Bluemix}}, puoi visualizzare, filtrare e analizzare i log Cloud Foundry (CF) attraverso il dashboard {{site.data.keyword.Bluemix_notm}}, Kibana e l'interfaccia riga di comando. Inoltre, puoi trasmettere i record dei log a uno strumento di gestione log esterno. 
{:shortdesc}

Quando esegui le tue applicazioni in un PaaS (platform-as-a-service) cloud come Cloud Foundry su {{site.data.keyword.Bluemix_notm}}, non puoi stabilire un tunnel SSH o FTP nell'infrastruttura in cui sono in esecuzione le tue applicazioni per accedere ai log. La piattaforma è controllata dal provider del cloud. Le applicazioni Cloud Foundry in esecuzione su {{site.data.keyword.Bluemix_notm}} utilizzano il componente Loggerator per inoltrare i record di log dall'interno dell'infrastruttura Cloud Foundry. Loggregator raccoglie automaticamente i dati STDOUT e STDERR. Puoi visualizzare e analizzare questi log attraverso il dashboard {{site.data.keyword.Bluemix_notm}}, Kibana e l'interfaccia riga di comando.

La seguente figura mostra una visualizzazione di alto livello della registrazione di applicazioni Cloud Foundry in {{site.data.keyword.Bluemix_notm}}:

![Panoramica dei componenti di alto livello per le applicazioni CF](../images/logging_cf_apps_ov.jpg "Panoramica dei componenti di alto livello per le applicazioni CF")
 
La registrazione delle applicazioni Cloud Foundry viene abilitata automaticamente quando utilizzi l'infrastruttura Cloud Foundry per eseguire le tue applicazioni su {{site.data.keyword.Bluemix_notm}}. Per visualizzare i log del runtime Cloud Foundry, devi scrivere i tuoi log in STDOUT e STDERR. Per ulteriori informazioni, vedi [Registrazione delle applicazioni di runtime attraverso le applicazioni CF](logging_writing_to_log_from_cf_app.html#logging_writing_to_log_from_cf_app).

{{site.data.keyword.Bluemix_notm}} conserva una quantità limitata di informazioni di log. Quando si registrano le informazioni, i dati precedenti vengono sostituiti con le informazioni più recenti. Se devi rispettare le politiche organizzative o di settore che richiedono di mantenere una parte o tutte le informazioni di log per scopi di controllo o altro, puoi trasmettere i tuoi log a un host di log esterno, quale un servizio di gestione log di terze parti o un altro host. Per ulteriori informazioni, vedi [Configurazione di host log esterni](../external/logging_external_hosts.html#thirdparty_logging).

## Metodi per analizzare i log dell'applicazione CF
{: #logging_bluemix_cf_apps_log_methods}

Puoi scegliere uno dei seguenti metodi per analizzare i log della tua applicazione Cloud Foundry:

* Analizza il log in {{site.data.keyword.Bluemix_notm}} per visualizzare l'ultima attività dell'applicazione.
    
    In {{site.data.keyword.Bluemix_notm}}, puoi visualizzare, filtrare e analizzare i log attraverso la scheda **Log** disponibile per ogni applicazione Cloud Foundry. Per ulteriori informazioni, vedi [Analisi dei log dell'applicazione CF dal dashboard Bluemix](../logging_view_dashboard.html#analyzing_logs_bmx_ui).
    
* Analizza i log in Kibana per eseguire attività di analisi avanzate.
    
    In {{site.data.keyword.Bluemix}}, puoi utilizzare Kibana, una piattaforma di analisi e visualizzazione open source, per monitorare, ricercare, analizzare e visualizzare i tuoi dati in una varietà di grafici, ad esempio, diagrammi e tabelle. Per ulteriori informazioni, vedi [Analisi dei log in Kibana](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana).

* Analizza i log attraverso la CLI per utilizzare i comandi per la gestione dei log a livello di programmazione.
    
    In {{site.data.keyword.Bluemix}}, puoi visualizzare, filtrare e analizzare i log attraverso l'interfaccia riga di comando utilizzando il comando **cf logs**. Per ulteriori informazioni, vedi [Analisi dei log dell'applicazione Cloud Foundry dall'interfaccia riga di comando](../logging_view_cli.html#analyzing_logs_cli).


## Origini log per le applicazioni CF
{: #logging_bluemix_cf_apps_log_sources}

Per la applicazioni Cloud Foundry (CF), sono disponibili le seguenti origini log:
    
| Origine log | Nome componente | Descrizione | 
|------------|----------------|-------------|
| LGR | Loggregator | Il componente LGR fornisce informazioni relative al Loggregator Cloud Foundry, che inoltra i log dall'interno di Cloud Foundry. |
| RTR | Router | Il componente RTR fornisce informazioni sulle richieste HTTP a un'applicazione. | 
| STG | In fase di preparazione | Il componente STG fornisce informazioni su come viene preparata o ripreparata un'applicazione. | 
| APP | Applicazione | Il componente APP fornisce i log dall'applicazione. Qui è dove vengono mostrati i stderr e stdout nel tuo codice. | 
| API | API Cloud Foundry | Il componente API fornisce informazioni sulle azioni interne che derivano dalla richiesta di un utente di modificare lo stato di un'applicazione. | 
| DEA | Droplet Execution Agent | Il componente DEA fornisce informazioni sull'avvio, l'interruzione o l'arresto anomalo di un'applicazione. <br> Questo componente è disponibile solo se la tua applicazione viene distribuita nell'architettura Cloud Foundry basata su DEA. | 
| CELL | Cella Diego | Il componente CELL fornisce informazioni sull'avvio, l'interruzione o l'arresto anomalo di un'applicazione. <br> Questo componente è disponibile solo se la tua applicazione viene distribuita nell'architettura Cloud Foundry basata su Diego.|
| SSH | SSH | Il componente SSH fornisce informazioni ogni volta che un utente accede a un'applicazione utilizzando il comando **cf ssh**. Questo componente è disponibile solo se la tua applicazione viene distribuita nell'architettura Cloud Foundry basata su Diego. |
{: caption="Tabella 1. Origini log" caption-side="top"}

La seguente figura mostra i diversi componenti (origini log ) in un'architettura Cloud Foundry basata su DEA (Droplet Execution Agent):
![Origini log in un'architettura DEA.](../images/logging_F1.png "Componenti (origini log) in un'architettura Cloud Foundry basata su DEA (Droplet Execution Agent).")


