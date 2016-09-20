---

copyright:
  years: 2015, 2016

---

# Collecte des données d'analyse d'utilisation
{: #usage-analytics}
Dernière mise à jour : 6 mai 2016
{: .last-updated}

Vous pouvez configurer l'enregistrement des données d'analyse d'utilisation et leur envoi au service {{site.data.keyword.amashort}} par le SDK client de {{site.data.keyword.amashort}}.

**Important** : une migration des fonctions de surveillance du service {{site.data.keyword.amashort}} est prévue vers le nouveau service [{{site.data.keyword.mobileanalytics_short}}](https://console.ng.bluemix.net/catalog/services/mobile-analytics). Le nouveau kit SDK Swift s'appuie sur le nouveau service {{site.data.keyword.mobileanalytics_short}}, qui fournit une expérience d'analyse beaucoup plus riche. Le service {{site.data.keyword.mobileanalytics_short}} est actuellement en phase expérimentale, et il devrait être disponible pour tous plus tard dans l'année. Il vous est donc conseillé de réfléchir à la migration de vos applications pour utiliser le nouveau service {{site.data.keyword.mobileanalytics_short}} et le SDK Swift, puisque les fonctions de surveillance du service {{site.data.keyword.amashort}} ne seront plus proposées quand {{site.data.keyword.mobileanalytics_short}} sera disponible.

**Remarque :** Vous devez avoir activé la capture de la journalisation avant de démarrer l'enregistrement des données d'analyse d'utilisation.

Utilisez les API suivantes pour démarrer l'enregistrement et l'envoi des données d'analyse d'utilisation :

### Android
{: #usage-analytics-android}

```Java
// Enable recording of usage analytics
MFPAnalytics.enable();

// Start recording application startup time
// Add this code in the onCreate method of your main Activity
MFPAnalytics.startLoggingApplicationStartup();

// Record the duration of application startup
// Add this code in the onStart method of your main Activity
MFPAnalytics.logApplicationStartup();

// Record application foreground and background events
// Add this code in the onPause and onResume methods of your main Activity
MFPAnalytics.logSessionStart();
MFPAnalytics.logSessionEnd();

// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
MFPAnalytics.send();
```

### iOS - Objective-C
{: #usage-analytics-objectc}

**Important** : Bien que que le SDK Objective-C reste complètement pris en charge et soit toujours considéré comme le SDK principal pour
{{site.data.keyword.Bluemix}} Mobile Services, il est envisagé de le retirer plus tard dans l'année et de le remplacer par le nouveau SDK Swift.

Le SDK Objective-C rapporte les données de surveillance à la console de surveillance du service {{site.data.keyword.amashort}}. Si vous dépendez des fonctions de surveillance du service {{site.data.keyword.amashort}}, continuez à utiliser le SDK Objective-C.

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
