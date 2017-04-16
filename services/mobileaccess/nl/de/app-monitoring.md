---

copyright:
  years: 2015, 2016
  
---

# Anwendungen überwachen
{: #app-monitoring}
Letzte Aktualisierung: 22. September 2016
{: .last-updated}

Neben Sicherheitseinrichtungen stellt {{site.data.keyword.amafull}} auch Überwachungs- und Analysefunktionen für Ihre mobilen Anwendungen bereit. Mit dem {{site.data.keyword.amashort}}-Client-SDK können Sie Clientprotokolle und Überwachungsdaten aufzeichnen. Entwickler können steuern, wann diese Daten an den {{site.data.keyword.amashort}}-Service gesendet werden sollen. Alle Sicherheitsereignisse, wie zum Beispiel erfolgreiche oder fehlgeschlagene Authentifizierungen, die im {{site.data.keyword.amashort}}-Service auftreten, werden automatisch protokolliert.
<!--
**Note**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available. -->

Wenn Daten an {{site.data.keyword.amashort}} übergeben werden, können Sie das {{site.data.keyword.amashort}}-Überwachungsdashboard verwenden, um Analyseerkenntnisse zu Ihren mobilen Anwendungen, Geräten und Clientprotokollen zu erhalten. Informationen zu Anforderungen, die Ihre Anwendung an Ressourcen sendet, die von {{site.data.keyword.amashort}} geschützt werden, werden standardmäßig aufgezeichnet.

Zu den automatisch aufgezeichneten Daten gehören Informationen wie die Anzahl der Authentifizierungen, der neuen Geräte und der neuen Benutzer. Darüber hinaus können Sie das {{site.data.keyword.amashort}}-Client-SDK so konfigurieren, dass es die folgenden Informationen zurückmeldet:

### Nutzungsstatistikdaten der mobilen Anwendungen
{: #usage-stats}

Sie können Ihre mobilen Anwendungen so konfigurieren, dass sie mit einigen einfachen API-Aufrufen Anwendungslebenzyklusereignisse aufzeichnen und die aufgezeichneten Daten an den {{site.data.keyword.amashort}}-Service senden. Sie können die Anzahl der Öffnungsvorgänge für Apps, der empfangenen Push-Benachrichtigungen usw. aufzeichnen.

### Clientseitige Protokollerfassung
{: #client-side-logcapture}

Bei Anwendungen in diesem Bereich kommt es ab und zu zu Problemen, die von einem Entwickler behoben werden müssen. Oft ist es schwierig, diese Probleme zu reproduzieren. Entwickler, die an dem Code gearbeitet haben, verfügen möglicherweise nicht über die Umgebung oder das richtige Gerät, um die entsprechenden Tests durchzuführen. In diesen Situationen ist es hilfreich, die Debugprotokolle von den Clientgeräten abrufen zu können, da die Probleme in der Umgebung auftreten, in der die Ereignisse stattfinden.

### Erfasste Daten beibehalten
{: #preserve-captureddata}

Es gibt keine Möglichkeit sicherzustellen, dass alle erfassten Daten auf der Clientseite erhalten bleiben. Benutzer können die mobile Anwendung offline verwenden und gleichzeitig erfasste Analyse- und Protokolldaten kumulieren. Da der Client offline begrenzten Dateisystemspeicherbereich hat, müssen ältere protokollierte Ereignisse gelöscht werden, um neuere protokollierte Ereignisse behalten zu können. Der Entwickler muss entscheiden, wann erfasste Daten über die bereitgestellten APIs an den {{site.data.keyword.amashort}}-Service gesendet werden sollen.

## {{site.data.keyword.amashort}}-Überwachungsdashboard verwenden
{: #monitoring-dashboard}

1. Öffnen Sie das {{site.data.keyword.Bluemix}}-Dashboard und klicken Sie auf Ihre {{site.data.keyword.Bluemix_notm}}-Anwendung.

2. Wenn Ihr {{site.data.keyword.Bluemix_notm}}-Anwendungsdashboard geöffnet ist, klicken Sie auf eine {{site.data.keyword.amashort}}-Kachel.

3. Klicken Sie in der {{site.data.keyword.amashort}}-Dashboard-Navigation auf die Schaltfläche **Überwachung**.


## Protokollfunktion aktivieren, konfigurieren und verwenden
{: #enable-logger}

Das {{site.data.keyword.amashort}}-Client-SDK stellt ein Protokollierungsframework bereit, das anderen Protokollierungsframeworks, mit denen Sie vielleicht vertraut sind, wie `java.util.logging` oder `log4j`, ähnlich ist. Das Protokollierungsframework unterstützt mehrere Protokollierungsinstanzen auf Paketbasis, verschiedene Protokollierungsstufen, die Erfassung von Stack-Traces für einen Anwendungsabsturz und weitere Funktionen.

Zudem können Sie die protokollierten Daten zur Speicherung in einem lokalen Speicher konfigurieren, der auf Anforderung an den {{site.data.keyword.amashort}}-Service gesendet werden kann.

Das Protokollierungsframework des {{site.data.keyword.amashort}}-Client-SDK unterstützt die folgenden Protokollierungsstufen, die mit steigender Ausführlichkeit sowie mit Hinweisen zur jeweils empfohlenen Verwendung aufgeführt werden:

* `FATAL` - Wird für nicht behebbare Abstürze oder Blockierungen verwendet. Die Stufe FATAL ist für die Protokollierung nicht behebbarer Fehler reserviert, die für Benutzer wie ein Anwendungsabsturz aussehen.
* `ERROR` - Wird für unerwartete Ausnahmen oder unerwartete Netzprotokollfehler verwendet.
* `WARN` - Dient zur Protokollierung von Warnungen, die nicht als kritische Fehler betrachtet werden (z. B. die Verwendung veralteter APIs oder langsame Netzantwortzeiten).
* `INFO` - Wird zur Meldung von Initialisierungsereignissen und anderen Daten verwendet, die von Nutzen sein können.
* `DEBUG` - Wird zur Meldung von Debuganweisungen verwendet, die Entwicklern bei der Behebung von Anwendungsmängeln helfen.

#### Szenario für Protokollebene
{: #log-level-scenario}

Wenn die Protokollierungsstufe mit `FATAL` konfiguriert ist, erfasst die Protokollfunktion nicht abgefangene Ausnahmebedingungen. Es werden jedoch keine Protokolle erfasst, die den Weg zum Absturzereignis aufzeigen. Sie können ausführlichere Protokollierungsstufe festlegen, um sicherzustellen, dass Protokolle, die zu einem Protokolleintrag der Stufe `FATAL` führen könnten, z. B. `WARN` oder `ERROR`, ebenfalls erfasst werden.

Stellen Sie sicher, dass Sie das {{site.data.keyword.amashort}}-Client-SDK initialisieren, bevor Sie das Protokollierungsframework verwenden. Die folgenden Beispiel veranschaulichen die grundlegende Verwendung des Protokollierungsframeworks aus dem {{site.data.keyword.amashort}}-Client-SDK.

<!-- **Important**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available.-->

#### Android
{: #enable-logger-android}

```Java
BMSClient.getInstance().initialize(this.getApplicationContext(), BMSClient.REGION_US_SOUTH); // Sicherstellen, dass auf eigene Region verwiesen wird

Logger logger = Logger.getLogger("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```
{: codeblock}

Der Parameter **bluemixRegion** gibt an, welche Bluemix-Bereitstellung Sie verwenden, z. B. `BMSClient.REGION_US_SOUTH` und `BMSClient.REGION_UK`. 

#### iOS - Swift
{: #enable-logger-swift}

```Swift
BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.REGION_US_SOUTH) // Sie können die Region ändern
Analytics.initializeWithAppName(your_app_name_here, apiKey: your_api_key_here, hasUserContext: false, deviceEvents: DeviceEvent.LIFECYCLE)

let logger = Logger.logger(forName: "myLogger")

logger.debug(“debug info")
logger.info(“info message")
logger.warn(“warning message")
logger.error(“error message")
logger.fatal(“fatal message")
```
{: codeblock}
<!--
**Note:** The {{site.data.keyword.amashort}} client SDK is implemented with Objective-C, therefore you might need to add the `IMFLoggerExtension.swift` file to your Swift project to use the previous logger API. You can find this file in the [{{site.data.keyword.amashort}} client SDK archive](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).
-->

#### Cordova
{: #enable-logger-android-cordova}

```JavaScript
BMSClient.initialize(BMSClient.REGION_US_SOUTH); // Sie können die Region ändern

var logger = BMSLogger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```
{: codeblock}

In den Logger-Klassen sind die folgenden zusätzlichen Methoden zu finden:

* `setCapture` - Dient zum Aktivieren oder Inaktivieren der Speicherung von Protokolldaten, die später an den {{site.data.keyword.amashort}}-Service gesendet werden sollen.
* `setLevel` - Dient zum Festlegen der Protokollierungsstufe für die Speicherung von Protokollnachrichten.
* `send` - Sendet gespeicherte Protokolle an den {{site.data.keyword.amashort}}-Service.

Wenn beispielsweise die Erfassung auf ON gesetzt und als Protokollierungsstufe FATAL konfiguriert ist, erfasst die Protokollfunktion nicht abgefangene Ausnahmebedingungen. Nicht abgefangene Ausnahmebedingungen erscheinen Benutzern häufig als Anwendungsabstürze. Es werden jedoch keine Protokolle erfasst, die den Weg zum Absturzereignis aufzeigen. Alternativ stellt eine ausführlichere Protokollierungsstufe sicher, dass Protokolle, die zu dem Protokolleintrag der Stufe FATAL geführt haben, wie zum Beispiel Warnungen (WARN) und Fehler (ERROR), auch erfasst werden.

**Anmerkung:** Vollständige Referenzinformationen zur Logger-API für jede Plattform finden Sie unter [SDKs, Beispiele und API-Referenzen](sdks-samples-apis.html). Die Logger-API gehört zum Kern (Core) des {{site.data.keyword.amashort}}-Client-SDK.


### Beispiel für die Verwendung der Protokollfunktion
{: #sample-logger-usage}

Die folgenden Code-Snippets zeigen ein Beispiel für die Verwendung der Protokollfunktion (Logger):

#### Android
{: #enable-logger-sample-android}

```Java
// Protokollfunktion zum Speichern der Protokolle auf dem Gerät konfigurieren, sodass sie später
// an den {{site.data.keyword.amashort}}-Service gesendet werden können
// Standardmäßig inaktiviert; zum Aktivieren auf true setzen
Logger.storeLogs(true);

// Mindestprotokollierungsebene ändern (optional)
// Die Standardeinstellung ist Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);

// Zwei Logger-Instanzen erstellen
// Sie können mehrere Protokollinstanzen zum Organisieren der Protokolle erstellen
Logger logger1 = Logger.getLogger("logger1");
Logger logger2 = Logger.getLogger("logger2");

// Nachrichten mit unterschiedlichen Stufen protokollieren
// Debugnachricht für Funktion 1
// Informationsnachricht für Funktion 2
logger1.debug("debug message");
// Die Nachricht logger1.debug wird nicht protokolliert, weil für logLevelFilter der Wert info eingestellt ist
logger2.info("info message");

// Protokolle an den {{site.data.keyword.amashort}}-Service senden
Logger.send();
```
{: codeblock}

#### iOS - Swift
{: #enable-logger-sample-swift}

```Swift
// Protokollfunktion zum Speichern der Protokolle auf dem Gerät konfigurieren, sodass sie später an den {{site.data.keyword.amashort}}-Service gesendet werden können
// Standardmäßig inaktiviert; zum Aktivieren auf true setzen
Logger.logStoreEnabled = true

// Mindestprotokollierungsebene ändern (optional)
// Die Standardeinstellung ist LogLevel.Debug
Logger.logLevelFilter = LogLevel.Info

// Zwei Logger-Instanzen erstellen
// Sie können mehrere Protokollinstanzen zum Organisieren der Protokolle erstellen
let logger1 = Logger.logger(forName: "feature1Logger")
let logger2 = Logger.logger(forName: "feature2Logger")

// Nachrichten mit unterschiedlichen Stufen protokollieren
logger1.debug("debug message for feature 1")
//Die Nachricht logger1.debug wird nicht protokolliert, weil für logLevelFilter der Wert info eingestellt ist
logger2.info("info message for feature 2")

// Protokolle an den {{site.data.keyword.amashort}}-Service senden
Logger.send()
```
{: codeblock}

#### Cordova
{: #enable-logger-sample-cordova}

```JavaScript
// Speicherung von Protokollen aktivieren
BMSLogger.setCapture(true);

// Auszugebende und zu speichernde Mindestprotokollstufe festlegen
BMSLogger.setLevel(BMSLogger.INFO);

// Zwei Logger-Instanzen erstellen
var logger1 = BMSLogger.getInstance("logger1");
var logger2 = BMSLogger.getInstance("logger2");

// Nachrichten mit unterschiedlichen Stufen protokollieren
logger1.debug("debug message");
logger2.info("info message");

// Gespeicherte Protokolle an den {{site.data.keyword.amashort}}-Service senden
BMSLogger.send(success, failure);
```
{: codeblock}

### Interne Protokolle für das {{site.data.keyword.amashort}}-Client-SDK aktivieren
{: #enable-logger-sdklogs}
Diese Funktion ist gegenwärtig nur in der Android-Version des {{site.data.keyword.amashort}}-Client-SDK verfügbar.

Das {{site.data.keyword.amashort}}-Client-SDK ermöglicht eine bequemere Entwicklungsarbeit, indem es die Logcat-Ausgabe nicht unbedingt durch interne Debugnachrichten erweitert. Daher werden interne Protokollnachrichten, die vom {{site.data.keyword.amashort}}-SDK bei der Stufe DEBUG generiert werden, standardmäßig nicht ausgegeben. Sie können die Ausgabe aller interner Protokollnachrichten des {{site.data.keyword.amashort}}-Client-SDK mit der folgenden API aktivieren:


```
Logger.setSDKInternalLoggingEnabled(true);
```
{: codeblock}

## Nutzungsanalysedaten erfassen
{: #usage-analytics}

Sie können das {{site.data.keyword.amashort}}-Client-SDK so konfigurieren, dass Nutzungsanalysedaten aufgezeichnet und die aufgezeichneten Daten an den {{site.data.keyword.amashort}}-Service gesendet werden.
<!--
**Important**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available. -->

**Anmerkung:** Stellen Sie sicher, dass Sie die Protokollerfassung aktiviert haben, bevor Sie die Aufzeichnung von Nutzungsanalysedaten starten.

Verwenden Sie die folgenden APIs, um die Aufzeichnung und das Senden von Nutzungsanalysedaten zu starten:

#### Android
{: #usage-analytics-android}

```Java
// Aufzeichnung der Nutzungsanalysedaten inaktivieren (z. B. zum Sparen von Speicherplatz)
// Aufzeichnung ist standardmäßig aktiviert
Analytics.disable();
	
// Aufzeichnung von Nutzungsanalysedaten aktivieren
Analytics.enable();
	
Analytics.log(eventJSONObject);
	
// Aufgezeichnete Nutzungsanalysedaten an den Mobile Analytics-Service senden
Analytics.send();
```
{: codeblock}

#### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Aufzeichnung der Nutzungsanalysedaten inaktivieren (z. B. zum Sparen von Speicherplatz)
// Aufzeichnung ist standardmäßig aktiviert
Analytics.enabled = false

// Aufzeichnung von Nutzungsanalysedaten aktivieren
Analytics.enabled = true

// Aufgezeichnete Nutzungsanalysedaten an den {{site.data.keyword.mobileanalytics_short}}-Service senden
Analytics.send()
```
{: codeblock}

#### Cordova
{: #usage-analytics-cordova}

```JavaScript
// Aufzeichnung von Nutzungsanalysedaten aktivieren
BMSAnalytics.enable();

// Aufgezeichnete Nutzungsanalysedaten an den {{site.data.keyword.amashort}}-Service senden
BMSAnalytics.send();
```
{: codeblock}

**Anmerkung:** Wenn Sie Cordova-Anwendungen entwickeln, verwenden Sie die native API, um die Aufzeichnung von Anwendungslebenszyklusereignissen zu aktivieren.
