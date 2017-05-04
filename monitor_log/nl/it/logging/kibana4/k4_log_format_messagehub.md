---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Formato dei log Kibana per Message Hub
{: #kibana_log_format_messagehub}

Puoi configurare Kibana in modo che visualizzi nella pagina *Ricerca* i seguenti campi per ogni voce di log:
{:shortdesc}

| Campo | Descrizione |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> L'ora dell'evento registrato. <br> La data e ora è definita fino al millisecondo. |
| @version | La versione dell'evento. |
| ALCH_TENANT_ID | L'ID dello spazio {{site.data.keyword.Bluemix_notm}}. |
| \_id | L'ID univoco per il tuo documento di log. |
| \_index | L'indice per la voce di log. |
| \_type | Il tipo di log, ad esempio *syslog*. |
| loglevel | La severità dell'evento registrato, ad esempio, **Info**. |
| module | Questo campo è impostato su **MessageHub**. |


Esempio di una voce di log: 

``` 	
March 8th 2017, 17:15:16.454	

message:
    Creating topic ABC
@version:
    1
@timestamp:
    March 8th 2017, 17:15:16.454
loglevel:
    Info
module:
    MessageHub
ALCH_TENANT_ID:
    3d8d2eae-f3f0-44f6-9717-126113a00b51
_id:
    AVqu6vJl1zcfr8KYMI95
_type:
    logs
_index:
    logstash-2017.03.08

```
