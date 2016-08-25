---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Informationen zur Analyse des Fahrverhaltens
{: #iotdriverinsights_overview}
Letzte Aktualisierung: 16. Juni 2016
{: .last-updated}


Die Analyse des Fahrverhaltens ist ein Service, mit dem Sie das Verhalten eines Fahrers aus Fahrzeugtestdaten und Kontextdaten analysieren können. 

{:shortdesc}


## Architektur
{: #drb}

Sie können verschiedene Arten des Fahrverhaltens wie Geschwindigkeit, Wenden und andere Kategorien, ermitteln und analysieren. Sie können zum Beispiel Vorkommnisse wie plötzliche Beschleunigung, Geschwindigkeitsüberschreitung, scharfe Wendemanöver, häufiges oder plötzliches Bremsen und andere Arten des Fahrerverhaltens festlegen. 

## Analysekonfiguration
{: #configurability}  

Mit Schwellenwertparametern für die Analyse wird festgelegt, wie die verschiedenen Arten des Fahrerverhaltens aus den Fahrzeugtest- und Kontextdaten, die dem System zugeführt werden, erkannt und analysiert werden. Sie können einige der Schwellenwertparameter für die Analyse des Fahrverhaltens über die Administrationskonsole des {{site.data.keyword.iotdriverinsights_short}}-Service konfigurieren. Zum Beispiel können Sie den Geschwindigkeitsbereich nach Straßenkategorie und den Wendekreis konfigurieren. 

Weitere Informationen zum Konfigurieren der Schwellenwertparameter für die Analyse des Fahrverhaltens finden Sie im Abschnitt [Parameter für den Service konfigurieren](drb_iotdriverinsights_admin.html#configureparameters). 

### Kategorien und Aktivitäten des Fahrverhaltens

In den folgenden Tabellen werden die Arten des Fahrverhaltens, die von dem Service erkannt und analysiert werden können, nach Kategorien aufgelistet: 

#### Tabelle 1: Fahrverhalten in Bezug auf Geschwindigkeit

|Verhaltensname|Verhaltens-ID|Beschreibung|
|--------|:-------:|------|
|Plötzliche Beschleunigung|1|Schwellenwert für plötzliche Beschleunigung entsprechend der Geschwindigkeit wird intern festgelegt. Plötzliche Beschleunigung wird erkannt, wenn Beschleunigungsdaten den Schwellenwert überschreiten. |
|Plötzliches Bremsen|2|Schwellenwert für plötzliches Bremsen entsprechend der Geschwindigkeit wird intern festgelegt. Plötzliches Bremsen wird erkannt, wenn die Bremsdaten für eine Fahrt den Schwellenwert überschreiten. |
|Geschwindigkeitsüberschreitung|3|Schwellenwert für Geschwindigkeitsüberschreitung nach Straßenkategorie wird festgelegt. Eine Geschwindigkeitsüberschreitung wird erkannt, wenn die Geschwindigkeitsdaten für die Fahrt den Schwellenwert überschreiten. Sie können den Schwellenwert für die Geschwindigkeitsüberschreitung konfigurieren.  |
|Häufiges Anhalten|4|Anhalten wird erkannt, wenn der Geschwindigkeitswert bei Null liegt. Häufiges Anhalten wird erkannt, wenn es innerhalb eines bestimmten Zeitrahmens während der Fahrt zu häufigen Stopps kommt. |
|Häufiges Beschleunigen|5|Schwellenwert für Beschleunigung entsprechend der Geschwindigkeit wird intern festgelegt. Häufiges Beschleunigen wird erkannt, wenn der Fahrer den Schwellenwert innerhalb eines bestimmten Zeitrahmens während der Fahrt häufig überschreitet. |
|Häufiges Bremsen|6|Schwellenwert für Bremsen entsprechend der Geschwindigkeit wird intern festgelegt. Häufiges Bremsen wird erkannt, wenn der Fahrer den Schwellenwert innerhalb eines bestimmten Zeitrahmens während der Fahrt häufig überschreitet. |

#### Tabelle 2: Fahrverhalten in Bezug auf Wendemanöver

|Verhaltensname|Verhaltens-ID|Beschreibung|
|-------|:--------:|-------|
|Scharfes Wenden (Wenden mit hoher Geschwindigkeit)|7|Schwellenwert für Geschwindigkeit beim Wenden wird festgelegt. Scharfes Wenden wird erkannt, wenn der Fahrer den Schwellenwert überschreitet. Sie können den Schwellenwert für scharfes Wenden konfigurieren. |Beschleunigung vor dem Wenden|8|Schwellenwert für Beschleunigung entsprechend der Geschwindigkeit wird intern festgelegt. Beschleunigung vor dem Wenden wird erkannt, wenn der Fahrer den Schwellenwert überschreitet. |Überbremsen vor dem Beenden des Wendens|9|Schwellenwert für Bremsen entsprechend der Geschwindigkeit wird intern festgelegt. Überbremsen vor dem Beenden des Wendens wird erkannt, wenn der Fahrer den Schwellenwert überschreitet.

#### Tabelle 3: Andere Arten des Fahrverhaltens

|Verhaltensname|Verhaltens-ID|Beschreibung|
|-------|:--------:|-------|
|Ermüdendes Fahren|10|Schwellenwert für Bremsen entsprechend der Geschwindigkeit wird intern festgelegt. Übermüdung des Fahrers wird erkannt, wenn die Geschwindigkeit den Schwellenwert überschreitet. |


### Fahrkontext
|Kontext-<br/>kategorie|ID der Kontext-<br/>kategorie|Kontextname|Kontext-ID|
|-------|:-----:|--------|:-------:|
|**Zeitbereich**|**4**|\-|\-|
|Zeitbereich|4|Tag|1|
|Zeitbereich|4|Nacht|2|
|Zeitbereich|4|Morgendliche Spitzenstunden|3|
|Zeitbereich|4|Nachmittägliche Spitzenstunden|4|
|**Straßenkategorie**|**3**|\-|\-|
|Straßenkategorie|3|Autobahn|1|
|Straßenkategorie|3|Stadtautobahn|2|
|Straßenkategorie|3|Schnellstraße|3|
|Straßenkategorie|3|Hauptstraße|4|
|Straßenkategorie|3|Nebenstraßen|5|
|**Geschwindigkeitsmuster**|**0**|\-|\-|
|Geschwindigkeitsmuster|0|Freier Fluss|0|
|Geschwindigkeitsmuster|0|Kontinuierlicher Fluss|1|
|Geschwindigkeitsmuster|0|Schwerwiegende Überlastung|2|
|Geschwindigkeitsmuster|0|Überlastung|3|
|Geschwindigkeitsmuster|0|Heterogene Bedingungen|4|


## REST-API
{: #rest_api}

Die REST-API {{site.data.keyword.iotdriverinsights_short}} stellt Anfragen bereit, die Sie zum Anpassen und Erstellen Ihrer {{site.data.keyword.Bluemix_notm}}-Anwendungen verwenden können: 

 1. Befehle für Fahrzeugdaten: 
   - `sendCarProbeData` sendet die zu analysierenden Fahrzeugtestdaten. 
   - `getCarProbeDataListAsDate` gibt die Liste der Fahrzeugtestdaten nach Datum zurück. 
   - `deleteCarProbeDataListByDate` löscht die Fahrzeugtestdaten. 
 2. Befehle für Analysejobs:
   - `sendJobRequest` sendet die Jobanforderung für die Analyse des Fahrverhaltens. 
   - `getJobInfo` gibt die Informationen des angegebenen Jobs zurück. 
   - `getJobInfoList` gibt die Liste der Jobinformationen zurück. 
 3. Befehle für Analyseergebnisse: 
   - `getAnalyzedTripSummaryList` gibt die Liste mit den Übersichtsdaten des analysierten Streckenverlaufs zurück. 
   - `getAnalyzedTripInfo` gibt die Daten des angegebenen analysierten Streckenverlaufs zurück. 
   - `deleteJobResult` löscht alle analysierten Ergebnisse bezüglich eines Jobs.

Weitere Informationen finden Sie in der Dokumentation zur [{{site.data.keyword.iotdriverinsights_short}}-API](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}. 

## Analyseinfrastruktur bei großen Datenmengen
{: #big_data_analysis_infrastructure}
{{site.data.keyword.iotdriverinsights_short}} verwendet Hadoop als Back-End-Infrastruktur. Hadoop bietet hohe Skalierbarkeit, sodass der {{site.data.keyword.iotdriverinsights_short}}-Service große Volumen an Fahrzeugtest- und Kontextdaten abrufen und analysieren kann. 
