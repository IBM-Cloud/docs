---

copyright:
  years: 2015, 2016

---
# Anwendungen mit {{site.data.keyword.mobileanalytics_short}} überwachen
{: #monitoringapps}
*Letzte Aktualisierung: 6. Mai 2016*
{: .last-updated}

Von {{site.data.keyword.mobileanalytics_full}} werden Überwachungs- und Analysefunktionen für mobile Anwendungen bereitgestellt. Mit dem {{site.data.keyword.mobileanalytics_short}}-Client-SDK können Sie Clientprotokolle aufzeichnen und Daten überwachen. Entwickler können steuern, wann diese Daten an den {{site.data.keyword.mobileanalytics_short}}-Service gesendet werden sollen. Wenn die Daten an {{site.data.keyword.mobileanalytics_short}} übergeben werden, können Sie mit {{site.data.keyword.mobileanalytics_short}} Erkenntnisse aus Analysen zu mobilen Anwendungen, Geräten und Clientprotokollen verwenden.
{: shortdesc}

## Daten mit angepassten Diagrammen darstellen
{: #custom-charts}

Sie können die erfassten Analysedaten im Analyse-Repository darstellen. Diese Darstellung ist eine hervorragende Möglichkeit, um Daten auf bestimmte Anwendungsfälle hin zu untersuchen. Zusätzlich zu den angepassten Daten in einem Bericht können Sie Diagramme mit Daten erstellen, die bereits mit Operational Analytics erfasst wurden.

### Benutzerdefinierte Diagramme für Clientprotokolle erstellen
{: #custom-charts-client-logs}

Sie können ein benutzerdefiniertes Diagramm für Clientprotokolle erstellen, die Protokollinformationen enthalten, die mit der Protokollfunktions-API für die Plattform gesendet wurden. Die Protokollinformationen umfassen auch Kontextinformationen zum Gerät, einschließlich Umgebung, App-Name und App-Version.

Im folgenden Beispiel wird aus den Daten eines Clientprotokolls ein Ablaufdiagramm erstellt. Im endgültigen Diagramm wird die Verteilung der Protokollebenen in einer bestimmten App dargestellt. Außerdem können folgende Daten in einem Diagramm angezeigt werden:

* Specific data (Spezifische Daten)
  * Log level (Protokollebene)
* Message data (Nachrichtendaten)
  * Timestamp (Zeitmarke)
* Device OS contextual data (Kontextdaten des Betriebssystems des Geräts)
  * Application name (Anwendungsname)
  * Application version (Anwendungsversion)
  * Device OS (Betriebssystem des Geräts)
* Device contextual data (Kontextdaten des Geräts)
  * Device ID (Geräte-ID)
  * Device model (Gerätemodell)
  * Device OS version (Version des Betriebssystems des Geräts)


1. Stellen Sie sicher, dass Sie über eine Anwendung verfügen, von der Geräteprotokolle oder Analysedaten erfasst werden.
2. Klicken Sie in der {{site.data.keyword.mobileanalytics_short}}-Konsole auf der Seite **Dashboard** auf die Registerkarte **Benutzerdefinierte Diagramme**. Sie können ein Diagramm auf der Basis der Analysenachrichten erstellen, die an den Server gesendet wurden.
3. Klicken Sie auf **Diagramm erstellen**, um ein neues angepasstes Diagramm zu erstellen, und geben Sie die folgenden Werte an:
  * Chart Title: Application and Log Levels (Diagrammtitel: Anwendung und Protokollebenen)
  * Event Type: Client Logs (Ereignistyp: Clientprotokolle)
  * Chart Type: Flow Chart (Diagrammtyp: Ablaufdiagramm)
5. Klicken Sie auf die Registerkarte **Diagrammdefinition** und geben Sie die folgenden Werte an:
  * Source: Application Name (Quelle: Anwendungsname)
  * Destination: Log Level (Ziel: Protokollebene)
  * Property: your app name (Eigenschaft: App-Name)
7. Klicken Sie auf **Speichern**.

### Angepasste Daten exportieren
{: #export-custom-data}

Sie können die Daten jedes benutzerdefinierten Diagramms in das JSON-, XML- oder CSV-Format exportieren.

Die Struktur der exportierten Daten hängt vom jeweils exportierten Diagramm ab. Klicken Sie zum Exportieren der Daten auf das Exportsymbol in der rechten oberen Ecke des angepassten Diagramms.



### Benutzerdefinierte Diagrammdefinitionen exportieren und importieren
{: #export-import-custom}

Sie können benutzerdefinierte Diagrammdefinitionen programmgestützt oder manuell im {{site.data.keyword.mobileanalytics_short}}-Dashboard importieren oder exportieren.

Stellen Sie sicher, dass Sie im {{site.data.keyword.mobileanalytics_short}}-Dashboard über mindestens ein benutzerdefiniertes Diagramm verfügen.
Im folgenden Beispiel exportieren und importieren Sie die Definitionen benutzerdefinierter Diagramme manuell.

1. Klicken Sie in der {{site.data.keyword.mobileanalytics_short}}-Konsole auf der Seite **Dashboard** auf die Registerkarte **Benutzerdefinierte Diagramme**.
2. Klicken Sie zum Exportieren der angepassten Diagrammdefinitionen auf **Diagramme exportieren**. Daraufhin wird ein Dialogfenster zum Speichern der Datei `customChartsDefinition.json` angezeigt.
3. Wählen Sie eine Position zum Speichern der Datei aus.
4. Klicken Sie auf das Symbol **Diagramm löschen** neben jedem angepassten Diagramm, um alle angepassten Diagramme zu löschen.
5. Klicken Sie zum Importieren einer angepassten Diagrammdefinition auf **Diagramme importieren**. Daraufhin wird ein Dialogfenster zum Auswählen einer Datei angezeigt.
6. Wählen Sie die Datei `customChartsDefinition.json` zum Öffnen aus, die Sie vorher exportiert haben.

Sie können benutzerdefinierte Diagrammdefinitionen mit einem HTTP-Client Ihrer Wahl (zum Beispiel CURL oder postman) auch programmgesteuert exportieren und importieren:
* Der GET-Endpunkt für den Export lautet `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/`.
* Der POST-Endpunkt für den Import lautet `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/import`.

**Hinweis:** Wenn Sie eine benutzerdefinierte Diagrammdefinition importieren, die bereits vorhanden ist, ist diese Definition doppelt vorhanden; dies bedeutet auch, dass das benutzerdefinierte Diagramm im {{site.data.keyword.mobileanalytics_short}}-Dashboard doppelt angezeigt wird.

## Alerts einstellen
{: #alerts}

Sie können Schwellenwerte in Alertdefinitionen in der {{site.data.keyword.mobileanalytics_short}}-Konsole einstellen, um die Aktivitäten besser zu überwachen.

Sie können Schwellenwerte so konfigurieren, dass bei ihrem Überschreiten Alerts ausgelöst werden, über die die {{site.data.keyword.mobileanalytics_short}}-Konsolenüberwachung benachrichtigt wird. Die ausgelösten Alerts können in der Konsole dargestellt oder von einem angepassten Web-Hook verarbeitet werden. Diese Funktion ist eine proaktive Möglichkeit, Clientprotokollfehler, Serverprotokollfehler, längere Zeiträume an Netzlatenz und Authentifizierungsfehler zu erkennen. Bei Verwendung von reaktiven Schwellenwerten und Alerts ist es nicht erforderlich, Daten zu untersuchen und für ein breites Spektrum an Granularität Schwellenwerte festzulegen.

### Alertdefinition für Clientprotokolle erstellen
{: #alert-def-client-logs}

Sie können eine Alertdefinition erstellen, die auf Clientprotokollen basiert.

Im folgenden Beispiel wird aus den Daten eines Clientprotokolls eine Alertdefinition erstellt. Vom Alert werden alle Clientprotokolle überwacht, die in den letzten fünf Minuten empfangen wurden; in Abständen von fünf Minuten werden sie vom Alert weiter überprüft, bis die Alertdefinition inaktiviert oder gelöscht wird. Ein Alert wird für jedes Geräte ausgelöst, von dem mindestens drei Clientfehlerprotokolle mit demselben App-Namen und derselben Version gesendet wurden.

1. Klicken Sie in der {{site.data.keyword.mobileanalytics_short}}-Konsole auf das Glockensymbol, um auf die Seite für **Alert-Protokolle** zu wechseln.
2. Rufen Sie die Seite **Alert-Management** auf und klicken Sie auf **Alert erstellen**.
3. Geben Sie die folgenden Werte an:
	* Alert Name: Alert for client logs (Alert-Name: Alert für die Clientprotokolle)
	* Message: Error Message Alert (Nachricht: Alert für Fehlernachricht)
	* Query Frequency: 5 minutes (Abfragehäufigkeit: 5 Minuten)
	* Event Type: Client Logs (Ereignistyp: Clientprotokolle)
		* Property: Log Level (Eigenschaft: Protokollebene)
			* Value: Error (Wert: Fehler)
			* Threshold (Schwellenwert)
				* Threshold Type: Total for Application Instance (Schwellenwerttyp: Gesamtwert für Anwendungsinstanz)

					**Hinweis:** Wenn Sie die Option für den Anwendungsdurchschnitt auswählen, wird aus den Clientprotokollen und der Anzahl der Geräte ein Durchschnittswert berechnet. Beispiel: Wenn Sie über zwei Geräte verfügen und von einem Gerät sechs Clientprotokolle gesendet werden, vom anderen Gerät dagegen nur drei Protokolle, beträgt der Durchschnitt 4,5 Protokolle.
				* Operator: is greater than or equals 3 (Operator: Größer gleich 3)(
	<!-- insert alert definition tab image? -->

4. Klicken Sie auf **Weiter** oder die Registerkarte für die Verteilungsmethode, und geben Sie den folgenden Wert an:
	* Method: Analytics Console Only (Methode: Nur Analytics-Konsole)

		Hinweis: Wählen Sie die Option für Analytics-Konsole und Network Post aus, wenn Sie zusätzlich eine POST-Nachricht mit JSON-vernetzen an die angepasste URL senden möchten. Wenn Sie diese Option auswählen, sind die folgenden Felder verfügbar:
		* Network Post URL (Network Post-URL)
        * Header (Header)
        * Authentication Type (Authentifizierungstyp)
5. Klicken Sie auf **Speichern**.

Sie haben eine Alertdefinition für einen Alert erstellt, der nach Ablauf eines Intervalls von fünf Minuten ausgelöst wird, wenn die Anzahl der Clientprotokolle den Schwellenwert von 3 Fehlerprotokollen erreicht oder überschreitet.

### Alertdefinition für App-Abstürze erstellen
{: #alert-def-app-crash}

Sie können eine Alertdefinition erstellen, die auf App-Abstürzen basiert.

Im folgenden Beispiel wird aus den Daten eines App-Absturzes eine Alertdefinition erstellt. Vom Alert werden alle App-Abstürze überwacht, die in den letzten zwei Minuten empfangen wurden; in Abständen von zwei Minuten werden sie vom Alert weiter überprüft, bis die Alertdefinition inaktiviert oder gelöscht wird. Ein Alert wird für jede App ausgelöst, die mindestens fünf Mal abgestürzt ist. Weitere Informationen zu App-Abstürzen finden Sie unter [App-Abstürze](app_crash/c_op_analytics_crashes.html).

1. Klicken Sie in der {{site.data.keyword.mobileanalytics_short}}-Konsole auf das Symbol **Alerts**. Daraufhin wird die Seite für Alert-Protokolle angezeigt.
2. Klicken Sie auf die Registerkarte **Alert-Management** und klicken Sie auf **Alert erstellen**.
3. Geben Sie die folgenden Werte an:
	* Alert Name: Alert for App Crashes (Alert-Name: Alert für App-Abstürze)
	* Message: App Crash Alert (Nachricht: App-Absturz-Alert)
	* Query Frequency: Application Crashes (Abfragehäufigkeit: Anwendungsabstürze)
		* Application Name: Any application (Anwendungsname: Jede Anwendung)
		* Application Version: Any version (Anwendungsversion: Jede Version)
    * Threshold (Schwellenwert)
      * Threshold Type: Crash Count (Schwellenwerttyp: Absturzanzahl)
      * Operator: is greater than or equals 5 (Operator: Größer gleich 5)
4. Klicken Sie auf die Registerkarte **Verteilungsmethode** und gegen Sie den folgenden Wert an:
  * Method: Analytics Console Only (Methode: Nur Analytics-Konsole)

    **Hinweis:** Wählen Sie die Option für Analytics-Konsole und Network Post aus, wenn Sie zusätzlich eine POST-Nachricht mit JSON-vernetzen an die angepasste URL senden möchten. Wenn Sie diese Option auswählen, sind die folgenden Felder verfügbar:
      * Network Post URL (required) (Network Post-URL (erforderlich))
      * Headers (optional) (Header (optional))
      * Authentication Type (required) (Authentifizierung (erforderlich))
5. Klicken Sie auf **Speichern**.

### Alertdefinitionen verwalten
{: #managing-alert-definitions}

Im folgenden Beispiel verwalten Sie Alertdefinitionen auf der Seite 'Alert-Management'.

1. Klicken Sie in der {{site.data.keyword.mobileanalytics_short}}-Konsole auf das Symbol **Alerts**. Daraufhin wird die Seite für Alert-Protokolle geöffnet.
2. Klicken Sie auf die Registerkarte **Alert-Management**.
3. Optional: Schalten Sie das Kontrollkästchen unter der Spalte **Enabled** (Aktiviert) ein bzw. aus, um eine bestimmte Alertdefinition zu aktivieren bzw. zu inaktivieren.
4. Optional: Klicken Sie auf das Symbol zum Duplizieren, wenn Sie eine Kopie einer Alertdefinition erstellen und einige Werte verändern möchten.
5. Optional: Klicken Sie auf das Stiftsymbol, wenn Sie eine Alertdefinition bearbeiten möchten.
6. Optional: Klicken Sie auf das Papierkorbsymbol, wenn Sie eine Alertdefinition löschen möchten.

### Alertdetails anzeigen
{: #viewing-alert-details}

Im folgenden Beispiel zeigen Sie die Details ausgelöster Alerts auf der Seite für Alert-Protokolle an.

1. Klicken Sie in der {{site.data.keyword.mobileanalytics_short}}-Konsole auf das Symbol **Alerts**. Daraufhin wird die Seite für Alert-Protokolle angezeigt.
2. Klicken Sie auf das Symbol **+** für einen beliebigen Alert. Daraufhin werden die Abschnitte mit den Alertdefinitionen und den Alert-Instanzen angezeigt.

    **Hinweis:** Wenn die entsprechende Alertdefinition nicht gelöscht oder geändert wurde, können Sie die Alertdefinition durch Klicken auf die Schaltfläche zum Bearbeiten von Alerts bearbeiten. Andernfalls ist die Schaltfläche zum Bearbeiten von Alerts nicht verfügbar und die folgende Nachricht wird angezeigt:

    `This alert definition has since been modified or deleted.`

3. Optional: Wählen Sie einen Alert aus und klicken Sie auf das Papierkorbsymbol, um den Alert zu löschen.

## App-Abstürze
{: #monitor-app-crash}

Sie können Informationen zu App-Abstürzen in der {{site.data.keyword.mobileanalytics_short}}-Konsole anzeigen, um Ihre Apps besser überwachen und entsprechende Fehler beheben zu können.

### Überwachung von App-Abstürzen
{: #app-crash}

Informationen zu App-Abstürzen können Sie im Abschnitt **Dashboard** der {{site.data.keyword.mobileanalytics_short}}-Konsole schnell anzeigen.

Auf der Seite **Übersicht** des Abschnitts **Dashboard** wird im Balkendiagramm mit den Abstürzen ein Histogramm der Abstürze im zeitlichen Verlauf angezeigt.

Sie können die Daten auf zwei Arten anzeigen:

1. Absturzrate anzeigen: Die Absturzrate im zeitlichen Verlauf
2. Gesamtsumme der Abstürze anzeigen: Gesamte Abstürze im zeitlichen Verlauf


### Fehlerbehebung für App-Abstürze
{: #app-crash-troubleshooting}

Sie können die Seite für Abstürze im Abschnitt **Anwendungen** der {{site.data.keyword.mobileanalytics_short}}-Konsole anzeigen, um die Apps besser verwalten zu können.

In der Tabelle mit der Absturzübersicht werden die folgenden Datenspalten angezeigt:

* App: app name (App: App-Name)
* Crashes: total number of crashes for that app (Abstürze: Gesamtzahl der Abstürze für diese App)
* Total Uses: total number of times a user opens and closes that app (Gesamte Verwendungen: Die Angabe, wie oft diese App geöffnet und geschlossen wurde)
* Crash Rate: percentage of crashes per use (Absturzrate: Der Prozentsatz der Abstürze pro Verwendung)

Die Tabelle für die Absturzzusammenfassung kann sortiert werden und besteht aus den folgenden Datenspalten:

* Crashes (Abstürze)
* Devices (Geräte)
* Last Crash (Letzter Absturz)
* App (App)
* OS (Betriebssystem)
* Message(Nachricht)

Sie können auf das Plussymbol (+) neben einem beliebigen Eintrag klicken, um die Tabelle mit den Absturzdetails anzuzeigen, in der die folgenden Spalten enthalten sind:

* Time Crashed (Absturzzeit)
* App Version (App-Version)
* OS Version (Version des Betriebssystems)
* Device Model (Gerätemodell)
* Device ID (Geräte-ID)
* Download: link to download the logs that led up to the crash (Download: Link zum Herunterladen der Protokolle führte zum Absturz)

Sie können einen Eintrag in der Tabelle mit den Absturzdetails erweitern, um weitere Details (u. a. einen Stack-Trace) anzuzeigen.

**Hinweis:** Die Daten für die Tabelle mit der Absturzzusammenfassung werden durch Abfragen der Clientprotokolle mit schwerwiegenden Fehlern gefüllt. Wenn von einer App keine Protokolle mit schwerwiegenden Fehlern erfasst werden, sind keine Daten verfügbar.


