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

Der {{site.data.keyword.iotmapinsights_short}}-Service basiert auf Straßennetzdaten, die im Speichercache gespeichert werden. Vom Service wird ein Hochgeschwindigkeitszugriff auf statische Straßennetzdaten, dynamische Ereignisdaten und auf dem Straßennetz basierende geografisch-räumliche Tools bereitgestellt,  The service provides high-speed access to static road network data, dynamic event data, and road network-based geospatial tools; dies ermöglicht der Anwendung das Integrieren geografisch-räumlicher Funktionen.
{:shortdesc}

## Abfrage statischer Kartendaten
{: #static_map_data_query}

Für den Zugriff auf Attributdaten für Straßenverbindungen wird vom {{site.data.keyword.iotmapinsights_short}}-Service eine REST-API-Schnittstelle für Verbindungsabfragen bereitgestellt. Von der Schnittstelle wird eine Verbindungs-ID als Parameter empfangen, der von einer Kartenabgleichsfunktion identifiziert werden kann und von dem detaillierte Informatonen zur angeforderten Verbindung zurückgegeben werden können, zum Beispiel Straßentyp, Länge, Arrays für Punkte für Detailumrisse, benachbarte Knoten und benachbarte Verbindungen. Mithilfe der abgefragen detaillierten Verbindungsinformationen kann die Anwendung ein Straßenverbindungsnetz unter Beachtung der benachbarten Verbindungsinformationen durchqueren. 

## Dynamische Ereignisdaten
{: #dynamic_event_data}

Ein Ereignis im {{site.data.keyword.iotmapinsights_short}}-Service ist ein Objektmodell für ein Verkehrsereignis, das auf einer bestimmten Straßenverbindung dynamisch platziert wird. Das Ereignis weist grundlegende Attribute eines Verkehrsereignisses auf, zum Beispiel GPS-Koordinaten, Zeit, Typ, Ereignisdauer und betroffene Länge. Sie können Ereignisse dynamisch einfügen und löschen. 

## Einfügen und Löschen von Ereignissen
{: #inject_event}

Mit der REST-API-Schnittstelle zum Einfügen von Ereignissen können Sie ein Ereignis auf einer Karte speichern. Wenn Sie ein Ereignis einfügen möchten, können Sie die Ereignisdaten mit einem definierten Ereignistyp an die Schnittstelle senden, um die Ereignisse und zugehörigen Attribute in Übereinstimmung mit der beabsichtigten Verwendung der Anwendung zu klassifizieren. Mit der REST-API-Schnittstelle zum Löschen von Ereignissen können Sie Ereignisse aus der Karte entfernen und so veraltete Ereignisse verwalten. 

## Ereignisabfrage
{: #query_event}

Mit der REST-API-Schnittstelle zum Abfragen von Ereignissen können Sie Ereignisse unter bestimmten Bedingungne abfragen, der als Abfrageparameter eingestellt werden. Für die Abfragebedingung können Sie einen Längengrad- und Breitengradbereich sowie Ereignisattribute zum Eingrenzen der Zielereignisse festlegen, die als Antwort auf die Anforderung zurückgegeben wird. 

## Geografisch-räumliche Tools
{: #geospatial_tools}

Für geografisch-räumliche Tools wird vom {{site.data.keyword.iotmapinsights_short}}-Service eine REST-API-Schnittstelle zum Kartenabgleich und für Routensuchfunktionen bereitgestellt. 

## Kartenabgleich
{: #map_matching}

Wenn die GPS-Daten der Geräte für die Analyse oder Visualisierung nicht genau genug sind, oder wenn die Attribute des Straßenverbindngsnetzes für die Anwendung erforderlich sind, können Sie die REST-API-Schnittstelle für den Kartenabgleich verwenden. Mit der REST-API-Schnittstelle für den Kartenabgleich kann die App einen GPS-Rohdatenpunkt an einen abgeglichenen Punkt auf der Straßenverbindung einpassen. Von der REST-API-Schnittstelle für den Kartenabgleich wird ein Punkt der GPS-Koordinatendaten aus Längengrad und Breitengrad empfangen und eine mit der Karte abgeglichener Punkt zurückgegeben. Dieser Punkt wird unter Berücksichtigung von Langzeitdaten für jedes Fahrzeug innerhalb eines bestimmten Zeitraums analysiert, um den wahrscheinlichsten Punkt in Echtzeit zu finden. Bei einem Punkt, der keine Langzeitpositionsdaten aufweist, wird von der Schnittstelle für den Kartenabgleich der Punkt auf der Straßenverbindung zurückgegeben, dessen Entfernung zum angefragten GPS-Punkt am niedrigsten ist. 

## Routensuche
{: #route_search}

Wenn Sie eine Anwendung mit geografisch-räumlichen Funktionen bereitstellen müssen, müssen Sie den kürzesten Weg zwischen zwei Punkten suchen. Von der REST-API-Schnittstelle für die Routensuche des {{site.data.keyword.iotmapinsights_short}}-Service wird der kürzeste Weg zwischen den GPS-Koordinaten des Startpunkts und des Endpunkts berechnet. Die empfangenen Koordinaten werden mithilfe der Funktion für den Kartenabgleich mit der nähesten Verbindung auf der Karte abgeglichen und der kürzeste Weg zwischen diesen mit der Karte abgeglichenen Punkten wird berechnet. 

## Beeinträchtigte Verbindungssuche
{: #link_search}

Wenn auf der Straße ein Ereignis auftritt, kann es unterschiedliche Straßenverbindungen beeinträchtigen. Mit den REST-APIs können Sie die beeinträchtigten Verbindungen durchsuchen and nach Straßenverbindungen suchen, über die die Fahrzeuge das Ereignis vermeiden können. Bei der Suche wird auch die Topologie des Straßenverbindungsnetzes berücksichtigt, nicht nur der Abstand von den Fahrzeugen zum Ereignis. 

