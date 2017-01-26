---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Introduzione a {{site.data.keyword.iotmapinsights_short}}
{: #iotdriverinsights_index}
Ultimo aggiornamento: 22 giugno 2016
{: .last-updated}

{{site.data.keyword.iotmapinsights_full}} è un servizio su {{site.data.keyword.Bluemix}} che puoi utilizzare per abilitare le funzioni geospaziali quali la messa in corrispondenza con la mappa e la ricerca del percorso più breve sulla base delle reti stradali in tutto il mondo, utilizzando le tue applicazioni.  
{:shortdesc}

Le seguenti funzioni sono disponibili tramite l'API REST {{site.data.keyword.iotmapinsights_short}}:

|Funzione|Utilizzata per...|
|:---|:---|
|Messa in corrispondenza con la mappa ad alta precisione|Metti in corrispondenza la tua posizione GPS con la reale rete stradale tracciata|
|Recupero dei dati di geometria stradale |Recupera la rete stradale mappata per disegnare forme delle strade su una mappa|
|Ricerca dinamica del percorso più breve|Ricerca la rotta più breve includendo eventi in tempo reale come il traffico|
|Manipolazione degli eventi di traffico in tempo reale|Aggiungi eventi messi in corrispondenza con la mappa in tempo reale, ad esempio le condizioni del traffico, per migliorare i risultati della pianificazione della rotta|

## Prima di cominciare
{: #byb}

1. Quando aggiungi un'istanza del servizio dal [{{site.data.keyword.Bluemix_notm}} catalogo](https://console.stage1.ng.bluemix.net/catalog/services/iot-automotive/){: new_window}, assicurati che non sia associata a un'applicazione e di prendere nota dei valori di ID tenant, nome utente e password che vengono generati automaticamente. Questi valori ti serviranno successivamente per accedere al servizio tramite l'API {{site.data.keyword.iotmapinsights_short}}.

2. Acquisisci familiarità con [OpenStreetMap](http://www.openstreetmap.org/){: new_window}.  

 Il servizio {{site.data.keyword.iotmapinsights_short}} utilizza i dati di rete stradale, in coordinate WGS84, che vengono estratti da [OpenStreetMap](http://www.openstreetmap.org/){: new_window}. Per l'analisi vengono utilizzate solo le strade su cui può transitare un'automobile.  

 Sono supportate le seguenti regioni delle mappe:

|Regione|ID mappa|
|:---|:---|
|Europa|id_mappa=1|
|Africa|id_mappa=2|
|Asia|id_mappa=3|
|Australia, Oceania|id_mappa=4|
|America del Nord|id_mappa=5|
|America centrale|id_mappa=6|
|America del Sud|id_mappa=7|

## Corrispondenza di mappe
{: #map_matching}
Per associare le coordinate GPS non elaborate con quelle messe in corrispondenza con la mappa, completa la seguente procedura:

1. Prepara una serie di coordinate GPS non elaborate da analizzare.
2. Invia le coordinate GPS non elaborate utilizzando il comando API `mapMatching`. Facoltativamente, imposta un angolo di direzione di ciascuna posizione in gradi per specificare la direzione del viaggio.
 - Richiesta: dati GPS non elaborati
 - Risposta: dati GPS messi in corrispondenza con la mappa, ID collegamento
3. Facoltativo: richiama i dati del tipo di strada utilizzando il comando API `getLinkInformation`. Puoi recuperare i dati delle forme delle strade corrispondenti sotto forma di serie di coordinate utilizzando l'API REST `getLinkInformation`.
 - Richiesta: ID collegamento
 - Risposta: tipo di strada

## Ricerca della rotta
{: #route_searching}

Trova informazioni sulla rotta più breve tra le coordinate di origine e di destinazione specificate utilizzando la seguente procedura:

1. Determina una posizione di inizio e una di fine per il percorso più breve.
2. Invia le coordinate di inizio e di fine con l'API REST `routeSearch`.
Facoltativamente, imposta un angolo di direzione per ciascuna posizione, in gradi, per specificare la direzione del viaggio.
 - Richiesta: coordinate di origine e destinazione
 - Risposta: rotta più breve messa in corrispondenza con la mappa

Utilizza i dati della forma del collegamento restituiti per disegnare la forma del percorso rilevato su una mappa.

## Aggiunta di eventi di traffico
{: #traffic_events}

Per aggiungere le informazioni sull'evento di traffico al servizio {{site.data.keyword.iotmapinsights_short}}, completa la seguente procedura:

1. Scegli il tipo e la posizione dell'evento di traffico che vuoi creare.
2. Inserisci l'evento utilizzando il comando API  `createEvent`.
Invia le informazioni sull'evento di traffico al servizio {{site.data.keyword.iotmapinsights_short}}.
 - Richiesta: informazioni sull'evento
 - Risposta: ID evento
3. Trova gli eventi utilizzando il comando API REST `queryEvent`.
Cerca gli eventi di traffico all'interno di una specifica area rettangolare e, facoltativamente, uno specifico tipo di evento di traffico.
 - Richiesta: informazioni sull'area.
 - Risposta: informazioni sull'evento.  
4. Facoltativo: rimuovi un evento di traffico non più valido utilizzando il comando API REST `deleteEvent`.
5. Facoltativo: richiama un'area sulla strada che è interessata da un evento di traffico utilizzando il comando API REST `getAffectedLinksInformation`.

# Link correlati
{: #rellinks}

## Esercitazioni ed esempi
{: #samples}

* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} - Esercitazione parte 1](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} - Esercitazione parte 2](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}
* [IoT for Automotive Starter Application](https://iot-automotive-starter.mybluemix.net){:new_window}

## Guida di riferimento API
{: #api}

* [Documenti API](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}

## Link correlati
{: #general}

* [Introduzione a {{site.data.keyword.iotdriverinsights_short}}](../IotDriverInsights/index.html){:new_window}
* [Introduzione a {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [dW Answers su IBM developerWorks](https://developer.ibm.com/answers/topics/iot-context-mapping){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/iot-context-mapping){:new_window}
* [What's new in Bluemix Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [OpenStreetMap](http://www.openstreetmap.org/){:new_window}
* [&copy; OpenStreetMap contributors](http://www.openstreetmap.org/copyright){:new_window}
* [Open Data Commons Open Database License (ODbL)](http://opendatacommons.org/licenses/odbl/){:new_window}
