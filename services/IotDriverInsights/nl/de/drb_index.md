---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Einführung in die Analyse des Fahrverhaltens
{: #drb_index}
Letzte Aktualisierung: 16. Juni 2016
{: .last-updated}

Die Analyse des Fahrverhaltens ist ein Service innerhalb des {{site.data.keyword.iotdriverinsights_full}}-Service von {{site.data.keyword.Bluemix_notm}}, mit dem Sie das Fahrerverhalten aus Fahrzeugtestdaten und Kontextdaten erfassen und analysieren können. Außerdem können Sie mithilfe der {{site.data.keyword.iotdriverinsights_short}}-API die analysierten Daten zum Fahrerverhalten in Ihre anderen {{site.data.keyword.Bluemix_notm}}-Anwendungen integrieren. 

{:shortdesc}

Im folgenden Diagramm wird die typische Sequenz von API-Aufrufen im Service zur Analyse des Fahrverhaltens dargestellt: 

![Typische Analysesequenz](images/sequence_diagram.png "Typische Analysesequenz")

Führen Sie nach der Erstellung und Bereitstellung von {{site.data.keyword.iotdriverinsights_short}} als nicht gebundene Serviceinstanz die folgenden Tasks aus, um Ihre Anwendungen in die {{site.data.keyword.iotdriverinsights_short}}-API zu integrieren.

Sie können auch das [Lernprogramm zu {{site.data.keyword.iotmapinsights_short}} und {{site.data.keyword.iotdriverinsights_short}}](https://github.com/IBM-Bluemix/car-data-management){:new_window} verwenden, um eine Beispielanwendung mit Fahrzeugtestbeispieldaten zu erstellen. 


## Vorbereitende Schritte
{: #drb_byb}

- Lesen Sie den Abschnitt [Informationen zur Analyse des Fahrverhaltens](drb_iotdriverinsights_overview.html), um sich mit den analysierbaren Verhaltensweisen und Kontexten vertraut zu machen. 
- Rufen Sie die automatisch generierten Werte für *Tenant-ID*, *Benutzername* und *Kennwort* ab, die erforderlich sind, um auf die {{site.data.keyword.iotdriverinsights_short}}-API zuzugreifen.

1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf die Kachel für den {{site.data.keyword.iotdriverinsights_short}}-Service. 
2. Wählen Sie die Ansicht **Verwalten** Ihrer Serviceinstanz aus. 
3. Notieren Sie die Werte für *Tenant-ID*, *Benutzername* und *Kennwort*, die angezeigt werden. 

- Optional: Wenn Sie geografisch-räumliche Funktionen mit Ihren Fahrerdaten verwenden möchten, stellen Sie den {{site.data.keyword.iotmapinsights_short}}-Service von {{site.data.keyword.Bluemix_notm}} in Ihrer Organisation bereit.

## Task 1: Fahrzeug- und Kontextdaten hochladen
{: #drb_task1}
Laden Sie ein oder mehrere Sets von Fahrtdaten eines Fahrers in Ihren {{site.data.keyword.iotdriverinsights_short}}-Tenant hoch, damit die Fahrerdaten für die Analyse bereitstehen. 

1. Optional: Wenn Sie den {{site.data.keyword.iotmapinsights_short}}-Service bereitgestellt haben, ordnen Sie die Fahrerdaten Geodaten zu.
Bevor Ihre Anwendung Fahrzeugtestdaten an die [{{site.data.keyword.iotdriverinsights_short}}-API](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window} sendet, können Sie diese Daten mit der [{{site.data.keyword.iotmapinsights_short}}-API](http://ibm.biz/IoTContextMapping_APIdoc){:new_window} Geodaten zuordnen. Geodaten verbessern die Qualität der Analyseergebnisse des Fahrerverhaltens. 

     1. Mit der Karte abgeglichene Fahrzeugtestdaten über die `mapMatching`-API abrufen.
     Beim Kartenabgleich werden die Fahrdaten des Fahrzeugtests mit den Geodaten der Straße abgeglichen. 
        - Anforderung: Fahrzeugtestdaten
        - Antwort: Mit der Karte abgeglichene Fahrzeugtestdaten
     2. Straßenkategoriedaten über die `getLinkInformation`-API abrufen.  
        - Anforderung: Straßenverbindungs-ID
        - Antwort: Straßenkategorie
2. Senden Sie Fahrzeugtestdaten zur Analyse über die `sendCarProbeData`-API an den Speicher.
Laden Sie die unaufbereiteten Fahrzeugtestdaten und optional die abgeglichenen Geodaten auf {{site.data.keyword.iotdriverinsights_short}} hoch.
   - Anforderung: Mit der Karte abgeglichene Fahrzeugtestdaten und Straßenkategorie

## Task 2: Fahrzeug- und Kontextdaten verarbeiten  
{: #drb_task2}
Verarbeiten Sie die Fahrzeug- und Kontextdaten mit den konfigurierbaren Analyseparametern. Informationen zum Konfigurieren der Analyseparameter finden Sie im Abschnitt [Parameter für den Service konfigurieren](drb_iotdriverinsights_admin.html#configureparameters). 

1. Senden Sie eine Jobanforderung zur Analyse der Fahrzeugtestdaten während eines bestimmten Zeitraums über die `sendJobRequest`-API. 
   - Anforderung: Datum von/bis
   - Antwort: Job-ID
2. Überprüfen Sie den Jobstatus über die `getJobInfo`-API.
Die Verarbeitung der Daten zum Fahrerverhalten ist beendet, wenn der zurückgegebene Jobstatus 'SUCCEEDED' lautet. Nun können Sie Fahrerverhaltensdaten anfordern. 
   - Anforderung: Job-ID
   - Antwort: Jobstatus

## Task 3: Fahrten analysieren
{: #drb_task3}
Analysieren Sie Fahrten eines bestimmten Datumsbereichs, um zu sehen, wie sie den Schwellenwertparametern der Analyse entsprechen. 

1. Rufen Sie die Zusammenfassungsliste der analysierten Fahrten über die `getAnalyzedTripSummaryList`-API ab. Die Fahrtzusammenfassungsliste enthält eine Zusammenfassung der Informationen zu analysierten Fahrten entsprechend den Eingabeparametern. 
   - Anforderung: Job-ID
   - Antwort: Zusammenfassungsliste der analysierten Fahrten
2. Rufen Sie detaillierte Informationen zu analysierten Fahrten über die `getAnalyzedTripInfo`-API ab.
Rufen Sie als Letztes die detaillierten Informationen zum Fahrerverhalten für eine bestimmte analysierte Fahrt ab. 
   - Anforderung: Fahrt-UUID
   - Antwort: Details der analysierten Fahrt

## Nächste Schritte
{: #drb_post}
Nachdem Sie die Schritte ausgeführt haben, wird ein Set von Fahrerverhaltensdaten in Ihrer Organisation generiert. Sie können die Informationen mit Ihren Anwendungen oder Ihrer bevorzugten Analysesoftware weiter verarbeiten, um aussagefähigere Geschäftsdaten zu erhalten. 

# Zugehörige Links
{: #rellinks}

## Lernprogramme und Beispiele
{: #samples}

* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} Lernprogramm Teil 1](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} Lernprogramm Teil 2](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}
* [IoT for Automotive Starter - Anwendung](https://iot-automotive-starter.mybluemix.net){:new_window}


## API-Referenz
{: #api}

* [API-Dokumente](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}

## Andere Ressourcen
{: #general}

* [Einführung in {{site.data.keyword.iotmapinsights_short}}](../IotMapInsights/index.html){:new_window}
* [Einführung in {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [dW Answers in IBM developerWorks](https://developer.ibm.com/answers/topics/iot-driver-behavior){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/iot-driver-behavior){:new_window}
* [Neuerungen in Bluemix Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
