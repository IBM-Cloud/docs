---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Informazioni su {{site.data.keyword.iotmapinsights_short}}
{: #iotmapinsights_overview}
Ultimo aggiornamento: 20 luglio 2016
{: .last-updated}

{{site.data.keyword.iotmapinsights_full}} è un servizio su {{site.data.keyword.Bluemix_notm}} che puoi utilizzare per ottenere un rapido accesso ai dati di rete stradale statici e dati di evento dinamici. {{site.data.keyword.iotmapinsights_short}} fornisce anche strumenti geospaziali per le reti stradali, che puoi utilizzare per integrare le funzionalità geospaziali con le tue applicazioni.
{:shortdesc}

Il servizio {{site.data.keyword.iotmapinsights_short}} fornisce le seguenti funzioni:

- Dati di mappa statici
- Dati di evento dinamici
- Strumenti geospaziali

Il servizio {{site.data.keyword.iotmapinsights_short}} raccoglie e utilizza i dati di rete stradale [OpenStreetMap](http://www.openstreetmap.org/){: new_window} che vengono memorizzati nella cache di memoria del servizio per l'elaborazione.

I dati provenienti da OpenStreetMap vengono resi disponibili in Open Data Common Open Database License (ODbL) mediante OpenStreetMap Foundation (OSMF). Per ulteriori informazioni, vedi [OpenStreetMap Copyright and License](http://www.openstreetmap.org/copyright){: new_window}.

## Dati di mappa statici
{: #static_map_data_query}

Una delle funzioni principali del prodotto è la possibilità di recuperare informazioni stradali dettagliate da utilizzare con le tue applicazioni. Utilizza l'interfaccia API REST per l'esecuzione di query dei collegamenti per eseguire una query dei dati di attributo statici della mappa stradale in base all'ID collegamento. Utilizza la [funzione di messa in corrispondenza con la mappa](#map_matching) di  {{site.data.keyword.iotmapinsights_short}} per identificare il parametro dell'ID collegamento richiesto.

I dati che vengono restituiti includono le seguenti informazioni relative all'ID di collegamento richiesto:

- Tipo di strada
- Lunghezza della strada
- Un array di punti di forma (shape point) dettagliati
- Informazioni relative a nodi adiacenti e collegamenti adiacenti

Eseguendo query di informazioni dettagliate sui collegamenti stradali, la tua applicazione può percorrere una rete di collegamenti stradali utilizzando in modo intelligente le informazioni sui collegamenti adiacenti che vengono restituite.

## Dati di evento dinamici
{: #dynamic_event_data}

Oltre ai dati di mappa statici, la reale condizione mondiale delle strade comprende necessariamente eventi dinamici come la congestione del traffico e i lavori stradali. Utilizza {{site.data.keyword.iotmapinsights_short}} per creare, gestire e integrare gli eventi di traffico con le [ricerche di collegamenti interessati](#link_search) ai fini della pianificazione dei percorsi.

### Inserimento ed eliminazione di eventi
{: #inject_event}

Utilizza l'API REST di inserimento di eventi del servizio {{site.data.keyword.iotmapinsights_short}} per inserire e rimuovere dinamicamente gli eventi di traffico sotto forma di modelli oggetto di mappa che vengono collocati su specifici collegamenti stradali. Ogni evento include attributi di base come le coordinate GPS, l'ora di inizio, il tipo di evento, la durata dell'evento e la lunghezza della strada interessata.

Utilizza l'interfaccia API REST di eliminazione di eventi per rimuovere eventi dalla mappa una volta ritenuti obsoleti.

### Query di eventi
{: #query_event}

Utilizza l'API REST di query di eventi per acquisire informazioni dettagliate su tutti gli eventi dinamici in una determinata area geografica. Puoi eseguire query in base all'area con un intervallo di longitudini e latitudini e puoi includere attributi di evento per restringere il numero di eventi di destinazione restituiti.

## Strumenti geospaziali
{: #geospatial_tools}

Migliora la tua applicazione con le funzioni di messa in corrispondenza con la mappa e di ricerca di rotte fornite dagli strumenti geospaziali {{site.data.keyword.iotmapinsights_short}}.

### Corrispondenza di mappe
{: #map_matching}

Utilizza l'interfaccia API REST di messa in corrispondenza con la mappa con la tua applicazione per mappare le coordinate GPS del dispositivo reale con i dati di rete stradale [OpenStreetMap](http://www.openstreetmap.org/){: new_window} per aumentare la precisione della localizzazione per i dati GPS inesatti. Puoi anche ricevere informazioni sugli attributi della strada in base alla posizione. L'API REST di messa in corrispondenza con la mappa consente alla tua applicazione di adattare un punto di dati GPS non elaborati a un punto messo in corrispondenza sul collegamento stradale.

L'interfaccia API REST di messa in corrispondenza con la mappa riceve un punto di dati di coordinate GPS di longitudine e latitudine e restituisce un punto messo in corrispondenza con la mappa. Il punto messo in corrispondenza con la mappa viene analizzato tenendo conto dei dati cronologici per ciascuna automobile entro uno specifico periodo di tempo per trovare il punto più probabile in tempo reale. Per i punti che non hanno dei dati di ubicazione cronologici, l'interfaccia di messa in corrispondenza con la mappa restituisce il punto più prossimo sul collegamento stradale dal punto GPS richiesto.

### Ricerca rotta
{: #route_search}

Una delle funzioni di base di un'applicazione con funzionalità geospaziali è la capacità di trovare il percorso più breve tra due punti.  

L'interfaccia API REST di ricerca delle rotte del servizio {{site.data.keyword.iotmapinsights_short}} calcola il percorso più breve tra le coordinate GPS di un punto di inizio e un punto di fine. Le coordinate ricevute vengono messe in corrispondenza con il collegamento della mappa più prossimo utilizzando la funzione di messa in corrispondenza con la mappa e viene calcolato il percorso più breve tra questi punti messi in corrispondenza con la mappa.

### Ricerca collegamenti interessati
{: #link_search}

Un evento che si verifica su una strada potrebbe interessare diversi collegamenti stradali. Puoi utilizzare le API REST per cercare i collegamenti interessati e per trovare anche i collegamenti stradali in cui le automobili potrebbero raggiungere l'evento. La ricerca tiene conto della topologia della rete di collegamenti stradali, non solo della distanza dalle automobili all'evento.
