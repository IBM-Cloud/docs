---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Registrazione per le applicazioni Cloud Foundry in Bluemix
{: #logging_bluemix_cf_apps}

In {{site.data.keyword.Bluemix}}, puoi visualizzare, filtrare e analizzare i log attraverso il dashboard {{site.data.keyword.Bluemix}}, Kibana e l'interfaccia riga di comando. Inoltre, puoi trasmettere i record dei log a uno strumento di gestione log esterno.
{:shortdesc}

Quando esegui le tue applicazioni in un PaaS (platform-as-a-service) cloud come Cloud Foundry su {{site.data.keyword.Bluemix_notm}}, non puoi stabilire un tunnel SSH o FTP nell'infrastruttura in cui sono in esecuzione le tue applicazioni per accedere ai log. La piattaforma è controllata dal provider del cloud. Le applicazioni Cloud Foundry in esecuzione su {{site.data.keyword.Bluemix_notm}} utilizzano il componente Loggerator per inoltrare i record di log dall'interno dell'infrastruttura Cloud Foundry. Loggregator raccoglie automaticamente i dati STDOUT e STDERR. Puoi visualizzare e analizzare questi log attraverso il dashboard {{site.data.keyword.Bluemix}}, Kibana e l'interfaccia riga di comando. 

La seguente figura mostra una visualizzazione di alto livello della registrazione di applicazioni Cloud Foundry in {{site.data.keyword.Bluemix_notm}}:

![Panoramica dei componenti di alto livello per le applicazioni CF](images/logging_cf_apps_ov.jpg)
 
La registrazione delle applicazioni Cloud Foundry viene abilitata automaticamente quando utilizzi l'infrastruttura Cloud Foundry per eseguire le tue applicazioni su {{site.data.keyword.Bluemix_notm}}. Per visualizzare i log del runtime Cloud Foundry, devi scrivere i tuoi log in STDOUT e STDERR. Per ulteriori informazioni, vedi [Registrazione delle applicazioni di runtime attraverso le applicazioni CF](cfapps/logging_writing_to_log_from_cf_app.html#logging_writing_to_log_from_cf_app).

Puoi scegliere uno dei seguenti metodi per analizzare i log della tua applicazione Cloud Foundry:

* Analizza il log in {{site.data.keyword.Bluemix_notm}} per visualizzare l'ultima attività dell'applicazione.
    
    In {{site.data.keyword.Bluemix}}, puoi visualizzare, filtrare e analizzare i log attraverso la scheda **Log** disponibile per ogni applicazione Cloud Foundry. Per ulteriori informazioni, vedi [Analisi dei log dell'applicazione CF dal dashboard Bluemix](logging_view_dashboard.html#analyzing_logs_bmx_ui).
    
* Analizza i log in Kibana per eseguire attività di analisi avanzate.
    
    In {{site.data.keyword.Bluemix}}, puoi utilizzare Kibana, una piattaforma di analisi e visualizzazione open source, per monitorare, ricercare, analizzare e visualizzare i tuoi dati in una varietà di grafici, ad esempio, diagrammi e tabelle. Per ulteriori informazioni, vedi [Analisi dei log in Kibana](logging_view_kibana3.html#analyzing_logs_Kibana).

* Analizza i log attraverso la CLI per utilizzare i comandi per la gestione dei log a livello di programmazione.
    
    In {{site.data.keyword.Bluemix}}, puoi visualizzare, filtrare e analizzare i log attraverso l'interfaccia riga di comando utilizzando il comando **cf logs**. Per ulteriori informazioni, vedi [Analisi dei log dell'applicazione Cloud Foundry dall'interfaccia riga di comando](logging_view_cli.html#analyzing_logs_cli).

{{site.data.keyword.Bluemix_notm}} conserva una quantità limitata di informazioni di log. Quando si registrano le informazioni, i dati precedenti vengono sostituiti con le informazioni più recenti. Se devi rispettare le politiche organizzative o di settore che richiedono di mantenere una parte o tutte le informazioni di log per scopi di controllo o altro, puoi trasmettere i tuoi log a un host di log esterno, quale un servizio di gestione log di terze parti o un altro host. Per ulteriori informazioni, vedi [Configurazione di host log esterni](logging_view_external.html#viewing_logs_external).



