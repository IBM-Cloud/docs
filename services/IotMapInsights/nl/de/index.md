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
{: #iotdriverinsights_index}
Letzte Aktualisierung: 22. Juni 2016
{: .last-updated}

{{site.data.keyword.iotmapinsights_full}} ist ein Service in {{site.data.keyword.Bluemix}}, mit dem Sie die Verwendung geografisch-räumlicher Funktionen wie den Kartenabgleich oder die Suche nach dem kürzesten Weg auf der Basis des weltweiten Straßennetzes für Ihre Anwendungen aktivieren können.   
{:shortdesc}

Die folgenden Funktionen stehen über die {{site.data.keyword.iotmapinsights_short}}-REST-API zur Verfügung: 

|Funktion|Verwendung...|
|:---|:---|
|Hochgenauer Kartenabgleich|Gleicht Ihre GPS-Position mit dem tatsächlichen, zugeordneten Straßennetz ab.|
|Abruf der Straßengeometriedaten|Ruft das zugeordnete Straßennetz ab, um den Straßenverlauf in einer Karte einzuzeichnen.|
|Dynamische Suche nach dem kürzesten Pfad|Sucht nach dem kürzesten Pfad unter Einbeziehung von Echtzeitereignissen wie dem Verkehr.|
|Bearbeitung von Verkehrsereignissen in Echtzeit|Fügt mit der Karte abgeglichene Echtzeitereignisse, wie zum Beispiel Verkehrsverhältnisse, hinzu, um die Ergebnisse der Routenplanung zu verbessern.|

## Vorbereitende Schritte
{: #byb}

1. Wenn Sie eine Instanz des Service aus dem [{{site.data.keyword.Bluemix_notm}}-Katalog](https://console.stage1.ng.bluemix.net/catalog/services/iot-automotive/){: new_window} hinzufügen, stellen Sie sicher, dass sie nicht an eine App gebunden ist, und notieren Sie die automatisch generierten Werte für Tenant-ID, Benutzername und Kennwort. Sie benötigen diese Werte später, um über die {{site.data.keyword.iotmapinsights_short}}-API auf den Service zuzugreifen.

2. Machen Sie sich mit [OpenStreetMap](http://www.openstreetmap.org/){: new_window} vertraut.  

 Vom {{site.data.keyword.iotmapinsights_short}}-Service werden die Straßennetzdaten in WGS84-Koordinaten verwendet, die von [OpenStreetMap](http://www.openstreetmap.org/){: new_window} extrahiert werden. Für die Analyse werden nur Straßen verwendet, auf denen ein Fahrzeug fahren kann.   

 Die folgenden Kartenregionen werden unterstützt: 

|Region|Karten-ID|
|:---|:---|
|Europa|map_id=1|
|Afrika|map_id=2|
|Asien|map_id=3|
|Australien / Ozeanien|map_id=4|
|Nordamerika|map_id=5|
|Mittelamerika|map_id=6|
|Südamerika|map_id=7|

## Kartenabgleich
{: #map_matching}
Führen Sie die folgenden Schritte aus, um unaufbereitete GPS-Koordinaten Koordinaten zuzuordnen, die mit Karten abgeglichen sind: 

1. Bereiten Sie unaufbereitete GPS-Koordinaten vor, die analysiert werden sollen. 
2. Senden Sie die unaufbereiteten GPS-Koordinaten mit dem `mapMatching`-API-Befehl. Legen Sie optional einen Gierwinkel für jede Position in Grad fest, um die Fahrtrichtung anzugeben. 
 - Anforderung: Unaufbereitete GPS-Daten
 - Antwort: Mit der Karte abgeglichene GPS-Daten, Verbindungs-ID
3. Optional: Rufen Sie die Straßenkategoriedaten mit dem `getLinkInformation`-API-Befehl ab. Sie können die abgeglichenen Straßenverlaufsdaten als Serie von Koordinaten mit der `getLinkInformation`-REST-API abrufen. 
 - Anforderung: Verbindungs-ID
 - Antwort: Straßenkategorie

## Routensuche
{: #route_searching}

Führen Sie die folgenden Schritte aus, um Informationen zum kürzesten Weg zwischen den angegebenen Start- und Zielkoordinaten zu suchen. 

1. Legen Sie die Start- und Endposition für den kürzesten Weg fest. 
2. Senden Sie die Start- und Endkoordinaten über die `routeSearch`-REST-API.
Legen Sie optional einen Gierwinkel für jede Position in Grad fest, um die Fahrtrichtung anzugeben. 
 - Anforderung: Start- und Zielkoordinaten
 - Antwort: Mit der Karte abgeglichene kürzeste Route

Sie können den Verlauf des gefundenen Wegs mithilfe der zurückgegebenen Daten des Verbindungsverlaufs in einer Karte einzeichnen. 

## Verkehrsereignisse hinzufügen
{: #traffic_events}

Führen Sie die folgenden Schritte aus, um Informationen zu Verkehrsereignissen zum {{site.data.keyword.iotmapinsights_short}}-Service hinzuzufügen: 

1. Wählen Sie Typ und Position des Verkehrsereignisses aus, das Sie erstellen möchten. 
2. Fügen Sie das Ereignis mit dem `createEvent`-API-Befehl ein.
Senden Sie die Informationen zu dem Verkehrsereignis an den {{site.data.keyword.iotmapinsights_short}}-Service.
 - Anforderung: Ereignisdaten
 - Antwort: Ereignis-ID
3. Suchen Sie Ereignisse mit dem `queryEvent`-REST-API-Befehl.
Suchen Sie nach Verkehrsereignissen in einem bestimmten rechteckigen Bereich, und optional nach einem bestimmten Typ von Verkehrsereignissen. 
 - Anforderung: Bereichsdaten
 - Antwort: Ereignisdaten  
4. Optional: Entfernen Sie ein Verkehrsereignis, das nicht mehr gültig ist, mit dem `deleteEvent`-API-Befehl. 
5. Optional: Rufen Sie einen Bereich auf einer Straße, der durch ein Verkehrsereignis beeinträchtigt wird, mit dem `getAffectedLinksInformation`-API-Befehl ab. 

# Zugehörige Links
{: #rellinks}

## Lernprogramme und Beispiele
{: #samples}

* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} Lernprogramm Teil 1 ](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} Lernprogramm Teil 2](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}
* [IoT for Automotive Starter - Anwendung](https://iot-automotive-starter.mybluemix.net){:new_window}

## API-Referenz
{: #api}

* [API-Dokumentation](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}

## Zugehörige Links
{: #general}

* [Einführung in {{site.data.keyword.iotdriverinsights_short}}](../IotDriverInsights/index.html){:new_window}
* [Einführung in {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [dW Answers zu IBM developerWorks](https://developer.ibm.com/answers/topics/iot-context-mapping){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/iot-context-mapping){:new_window}
* [Neuerungen in Bluemix-Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [OpenStreetMap](http://www.openstreetmap.org/){:new_window}
* [&copy; OpenStreetMap Contributors](http://www.openstreetmap.org/copyright){:new_window}
* [Open Data Commons Open Database License (ODbL)](http://opendatacommons.org/licenses/odbl/){:new_window}
