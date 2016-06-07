---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Informationen zu {{site.data.keyword.iotdriverinsights_short}}
{: #iotdriverinsights_overview}

Sie können {{site.data.keyword.iotdriverinsights_full}} verwenden, um das Fahrerverhalten mithilfe von Fahrzeugtestdaten und Kontextdaten zu analysieren.
{:shortdesc}

## Analyse des Fahrerverhaltens
{: #driver_behavior_analysis}
Sie können das Fahrerverhalten wie plötzliche Beschleunigung oder plötzliches Bremsen, häufiges Bremsen, Geschwindigkeitsüberschreitungen, scharfe Wendemanöver und andere Aktionen mithilfe der Fahrzeugtestdaten und der Kontextdaten analysieren. 

Die folgenden Aktivitäten und Kontexte sind eingeschlossen: 
 - Fahrerverhalten 
    - Auf die Geschwindigkeit bezogen
       - Plötzliche Beschleunigung
       - Plötzliches Bremsen
       - Geschwindigkeitsüberschreitung
       - Häufiges Anhalten
       - Häufiges Beschleunigen
       - Häufiges Bremsen
    - Auf Wendemanöver bezogen
       - Schafes Wenden (Wenden mit hoher Geschwindigkeit)
       - Beschleunigung vor dem Wenden
       - Überbremsen während des Wendens
    - Andere
       - Ermüdendes Fahren
 - Fahrkontext
    - Zeitbereich
       - Morgendliche Spitzenstunden
       - Nachmittägliche Spitzenstunden
       - Tag
       - Nacht
    - Straßenkategorie
       - Autobahn
       - Stadtautobahn
       - Schnellstraße
       - Hauptstraße
       - Nebenstraßen
    - Geschwindigkeitsmuster auf Grundlage der Straßenkategorie
       - Freier Fluss
       - Kontinuierlicher Fluss
       - Überlastung
       - Schwerwiegende Überlastung
       - Heterogene Bedingungen

## Analyseinfrastruktur bei großen Datenmengen
{: #big_data_analysis_infrastructure}
{{site.data.keyword.iotdriverinsights_short}} verwendet Hadoop als Back-End-Infrastruktur. Hadoop ermöglicht es {{site.data.keyword.iotdriverinsights_short}}, eine hohe Skalierbarkeit für die Analyse von großen Datenmengen und einer großen Datenvielfalt von Fahrzeugtestdaten und Kontextdaten zu realisieren. 

## REST-API
{: #rest_api}
Entwickler können die Analyseergebnisse mit der REST-API abrufen und diese in der {{site.data.keyword.Bluemix_notm}}-Anwendung verwenden. 
 1. Fahrzeugdaten
   - `sendCarProbeData` sendet die zu analysierenden Fahrzeugtestdaten. 
   - `getCarProbeDataListAsDate` gibt die Liste der Fahrzeugtestdaten auf Grundlage des Datums zurück. 
   - `deleteCarProbeDataListByDate` löscht die Fahrzeugtestdaten. 
 2. Analysejob
   - `sendJobRequest` sendet die Jobanforderung für die Analyse des Fahrverhaltens. 
   - `getJobInfo` gibt die Informationen des angegebenen Jobs zurück. 
   - `getJobInfoList` gibt die Liste der Jobinformationen zurück. 
 3. Analyseergebnis 
   - `getAnalyzedTripSummaryList` gibt die Liste der analysierten Flugbahnübersichtsdaten zurück. 
   - `getAnalyzedTripInfo` gibt die Daten der angegebenen analysierten Flugbahn zurück. 
   - `deleteJobResult` löscht alle analysierten Ergebnisse bezüglich eines Jobs.

## Konfigurierbarkeit
{: #configurability}
Einige der Schwellenwertparameter für die Analyse (zum Beispiel der Geschwindigkeitsbereich der Straßenkategorie, der Wendekreis usw.) können von der Benutzerschnittstelle aus konfiguriert werden. 
