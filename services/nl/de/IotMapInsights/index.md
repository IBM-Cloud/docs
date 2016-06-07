---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Einführung in {{site.data.keyword.iotmapinsights_short}}
{: #gettingstartedtemplate}
*Letzte Aktualisierung: 13. Mai 2016*

{{site.data.keyword.iotmapinsights_full}} erleichtert es Entwicklern, ihren Anwendungen die Verwendung geografisch-räumlicher Funktionen wie den Kartenabgleich oder die Suche nach dem kürzesten Weg auf der Basis des weltweiten Straßennetzes zu ermöglichen.
{:shortdesc}

Über die {{site.data.keyword.iotmapinsights_short}}-REST-API können Sie folgenden Funktionen verwenden: 

- Hochgenauer Kartenabgleich über die Straßennetzgeometrie. 
- Bearbeitung von Echtzeit-Ereignissen auf einer Karte, zum Beispiel des Verkehrs. 
- Dynamische Suche nach dem kürzesten Weg (Routensuche) unter Berücksichtigung von Echtzeit-Ereignissen, wie zum Beispiel des Verkehrs. 
- Abrufen der Straßengeometriedaten, die zum Zeichnen der Straßenkonturen auf einer Karte verwendet werden können. 

Vom {{site.data.keyword.iotmapinsights_short}}-Service werden die Straßennetzdaten in WGS84-Koordinaten verwendet, die von OpenStreetMap extrahiert werden. Für die Analyse werden nur Straßen verwendet, auf denen ein Fahrzeug fahren kann. 

Folgende Kartenregionen werden unterstützt: 

- Europa (Karten-ID 1)
- Afrika (Karten-ID 2)
- Asien (Karten-ID 3)
- Australien/Ozeanien (Karten-ID 4)
- Nordamerika (Karten-ID 5)
- Mittelamerika (Karten-ID 6)
- Südamerika (Karten-ID 7)


Führen Sie die folgenden Schritte aus, um die Analysefunktionen des {{site.data.keyword.iotmapinsights_short}}-Service zu verwenden. 

## {{site.data.keyword.iotmapinsights_short}} zum Kartenabgleich verwenden

1. Bereiten Sie unaufbereitete GPS-Koordinaten vor, die analysiert werden sollen. 
2. Senden Sie die unaufbereiteten GPS-Koordinaten in einer Zeitreihenfolge über die `mapMatching`-REST-API an den {{site.data.keyword.iotmapinsights_short}}-Service. Legen Sie optional einen Gierwinkel für jede Position in Grad fest (Norden ist 0, Winkel im Uhrzeigersinn), um die Fahrtrichtung anzugeben. 
3. Empfangen Sie die mit der Karte abgeglichenen Koordinaten und Straßenverbindungsinformationen als Antwort auf den Aufruf der `mapMatching`-REST-API. 
4. Rufen Sie optional die Daten zu den Straßenumrissen der mit der Karte abgeglichenen Straßenverbindung über die `getLinkInformation`-REST-API ab. Rufen Sie die `getLinkInformation`-REST-API mit einer Link-ID auf, um eine Reihe von Koordinaten abzurufen, die aus einem Straßenumriss bestehen. 

## {{site.data.keyword.iotmapinsights_short}} für die Routensuche verwenden

1. Legen Sie die Start- und Endposition für die Strecke fest, für die der kürzeste Weg berechnet werden soll. 
2. Senden Sie die Start- und Endkoordinaten über die `routeSearch`-REST-API an den {{site.data.keyword.iotmapinsights_short}}-Service. Legen Sie optional einen Gierwinkel für jede Position in Grad fest (Norden ist 0, Winkel im Uhrzeigersinn), um die Fahrtrichtung anzugeben. 
3. Empfangen Sie als Antwort auf den Aufruf über die `routeSearch`-REST-API eine Liste der Straßenverbindungen. Sie können den Umriss des gefundenen Wegs mithilfe der in den Ergebnisdaten enthaltenen Umrissdaten auf einer Karte anzeigen. 

## {{site.data.keyword.iotmapinsights_short}} zum Bearbeiten von Verkehrsereignissen verwenden

1. Legen Sie Typ und Position für ein Verkehrsereignisses fest, das Sie erstellen möchten. 
2. Senden Sie die Informationen zu diesem Verkehrsereignis über die `createEvent`-REST-API an {{site.data.keyword.iotmapinsights_short}}-Service. 
3. Empfangen Sie als Antwort auf den Aufruf über die `createEvent`-REST-API eine Ereignis-ID zum erstellten Verkehrsereignis. 
4. Durchsuchen Sie mit der `queryEvent`-REST-API die Verkehrsereignisse in einem bestimmten rechteckigen Bereich, und optional unter Verwendung eines bestimmten Ereignistyps. 

- Entfernen Sie bei Bedarf über die `deleteEvent`-REST-API ein Verkehrsereignis, das nicht mehr gültig ist. 
- Rufen Sie optional über die `getAffectedLinksInformation`-REST-API einen Bereich auf einer Straße ab, der durch ein Verkehrsereignis beeinträchtigt wird. 


# Zugehörige Links
{: #rellinks}
## Lernprogramme und Beispiele
{: #samples}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} Lernprogramm Teil 1 ](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} Lernprogramm Teil 2](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}

## API-Referenz
{: #api}

* [API-Dokumentation](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}

## Zugehörige Links
{: #general}
* [Einführung in {{site.data.keyword.iotdriverinsights_short}}](../IotDriverInsights/index.html){:new_window}
* [Einführung in {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [dW-Antworten zu IBM developerWorks](https://developer.ibm.com/answers/topics/iot-context-mapping){:new_window}
* [Stacküberlauf](http://stackoverflow.com/questions/tagged/iot-context-mapping){:new_window}
* [Neuerungen in Bluemix-Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [OpenStreetMap](http://www.openstreetmap.org/){:new_window}

