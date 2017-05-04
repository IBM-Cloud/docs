---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Accesso al dashboard Kibana dal dashboard Bluemix
{: #launch_Kibana_from_bluemix}

Avvia Kibana dalla IU {{site.data.keyword.Bluemix}} per visualizzare i log specifici di un'applicazione Cloud Foundry o un contenitore Docker.
{:shortdesc}

La query che viene utilizzata per filtrare i dati visualizzati in Kibana richiama le voci di log per l'applicazione CF o il contenitore {{site.data.keyword.Bluemix_notm}} da cui è stato avviato Kibana. 

Per visualizzare i log di un'applicazione Cloud Foundry o un contenitore Docker in Kibana, completa la seguente procedura: 

1. Accedi a {{site.data.keyword.Bluemix_notm}} e fai clic sul nome applicazione o sul contenitore dal dashboard {{site.data.keyword.Bluemix_notm}}. 
    
2. Apri la scheda del log nella IU {{site.data.keyword.Bluemix_notm}}.

    * Per le applicazioni CF, fai clic su **Log** nella barra di navigazione. 
    * Per i contenitori, seleziona **Monitoraggio e log** nella barra di navigazione e fai quindi clic sulla scheda **Registrazione**. 
    
    Viene visualizzata la scheda Log. 
    
3. Fai clic su **Vista avanzata**. Si aprirà il dashboard **Kibana 4**.

    Per impostazione predefinita, la pagina **Ricerca** viene caricata con il modello di indice predefinito selezionato e un filtro temporale impostato sugli ultimi 30 secondi. La query di ricerca è configurata per corrispondere a tutte le voci per la tua applicazione CF o contenitore Docker.

    Se la pagina Rileva non mostra alcuna voce di log, modifica il selezionatore di tempo. Per ulteriori informazioni, consulta [Configurazione di un filtro temporale](logging_kibana_set_time_filter.html#set_time_filter).

Per ulteriori informazioni su Kibana, consulta [Kibana User Guide ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.

