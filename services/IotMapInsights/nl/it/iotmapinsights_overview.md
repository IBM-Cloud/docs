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

Il servizio {{site.data.keyword.iotmapinsights_short}} è basato sui dati di rete stradale memorizzati nella cache di memoria. Il servizio fornisce un accesso ad alta velocità ai dati sulla rete stradale statici, ai dati di evento dinamici e agli strumenti geospaziali basati sulla rete, che abilita la tua applicazione a integrare le funzionalità geospaziali.
{:shortdesc}

## Query di dati di mappa statici
{: #static_map_data_query}

Per accedere ai dati di attributo di collegamento stradale, il servizio {{site.data.keyword.iotmapinsights_short}} fornisce un'interfaccia API REST per l'esecuzione di query dei collegamenti. L'interfaccia riceve un ID collegamento come un parametro che può essere identificato da una funzione di messa in corrispondenza con la mappa e restituisce le informazioni dettagliate per il collegamento richiesto, come il tipo di strada, la lunghezza, gli array di punti di forma (shape point) dettagliati, i nodi adiacenti e i collegamenti adiacenti.Utilizzando le informazioni sui collegamenti dettagliate oggetto delle query, la tua applicazione può percorrere una rete di collegamenti stradali osservando le informazioni sui collegamenti adiacenti.

## Dati di evento dinamici
{: #dynamic_event_data}

Un evento nel servizio {{site.data.keyword.iotmapinsights_short}} è un modello di oggetto per un evento di traffico che viene posizionato dinamicamente su uno specifico collegamento stradale. L'evento ha degli attributi di base di un evento di traffico, come le coordinate GPS, l'ora, il tipo, la durata dell'evento e la lunghezza interessata. Puoi inserire ed eliminare eventi in modo dinamico.

## Inserimento ed eliminazione di eventi
{: #inject_event}

Con l'interfaccia API REST di inserimento di eventi, puoi archiviare un evento su una mappa. Per inserire un evento, puoi pubblicare le informazioni sull'evento sull'interfaccia con il tipo di evento definito per classificare gli eventi e i suoi attributi conformemente all'uso previsto della tua applicazione. Con l'interfaccia API REST di eliminazione di eventi, puoi rimuovere gli eventi dalla mappa per consentire la gestione degli eventi obsoleti.

## Query di eventi
{: #query_event}

Con l'interfaccia API REST di query di eventi, puoi eseguire query di eventi, a determinate condizioni impostate come parametri di richiesta. Per una condizione di query, puoi impostare l'area con un intervallo di longitudini e latitudini e degli attributi di evento per restringere gli eventi di destinazione restituiti come una risposta alla richiesta.

## Strumenti geospaziali
{: #geospatial_tools}

Per gli strumenti geospaziali, il servizio {{site.data.keyword.iotmapinsights_short}} fornisce un'interfaccia API REST per le funzioni di messa in corrispondenza con la mappa e di ricerca di rotte.

## Corrispondenza di mappe
{: #map_matching}

Se i dati GPS non sono sufficientemente accurati per utilizzare l'analisi o la visualizzazione, o se gli attributi della rete di collegamenti stradali sono richiesti per la tua applicazione, puoi utilizzare l'interfaccia API REST di messa in corrispondenza con la mappa. L'API REST di messa in corrispondenza con la mappa abilita la tua applicazione ad adattare un punto di dati GPS non elaborati a un punto messo in corrispondenza sul collegamento stradale. L'interfaccia API REST di messa in corrispondenza con la mappa riceve un punto di dati di coordinate GPS di longitudine e latitudine e restituisce un punto messo in corrispondenza con la mappa. Questo punto viene analizzato tenendo conto dei dati cronologici per ciascun veicolo entro uno specifico periodo di tempo per trovare il punto più probabile in tempo reale. Per i punti che non hanno dei dati di ubicazione cronologici, l'interfaccia di messa in corrispondenza con la mappa restituisce il punto più prossimo sul collegamento stradale per il punto GPS richiesto.

## Ricerca rotta
{: #route_search}

Se devi implementare un'applicazione con delle funzioni geospaziali, dovrai cercare il percorso più breve tra due punti. L'interfaccia API REST di ricerca delle rotte del servizio
{{site.data.keyword.iotmapinsights_short}} calcola il percorso più breve tra le coordinate GPS di punto di inizio e punto di fine. Le coordinate ricevute vengono messe in corrispondenza con il collegamento della mappa più prossimo utilizzando la funzione di messa in corrispondenza con la mappa e viene calcolato il percorso più breve tra questi punti messi in corrispondenza con la mappa.

## Ricerca collegamenti interessati
{: #link_search}

Un evento che si verifica su una strada potrebbe interessare diversi collegamenti stradali. Puoi utilizzare le API REST per cercare i collegamenti interessati dove i veicoli potrebbero raggiungere l'evento. La ricerca tiene conto della topologia delle reti di collegamenti stradali, non solo della distanza dai veicoli all'evento.

