---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-07"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Domande e risposte frequenti
{: #logging_qa}

Queste sono le risposte alle domandi comuni sull'utilizzo delle funzionalità di registrazione {{site.data.keyword.Bluemix}}. {:shortdesc}

* [Cosa posso fare se non posso visualizzare i dati nella pagina Rileva in Kibana](logging_qa.html#logging_qa_no_data_discover_kibana)

* [Cosa posso fare se ricevo un'eccezione di autenticazione](logging_qa.html#logging_qa_no_data_dashboard_kibana)





## Cosa posso fare se non posso visualizzare i dati nella pagina Rileva in Kibana 
{: #logging_qa_no_data_discover_kibana}

Esistono vari scenari per cui potresti non visualizzare i dati in Kibana:

1. Quando avvii Kibana, potresti non visualizzare alcun dato nella pagine Rileva. Ricevi il seguente messaggio: **Nessun risultato trovato.**. 
2. Potresti star utilizzando la pagina Rileva in Kibana. Tuttavia, dopo un breve periodo di tempo, ricevi il messaggio: **Nessun risultato trovato.** quando tenti di eseguire un'attività in Kibana.

Per risolvere questo problema, completare i seguenti passi:

1. Controlla che il *Selezionatore di tempo* sia configurato nella pagina Rileva e aumenta il periodo di tempo. 

    **Nota**: per impostazione predefinita, in {{site.data.keyword.Bluemix_notm}}, il *Selezionatore di tempo* è configurato per mostrare i dati degli ultimi 15 minuti.

    Per ulteriori informazioni su come impostare il *Selezionatore di tempo*, consulta [Configurazione di un filtro temporale](../kibana4/logging_kibana_set_time_filter.html#set_time_filter).
       
2. Fai clic sulla lente di ingrandimento ubicata nella barra di ricerca della pagina *Rileva*. I dati della pagina vengono aggiornati in base alla query di ricerca predefinita.

    In alternativa, puoi impostare un periodo di *Aggiornamento automatico*.

    **Nota**: per impostazione predefinita, in {{site.data.keyword.Bluemix_notm}}, il periodo di *Aggiornamento automatico* è impostato su **DISATTIVO**.
    
    Per ulteriori informazioni su come abilitarlo, consulta [Aggiornamento automatico dei dati](../kibana4/logging_kibana_analize_logs_interactively.html#kibana_discover_view_refresh_interval).



## Cosa posso fare se ricevo un'eccezione di autenticazione 
{: #logging_qa_no_data_dashboard_kibana}

Quando non puoi visualizzare i dati nelle tue visualizzazioni in una pagina Dashboard e ricevi il messaggio di errore: **Errore: Eccezione di autorizzazione.**, controlla le tue autorizzazioni per visualizzare i dati in ogni visualizzazione.

Considera le seguenti informazioni:
Puoi configurare una o più visualizzazioni in una pagina Dashboard. Quando la pagina Dashboard effettua una richiesta per raccogliere i dati visualizzati tramite queste visualizzazioni, viene emessa solo una richiesta per tutte le visualizzazioni. Se non disponi delle autorizzazioni per visualizzare i dati per una delle visualizzazioni, l'intera richiesta ha esito negativo.

Per risolvere questo problema, completa la seguente procedura:

1. Identifica le visualizzazioni per cui non disponi delle autorizzazioni.

    1. Fai clic sull'icona *matita* di una visualizzazione nella pagina *Dashboard*. Viene aperta la visualizzazione nella pagina *Visualizza*. In alternativa, nella pagina *Visualizza*, carica una visualizzazione. 
    2. Verifica di poter visualizzare i dati.
    
    Ripeti questi passi per ogni visualizzazione.

2. Richiedi l'accesso per visualizzare i dati per le visualizzazioni all'amministratore cloud.

3. Crea una nuova pagina Dashboard che esclude le visualizzazioni per cui non hai le autorizzazioni mentre hai concesso l'accesso a visualizzare i dati per le visualizzazioni che stanno provocando il problema. 

    Se condividi il Dashboard, non eliminare le visualizzazioni finché questo problema impedirà ad altri membri del team di utilizzare lo stesso dashboard.


