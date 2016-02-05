{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}


# Problemi dei servizi generali
{: #general}

*Ultimo aggiornamento: 9 dicembre 2015*

I problemi relativi ai servizi {{site.data.keyword.Bluemix}}
potrebbero includere un errore di timeout del gateway che si verifica quando elimini
un'istanza del servizio. Tuttavia, in molti casi, puoi eseguire un ripristino da tali problemi seguendo pochi semplici passi.
{:shortdesc}

## Viene visualizzato un messaggio di errore di timeout del gateway quando
elimini un'istanza del servizio
{: #ts_service_broker}

Quando tenti di eliminare un'istanza del servizio che è già stata eliminata dal controller cloud,
potresti ricevere un messaggio di errore.
{:shortdesc}


Quando provi a eliminare un'istanza del servizio, vedi il messaggio di errore del broker dei servizi, ```Timeout gateway```.
{: tsSymptoms}


Questo problema si verifica se
    l'istanza del servizio è già stata eliminata
dal controller cloud.
{: tsCauses}


Per
    risolvere questo problema, crea un'istanza del servizio con lo stesso
nome servizio, quindi eseguine il bind alle tue applicazioni. Dopo di che,
puoi eliminare l'istanza del servizio e le applicazioni che utilizzano
il servizio.   
{: tsResolve}


