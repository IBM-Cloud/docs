---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Einführung in {{site.data.keyword.iot4auto_short}} (Beta)
{: #getting_started_iotautomotive}

Letzte Aktualisierung: 29. Juli 2016
{: .last-updated}

Bei {{site.data.keyword.iot4auto_full}} handelt es sich um einen {{site.data.keyword.Bluemix_notm}}-Service, mit dessen Hilfe Sie eine große Datenmenge und -vielfalt aus verbundenen Fahrzeugen abrufen, verwalten und analysieren können. Die Analyse von {{site.data.keyword.iot4auto_short}} liefert leistungsfähige und verlässliche Informationen zum Fahrverhalten, zur Fahrzeugposition sowie zu anderen interessanten Aktivitäten und Ereignissen im Automobilbereich.

{:shortdesc}

Mit {{site.data.keyword.iot4auto_short}} können Sie die folgenden Tasks ausführen:

- Autotestdaten und normalisierte Autodaten zur Analyse an den Datenspeicher senden
- Ereignisse in die Kontextzuordnung einfügen und die Ereignisse abrufen, die sich auf bestimmte Fahrzeuge auswirken
- Neue Ereignisse anhand der Autotestdaten ermitteln
- Informationen zu verbundenen Fahrzeugen abrufen
- Assetdaten für Fahrer, Fahrzeuge, Ereignisregeln, Ereignistypen und Anbieter verwalten


Der Service {{site.data.keyword.iot4auto_short}} umfasst die folgenden {{site.data.keyword.Bluemix_notm}}-Services, die im {{site.data.keyword.Bluemix_notm}}-Katalog auch separat erhältlich sind:

|Service|Beschreibung|
|:---|:---|
|[Driver Behavior](../IotDriverInsights/index.html){:new_window}| Ein Service, mit dem das Fahrerverhalten analysiert und Bewegungsmuster einer Fahrt aus den Autotest- und Kontextdaten ermittelt werden können, die aus einem verbundenen Fahrzeug abgerufen werden.
|[Context Mapping](../IotMapInsights/index.html){:new_window}| Ein Service, der Geofunktionen bereitstellt, z. B. Kartenabgleich und Suche des kürzesten Pfads für Straßennetze.
*Tabelle 1. Services von {{site.data.keyword.iot4auto_short}}*

Vor der Integration Ihrer Fahrzeuggeräte und -anwendungen mit dem Service müssen Sie sicherstellen, dass Sie die folgenden Schritte ausgeführt haben:

1. Sie haben den Abschnitt [Informationen zu {{site.data.keyword.iot4auto_short}}](iotautomotive_overview.html) gelesen, um sich mit den Features und der Analyse vertraut zu machen, die für den Service verfügbar sind und unterstützt werden.
2. Beim Hinzufügen einer Instanz des Service aus dem [{{site.data.keyword.Bluemix_notm}}-Katalog](https://console.ng.bluemix.net/catalog/labs/){:new_window} müssen Sie sicherstellen, dass er nicht an eine App gebunden ist; außerdem müssen Sie sich die automatisch generierte Tenant-ID und die Werte für Benutzername und Kennwort notieren. Diese Werte benötigen Sie zu einem späteren Zeitpunkt für den Zugriff auf den Service über die {{site.data.keyword.iot4auto_short}}-API.
3. Mithilfe der Konsole im Dashboard konfigurieren Sie die Ports, Zielhostnamen und andere Einstellungen für Ihre Instanz von {{site.data.keyword.iot4auto_short}}. Weitere Informationen finden Sie im Thema zur [Verwaltung](iotautomotive_admin.html).

Sie können Ihre Fahrzeuggeräte und -anwendungen mit diesem Service unter Verwendung der {{site.data.keyword.iot4auto_short}}-REST-API-Befehle integrieren.

Führen Sie für einen Start ohne zeitliche Verzögerung die folgenden Schritte aus:

1. Einfügen von Ereignissen mithilfe des API-Anforderungsbefehls `sendEvent`, um zu analysierende Ereignisse zu senden.
  - Anforderung: Ereignisdaten mit Position
2. Bestätigen, dass die Ereignisdaten mit Map Matching gespeichert werden, und zwar unter Verwendung des API-Anforderungsbefehls `getEvent` zum Abrufen des Ereignisses.
  - Anforderung: Flächendaten (Längengrad und Breitengrad der Start- oder Endpunkte)
  - Antwort: Ereignisdaten mit ID für Straßenverbindung
3.  Senden der zu analysierenden Autotestdaten mithilfe des API-Anforderungsbefehls `sendCarProbe`.
  - Anforderung: Autotestdaten mit Position
4. Bestätigen, dass die Autotestdaten mit Map Matching gespeichert werden, und zwar unter Verwendung des API-Anforderungsbefehls `getCarProbe` zum Abrufen der Daten.
  - Anforderung: Flächendaten (Längengrad und Breitengrad der Start- oder Endpunkte)
  - Antwort: Autotestdaten mit ID für Straßenverbindung
5. Analysieren der Fahrerdaten. Weitere Informationen finden Sie unter [Driver Behavior (Fahrerverhalten)](../IotDriverInsights/index.html){:new_window}.

# Zugehörige Links
{: #rellinks}

## API-Referenz
{: #api}
* [{{site.data.keyword.iot4auto_short}}-API-Dokumentation](http://ibm.biz/IoT4Automotive_APIdoc){:new_window}
* [Context Mapping - Service-APIs](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}
* [Driver Behavior - Service-APIs]( http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}


## Zugehörige Links
{: #general}
* [Einführung in {{site.data.keyword.iotdriverinsights_short}}](../IotDriverInsights/index.html){:new_window}
* [Einführung in {{site.data.keyword.iotmapinsights_short}}](../IotMapInsights/index.html){:new_window}
* [Einführung in {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [Neuerungen bei den Bluemix-Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [dW Answers in IBM developerWorks](https://developer.ibm.com/answers/topics/iot-for-automotive){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/iot-for-automotive){:new_window}
