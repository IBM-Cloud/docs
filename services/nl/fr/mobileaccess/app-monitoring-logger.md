---

Copyright : 2015, 2016
  
---

# Activation, configuration et utilisation de Logger
{: #enable-logger}

Le SDK client de {{site.data.keyword.amashort}} fournit une
infrastructure de journalisation similaire à d'autres infrastructures que vous pouvez connaître, telles que `java.util.logging` ou `log4j`. L'infrastructure de journalisation prend notamment en charge plusieurs instances de consignateur par package, différents niveaux de journalisation et la capture des traces de pile.

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

**Remarque :** Le SDK client de {{site.data.keyword.amashort}} est implémenté à l'aide d'Objective-C. Il peut donc être nécessaire d'ajouter le fichier `IMFLoggerExtension.swift` à votre projet Swift pour utiliser l'ancienne API de consignation. Se fichier se trouve dans l'[archive du SDK client de Mobile Client Access](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).


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


## Exemple d'utilisation
{: #sample-logger-usage}

Le fragment de code suivant est un exemple d'utilisation de Logger :

### Android
{: #enable-logger-sample-android}

```Java
// Enable persisting logs
Logger.setCapture(true);

// Set the minimum log level to be printed and persisted
Logger.setLevel(Logger.LEVEL.INFO);

// Create two logger instances
Logger logger1 = Logger.getInstance("logger1");
Logger logger2 = Logger.getInstance("logger2");

// Log messages with different levels
logger1.debug("debug message");
logger2.info("info message");

// Envoi des journaux conservés au service {{site.data.keyword.amashort}}
Logger.send();
```

### iOS - Objective-C
{: #enable-logger-sample-objectc}

```Objective-C
// Enable persisting logs
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

// Envoi des journaux conservés au service {{site.data.keyword.amashort}}
[IMFLogger send];
```

### iOS - Swift
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

// Envoi des journaux conservés au service {{site.data.keyword.amashort}}
IMFLogger.send()

```

### Cordova
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

// Envoi des journaux conservés au service {{site.data.keyword.amashort}}
MFPLogger.send(success, failure);
```

## Activation des journaux internes du SDK client de {{site.data.keyword.amashort}}
{: #enable-logger-sdklogs}
Cette fonctionnalité n'est actuellement disponible que dans la version Android du SDK client de {{site.data.keyword.amashort}}.

Le SDK client de {{site.data.keyword.amashort}} offre une meilleure expérience de développement car il n'alourdit pas de manière inutile la sortie Logcat avec des messages de débogage internes. Ainsi, par défaut, les messages de journaux internes de niveau DEBUG générés par le SDK client de {{site.data.keyword.amashort}} ne sont pas imprimés. Vous pouvez activer l'impression de tous les messages de journal internes du SDK client de {{site.data.keyword.amashort}} avec l'API suivante :


```
Logger.setSDKInternalLoggingEnabled(true);
```
