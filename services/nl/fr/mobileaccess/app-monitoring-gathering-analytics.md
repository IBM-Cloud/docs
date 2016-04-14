---

Copyright : 2015, 2016

---

# Collecte des données d'analyse d'utilisation
{: #usage-analytics}

Vous pouvez configurer l'enregistrement des données d'analyse d'utilisation et leur envoi au service {{site.data.keyword.amashort}} par le SDK client de {{site.data.keyword.amashort}}.

**Remarque :** Vous devez avoir activé la capture de la journalisation avant de démarrer l'enregistrement des données d'analyse d'utilisation.

Utilisez les API suivantes pour démarrer l'enregistrement et l'envoi des données d'analyse d'utilisation :

### Android
{: #usage-analytics-android}

```Java
// Activation de l'enregistrement de l'analyse d'utilisation
MFPAnalytics.enable();

// Lancement de l'enregistrement de l'heure de démarrage de l'application
// Ajout de ce code dans la méthode onCreate de votre activité principale
MFPAnalytics.startLoggingApplicationStartup();

// Enregistrement de la durée de démarrage de l'application
// Ajout de ce code dans la méthode onStart de votre activité principale
MFPAnalytics.logApplicationStartup();

// Enregistrement des événements d'avant-plan et d'arrière-plan
// Ajout de ce code dans les méthodes onPause et onResume de votre activité principale
MFPAnalytics.logSessionStart();
MFPAnalytics.logSessionEnd();

// Envoi des analyses d'utilisation enregistrées au service {{site.data.keyword.amashort}}
MFPAnalytics.send();
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
