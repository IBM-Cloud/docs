---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analisi delle metriche in Grafana
{:#analyzing_metrics_grafana}

In {{site.data.keyword.Bluemix}}, puoi utilizzare Grafana, una piattaforma di analisi e visualizzazione open source, per monitorare, ricercare, analizzare e visualizzare le tue metriche in una varietà di grafici, ad esempio, diagrammi e tabelle. Utilizza Grafana per eseguire attività di analisi avanzate.
{:shortdesc}

Puoi avviare Grafana in uno dei seguenti modi:

* Da {{site.data.keyword.Bluemix_notm}}

    Puoi avviare le metriche del tuo specifico contenitore Docker in Grafana, nel contesto di quello specifico contenitore. 
    
    Per ulteriori informazioni, vedi [Passaggio al dashboard Grafana dal dashboard {{site.data.keyword.Bluemix_notm}}]
    (monitoring_analyzing_metrics_grafana.html#launch_grafana_from_bluemix).

* Da un link diretto del browser

    Puoi avviare Grafana in modo che i dati che visualizzi aggreghino i log dai servizi all'interno di uno spazio {{site.data.keyword.Bluemix_notm}} fornito.
    
    Per ulteriori informazioni, vedi [Passaggio al dashboard Kibana da un browser web](monitoring_analyzing_metrics_grafana.html#launch_grafana_from_browser).
    
Per ulteriori informazioni su Grafana, consulta [Grafana User Guide ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://docs.grafana.org/guides/getting_started/){: new_window}.


##  Passaggio al dashboard Grafana dal dashboard Bluemix
{: #launch_grafana_from_bluemix}

La query che viene utilizzata per filtrare i dati visualizzati in Grafana richiama i dati per il contenitore {{site.data.keyword.Bluemix_notm}} da cui è stato avviato Kibana. 

Per visualizzare le metriche di un contenitore Docker in Grafana, completa la seguente procedura:

1. Accedi a {{site.data.keyword.Bluemix_notm}} e fai clic sul contenitore dal dashboard {{site.data.keyword.Bluemix_notm}}. 
    
2. Nella barra di navigazione, fai clic su **Monitoraggio e log**. Viene visualizzata la scheda monitoraggio. 
    
3. Fai clic su **Vista avanzata**. Si aprirà il dashboard **Grafana**.


##  Passaggio al dashboard Grafana da un browser web
{: #launch_grafana_from_browser}

La query utilizzata per filtrare i dati visualizzati in Grafana richiama i dati per uno spazio nell'organizzazione {{site.data.keyword.Bluemix_notm}}. Le informazioni sulle metriche visualizzate da Grafana includono i record per tutte le risorse che vengono distribuite all'interno dello spazio dell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui sei connesso.

Completa la seguente procedura per avviare Grafana da un browser:

1. Apri [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) per accedere all'interfaccia utente Grafana.

2. Seleziona **Grafana**.
     

