# Collecte des données d'analyse d'utilisation
{: #usage-analytics}

Vous pouvez configurer l'enregistrement des données d'analyse d'utilisation et leur envoi au service {{site.data.keyword.amashort}} par le SDK client de {{site.data.keyword.amashort}}.

**Remarque :** Vous devez avoir activé la capture de la journalisation avant de démarrer l'enregistrement des données d'analyse d'utilisation.

Utilisez les API suivantes pour démarrer l'enregistrement et l'envoi des données d'analyse d'utilisation :

### Android
{: #usage-analytics-android}

```Java
// Enable recording of usage analytics
MFPAnalytics.enable()

// Start recording application startup time
// Add this code in the onCreate method of your main Activity
MFPAnalytics.startLoggingApplicationStartup()

// Record the duration of application startup
// Add this code in the onStarted method of your main Activity
MFPAnalytics.logApplicationStartup()

// Record application foreground and background events
// Add this code in the onPause and onResume methods of your main Activity
MFPAnalytics.logSessionStart()
MFPAnalytics.logSessionEnd()

// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
MFPAnalytics.send()
```

### iOS - Objective-C
{: #usage-analytics-objectc}

```Objective-C
// Enable usage analytics recording
[[IMFAnalytics sharedInstance] setEnabled:YES];

// Start recording application lifecycle events
[[IMFAnalytics sharedInstance] startRecordingApplicationLifecycleEvents];


// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
[[IMFAnalytics sharedInstance] sendPersistedLogs];
```

### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Enable usage analytics recording
IMFAnalytics.sharedInstance().setEnabled(true)

// Start recording application lifecycle events
IMFAnalytics.sharedInstance().startRecordingApplicationLifecycleEvents()


// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
IMFAnalytics.sharedInstance().sendPersistedLogs()
```

### Cordova
{: #usage-analytics-cordova}

```JavaScript
// Enable usage analytics recording
MFPAnalytics.enable();

// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
MFPAnalytics.send();
```
**Remarque :** Lorsque vous développez des applications Cordova, utilisez l'API native pour activer l'enregistrement des événements de leur cycle de vie.
