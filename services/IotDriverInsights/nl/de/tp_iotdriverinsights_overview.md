---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Informationen zur Analyse des Streckenverlaufsmusters
{: #tp_iotdriverinsights_overview}
Letzte Aktualisierung: 16. Juni 2016
{: .last-updated}

Die API für die Analyse des Streckenverlaufsmusters ist ein von {{site.data.keyword.iotdriverinsights_full}} bereitgestellter Service,  mit dem Sie die Start/Ziel-Muster (S/Z-Muster) und Routenmuster von Fahrten aus Fahrzeugtestdaten analysieren können. 

{:shortdesc}

## Analyse des Streckenverlaufsmusters der Route
{: #tpa}

Sie können S/Z- und Routenmuster aus mehreren Fahrten ermitteln und analysieren.
Im folgenden Diagramm wird ein einfaches Beispiel der S/Z- und Routenmuster eines Fahrzeugs (Fahrzeug-1) dargestellt, die aus mehreren Fahrten ermittelt wurden. In diesem Beispiel werden durch die Analyse des Streckenverlaufsmusters zwei S/Z-Muster ermittelt: 
- Ein S/Z-Muster vom Wohnsitz (Start1) zum Büro (Ziel1) mit zwei Routenmustern.
- Ein S/Z-Muster vom Wohnsitz (Start1) zum Geschäft (Ziel2) mit einem Routenmuster.

![Beispiel für S/Z-Muster](images/tp_odroute_example.png "Beispiel für S/Z- und Routenmuster")

Bei der Analyse des Streckenverlaufsmusters werden für jedes Fahrzeug auch einige Diversitätsmetriken berechnet, die in der folgenden Tabelle aufgeführt sind. Mithilfe dieser Metriken können Sie das Fahrverhalten eines Fahrers beurteilen. 

|Metrikname|Beschreibung|
|:---|:---|
|Seltenes S/Z - Verhältnis|Das Verhältnis der Anzahl Fahrten, die nicht durch S/Z-Muster abgedeckt sind, zu der Gesamtanzahl an eingegebenen Fahrten. |
|Seltene Kilometerleistung - Verhältnis|Das Verhältnis der Kilometerleistung, die nicht durch Routenmuster abgedeckt ist, zur Gesamtkilometerleistung der eingegebenen Fahrten.|
|Seltene Fahrten - Verhältnis|Das Verhältnis der Anzahl Fahrten, die nicht durch Routenmuster abgedeckt sind, zu der Gesamtanzahl eingegebener Fahrten. |


## REST-API
{: #rest_api}

Die REST-API zur Analyse des Streckenverlaufsmusters stellt Anforderungen bereit, die Sie zum Anpassen und Erstellen Ihrer {{site.data.keyword.Bluemix_notm}}-Anwendungen verwenden können: 

 1. Befehle für Fahrzeugdaten: 
   - `sendCarProbeData` sendet die zu analysierenden Fahrzeugtestdaten. 
   - `getCarProbeDataListAsDate` gibt die Liste der Fahrzeugtestdaten nach Datum zurück. 
   - `deleteCarProbeDataListByDate` löscht die Fahrzeugtestdaten. 
 2. Befehle für Analysejobs:
   - `sendJobRequest` sendet die Jobanforderung für die Analyse des Streckenverlaufsmusters. 
   - `getJobInfo` gibt die Informationen des angegebenen Jobs zurück. 
   - `getJobInfoList` gibt die Liste der Jobinformationen zurück. 
 3. Befehle für Analyseergebnisse: 
   - `getResultSummary` gibt die analysierten Zusammenfassungsinformationen der Analyse des Streckenverlaufsmusters zurück. 
   - `getAnalyzedODDetail` gibt die Detailinformationen des angegebenen analysierten S/Z-Musters zurück. 
   - `getRouteGPSList` gibt die Liste der GPS-Informationen des angegebenen analysierten Routenmusters zurück.
   - `getODList` gibt die Liste der S/Z-Muster des angegebenen Arguments zurück. 
   - `deleteJobResult` löscht alle analysierten Ergebnisse bezüglich eines Jobs.

Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iotdriverinsights_short}}-API](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}. 
