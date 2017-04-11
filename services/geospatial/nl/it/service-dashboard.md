---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Dashboard di gestione del servizio
{: #service-dashboard}


Mediante il dashboard di gestione del servizio puoi visualizzare lo stato della tua istanza del servizio {{site.data.keyword.geospatialshort_Geospatial}}
e arrestare o riavviare tale istanza. Puoi ottenere il dashboard di gestione del servizio
facendo clic sul tile {{site.data.keyword.geospatialshort_Geospatial}} nel
dashboard {{site.data.keyword.geospatialshort_Geospatial}}. Se utilizzi
l'applicazione di esempio e la tua istanza del servizio raggiunge il limite di eventi e si arresta, puoi riavviare il
servizio. L'arresto del servizio rimuove il limite di eventi. Gli eventi continuano a essere ricevuti finché
non arresti il servizio. Il dashboard di gestione del servizio visualizza inoltre lo stato dell'istanza del servizio
e le statistiche.
{:shortdesc}

##Controlli regione {{site.data.keyword.geospatialshort_Geospatial}}

{{site.data.keyword.geospatialshort_Geospatial}} monitora i dispositivi
in movimento da Internet of Things. Ogni dispositivo monitorato invia messaggi dispositivo contenenti un identificativo univoco
con la posizione corrente, comprese latitudine e longitudine. La posizione del dispositivo
viene controllata tramite le coordinate di ogni regione geografica definita. Il servizio produce
quindi gli eventi quando i dispositivi entrano, escono o sono "in hangout" in una regione specifica.

Un Controllo regione viene utilizzato come unità per misurare l'utilizzo di {{site.data.keyword.geospatialfull}}. Per ogni messaggio dispositivo,
viene eseguito un controllo regione se viene specificato il rilevamento per l'entrata, l'uscita o entrambi per una regione. Per ogni
messaggio dispositivo, viene eseguito un controllo regione se viene specificato il rilevamento in hangout per la regione. Se non viene definita alcuna regione, per ogni messaggio dispositivo, viene conteggiato un controllo regione come se
fosse presente 1 regione. Questo significa che se hai 100 regioni definite per il controllo di entrata, uscita e hangout,
un solo messaggio dispositivo produrrà 200 controlli regione.
