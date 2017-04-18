---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Informationen zu {{site.data.keyword.iotmapinsights_short}}
{: #iotmapinsights_overview}
Letzte Aktualisierung: 20. Juli 2016
{: .last-updated}

{{site.data.keyword.iotmapinsights_full}} ist ein Service in {{site.data.keyword.Bluemix_notm}}, über den Sie schnellen Zugriff auf statische Straßennetzdaten und dynamische Ereignisdaten erhalten. {{site.data.keyword.iotmapinsights_short}} stellt auch geografisch-räumliche Tools für Straßennetze bereit, mit denen Sie geografisch-räumliche Funktionen in Ihre Anwendungen integrieren können.
{:shortdesc}

Der {{site.data.keyword.iotmapinsights_short}}-Service stellt folgende Funktionen bereit: 

- Statische Kartendaten
- Dynamische Ereignisdaten
- Geografisch-räumliche Tools

Der {{site.data.keyword.iotmapinsights_short}}-Service erfasst und verwendet Straßennetzdaten von [OpenStreetMap](http://www.openstreetmap.org/){: new_window}, die im Speichercache des Service zur Verarbeitung gespeichert werden. 

Daten von OpenStreetMap sind unter der Open Data Common Open Database License (ODbL) der OpenStreetMap Foundation (OSMF) verfügbar. Weitere Informationen finden Sie unter [OpenStreetMap Copyright and License](http://www.openstreetmap.org/copyright){: new_window}.

## Statische Kartendaten
{: #static_map_data_query}

Eine der wichtigsten Merkmale des Produkts ist die Funktion zum Abrufen detaillierter Straßendaten zur Verwendung mit Ihren Anwendungen. Verwenden Sie die REST-API-Schnittstelle zur Abfrage von Verbindungen, um statische Kartenattributdaten für Straßen nach Verbindungs-ID abzurufen. Verwenden Sie die [Kartenabgleichsfunktion](#map_matching) von {{site.data.keyword.iotmapinsights_short}}, um die erforderlichen Verbindungs-ID-Parameter zu ermitteln. 

Die zurückgegebenen Daten enthalten folgende Informationen zur angeforderten Verbindungs-ID:

- Straßenkategorie
- Straßenlänge
- Ein Array mit detaillierten Verlaufspunkten
- Informationen zu benachbarten Knoten und Verbindungen

Über die Abfrage von detaillierten Straßenverbindungsinformationen kann Ihre Anwendung ein Straßenverbindungsnetz durch die intelligente Nutzung der zurückgegebenen Informationen zu benachbarten Verbindungen durchqueren. 

## Dynamische Ereignisdaten
{: #dynamic_event_data}

Außer den statischen Kartendaten umfassen die realen Straßenbedingungen notwendigerweise auch dynamische Ereignisse wie Verkehrsstaus und Baustellen. Mit {{site.data.keyword.iotmapinsights_short}} können Sie Verkehrsereignisse mit der [Suche nach betroffenen Verbindungen](#link_search) für die Routenplanung erstellen, verwalten und integrieren. 

### Ereignisse einfügen und löschen
{: #inject_event}

Mit der REST-API zum Einfügen von Ereignissen des {{site.data.keyword.iotmapinsights_short}}-Service können Sie Verkehrsereignisse in Form von Kartenobjektmodellen, die auf bestimmten Straßenverbindungen platziert werden, dynamisch einfügen und entfernen. Jedes Ereignis umfasst grundlegende Attribute wie GPS-Koordinaten, Startzeit, Ereignistyp, Ereignisdauer und die betroffene Länge der Straße. 

Mit der REST-API-Schnittstelle zum Löschen von Ereignissen können Sie Ereignisse aus der Karte entfernen, wenn sie nicht mehr aktuell sind. 

### Ereignisabfrage
{: #query_event}

Mit der REST-API zum Abfragen von Ereignissen können Sie Detailinformationen zu allen dynamischen Ereignissen in einem bestimmten geografischen Bereich abrufen. Sie können mit einem Bereich aus Längengrad und Breitengrad nach Region abfragen und Ereignisattribute einbeziehen, um die Anzahl zurückgegebener Zielereignisse einzugrenzen. 

## Geografisch-räumliche Tools
{: #geospatial_tools}

Erweitern Sie Ihre Anwendung mit den Funktionen für Kartenabgleich und Routensuche, die von den geografisch-räumlichen Tools von {{site.data.keyword.iotmapinsights_short}} bereitgestellt werden. 

### Kartenabgleich
{: #map_matching}

Verwenden Sie die REST-API-Schnittstelle für den Kartenabgleich mit Ihrer Anwendung, um die tatsächlichen GPS-Gerätekoordinaten mit Straßennetzdaten von [OpenStreetMap](http://www.openstreetmap.org/){: new_window} abzugleichen und so die Positionsgenauigkeit für inakkurate GPS-Daten zu verbessern. Sie können auch Informationen zu Straßenattributen basierend auf der Position empfangen. Mit der REST-API für den Kartenabgleich kann Ihre Anwendung einen GPS-Rohdatenpunkt an einem abgeglichenen Punkt auf der Straßenverbindung einpassen. 

Von der REST-API-Schnittstelle für den Kartenabgleich wird ein Punkt der GPS-Koordinatendaten aus Längengrad und Breitengrad empfangen und ein mit der Karte abgeglichener Punkt zurückgegeben. Der mit der Karte abgeglichene Punkt wird unter Berücksichtigung von Langzeitdaten für jedes Fahrzeug innerhalb eines bestimmten Zeitraums analysiert, um den wahrscheinlichsten Punkt in Echtzeit zu finden. Bei Punkten, die keine Langzeitpositionsdaten aufweisen, wird von der Schnittstelle für den Kartenabgleich der Punkt auf der Straßenverbindung zurückgegeben, dessen Entfernung zum angefragten GPS-Punkt am kürzesten ist. 

### Routensuche
{: #route_search}

Eines der grundlegenden Merkmale einer Anwendung mit geografisch-räumlichen Funktionen ist die Möglichkeit, den kürzesten Weg zwischen zwei Punkten zu suchen.   

Von der REST-API-Schnittstelle für die Routensuche des {{site.data.keyword.iotmapinsights_short}}-Service wird der kürzeste Weg zwischen den GPS-Koordinaten des Startpunkts und des Endpunkts berechnet. Die empfangenen Koordinaten werden mithilfe der Funktion für den Kartenabgleich mit der nächsten Verbindung auf der Karte abgeglichen und der kürzeste Weg zwischen diesen mit der Karte abgeglichenen Punkten wird berechnet. 

### Suche nach betroffenen Verbindungen
{: #link_search}

Wenn auf einer Straße ein Ereignis auftritt, kann es unterschiedliche Straßenverbindungen beeinträchtigen. Mit den REST-APIs können Sie nach betroffenen Verbindungen und nach Straßenverbindungen suchen, über die die Fahrzeuge das Ereignis erreichen können. Bei der Suche wird die Topologie des Straßenverbindungsnetzes berücksichtigt, nicht nur der Abstand von den Fahrzeugen zum Ereignis. 
