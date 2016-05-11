---

copyright:
  years: 2015, 2016
  
---

# Protokollfunktion aktivieren, konfigurieren und verwenden
{: #enable-logger}

Das {{site.data.keyword.amashort}}-Client-SDK stellt ein Protokollierungsframework bereit, das anderen Protokollierungsframeworks, mit denen Sie vielleicht vertraut sind, wie `java.util.logging` oder `log4j`, ähnlich ist. Das Protokollierungsframework unterstützt mehrere Protokollierungsinstanzen auf Paketbasis, verschiedene Protokollierungsstufen, die Erfassung von Stack-Traces für einen Anwendungsabsturz und weitere Funktionen.

Zudem können Sie die protokollierten Daten zur Speicherung in einem lokalen Speicher konfigurieren, der auf Anforderung an den {{site.data.keyword.amashort}}-Service gesendet werden kann.

Das Protokollierungsframework des {{site.data.keyword.amashort}}-Client-SDK unterstützt die folgenden Protokollierungsstufen, die mit steigender Ausführlichkeit sowie mit Hinweisen zur jeweils empfohlenen Verwendung aufgeführt werden:

* `FATAL` - Wird für nicht behebbare Abstürze oder Blockierungen verwendet. Die Stufe FATAL ist für die Protokollierung nicht behebbarer Fehler reserviert, die für Benutzer wie ein Anwendungsabsturz aussehen.
* `ERROR` - Wird für unerwartete Ausnahmen oder unerwartete Netzprotokollfehler verwendet.
* `WARN` - Dient zur Protokollierung von Warnungen, die nicht als kritische Fehler betrachtet werden (z. B. die Verwendung veralteter APIs oder langsame Netzantwortzeiten).
* `INFO` - Wird zur Meldung von Initialisierungsereignissen und anderen Daten verwendet, die von Nutzen sein können.
* `DEBUG` - Wird zur Meldung von Debuganweisungen verwendet, die Entwicklern bei der Behebung von Anwendungsmängeln helfen.

Stellen Sie sicher, dass Sie das {{site.data.keyword.amashort}}-Client-SDK initialisieren, bevor Sie das Protokollierungsframework verwenden. Die folgenden Beispiel veranschaulichen die grundlegende Verwendung des Protokollierungsframeworks aus dem {{site.data.keyword.amashort}}-Client-SDK.

### Android
{: #enable-logger-android}

```Java
BMSClient.getInstance().initialize(context, appRoute, appGUID);

Logger logger = Logger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```

### iOS - Objective-C
{: #enable-logger-objectc}

```Objective-C
[[IMFClient sharedInstance] initializeWithBackendRoute:appRoute backendGUID:appGUID];

IMFLogger *logger = [IMFLogger loggerForName:@"myLogger"];

[logger logDebugWithMessages:@"debug"];
[logger logInfoWithMessages:@"info"];
[logger logWarnWithMessages:@"warn"];
[logger logErrorWithMessages:@"error"];
[logger logFatalWithMessages:@"fatal"];

```

### iOS - Swift
{: #enable-logger-swift}

```Swift
IMFClient.sharedInstance().initializeWithBackendRoute(appRoute, backendGUID: appGuid)

let logger = IMFLogger(forName: "myLogger");

logger.logDebugWithMessages("debug");
logger.logInfoWithMessages("info");
logger.logWarnWithMessages("warn");
logger.logErrorWithMessages("error");
logger.logFatalWithMessages("fatal");
```

**Anmerkung:** Das {{site.data.keyword.amashort}}-Client-SDK ist mit Objective-C implementiert. Daher müssen Sie Ihrem Swift-Projekt möglicherweise die Datei `IMFLoggerExtension.swift` hinzufügen, um die vorherige Protokollierungs-API verwenden zu können. Sie finden diese Datei im [Mobile Client Access-Client-SDK-Archiv](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).


### Cordova
{: #enable-logger-android-cordova}

```JavaScript
BMSClient.initialize(appRoute , appGUID);

var logger = MFPLogger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");

```

In den Logger-Klassen sind die folgenden zusätzlichen Methoden zu finden:

* `setCapture` - Dient zum Aktivieren oder Inaktivieren der Speicherung von Protokolldaten, die später an den {{site.data.keyword.amashort}}-Service gesendet werden sollen.
* `setLevel` - Dient zum Festlegen der Protokollierungsstufe für die Speicherung von Protokollnachrichten.
* `send` - Sendet gespeicherte Protokolle an den {{site.data.keyword.amashort}}-Service.

Wenn beispielsweise die Erfassung auf ON gesetzt und als Protokollierungsstufe FATAL konfiguriert ist, erfasst die Protokollfunktion nicht abgefangene Ausnahmebedingungen. Nicht abgefangene Ausnahmebedingungen erscheinen Benutzern häufig als Anwendungsabstürze. Es werden jedoch keine Protokolle erfasst, die den Weg zum Absturzereignis aufzeigen. Alternativ stellt eine ausführlichere Protokollierungsstufe sicher, dass Protokolle, die zu dem Protokolleintrag der Stufe FATAL geführt haben, wie zum Beispiel Warnungen (WARN) und Fehler (ERROR), auch erfasst werden.

**Anmerkung:** Vollständige Referenzinformationen zur Logger-API für jede Plattform finden Sie unter [SDKs, Beispiele und API-Referenzen](sdks-samples-apis.html). Die Logger-API gehört zum Kern (Core) des {{site.data.keyword.amashort}}-Client-SDK.


## Verwendungsbeispiel
{: #sample-logger-usage}

Die folgenden Code-Snippets zeigen ein Beispiel für die Verwendung der Protokollfunktion (Logger):

### Android
{: #enable-logger-sample-android}

```Java
// Speicherung von Protokollen aktivieren
Logger.setCapture(true);

// Auszugebende und zu speichernde Mindestprotokollstufe festlegen
Logger.setLevel(Logger.LEVEL.INFO);

// Zwei Logger-Instanzen erstellen
Logger logger1 = Logger.getInstance("logger1");
Logger logger2 = Logger.getInstance("logger2");

// Nachrichten mit unterschiedlichen Stufen protokollieren
logger1.debug("debug message");
logger2.info("info message");

// Gespeicherte Protokolle an den {{site.data.keyword.amashort}}-Service senden
Logger.send();
```

### iOS - Objective-C
{: #enable-logger-sample-objectc}

```Objective-C
// Speicherung von Protokollen aktivieren
[IMFLogger setCapture:YES];

// Erfassung nicht abgefangener Ausnahmen starten
[IMFLogger captureUncaughtExceptions];

// Auszugebende und zu speichernde Mindestprotokollstufe festlegen
[IMFLogger setLogLevel:IMFLogLevelInfo];

// Zwei Logger-Instanzen erstellen
IMFLogger *logger1 = [IMFLogger loggerForName:@"logger1"];
IMFLogger *logger2 = [IMFLogger loggerForName:@"logger2"];

// Nachrichten mit unterschiedlichen Stufen protokollieren
[logger1 logDebugWithMessages:@"debug message"];
[logger2 logInfoWithMessages:@"info message"];

// Gespeicherte Protokolle an den {{site.data.keyword.amashort}}-Service senden
[IMFLogger send];
```

### iOS - Swift
{: #enable-logger-sample-swift}

```Swift
// Speicherung von Protokollen aktivieren
IMFLogger.setCapture(true)

// Erfassung nicht abgefangener Ausnahmen starten
IMFLogger.captureUncaughtExceptions()

// Auszugebende und zu speichernde Mindestprotokollstufe festlegen
IMFLogger.setLogLevel(IMFLogLevel.Info)

// Zwei Logger-Instanzen erstellen
let logger1 = IMFLogger(forName: "logger1");
let logger2 = IMFLogger(forName: "logger2");

// Nachrichten mit unterschiedlichen Stufen protokollieren
logger1.logDebugWithMessages("debug message")
logger2.logInfoWithMessages("info message")

// Gespeicherte Protokolle an den {{site.data.keyword.amashort}}-Service senden
IMFLogger.send()

```

### Cordova
{: #enable-logger-sample-cordova}

```JavaScript
// Speicherung von Protokollen aktivieren
MFPLogger.setCapture(true);

// Auszugebende und zu speichernde Mindestprotokollstufe festlegen
MFPLogger.setLevel(MFPLogger.INFO);

// Zwei Logger-Instanzen erstellen
var logger1 = MFPLogger.getInstance("logger1");
var logger2 = MFPLogger.getInstance("logger2");    

// Nachrichten mit unterschiedlichen Stufen protokollieren
logger1.debug ("debug message");
logger2.info ("info message");

// Gespeicherte Protokolle an den {{site.data.keyword.amashort}}-Service senden
MFPLogger.send(success, failure);
```

## Interne Protokolle für das {{site.data.keyword.amashort}}-Client-SDK aktivieren
{: #enable-logger-sdklogs}
Diese Funktion ist gegenwärtig nur in der Android-Version des {{site.data.keyword.amashort}}-Client-SDK verfügbar.

Das {{site.data.keyword.amashort}}-Client-SDK ermöglicht eine bequemere Entwicklungsarbeit, indem es die Logcat-Ausgabe nicht unbedingt durch interne Debugnachrichten erweitert. Daher werden interne Protokollnachrichten, die vom {{site.data.keyword.amashort}}-SDK bei der Stufe DEBUG generiert werden, standardmäßig nicht ausgegeben. Sie können die Ausgabe aller interner Protokollnachrichten des {{site.data.keyword.amashort}}-Client-SDK mit der folgenden API aktivieren:


```
Logger.setSDKInternalLoggingEnabled(true);
```
