---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Risoluzione dei problemi di {{site.data.keyword.geospatialshort_Geospatial}} 
{: #ts_geospatial}


Ottieni le risposte alle diverse domande più comuni relative all'utilizzo di {{site.data.keyword.geospatialshort_Geospatial}} su {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

##Quando arresto la mia applicazione, il servizio continua a monitorare le regioni
{: #stop-monitoring}


L'arresto dell'applicazione non arresta automaticamente {{site.data.keyword.geospatialshort_Geospatial}}.
{:shortdesc}


Hai arrestato la tua applicazione che utilizza {{site.data.keyword.geospatialshort_Geospatial}}, ma sul dashboard di gestione
vedi che il servizio sta ancora monitorando le regioni da te specificate nella
tua applicazione.
{: tsSymptoms}


Se arresti la tua applicazione, l'istanza del servizio {{site.data.keyword.geospatialshort_Geospatial}} continuerà l'esecuzione. Il servizio continua a monitorare le regioni finché non lo arresti, indipendentemente dal fatto che la tua
applicazione sia in esecuzione. 
{: tsCauses}


Arresta {{site.data.keyword.geospatialshort_Geospatial}} dal dashboard di gestione del servizio. In alternativa, puoi modificare la tua applicazione per arrestare il servizio utilizzando l'API REST ed inserendo quindi nuovamente le modifiche in {{site.data.keyword.Bluemix_short}}.
{: tsResolve}

##Il servizio sta monitorando delle regioni che non ho specificato nella mia applicazione
{: #unspecified-region}



Se hai più di un'applicazione associata alla stessa istanza del servizio, è possibile che un'altra applicazione abbia aggiunto queste regioni.
{:shortdesc}



Quando visualizzi la tua istanza di {{site.data.keyword.geospatialshort_Geospatial}} sul dashboard di gestione del servizio, vedi che sta monitorando più regioni di quante tu ne abbia specificate in una delle tue applicazioni.
{: tsSymptoms}

Una singola istanza di {{site.data.keyword.geospatialshort_Geospatial}} monitora le regioni di tutte le applicazioni ad essa associate. Questo significa che, quando visualizzi il tuo dashboard di gestione del servizio, vedrai informazioni per le regioni specificate da tutte le tue applicazioni.
{: tsCauses}

Per fare in modo che {{site.data.keyword.geospatialshort_Geospatial}} non monitori più delle specifiche regioni:

1. Arresta il servizio.
2. Modifica la tua applicazione o le tue applicazioni per rimuovere tali regioni.
3. Esegui nuovamente il push della tua applicazione o delle tue applicazioni in {{site.data.keyword.Bluemix_short}}.
{: tsResolve}


##Risoluzione dei problemi dal dashboard di gestione del servizio
{: #dashboard}

Quando risolvi i problemi relativi alla tua applicazione, puoi passare al
dashboard di gestione del servizio per controllare lo stato
della tua istanza del servizio. Se non vi sono dei dati in elaborazione, puoi
  riuscire a correggere il problema arrestando e riavviando il
servizio.
{:shortdesc}

Lo stato della tua istanza del servizio {{site.data.keyword.geospatialshort_Geospatial}} è separato dallo
stato della tua applicazione e più applicazioni possono essere associate alla stessa istanza del servizio. 

Il
dashboard di gestione del servizio fornisce informazioni sullo stato di {{site.data.keyword.geospatialshort_Geospatial}}, non delle applicazioni associate
a esso. Gli stati separati della tua istanza del servizio e di una o più applicazioni
indicano che se arresti l'applicazione, l'istanza del servizio {{site.data.keyword.geospatialshort_Geospatial}} continua l'esecuzione. Il
servizio continua a monitorare le regioni selezionate finché non le rimuovi, a prescindere
dal fatto che la tua
applicazione sia in esecuzione.
