---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Anwendungen mit {{site.data.keyword.mobileanalytics_short}} überwachen
{: #monitoringapps}

Von {{site.data.keyword.mobileanalytics_full}} werden Überwachungs- und Analysefunktionen für mobile Anwendungen bereitgestellt. Mit dem {{site.data.keyword.mobileanalytics_short}}-Client-SDK können Sie Anwendungsprotokolle aufzeichnen und Daten überwachen. Entwickler können steuern, wann diese Daten an den {{site.data.keyword.mobileanalytics_short}}-Service gesendet werden sollen. Wenn die Daten an {{site.data.keyword.mobileanalytics_short}} übergeben werden, können Sie über die {{site.data.keyword.mobileanalytics_short}}-Konsole Erkenntnisse aus Analysen zu mobilen Anwendungen, Geräten und Anwendungsprotokollen erhalten.
{: shortdesc}

<!--

## Visualizing data with custom charts
{: #custom-charts notoc}

You can visualize the collected analytics data in your analytics repository. This visualization is a powerful way to inspect data for specific use cases. You can create charts with data that is already collected by Operational Analytics, in addition to custom data that you report.


### Creating custom charts for app logs
{: #custom-charts-client-logs notoc}

You can create a custom chart for app logs that contain log information that is sent with the Logger API for the platform. The log information also includes contextual information about the device, including environment, app name, and app version.

In this example, you use app log data to create a flow chart. The final graph shows the distribution of log levels in a specific app. You also have the following data available to show in a chart:

* Specific data
  * Log level
* Message data
  * Timestamp
* Device OS contextual data
  * Application name
  * Application version
  * Device OS
* Device contextual data
  * Device ID
  * Device model
  * Device OS version


1. Make sure that you have an application that is collecting device logs or gathering analytics.
2. In the {{site.data.keyword.mobileanalytics_short}} console, click the **Custom Charts** tab on the **Dashboard** page. You can create a chart that is based on the analytics messages that were sent to the server.
3. Click **Create Chart** to create a new custom chart and provide the following values:
  * Chart Title: Application and Log Levels
  * Event Type: App Logs
  * Chart Type: Flow Chart
5. Click the **Chart Definition** tab and provide the following values:
  * Source: Application Name
  * Destination: Log Level
  * Property: your application name
7. Click **Save**

### Exporting custom data
{: #export-custom-data notoc}

You can export the data from each custom chart into JSON, XML, or CSV format.

The structure of the exported data depends on the chart that is being exported. To export data, click the export icon at the upper right of the custom chart.



### Exporting and importing custom chart definitions
{: #export-import-custom notoc}

You can import and export custom chart definitions programmatically or manually in the {{site.data.keyword.mobileanalytics_short}} Dashboard.

Ensure that you have at least one custom chart in the {{site.data.keyword.mobileanalytics_short}} Dashboard.
In this example, you manually export and import custom chart definitions.

1. In the {{site.data.keyword.mobileanalytics_short}} console, click the **Custom Charts** tab in the **Dashboard** page.
2. To export the custom chart definitions, click **Export Charts**. This action displays a dialog to save a `customChartsDefinition.json` file.
3. Choose a location to save the file.
4. Click the **Delete Chart** icon next to each custom chart to delete all custom charts.
5. To import a custom chart definition, click **Import Charts**. This action displays a dialog to choose a file.
6. Choose the `customChartsDefinition.json` file that you previously exported to open.

You can also export and import custom chart definitions programmatically by using your HTTP client of choice (for example, CURL or postman):
* The GET endpoint for export is `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/`.
* The POST endpoint for import is `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/import`.

**Note**: If you import a custom chart definition that exists, you end up with duplicate definitions, which also means that the {{site.data.keyword.mobileanalytics_short}} Dashboard shows duplicate custom charts.

-->

## Alerts einstellen
{: #alerts}

Sie können Schwellenwerte in Alertdefinitionen in der {{site.data.keyword.mobileanalytics_short}}-Konsole einstellen, um die Aktivitäten besser zu überwachen.

Sie können Schwellenwerte so konfigurieren, dass bei ihrem Überschreiten Alerts ausgelöst werden, über die die {{site.data.keyword.mobileanalytics_short}}-Konsolenüberwachung benachrichtigt wird. Die ausgelösten Alerts können in der Konsole dargestellt oder von einem angepassten Web-Hook verarbeitet werden.<!-- This feature provides a proactive means of detecting app log errors, server log errors, extended periods of network latency, and authentication failures.--> Diese Funktion ist eine proaktive Möglichkeit, um Anwendungsprotokollfehler und Serverprotokollfehler zu Anwendungsabstürzen zu erkennen. Bei Verwendung von reaktiven Schwellenwerten und Alerts ist es nicht erforderlich, Daten zu untersuchen und für ein breites Spektrum an Granularität Schwellenwerte festzulegen.

### Alertdefinition für Anwendungsprotokolle erstellen
{: #alert-def-client-logs notoc}

Sie können eine Alertdefinition erstellen, die auf Anwendungsprotokollen basiert.

Im folgenden Beispiel wird aus den Daten eines Anwendungsprotokolls eine Alertdefinition erstellt. Vom Alert werden alle Anwendungsprotokolle überwacht, die in den letzten fünf Minuten empfangen wurden; in Abständen von fünf Minuten werden sie vom Alert weiter überprüft, bis die Alertdefinition inaktiviert oder gelöscht wird. Ein Alert wird für jedes Gerät ausgelöst, von dem mindestens drei Anwendungsfehlerprotokolle mit demselben Anwendungsnamen und derselben Version gesendet wurden.

1. Klicken Sie in der {{site.data.keyword.mobileanalytics_short}}-Konsole auf **Definitionen**, um die Seite mit den Alertdefinitionen zu öffnen.
2. Klicken Sie auf **Alert erstellen**, um einen Alert zu erstellen.
3. Geben Sie die folgenden Werte an:
	* Alert Name: Alert for app logs (Alert-Name: Alert für App-Protokolle)
	* Message: Error Message Alert (Nachricht: Alert für Fehlernachricht)
	* Query Frequency: 5 minutes (Abfragehäufigkeit: 5 Minuten)
	* Event Type: App Logs (Ereignistyp: App-Protokolle)
		* Property: Log Level (Eigenschaft: Protokollebene)
			* Value: Error (Wert: Fehler)
			* Threshold (Schwellenwert)
				* Threshold Type: Total for Application Instance (Schwellenwerttyp: Gesamtwert für Anwendungsinstanz)

					**Hinweis**: Wenn Sie die Option für den Anwendungsdurchschnitt auswählen, wird aus den App-Protokollen und der Anzahl der Geräte ein Durchschnittswert berechnet. Beispiel: Wenn Sie über zwei Geräte verfügen und von einem Gerät sechs App-Protokolle gesendet werden, vom anderen Gerät dagegen nur drei Protokolle, beträgt der Durchschnitt 4,5 Protokolle.
				* Operator: is greater than or equals 3 (Operator: Größer gleich 3)(
	<!-- insert alert definition tab image? -->

4. Klicken Sie auf **Weiter** und geben Sie den folgenden Wert an:
	* Method: Analytics Console Only (Methode: Nur Analytics-Konsole)

		**Hinweis**: Wählen Sie die Option für Analytics-Konsole und Network Post aus, wenn Sie zusätzlich eine POST-Nachricht mit einer JSON-Nutzlast an die angepasste URL senden wollen. Wenn Sie diese Option auswählen, sind die folgenden Felder verfügbar:
		* Network Post URL (Network Post-URL)
        * Header (Header)
        * Authentication Type (Authentifizierungstyp)
5. Klicken Sie auf **Speichern**.

Sie haben eine Alertdefinition für einen Alert erstellt, der nach Ablauf eines Intervalls von fünf Minuten ausgelöst wird, wenn die Anzahl der App-Protokolle den Schwellenwert von 3 Fehlerprotokollen erreicht oder überschreitet.

### Alertdefinition für Anwendungsabstürze erstellen
{: #alert-def-app-crash notoc}

Sie können eine Alertdefinition erstellen, die auf Anwendungsabstürzen basiert.

Im folgenden Beispiel wird aus den Daten eines Anwendungsabsturzes eine Alertdefinition erstellt. Vom Alert werden alle Anwendungsabstürze überwacht, die in den letzten zwei Minuten empfangen wurden; in Abständen von zwei Minuten werden sie vom Alert weiter überprüft, bis die Alertdefinition inaktiviert oder gelöscht wird. Ein Alert wird für jede Anwendung ausgelöst, die mindestens fünf Mal abgestürzt ist. Weitere Informationen zu Anwendungsabstürzen finden Sie unter [Anwendungsabstürze](#app_crash).

1. Klicken Sie in der {{site.data.keyword.mobileanalytics_short}}-Konsole auf **Definitionen**, um die Seite mit den Alertdefinitionen anzuzeigen.
2. Klicken Sie auf **Alert erstellen**.
3. Geben Sie die folgenden Werte an:
	* Alert Name: Alert for Application Crashes (Alert-Name: Alert für Anwendungsabstürze)
	* Message: App Crash Alert (Nachricht: App-Absturz-Alert)
	* Query Frequency: Application Crashes (Abfragehäufigkeit: Anwendungsabstürze)
		* Query Frequency: 2 minutes (Abfragehäufigkeit: 2 Minuten)
	* Event Type: Application Crashes (Ereignistyp: Anwendungsabstürze)
		* Application Name: Any application (Anwendungsname: Jede Anwendung)
		* Application Version: Any version (Anwendungsversion: Jede Version)
    * Threshold (Schwellenwert)
      * Threshold Type: Crash Count (Schwellenwerttyp: Absturzanzahl)
      * Operator: is greater than or equals 5 (Operator: Größer gleich 5)
4. Klicken Sie auf die Registerkarte **Verteilungsmethode** und geben Sie den folgenden Wert an:
  * Method: Analytics Console Only (Methode: Nur Analytics-Konsole)

    **Hinweis:** Wählen Sie die Option für Analytics-Konsole und Network Post aus, wenn Sie zusätzlich eine POST-Nachricht mit JSON-vernetzen an die angepasste URL senden möchten. Wenn Sie diese Option auswählen, sind die folgenden Felder verfügbar:
      * Network Post URL (required) (Network Post-URL (erforderlich))
      * Headers (optional) (Header (optional))
      * Authentication Type (required) (Authentifizierung (erforderlich))
5. Klicken Sie auf **Speichern**.

### Alertdefinitionen verwalten
{: #managing-alert-definitions notoc}

Im folgenden Beispiel verwalten Sie Alertdefinitionen auf der Seite 'Alert-Management'.

1. Klicken Sie in der {{site.data.keyword.mobileanalytics_short}}-Konsole auf **Protokolle**. Daraufhin wird die Seite für Alertprotokolle geöffnet.
2. Optional: Schalten Sie das Kontrollkästchen unter der Spalte **Enabled** (Aktiviert) ein bzw. aus, um eine bestimmte Alertdefinition zu aktivieren bzw. zu inaktivieren.
3. Optional: Klicken Sie auf das Symbol zum Duplizieren, wenn Sie eine Kopie einer Alertdefinition erstellen und einige Werte verändern möchten.
4. Optional: Klicken Sie auf das Stiftsymbol, wenn Sie eine Alertdefinition bearbeiten möchten.
5. Optional: Klicken Sie auf das Papierkorbsymbol, wenn Sie eine Alertdefinition löschen möchten.

### Alertdetails anzeigen
{: #viewing-alert-details notoc}

Im folgenden Beispiel zeigen Sie die Details ausgelöster Alerts auf der Seite für Alertprotokolle an.

1. Klicken Sie in der {{site.data.keyword.mobileanalytics_short}}-Konsole auf **Protokolle**. Daraufhin wird die Seite für Alertprotokolle angezeigt.
2. Klicken Sie auf das Symbol **+** für einen beliebigen Alert. Daraufhin werden die Abschnitte mit den Alertdefinitionen und den Alert-Instanzen angezeigt.

    **Hinweis:** Wenn die entsprechende Alertdefinition nicht gelöscht oder geändert wurde, können Sie die Alertdefinition durch Klicken auf die Schaltfläche zum Bearbeiten von Alerts bearbeiten. Andernfalls ist die Schaltfläche zum Bearbeiten von Alerts nicht verfügbar und die folgende Nachricht wird angezeigt:

    `This alert definition has since been modified or deleted.`

3. Optional: Wählen Sie einen Alert aus und klicken Sie auf das Papierkorbsymbol, um den Alert zu löschen.

## Anwendungsabstürze überwachen
{: #monitor-app-crash}

Sie können Informationen zu Anwendungsabstürzen in der {{site.data.keyword.mobileanalytics_short}}-Konsole anzeigen, um Ihre Anwendungen besser überwachen und entsprechende Fehler beheben zu können.

### Überwachung von Anwendungsabstürzen
{: #app-crash notoc}

Auf der Seite mit den Abstürzen sehen Sie in der Tabelle mit der Absturzübersicht die folgenden Datenspalten:

* Application: Any application (Anwendung: Jede Anwendung)
* Crashes: total number of crashes for that app (Abstürze: Gesamtzahl der Abstürze für diese App)
* Total Uses: total number of times a user opens and closes that app (Gesamte Verwendungen: Die Angabe, wie oft diese App geöffnet und geschlossen wurde)
* Crash Rate: percentage of crashes per use (Absturzrate: Der Prozentsatz der Abstürze pro Verwendung)

In der Tabelle für Abstürze werden umgehend Informationen zu Ihren Anwendungsabstürzen angezeigt.<!--In the **Overview** page of the **Dashboard** section,--> Das Balkendiagramm für Abstürze zeigt ein Histogramm der Abstürze im zeitlichen Verlauf an.

Sie können Absturzdaten auf zwei Arten anzeigen:

1. Absturzrate anzeigen: Die Absturzrate im zeitlichen Verlauf
2. Gesamtsumme der Abstürze anzeigen: Gesamte Abstürze im zeitlichen Verlauf

### Fehlerbehebung für App-Abstürze
{: #app-crash-troubleshooting notoc}

Die Seite Zur Fehlerbehebung in der <!-- **Applications** section of the --> {{site.data.keyword.mobileanalytics_short}}-Konsole bietet eine differenzierte Ansicht der App-Abstürze; hierfür wird die Tabelle mit der Zusammenfassung der Abstürze verwendet.

Die Tabelle für die Absturzzusammenfassung kann sortiert werden und besteht aus den folgenden Datenspalten:

* Crashes (Abstürze)
* Devices (Geräte)
* Last Crash (Letzter Absturz)
* Anwendung
* OS (Betriebssystem)
* Message(Nachricht)

Sie können auf das Plussymbol (+) neben einem beliebigen Eintrag klicken, um die Tabelle für Absturzdetails mit den folgenden Spalten anzuzeigen:

* Time Crashed (Absturzzeit)
* Application Version (Anwendungsversion)
* OS Version (Version des Betriebssystems)
* Device Model (Gerätemodell)
* Device ID (Geräte-ID)
* Download: link to download the logs that led up to the crash (Download: Link zum Herunterladen der Protokolle führte zum Absturz)

Sie können einen Eintrag in der Tabelle für Absturzdetails erweitern, um weitere Details, u. a. einen Stack-Trace, anzuzeigen.

**Hinweis:** Die Daten für die Tabelle mit der Absturzzusammenfassung werden durch Abfragen der App-Protokolle mit schwerwiegenden Fehlern gefüllt. Wenn Ihre Anwendung keine Anwendungsprotokolle mit schwerwiegenden Fehlern erfasst, sind keine Daten verfügbar.

## Netzanforderungen überwachen
{: #monitor-network-requests}


Zeigen Sie in der {{site.data.keyword.mobileanalytics_short}}-Konsole Netzanforderungsdaten für Ihre Anwendungen an. 

Es stehen Daten für die folgenden Messungen zur Verfügung:
	
* Umlaufzeit: Definiert die Zeitdauer (in Millisekunden) an, die Ihre App für Netzanforderungen benötigt.
* Anzahl der Anforderungen: Zeigt an, wie häufig eine App Netzanforderungen absetzt. Daten werden auch als Durchschnitt angezeigt.

## Daten nach dashDB exportieren
{: #dashdb}

Die in der {{site.data.keyword.mobileanalytics_short}}-Konsole sichtbaren Metriken sind nur ein Beispiel für die Erkenntnisse, die Sie aus Ihren mobilen Daten gewinnen können. Sie können Ihre mobilen Daten automatisch über eine Pipe an das {{site.data.keyword.IBM}} dashDB-Data-Warehouse leiten; dort können Sie Ihre Analysen anpassen, Ihre Daten mit anderen öffentlichen und privaten Datenquellen zusammenfassen und innovative Analysen für ausführliche und zukunftsweisende Einblicke anwenden, mit deren Hilfe Sie Ihr Geschäft lernen zu verstehen und zu betreiben.

Richten Sie dashDB in der {{site.data.keyword.mobileanalytics_short}}-Konsole ein; klicken Sie hierfür auf der Seite für den **Export** auf **DashDB**. Nach dem Setup werden neue Daten, die an {{site.data.keyword.mobileanalytics_short}} gesendet werden, innerhalb von 1 bis 2 Stunden auch an dashDB weitergeleitet. 

<!--
If you have existing DashDB instances, those instances will no longer accept new data because the incoming data no longer matches the schema. Manually add columns for the new data to resume incoming data. Modifying {{site.data.keyword.mobileanalytics_short}} collection tables by adding new columns also breaks the stream of incoming data.
-->

