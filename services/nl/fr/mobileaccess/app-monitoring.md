---

copyright:
  years: 2015, 2016
  
---

# Surveillance des applications
{: #app-monitoring}
Dernière mise à jour : 28 juin 2016
{: .last-updated}

Outre les fonctions de sécurité, {{site.data.keyword.amafull}} fournit également des fonctions de surveillance et d'analyse à vos applications mobiles. Le SDK client de {{site.data.keyword.amashort}} vous permet d'enregistrer les journaux client et de surveiller les données. Les développeurs peuvent contrôler le moment auquel ces données doivent être envoyées au service {{site.data.keyword.amashort}}. Tous les événements de sécurité, tels que les réussites et les échecs d'authentification, qui se produisent dans le service {{site.data.keyword.amashort}} sont automatiquement journalisés.

**Remarque** : une migration des fonctions de surveillance du service {{site.data.keyword.amashort}} est prévue vers le nouveau service [{{site.data.keyword.mobileanalytics_short}}](https://console.ng.bluemix.net/catalog/services/mobile-analytics). Le nouveau kit SDK Swift s'appuie sur le nouveau service {{site.data.keyword.mobileanalytics_short}}, qui fournit une expérience d'analyse beaucoup plus riche. Le service {{site.data.keyword.mobileanalytics_short}} est actuellement en phase expérimentale, et il devrait être disponible pour tous plus tard dans l'année. Il vous est donc conseillé de réfléchir à la migration de vos applications pour utiliser le nouveau service {{site.data.keyword.mobileanalytics_short}} et le SDK Swift, puisque les fonctions de surveillance du service {{site.data.keyword.amashort}} ne seront plus proposées quand {{site.data.keyword.mobileanalytics_short}} sera disponible.

Lorsque les données ont été fournies à {{site.data.keyword.amashort}}, vous pouvez utiliser le tableau de bord de surveillance de {{site.data.keyword.amashort}} pour analyser les performances pour vos applications mobiles, de vos périphériques et de vos journaux client. Les informations sur les demandes que votre application envoie aux ressources qui sont protégées par
{{site.data.keyword.amashort}} sont enregistrées par défaut.

Les données enregistrées automatiquement comprennent des informations telles que le nombre d'authentifications, les nouveaux périphériques et les nouveaux utilisateurs. En outre, vous pouvez configurer le SDK client de {{site.data.keyword.amashort}} pour signaler les informations suivantes :

### Statistiques d'utilisation de vos applications mobiles
{: #usage-stats}

Vous pouvez configurer l'enregistrement des événements de cycle de vie des applications et l'envoi des données de
journalisation au service {{site.data.keyword.amashort}} par votre application mobile avec quelques appels d'API
simples. Vous pouvez enregistrer le nombre d'ouvertures
d'application, de notifications push reçues, etc.

### Capture de journaux côté client
{: #client-side-logcapture}

Les applications utilisées en production rencontrent parfois des problèmes qu'un développeur devra corriger. Il est souvent difficile de reproduire ces
problèmes. <!--in R&D.--> Les développeurs qui ont travaillé sur le code peuvent ne pas disposer de l'environnement ou du périphérique exact devant servir au test. Dans
ce cas, il est utile de pouvoir extraire les journaux de débogage depuis les périphériques client car les problèmes surviennent dans l'environnement dans
lesquels ils s'exécutent.

### Conservation des données capturées
{: #preserve-captureddata}

Du côté client, la conservation de toutes les données capturées ne peut pas être garantie. Vos utilisateurs peuvent exécuter l'application
mobile hors ligne et accumuler en même temps des données d'analyse et de journal capturées. Etant donné que le client est hors ligne et dispose d'un espace
de système de fichiers limité, les événements journalisés les plus anciens doivent être purgés afin de pouvoir conserver des événements journalisés plus
récemment. Il revient au développeur de décider à quel moment les données capturées doivent être envoyées au service {{site.data.keyword.amashort}} à l'aide des API fournies.

## Utilisation du tableau de bord de surveillance de {{site.data.keyword.amashort}}
{: #monitoring-dashboard}

1. Ouvrez le Tableau de bord {{site.data.keyword.Bluemix}} et cliquez sur votre application
{{site.data.keyword.Bluemix_notm}}.

2. Une fois ouvert le tableau de bord de votre application {{site.data.keyword.Bluemix_notm}}, cliquez sur une vignette
{{site.data.keyword.amashort}}.

3. Cliquez sur le lien **Surveillance** dans la barre de navigation du tableau de bord {{site.data.keyword.amashort}}.


## Activation, configuration et utilisation de Logger
{: #enable-logger}

Le SDK client de {{site.data.keyword.amashort}} fournit une infrastructure de journalisation similaire à d'autres infrastructures que vous pouvez connaître, telles que `java.util.logging` ou `log4j`. L'infrastructure de journalisation prend notamment en charge plusieurs instances de consignateur par package, différents niveaux de journalisation et la capture des traces de pile.

Vous pouvez aussi configurer les données de journal de sorte à les conserver dans un stockage local qui pourra être envoyé sur demande au service
{{site.data.keyword.amashort}}.

L'infrastructure de journalisation du SDK client de {{site.data.keyword.amashort}} prend en charge
les niveaux de journalisation suivants, répertoriés du moins prolixe au plus prolixe, avec leur utilisation recommandée :

* `FATAL` - Pour les pannes ou les blocages irrémédiables. Le niveau FATAL est réservé à la consignation d'erreurs irrémédiables qui se
matérialisent pour l'utilisateur sous forme de panne de l'application.
* `ERROR` - Destiné aux exceptions inattendues ou aux erreurs de protocole réseau inattendues.
* `WARN` - Destiné à consigner des avertissements qui ne sont pas considérés comme des erreurs critiques, comme l'utilisation
d'API obsolètes ou une lenteur des réponses réseau.
* `INFO` - Destiné à signaler des événements d'initialisation et d'autres données potentiellement utiles.
* `DEBUG` - Destiné à communiquer des informations de débogage pouvant aider les développeurs à résoudre les bogues de l'application.

Vous devez avoir initialisé le SDK client de {{site.data.keyword.amashort}} avant d'utiliser l'infrastructure de journalisation. Les exemples suivants illustrent l'utilisation de base de l'infrastructure de journalisation du SDK client de {{site.data.keyword.amashort}}.

**Important** : une migration des fonctions de surveillance du service {{site.data.keyword.amashort}} est prévue vers le nouveau service [{{site.data.keyword.mobileanalytics_short}}](https://console.ng.bluemix.net/catalog/services/mobile-analytics). Le nouveau kit SDK Swift s'appuie sur le nouveau service {{site.data.keyword.mobileanalytics_short}}, qui fournit une expérience d'analyse beaucoup plus riche. Le service {{site.data.keyword.mobileanalytics_short}} est actuellement en phase expérimentale, et il devrait être disponible pour tous plus tard dans l'année. Il vous est donc conseillé de réfléchir à la migration de vos applications pour utiliser le nouveau service {{site.data.keyword.mobileanalytics_short}} et le SDK Swift, puisque les fonctions de surveillance du service {{site.data.keyword.amashort}} ne seront plus proposées quand {{site.data.keyword.mobileanalytics_short}} sera disponible.

#### Android
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

#### iOS - Objective-C
{: #enable-logger-objectc}

**Important** : Bien que le SDK Objective-C reste complètement pris en charge et soit toujours considéré comme le SDK principal pour
{{site.data.keyword.Bluemix}} Mobile Services, il est envisagé de le retirer plus tard dans l'année et de le remplacer par le nouveau SDK
Swift.

Le SDK Objective-C rapporte les données de surveillance à la console de surveillance du service {{site.data.keyword.amashort}}. Si vous dépendez des fonctions de surveillance du service {{site.data.keyword.amashort}}, continuez à utiliser le SDK Objective-C.

```Objective-C
[[IMFClient sharedInstance] initializeWithBackendRoute:appRoute backendGUID:appGUID];

IMFLogger *logger = [IMFLogger loggerForName:@"myLogger"];

[logger logDebugWithMessages:@"debug"];
[logger logInfoWithMessages:@"info"];
[logger logWarnWithMessages:@"warn"];
[logger logErrorWithMessages:@"error"];
[logger logFatalWithMessages:@"fatal"];

```

#### iOS - Swift
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

**Remarque :** Le SDK client de {{site.data.keyword.amashort}} est implémenté à l'aide d'Objective-C. Il peut donc être nécessaire d'ajouter le fichier `IMFLoggerExtension.swift` à votre projet Swift pour utiliser l'ancienne API de consignation. Ce fichier se trouve dans l'[archive du SDK client de {{site.data.keyword.amashort}}](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).


#### Cordova
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

Les classes Logger comprennent également les méthodes suivantes :

* `setCapture` - Active ou désactive la conservation des données de journalisation en vue de leur envoi ultérieur au service
{{site.data.keyword.amashort}}.
* `setLevel` - Définit le niveau de journalisation minimal pour la conservation des messages de journal.
* `send` - Envoie les journaux conservés au service {{site.data.keyword.amashort}}.

Par exemple, lorsque la capture est activée et que le niveau de journalisation est FATAL, le consignateur capture les exceptions non interceptées. Celles-ci apparaissent souvent en cas de panne de l'application, mais ne capturent pas les journaux menant à l'événement à l'origine de la panne. Par
ailleurs, un niveau de journalisation plus prolixe permet de garantir que les journaux menant à une entrée de consignateur FATAL, par exemple WARN et ERROR, sont
également
capturés.

**Remarque :** Les références complètes sur l'API Logger pour chaque plateforme figurent à la rubrique [Logiciels SDK, exemples et référence d'API](sdks-samples-apis.html). L'API Logger est un composant central du SDK client de {{site.data.keyword.amashort}}.


### Exemple d'utilisation
{: #sample-logger-usage}

Le fragment de code suivant est un exemple d'utilisation de Logger :

#### Android
{: #enable-logger-sample-android}

```Java
// Activation de journaux persistants
Logger.setCapture(true);

// Set the minimum log level to be printed and persisted
Logger.setLevel(Logger.LEVEL.INFO);

// Create two logger instances
Logger logger1 = Logger.getInstance("logger1");
Logger logger2 = Logger.getInstance("logger2");

// Log messages with different levels
logger1.debug("debug message");
logger2.info("info message");

// Send persisted logs to the {{site.data.keyword.amashort}} service
Logger.send();
```

#### iOS - Objective-C
{: #enable-logger-sample-objectc}

```Objective-C
// Activation de journaux persistants
[IMFLogger setCapture:YES];

// Start capturing uncaught exceptions
[IMFLogger captureUncaughtExceptions];

// Set the minimum log level to be printed and persisted
[IMFLogger setLogLevel:IMFLogLevelInfo];

// Create two logger instances
IMFLogger *logger1 = [IMFLogger loggerForName:@"logger1"];
IMFLogger *logger2 = [IMFLogger loggerForName:@"logger2"];

// Log messages with different levels
[logger1 logDebugWithMessages:@"debug message"];
[logger2 logInfoWithMessages:@"info message"];

// Send persisted logs to the {{site.data.keyword.amashort}} service
[IMFLogger send];
```

#### iOS - Swift
{: #enable-logger-sample-swift}

```Swift
// Enable persisting logs
IMFLogger.setCapture(true)

// Start capturing uncaught exceptions
IMFLogger.captureUncaughtExceptions()

// Set the minimum log level to be printed and persisted
IMFLogger.setLogLevel(IMFLogLevel.Info)

// Create two logger instances
let logger1 = IMFLogger(forName: "logger1");
let logger2 = IMFLogger(forName: "logger2");

// Log messages with different levels
logger1.logDebugWithMessages("debug message")
logger2.logInfoWithMessages("info message")

// Send persisted logs to the {{site.data.keyword.amashort}} service
IMFLogger.send()

```

#### Cordova
{: #enable-logger-sample-cordova}

```JavaScript
// Enable persisting logs
MFPLogger.setCapture(true);

// Set the minimum log level to be printed and persisted
MFPLogger.setLevel(MFPLogger.INFO);

// Create two logger instances
var logger1 = MFPLogger.getInstance("logger1");
var logger2 = MFPLogger.getInstance("logger2");    

// Log messages with different levels
logger1.debug ("debug message");
logger2.info ("info message");

// Send persisted logs to the {{site.data.keyword.amashort}} service
MFPLogger.send(success, failure);
```

### Activation des journaux internes du SDK client de {{site.data.keyword.amashort}}
{: #enable-logger-sdklogs}
Cette fonctionnalité n'est actuellement disponible que dans la version Android du SDK client de {{site.data.keyword.amashort}}.

Le SDK client de {{site.data.keyword.amashort}} offre une meilleure expérience de développement car il n'alourdit pas de manière inutile la sortie Logcat avec des messages de débogage internes. Ainsi, par défaut, les messages de journaux internes de niveau DEBUG générés par le SDK client de {{site.data.keyword.amashort}} ne sont pas imprimés. Vous pouvez activer l'impression de tous les messages de journal internes du SDK client de {{site.data.keyword.amashort}} avec l'API suivante :


```
Logger.setSDKInternalLoggingEnabled(true);
```

## Collecte des données d'analyse d'utilisation
{: #usage-analytics}

Vous pouvez configurer l'enregistrement des données d'analyse d'utilisation et leur envoi au service {{site.data.keyword.amashort}} par le SDK client de {{site.data.keyword.amashort}}.

**Important** : une migration des fonctions de surveillance du service {{site.data.keyword.amashort}} est prévue vers le nouveau service [{{site.data.keyword.mobileanalytics_short}}](https://console.ng.bluemix.net/catalog/services/mobile-analytics). Le nouveau kit SDK Swift s'appuie sur le nouveau service {{site.data.keyword.mobileanalytics_short}}, qui fournit une expérience d'analyse beaucoup plus riche. Le service {{site.data.keyword.mobileanalytics_short}} est actuellement en phase expérimentale, et il devrait être disponible pour tous plus tard dans l'année. Il vous est donc conseillé de réfléchir à la migration de vos applications pour utiliser le nouveau service {{site.data.keyword.mobileanalytics_short}} et le SDK Swift, puisque les fonctions de surveillance du service {{site.data.keyword.amashort}} ne seront plus proposées quand {{site.data.keyword.mobileanalytics_short}} sera disponible.

**Remarque :** Vous devez avoir activé la capture de la journalisation avant de démarrer l'enregistrement des données d'analyse d'utilisation.

Utilisez les API suivantes pour démarrer l'enregistrement et l'envoi des données d'analyse d'utilisation :

#### Android
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

#### iOS - Objective-C
{: #usage-analytics-objectc}

**Important** : Bien que que le SDK Objective-C reste complètement pris en charge et soit toujours considéré comme le SDK principal pour
{{site.data.keyword.Bluemix}} Mobile Services, il est envisagé de le retirer plus tard dans l'année et de le remplacer par le nouveau SDK
Swift.

Le SDK Objective-C rapporte les données de surveillance à la console de surveillance du service {{site.data.keyword.amashort}}. Si vous dépendez des fonctions de surveillance du service {{site.data.keyword.amashort}}, continuez à utiliser le SDK Objective-C.

```Objective-C
// Enable usage analytics recording
[[IMFAnalytics sharedInstance] setEnabled:YES];

// Start recording application lifecycle events
[[IMFAnalytics sharedInstance] startRecordingApplicationLifecycleEvents];


// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
[[IMFAnalytics sharedInstance] sendPersistedLogs];
```

#### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Enable usage analytics recording
IMFAnalytics.sharedInstance().setEnabled(true)

// Start recording application lifecycle events
IMFAnalytics.sharedInstance().startRecordingApplicationLifecycleEvents()


// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
IMFAnalytics.sharedInstance().sendPersistedLogs()
```

#### Cordova
{: #usage-analytics-cordova}

```JavaScript
// Enable usage analytics recording
MFPAnalytics.enable();

// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
MFPAnalytics.send();
```
**Remarque :** Lorsque vous développez des applications Cordova, utilisez l'API native pour activer l'enregistrement des événements de leur cycle de vie.
