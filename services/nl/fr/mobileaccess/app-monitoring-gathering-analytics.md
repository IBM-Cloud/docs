---

copyright:
  years: 2015, 2016

---

# Collecte des données d'analyse d'utilisation
{: #usage-analytics}
*Dernière mise à jour : 6 mai 2016*
{: .last-updated}

Vous pouvez configurer l'enregistrement des données d'analyse d'utilisation et leur envoi au service {{site.data.keyword.amashort}} par le SDK client de {{site.data.keyword.amashort}}.

**Important** : une migration des fonctions de surveillance du service {{site.data.keyword.amashort}} est prévue vers le nouveau service [{{site.data.keyword.mobileanalytics_short}}](https://console.ng.bluemix.net/catalog/services/mobile-analytics). Le nouveau kit SDK Swift s'appuie sur le nouveau service {{site.data.keyword.mobileanalytics_short}}, qui fournit une expérience d'analyse beaucoup plus riche. Le service {{site.data.keyword.mobileanalytics_short}} est actuellement en phase expérimentale, et il devrait être disponible pour tous plus tard dans l'année. Il vous est donc conseillé de réfléchir à la migration de vos applications pour utiliser le nouveau service {{site.data.keyword.mobileanalytics_short}} et le SDK Swift, puisque les fonctions de surveillance du service {{site.data.keyword.amashort}} ne seront plus proposées quand {{site.data.keyword.mobileanalytics_short}} sera disponible.

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

**Important** : alors que le SDK Objective-C reste complètement pris en charge et est toujours considéré comme le SDK principal pour {{site.data.keyword.Bluemix}} Mobile Services, il est prévu qu'il soit interrompu plus tard dans l'année et remplacé par le nouveau SDK Swift.

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
