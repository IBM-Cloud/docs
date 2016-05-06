---

copyright:
  years: 2015, 2016

---

# Nutzungsanalysedaten erfassen
{: #usage-analytics}

Sie können das {{site.data.keyword.amashort}}-Client-SDK so konfigurieren, dass Nutzungsanalysedaten aufgezeichnet und die aufgezeichneten Daten an den {{site.data.keyword.amashort}}-Service gesendet werden.

**Anmerkung:** Stellen Sie sicher, dass Sie die Protokollerfassung aktiviert haben, bevor Sie die Aufzeichnung von Nutzungsanalysedaten starten.

Verwenden Sie die folgenden APIs, um die Aufzeichnung und das Senden von Nutzungsanalysedaten zu starten:

### Android
{: #usage-analytics-android}

```Java
// Aufzeichnung von Nutzungsanalysedaten aktivieren.
MFPAnalytics.enable();

// Aufzeichnung der Anwendungsstartzeit starten.
// Fügen Sie diesen Code in der Methode 'onCreate' Ihrer Hauptaktivität hinzu.
MFPAnalytics.startLoggingApplicationStartup();

// Dauer des Anwendungsstarts aufzeichnen.
// Fügen Sie diesen Code in der Methode 'onStart' Ihrer Hauptaktivität hinzu.
MFPAnalytics.logApplicationStartup();

// Vorder- und Hintergrundereignisse der Anwendung aufzeichnen.
// Fügen Sie diesen Code in den Methoden 'onPause' und 'onResume' Ihrer Hauptaktivität hinzu.
MFPAnalytics.logSessionStart();
MFPAnalytics.logSessionEnd();

// Aufgezeichnete Nutzungsanalysedaten an {{site.data.keyword.amashort}}-Service senden
MFPAnalytics.send();
```

### iOS - Objective-C
{: #usage-analytics-objectc}

```Objective-C
// Aufzeichnung von Nutzungsanalysedaten aktivieren
[[IMFAnalytics sharedInstance] setEnabled:YES];

// Aufzeichnung von Anwendungslebenszyklusereignissen starten
[[IMFAnalytics sharedInstance] startRecordingApplicationLifecycleEvents];


// Aufgezeichnete Nutzungsanalysedaten an {{site.data.keyword.amashort}}-Service senden
[[IMFAnalytics sharedInstance] sendPersistedLogs];
```

### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Aufzeichnung von Nutzungsanalysedaten aktivieren
IMFAnalytics.sharedInstance().setEnabled(true)

// Aufzeichnung von Anwendungslebenszyklusereignissen starten
IMFAnalytics.sharedInstance().startRecordingApplicationLifecycleEvents()


// Aufgezeichnete Nutzungsanalysedaten an {{site.data.keyword.amashort}}-Service senden
IMFAnalytics.sharedInstance().sendPersistedLogs()
```

### Cordova
{: #usage-analytics-cordova}

```JavaScript
// Aufzeichnung von Nutzungsanalysedaten aktivieren
MFPAnalytics.enable();

// Aufgezeichnete Nutzungsanalysedaten an {{site.data.keyword.amashort}}-Service senden
MFPAnalytics.send();
```
**Anmerkung:** Wenn Sie Cordova-Anwendungen entwickeln, verwenden Sie die native API, um die Aufzeichnung von Anwendungslebenszyklusereignissen zu aktivieren.
