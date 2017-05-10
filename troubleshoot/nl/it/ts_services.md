---

copyright:
  year: 2015, 2016
  
lastupdated: "2016-08-12"

---



{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}


# Risoluzione dei problemi relativi ai servizi
{: #services}


I problemi relativi ai servizi {{site.data.keyword.Bluemix}} potrebbero includere un errore di timeout del gateway che si verifica quando elimini un'istanza del servizio. Puoi risolvere questi problemi seguendo pochi semplici passi.
{:shortdesc}

## Si verifica un errore del broker di servizi quando elimini un'istanza del servizio
{: #ts_service_broker}

Quando tenti di eliminare un'istanza del servizio che è già stata eliminata dal controller cloud,
potresti ricevere un messaggio di errore.
{:shortdesc}

Quando tenti di eliminare un'istanza del servizio, visualizzi il seguente messaggio di errore del broker dei servizi:
{: tsSymptoms}
`Timeout del gateway`

Questo problema si verifica se
    l'istanza del servizio è già stata eliminata
dal controller cloud.
{: tsCauses}

Crea un'istanza del servizio con lo stesso nome servizio, quindi eseguine il bind alle tue applicazioni. Puoi quindi eliminare l'istanza del servizio e le applicazioni che utilizzano il servizio.   
{: tsResolve}
