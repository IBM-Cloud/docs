---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Informationen zu {{site.data.keyword.iot4auto_short}} (Beta)
{: #iotautomotive_overview}

Letzte Aktualisierung: 29. Juli 2016
{: .last-updated}

Bei {{site.data.keyword.iot4auto_full}} handelt es sich um einen {{site.data.keyword.Bluemix_notm}}-Service, mit dessen Hilfe Sie eine große Datenmenge und -vielfalt aus Fahrzeugen anzeigen und analysieren können.

Mithilfe des Service {{site.data.keyword.iot4auto_short}} können Sie umfangreiche Mengen von Daten aus Fahrzeugen erfassen und verarbeiten. Die Analyse von {{site.data.keyword.iot4auto_short}} liefert leistungsfähige und verlässliche Informationen zum Fahrerverhalten, zur Fahrzeugposition sowie zu anderen interessanten Aktivitäten und Ereignissen im Automobilbereich.
{:shortdesc}

## Architektur
{: #architecture}
{{site.data.keyword.iot4auto_short}} ist eine Basisplattform mit einer echtzeitorientierten Infrastruktur für Anwendungen im Automobilbereich und verbundene Fahrzeuggeräte. Der Service wurde auch zur zukünftigen Unterstützung im immer stärker werdenden Bereich des autonomen Fahrens entworfen.

![{{site.data.keyword.iot4auto_full}}-Architektur](images/architecture_iotautomotive.png "{{site.data.keyword.iot4auto_full}}-Architektur")

Der Service {{site.data.keyword.iot4auto_short}} umfasst die folgenden {{site.data.keyword.Bluemix_notm}}-Services, die im {{site.data.keyword.Bluemix_notm}}-Katalog auch separat erhältlich sind:

|Service|Beschreibung|
|:---|:---|
|[Driver Behavior](../IotDriverInsights/index.html)| Ein Service, mit dem das Fahrerverhalten analysiert und Bewegungsmuster einer Fahrt aus den Autotest- und Kontextdaten ermittelt werden können, die aus einem verbundenen Fahrzeug abgerufen werden.
|[Context Mapping](../IotMapInsights/index.html)| Ein Service, der Geofunktionen bereitstellt, z. B. Kartenabgleich und Suche des kürzesten Pfads für Straßennetze.
*Tabelle 1. {{site.data.keyword.iot4auto_short}}-Services*

## Features
{: #features}

{{site.data.keyword.iot4auto_short}} unterstützt die folgenden Features und Funktionen für Lösungen, die Autotestdaten aus verbundenen Fahrzeuggeräten bereitstellen:

### Datenabruf aus {{site.data.keyword.iot4auto_short}}-Geräten

- Unterstützt die folgenden Protokolle und Datenmodelle:
   - TPEG
   - ITS
   - ISO-Standards für den Automobilbereich
- Unterstützt weitere Geräte und Sensoren außerhalb des Fahrzeugbereichs

### Datennormalisierung und Datenspeicherung

- Ermittelt und filtert unregelmäßige Daten
- Ordnet Daten für die Analyse zum Standarddatenmodell zu und konvertiert und formatiert sie
- Stellt Daten in Abhängigkeit von ihrem Umfang, der Latenzzeit sowie der Nutzung der Anwendung oder des Service in einen der folgenden Datenspeicher:
   -  Hadoop-Datenspeicher für die Analyse einer großen Datenmenge und -vielfalt
   -  Agentendatenspeicher für eine Echtzeitanalyse

### Geodatenkartenbasierter Service

- Echtzeitorientierter Kartenabgleich
- Ereignisservice
- Dynamische Ereignisinjektion aus Fahrzeugen und externen Quellen
- Link- oder knotenbasierte, topologiesensitive Suche
- Unterstützung für Kontextzuordnung mit integrierten Wetterdaten

### Hoch skalierbare Echtzeitanalyseplattform mit niedriger Latenzzeit

- Agentenbasierte Technologie
- Personalisierte Analyse
- Flexible, regelbasierte Analyse

### MOMA (Moving Object Map Analysis, Kartenanalyse zu einem sich bewegenden Objekt)

- Stapelanalyse (Analyse einer großen Datenmenge und -vielfalt) mit Daten aus dem Fahrzeug
- Analyse des Fahrerverhaltens
- Erstellung eines Fahrerprofils
- Analyse des Bewegungsablaufmusters

### Datenanbieterservice

- APIs für Anwendungen und Services von Drittanbietern

### Integration mit Asset-Management

- Asset-Management-Systeme für Fahrzeuge

## REST-API
{: #api}

Die [{{site.data.keyword.iot4auto_short}}-API](http://ibm.biz/IoT4Automotive_APIdoc) stellt Befehle bereit, mit deren Hilfe Sie {{site.data.keyword.iot4auto_short}} für Ihre Anforderungen weiter entwickeln können.

Mithilfe der verfügbaren REST-API-Befehle können Sie die Instanz Ihres {{site.data.keyword.iot4auto_short}}-Service anpassen:

- Bestimmte Ereignisse in das System einfügen
- Die normalisierten Autotestdaten aus einem Fahrzeug im bevorzugten Analysedatenspeicher speichern
- Die für Sie interessanten Ereignisse in Echtzeit zusammen mit dem Standort des Fahrzeugs abrufen

### REST-API-Befehle

|Ziel |API-Befehl |Beschreibung |
|:---|:---|:---|
|Ereignis einfügen|`sendEvent`|Sendet Verkehrsdaten oder andere Ereignisse an die Plattform.|
|Autotestdaten senden|`sendCarProbe`|Sendet die positionsbasierten Sensordaten aus dem Fahrzeug und ruft die betroffenen Ereignisse für das Fahrzeug nach Ergebnis der Echtzeitanalyse ab.|
|Fahrzeugdaten erstellen|`createVehicle`|Es wird ein Datensatz des Fahrzeugs als Asset erstellt. Diese Informationen werden für Authentifizierung, Inventarisierung und andere Zwecke verwendet.|
|APIs zuordnen|Nicht anwendbar|Weitere Informationen finden Sie bei den [APIs für den Service 'Context Mapping'](http://ibm.biz/IoTContextMapping_APIdoc).|
|Analyse-APIs|Nicht anwendbar|Weitere Informationen finden Sie bei den [APIs für den Service 'Driver Behavior']( http://ibm.biz/IoTDriverBehavior_APIdoc).|
|Autotestdaten abrufen|`getCarProbe`|Ruft die aktuellen Autotestdaten des Fahrzeugs ab, die mithilfe des API-Befehls `sendCarProbe` gesendet wurden.|
|Kartenereignisse abrufen|`getEvent` |Ruft die Ereignisse für die Karte ab, die mithilfe des API-Befehls `sendEvent` gesendet wurden.|
|Fahrzeugassetdaten abrufen|`getVehicle`| Ruft die Fahrzeugdaten mithilfe des API-Befehls `createVehicle` als Asset ab.|
*Tabelle 2. {{site.data.keyword.iot4auto_short}}-REST-API-Befehle*
