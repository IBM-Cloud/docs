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
{: #gettingstartedtemplate}
*Ultimo aggiornamento: 13 maggio 2016*

{{site.data.keyword.iotmapinsights_full}} consente agli sviluppatori di abilitare facilmente le loro applicazioni a utilizzare le funzioni geospaziali quali la messa in corrispondenza con la mappa e la ricerca del percorso più breve sulla base delle reti stradali in tutto il mondo.
{:shortdesc}

Puoi utilizzare le seguenti funzioni tramite la API REST {{site.data.keyword.iotmapinsights_short}}:

- Messa in corrispondenza con la mappa ad alta precisione che utilizza la geometria delle reti stradali.
- Manipolazione di eventi in tempo reale su una mappa, come il traffico.
- Ricerca dinamica del percorso più breve (ricerca della rotta), tenendo conto di eventi in tempo reale, come il traffico.
- Richiamo dei dati di geometria stradale che possono essere utilizzati per tracciare forme di strade su una mappa.

Il servizio {{site.data.keyword.iotmapinsights_short}} utilizza i dati di rete stradale, in coordinate WGS84, che vengono estratti daOpenStreetMap. Per l'analisi vengono utilizzate solo le strade su cui può transitare un veicolo.

Le regioni di mappe supportate sono:

- Europa (map_id=1)
- Africa (map_id=2)
- Asia (map_id=3)
- Australia Oceania (map_id=4)
- Nord America (map_id=5)
- America Centrale (map_id=6)
- Sud America (map_id=7)


Attieniti alla seguente procedura per utilizzare le funzioni di analisi del servizio {{site.data.keyword.iotmapinsights_short}}.

## Utilizzo di {{site.data.keyword.iotmapinsights_short}} per la messa in corrispondenza con la mappa

1. Prepara una serie di dati di coordinate GPS non elaborate da analizzare.
2. Invia i dati di coordinate GPS non elaborate nell'ordine della serie temporale al servizio {{site.data.keyword.iotmapinsights_short}} utilizzando
l'API REST `mapMatching`. Facoltativamente, imposta un angolo di direzione di ciascuna posizione in gradi (il nord è 0, angolo in senso
orario) per specificare la direzione del viaggio.
3. Ricevi le coordinate messe in corrispondenza con la mappa e le informazioni sui collegamenti stradali in risposta alla chiamata API REST `mapMatching`.
4. Facoltativamente, richiama i dati sulla forma della strada del collegamento stradale messo in corrispondenza con la mappa utilizzando l'API REST `getLinkInformation`. Richiama l'API REST `getLinkInformation` con un ID collegamento per ottenere una serie di coordinate che consiste in una forma della strada.

## Utilizzo {{site.data.keyword.iotmapinsights_short}} per la ricerca delle rotte

1. Determina una posizione di inizio e una di fine per cui vuoi ottenere un percorso più breve.
2. Invia le coordinate di inizio e fine al servizio {{site.data.keyword.iotmapinsights_short}} utilizzando
l'API REST `routeSearch`. Facoltativamente, imposta un angolo di direzione di ciascuna posizione in gradi (il nord è 0, angolo in senso
orario) per specificare la direzione del viaggio.
3. Ricevi un elenco di collegamenti stradali in risposta alla chiamata dell'API REST `routeSearch`. Puoi tracciare la forma del percorso trovato su una mappa utilizzando i dati di forma inclusi nei dati del risultato.

## Utilizzo di {{site.data.keyword.iotmapinsights_short}} per la manipolazione degli eventi di traffico

1. Determina un tipo e una posizione di un evento di traffico che vuoi creare.
2. Invia le informazioni sull'evento di traffico al servizio {{site.data.keyword.iotmapinsights_short}} utilizzando l'API REST `createEvent`.
3. Ricevi un ID evento dell'evento di traffico creato in risposta alla chiamata dell'API REST `createEvent`.
4. Cerca gli eventi di traffico in una specifica area rettangolare e, facoltativamente, con uno specifico tipo di evento di traffico, utilizzando
l'API REST `queryEvent`.

- Facoltativamente, rimuovi un evento di traffico che non è più valido utilizzando l'API REST `deleteEvent`.
- Facoltativamente, richiama un'area sulla strada che è interessata da un evento di traffico utilizzando l'API REST `getAffectedLinksInformation`.


# Link correlati
{: #rellinks}
## Esercitazioni ed esempi
{: #samples}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} - Esercitazione parte 1](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} - Esercitazione parte 2](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}

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

