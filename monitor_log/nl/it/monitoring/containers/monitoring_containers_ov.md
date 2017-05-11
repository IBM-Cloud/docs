---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-27"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Monitoraggio del servizio IBM Bluemix Container
{: #monitoring_bmx_containers_ov}

In {{site.data.keyword.Bluemix}}, le metriche del contenitore vengono raccolte automaticamente dall'esterno del contenitore, senza dover installare e conservare gli agent nel contenitore.
{:shortdesc}

Gli agent nei contenitori possono avere sovraccarichi e tempi di configurazione significativi per istanze cloud leggere e di breve durata e per i gruppi con ridimensionamento automatico, dove i contenitori possono essere creati e distrutti rapidamente. Questo approccio alla raccolta di dati fuori banda elimina queste difficoltà e rimuove l'onere del monitoraggio da parte degli utenti.

Un processo eseguito nell'host effettua il monitoraggio senza agent delle metriche. Questo processo, che viene anche chiamato crawler, raccoglie costantemente le seguenti metriche da tutti i contenitori per impostazione predefinita:

* CPU
* Memoria
* Informazioni di rete

I dati della metrica vengono raccolti in Graphite e visualizzati nella IU {{site.data.keyword.Bluemix_notm}} e in Grafana. 

Puoi avviare Grafana dalla IU {{site.data.keyword.Bluemix_notm}} o direttamente da un browser. Per ulteriori informazioni, vedi [Analisi delle metriche in Grafana](../grafana/monitoring_analyzing_metrics_grafana.html#analyzing_metrics_grafana).

Le informazioni di account di gruppi e convenzioni di Docker sono utilizzate come meccanismo di base per la raccolta di dati di monitoraggio.

## Conservazione delle metriche

Viene raccolto fino a un punto dati al minuto. Le metriche del contenitore che non sono state scritte per 7 giorni vengono eliminate.
    
## Ordinamento delle metriche

I dati vengono visualizzati e ordinati in base all'ID contenitore. 

Dalla riga di comando, puoi eseguire il comando `cf ic ps` per visualizzare un elenco di ID del contenitore nel tuo registro delle immagini {{site.data.keyword.Bluemix_notm}} privato.

