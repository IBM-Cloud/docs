---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Analisi di un campo del messaggio JSON che fa parte di una voce di log del contenitore
{: #logging_containers_analyze_json_field}

In Kibana, per analizzare i dati di log del contenitore, puoi definire nuove ricerche e applicare dei filtri per i campi di tipo stringa definiti in un campo del messaggio con formattazione JSON.
{:shortdesc}

Completa la seguente procedura per analizzare un campo di tipo JSON in Kibana:

1. Per separare un campo del messaggio JSON in più campi, registra il messaggio in formato JSON in un file diverso da STDOUT. 

    Quando le voci di log JSON vengono inviate al file di log Docker di un contenitore come STDOUT, non vengono analizzate come JSON. Non è possibile ordinare il messaggio in base al campo @timestamp per modificarne l'ordine.  

2. Aggiungi il file di log all'elenco di log non predefiniti che sono disponibili per l'analisi da un contenitore. Per ulteriori informazioni, vedi [Raccolta di dati di log non predefiniti da un contenitore](logging_containers_other_logs.html#logging_containers_collect_data). 

3. Analizza il tuo log in Kibana. Per ulteriori informazioni, vedi [Analisi log avanzata con Kibana](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana).

    **Nota:** se un campo viene definito come JSON valido, viene analizzato e da esso vengono creati nuovi campi. Solo i valori dei campi di tipo stringa sono disponibili per il filtro e l'ordinamento in Kibana.
    
    Il valore del campo @timestamp che viene visualizzato corrisponde alla data/ora in cui la voce di log è stata ricevuta da ElasticSearch. La data/ora che indica il momento della generazione della voce di log nel contenitore viene visualizzata come parte dei campi del messaggio.
    


