---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Formato dei log Kibana per le applicazioni Cloud Foundry
{: #kibana_log_format_cf}

Puoi configurare Kibana in modo che visualizzi nella pagina *Ricerca* i seguenti campi per ogni voce di log:
{:shortdesc}

| Campo | Descrizione |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> L'ora dell'evento registrato. <br> La data e ora è definita fino al millisecondo. |
| @version | La versione dell'evento.  |
| ALCH_TENANT_ID | L'ID dello spazio {{site.data.keyword.Bluemix_notm}}. |
| \_id | L'ID univoco per il tuo documento di log. |
| \_index | L'indice per la voce di log. |
| \_type | Il tipo di log, ad esempio *syslog*. |
| app_name | Il nome della tua applicazione {{site.data.keyword.Bluemix_notm}}. |
| application_id | L'ID univoco della tua applicazione {{site.data.keyword.Bluemix_notm}}. |
| host | Il nome della tua applicazione che ha prodotto i dati di log. |
| instance_id | L'ID dell'istanza della tua applicazione che ha prodotto i dati di log. |
| loglevel | La severità dell'evento registrato. |
| message | Il messaggio che viene emesso dal componente. <br> Il messaggio varia a seconda dal contesto. |
| message_type | Il flusso in cui viene scritto il messaggio di log. <br> * **OUT** fa riferimento al flusso stdout <br> * **ERR** fa riferimento al flusso stderr. |
| org_id | L'ID univoco della tua organizzazione {{site.data.keyword.Bluemix_notm}}  |
| org_name | Il nome dell'organizzazione {{site.data.keyword.Bluemix_notm}} in cui viene preparata la tua applicazione. |
| origin | Il componente in cui l'evento è stato creato. |
| source_id | Il componente che produce i log. <br> Il seguente elenco descrive i log di ogni componente: <br> * **API**: le risposte registrate per le chiamate API che richiedono una modifica allo stato della tua applicazione. <br> * **APP**: le risposte registrate dalla tua applicazione. <br> * **CELL**: le risposte registrate dalla cella Diego che indicano quando un'applicazione viene avviata, interrotta o arrestata in modo anomalo <br> * **LGR**: le risposte registrate dal loggregator che indicano problemi con il processo di registrazione. <br> * **RTR**: le risposte registrate dal Router quando istrada le richieste HTTP alla tua applicazione. <br> * **SSH**: le risposte registrate dalla cella Diego quando un utente accede a un contenitore applicazioni utilizzando il comando `cf ssh`. <br> * **STG**: le risposte registrate dalla cella Diego o dal DEA (Droplet Execution Agent) quando la tua applicazione viene preparata o ripreparata. |
| space_name | Il nome dello spazio {{site.data.keyword.Bluemix_notm}} in cui viene preparata la tua applicazione. |
| timestamp | L'ora dell'evento registrato. La data e ora è definita fino al millisecondo. |




