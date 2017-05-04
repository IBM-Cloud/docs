---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Formato dei log Kibana per i contenitori Docker
{: #kibana_log_format_containers}

Puoi configurare Kibana in modo che visualizzi nella pagina *Ricerca* i seguenti campi per ogni voce di log:
{:shortdesc}

| Campo | Descrizione |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> L'ora dell'evento registrato. <br> La data e ora è definita fino al millisecondo. |
| @version | La versione dell'evento. |
| ALCH_TENANT_ID | L'ID dello spazio {{site.data.keyword.Bluemix_notm}}. |
| \_id | L'ID univoco per il tuo documento di log. |
| \_index | L'indice per la voce di log. |
| \_type | Il tipo di log, ad esempio *logs*. |
| group_id | L'ID gruppo <br> * Per un singolo contenitore, il valore è **0000**. <br> * Per un gruppo di contenitori, il valore è il GUID del gruppo.  |
| host | Il nome host in cui il contenitore è in esecuzione.  |
| instance | Il GUID dell'istanza per un singolo contenitore. Elenco di ID istanza per un gruppo di contenitori. |
| log | Messaggio breve.  |
| message | Messaggio completo.  |
| path | Il percorso e il nome del log in cui il log è ubicato all'interno del contenitore. |
| stream | Specifica il tipo di log: stdout, stderr  |
| time | La data e l'ora di quando si è verificato l'evento. La data e ora è definita fino al millisecondo.|
| timestamp | La data e l'ora dell'evento registrato. La data e ora è definita fino al millisecondo. |



