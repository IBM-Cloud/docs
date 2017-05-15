---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Domande e risposte frequenti
{: #logging_qa}

Queste sono le risposte alle domandi comuni sull'utilizzo delle funzionalità di registrazione {{site.data.keyword.Bluemix}}. {:shortdesc}

* [Cosa posso fare se non riesco a visualizzare i log JSON generati dal mio contenitore in Kibana](logging_qa.html#logging_qa_no_JSON_data_kibana)


## Cosa posso fare se non riesco a visualizzare i log JSON generati dal mio contenitore in Kibana
{: #logging_qa_no_JSON_data_kibana}

Quando i log JSON vengono inviati ai log Docker come stdout, non vengono analizzati come JSON e, pertanto, non possono essere ordinati in base al campo @timestamp per modificarne l'ordine. 

I valori @timestamp visualizzati corrispondono alle date/ore in cui i log sono stati ricevuti da ElasticSearch. 

Le date/ore che riflettono quando sono stati generati i log nel contenitore sono visualizzate come parte del campo del messaggio.

Per separare il campo del messaggio in più campi, registra JSON in un file invece di stdout. Ordina quindi i log in Kibana.
