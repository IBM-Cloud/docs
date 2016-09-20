---

copyright:
  years: 2015, 2016

---

# Nutzungsanalysedaten erfassen
{: #usage-analytics}
Letzte Aktualisierung: 6. Mai 2016
{: .last-updated}

Sie können das {{site.data.keyword.amashort}}-Client-SDK so konfigurieren, dass Nutzungsanalysedaten aufgezeichnet und die aufgezeichneten Daten an den {{site.data.keyword.amashort}}-Service gesendet werden.

**Wichtig**: Die Überwachungsfunktionen des Service {{site.data.keyword.amashort}} sollen auf den neuen Service [{{site.data.keyword.mobileanalytics_short}}](https://console.ng.bluemix.net/catalog/services/mobile-analytics) migriert werden. Das neue Swift-SDK nutzt den neuen Service {{site.data.keyword.mobileanalytics_short}}, der eine deutlich umfangreichere Analyseerfahrung bereitstellt. Der Service {{site.data.keyword.mobileanalytics_short}} befindet sich aktuell in der Versuchsphase und soll planmäßig noch dieses Jahr allgemein verfügbar gemacht werden. Es empfiehlt sich, die Migration Ihrer Anwendungen zum Verwenden des neuen Service {{site.data.keyword.mobileanalytics_short}} und des Swift-SDK zu überprüfen, da die Verwendung und Unterstützung der Überwachungsfunktionen des Service {{site.data.keyword.amashort}} eingestellt werden sollen, wenn {{site.data.keyword.mobileanalytics_short}} allgemein verfügbar ist.

**Anmerkung:** Stellen Sie sicher, dass Sie die Protokollerfassung aktiviert haben, bevor Sie die Aufzeichnung von Nutzungsanalysedaten starten.

Verwenden Sie die folgenden APIs, um die Aufzeichnung und das Senden von Nutzungsanalysedaten zu starten:

### Android
{: #usage-analytics-android}

```Java
// Aufzeichnung von Nutzungsanalysedaten aktivieren
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

// Aufgezeichnete Nutzungsanalysedaten an den {{site.data.keyword.amashort}}-Service senden
MFPAnalytics.send();
```

### iOS - Objective-C
{: #usage-analytics-objectc}

**Wichtig**: Das Objective-C-SDK wird zwar weiterhin vollständig unterstützt und gilt noch als primäres SDK für {{site.data.keyword.Bluemix}} Mobile Services, seine Verwendung und Unterstützung sollen jedoch zugunsten des neuen Swift-SDK noch dieses Jahr eingestellt werden.

Das Objective-C-SDK meldet Überwachungsdaten an die Überwachungskonsole des Service {{site.data.keyword.amashort}}. Falls Sie auf die Überwachungsfunktionen des Service {{site.data.keyword.amashort}} angewiesen sind, verwenden Sie weiterhin das Objective-C-SDK.

```Objective-C
// Aufzeichnung von Nutzungsanalysedaten aktivieren
[[IMFAnalytics sharedInstance] setEnabled:YES];

// Aufzeichnung von Anwendungslebenszyklusereignissen starten
[[IMFAnalytics sharedInstance] startRecordingApplicationLifecycleEvents];


// Aufgezeichnete Nutzungsanalysedaten an den {{site.data.keyword.amashort}}-Service senden
[[IMFAnalytics sharedInstance] sendPersistedLogs];
```

### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Aufzeichnung von Nutzungsanalysedaten aktivieren
IMFAnalytics.sharedInstance().setEnabled(true)

// Aufzeichnung von Anwendungslebenszyklusereignissen starten
IMFAnalytics.sharedInstance().startRecordingApplicationLifecycleEvents()


// Aufgezeichnete Nutzungsanalysedaten an den {{site.data.keyword.amashort}}-Service senden
IMFAnalytics.sharedInstance().sendPersistedLogs()
```

### Cordova
{: #usage-analytics-cordova}

```JavaScript
// Aufzeichnung von Nutzungsanalysedaten aktivieren
MFPAnalytics.enable();

// Aufgezeichnete Nutzungsanalysedaten an den {{site.data.keyword.amashort}}-Service senden
MFPAnalytics.send();
```
**Anmerkung:** Wenn Sie Cordova-Anwendungen entwickeln, verwenden Sie die native API, um die Aufzeichnung von Anwendungslebenszyklusereignissen zu aktivieren.
