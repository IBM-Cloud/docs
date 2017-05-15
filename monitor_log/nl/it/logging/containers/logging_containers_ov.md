---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Registrazione del servizio IBM Bluemix Container
{: #logging_containers_ov}

In {{site.data.keyword.Bluemix}}, puoi visualizzare, filtrare e analizzare i log del contenitore attraverso il dashboard {{site.data.keyword.Bluemix_notm}}, Kibana e l'interfaccia riga di comando.
{:shortdesc}

I log del contenitore sono monitorati e inoltrati dall'esterno del contenitore utilizzando i crawler. I dati vengono inviati dai crawler a un
Elasticsearch a più tenant in {{site.data.keyword.Bluemix_notm}}.

**Nota:** puoi analizzare i log del contenitore in {{site.data.keyword.Bluemix_notm}} per i contenitori Docker distribuiti nell'infrastruttura cloud gestita da {{site.data.keyword.IBM}}.

La seguente figura mostra una visualizzazione di alto livello della registrazione per {{site.data.keyword.containershort}}:

![Panoramica dei componenti di alto livello per i contenitori](images/logging_containers_ov.jpg "Panoramica dei componenti di alto livello per i contenitori")

La registrazione dei contenitori viene automaticamente abilitata quando distribuisci tale contenitore in {{site.data.keyword.Bluemix_notm}}.


## Metodi per analizzare i log del contenitore
{: #logging_containers_ov_methods}
 
Puoi scegliere uno dei seguenti metodi per analizzare i log del tuo contenitore:

* Analizza il log in {{site.data.keyword.Bluemix_notm}} per visualizzare l'ultima attività del contenitore.
    
    Puoi visualizzare, filtrare e analizzare i log attraverso la scheda **Monitoraggio e log** disponibile per ogni contenitore. Per ulteriori informazioni, vedi [Analisi dei log dal dashboard Bluemix](../logging_view_dashboard.html#analyzing_logs_bmx_ui).
    
* Analizza i log in Kibana per eseguire attività di analisi avanzate.
    
    Puoi utilizzare Kibana, una piattaforma di analisi e visualizzazione open source, per monitorare, ricercare, analizzare e visualizzare i tuoi dati in una varietà di grafici, ad esempio, diagrammi e tabelle. Per ulteriori informazioni, vedi [Analisi dei log in Kibana](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana).

* Analizza i log attraverso la CLI per utilizzare i comandi per la gestione dei log a livello di programmazione.
    
    Puoi visualizzare, filtrare e analizzare i log attraverso l'interfaccia riga di comando utilizzando il comando **cf ic logs**. Per ulteriori informazioni, vedi [Analisi dei log dall'interfaccia riga di comando](../logging_view_cli.html#analyzing_logs_cli).

## Log raccolti per i contenitori
{: #logging_containers_ov_logs_collected}

Per impostazione predefinita, vengono raccolti i seguenti log:

<table>
  <caption>Tabella 1. Log</caption>
  <tbody>
    <tr>
      <th align="center">Log</th>
      <th align="center">Descrizione</th>
    </tr>
    <tr>
      <td align="left" width="30%">/var/log/messages</td>
      <td align="left" width="70%"> Per impostazione predefinita, i messaggi Docker vengono archiviati nella cartella /var/log/messages del contenitore. Questo log include i messaggi di sistema.
      </td>
    </tr>
    <tr>
      <td align="left">./docker.log</td>
      <td align="left">Questo log è il log Docker. <br> Il file di log Docker non è memorizzato come file interno di un contenitore, ma viene raccolto comunque. Questo file di log viene raccolto per impostazione predefinita poiché è la convenzione Docker standard per esporre le informazioni stdout (output standard) e stderr (errore standard) per il contenitore. Se un qualsiasi processo del contenitore stampa un output in stdout o stderr, tale informazione viene raccolta. 
      </td>
     </tr>
  </tbody>
</table>

Per raccogliere ulteriori log, aggiungi la variabile di ambiente **LOG_LOCATIONS** con un percorso al file di log quando crei il contenitore. Puoi aggiungere più file di log separandoli con le virgole. Per ulteriori informazioni, vedi [Raccolta di dati di log non predefiniti da un contenitore](logging_containers_other_logs.html#logging_containers_collect_data).



## Conservazione log
{: #logging_containers_ov_log_retention}

Tieni conto delle seguenti informazioni sulla conservazione dei log:

* Viene memorizzato un massimo di 1 GB per spazio di dati al giorno. I log che superano questo limite di 1 GB vengono eliminati. Le assegnazioni dei limiti vengono reimpostate ogni giorno alle
00:30 UTC. 

    Puoi incrementare la tua assegnazione contattando il supporto. Nel ticket di supporto, includi il tuo ID dello spazio per la richiesta di incremento dell'attestazione, la nuova dimensione e il motivo della richiesta.

* Sono ricercabili fino a 7 GB di dati per un massimo di 7 giorni. Viene eseguito il rollover (la prima voce inserita è la prima a essere eliminata) dei dati di log quando vengono raggiunti i 7 GB di dati o vengono superati i 7 giorni

