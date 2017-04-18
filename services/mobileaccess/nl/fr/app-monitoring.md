---

copyright:
  years: 2015, 2016
  
---

# Surveillance des applications
{: #app-monitoring}
Dernière mise à jour : 22 septembre 2016
{: .last-updated}

Outre les fonctions de sécurité, {{site.data.keyword.amafull}} fournit également des fonctions de surveillance et d'analyse à vos applications mobiles. Le SDK client de {{site.data.keyword.amashort}} vous permet d'enregistrer les journaux client et de surveiller les données. Les développeurs peuvent contrôler le moment auquel ces données doivent être envoyées au service {{site.data.keyword.amashort}}. Tous les événements de sécurité, tels que les réussites et les échecs d'authentification, qui se produisent dans le service {{site.data.keyword.amashort}} sont automatiquement journalisés.
<!--
**Note**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available. -->

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

Les applications utilisées en production rencontrent parfois des problèmes qu'un développeur devra corriger. Il est souvent difficile de reproduire ces problèmes. Les développeurs qui ont travaillé sur le code peuvent ne pas disposer de l'environnement ou du périphérique exact devant servir au test. Dans
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

3. Cliquez sur le bouton **Surveillance** dans le panneau de navigation du tableau de bord {{site.data.keyword.amashort}}.


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

#### Scénario de niveau de journalisation
{: #log-level-scenario}

Lorsque le niveau du journal d'événements a pour valeur `FATAL`, ce dernier capture les exceptions non interceptées, mais pas les journaux qui produisent l'événement de panne. Vous pouvez définir un niveau de journalisation plus prolixe pour garantir que les journaux susceptibles de produire une entrée `FATAL`, comme `WARN` ou `ERROR`, soient également capturés.

Vous devez avoir initialisé le SDK client de {{site.data.keyword.amashort}} avant d'utiliser l'infrastructure de journalisation. Les exemples suivants illustrent l'utilisation de base de l'infrastructure de journalisation du SDK client de {{site.data.keyword.amashort}}.

<!-- **Important**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available.-->

#### Android
{: #enable-logger-android}

```Java
BMSClient.getInstance().initialize(this.getApplicationContext(), BMSClient.REGION_US_SOUTH); // Make sure that you point to your region

Logger logger = Logger.getLogger("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```
{: codeblock}

Le paramètre **bluemixRegion** spécifie le déploiement Bluemix que vous utilisez, par exemple
`BMSClient.REGION_US_SOUTH` ou `BMSClient.REGION_UK`. 

#### iOS - Swift
{: #enable-logger-swift}

```Swift
BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.REGION_US_SOUTH) // You can change the region
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
BMSClient.initialize(BMSClient.REGION_US_SOUTH); // You can change the region

var logger = BMSLogger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```
{: codeblock}

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


### Exemple d'utilisation de journal d'événements
{: #sample-logger-usage}

Le fragment de code suivant est un exemple d'utilisation de Logger :

#### Android
{: #enable-logger-sample-android}

```Java
// Configure Logger to save logs to the device so that they 
// can later be sent to the {{site.data.keyword.amashort}} service
// Disabled by default; set to true to enable
Logger.storeLogs(true);

// Change the minimum log level (optional)
// The default setting is Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);

// Create two logger instances
// You can create multiple log instances to organize your logs
Logger logger1 = Logger.getLogger("logger1");
Logger logger2 = Logger.getLogger("logger2");

// Log messages with different levels
// Debug message for feature 1
// Info message for feature 2
logger1.debug("debug message"); 
//the logger1.debug message is not logged because the logLevelFilter is set to Info
logger2.info("info message");

// Send logs to the {{site.data.keyword.amashort}} service
Logger.send();
```
{: codeblock}

#### iOS - Swift
{: #enable-logger-sample-swift}

```Swift
// Configure Logger to save logs to the device so that they can later be sent to the {{site.data.keyword.amashort}} service
// Disabled by default; set to true to enable
Logger.logStoreEnabled = true

// Change the minimum log level (optional)
// The default setting is LogLevel.Debug
Logger.logLevelFilter = LogLevel.Info

// Create two logger instances
// You can create multiple log instances to organize your logs
let logger1 = Logger.logger(forName: "feature1Logger")
let logger2 = Logger.logger(forName: "feature2Logger")

// Log messages with different levels
logger1.debug("debug message for feature 1") 
//the logger1.debug message is not logged because the logLevelFilter is set to Info
logger2.info("info message for feature 2")

// Send logs to the {{site.data.keyword.amashort}} service
Logger.send()
```
{: codeblock}

#### Cordova
{: #enable-logger-sample-cordova}

```JavaScript
// Enable persisting logs
BMSLogger.setCapture(true);

// Set the minimum log level to be printed and persisted
BMSLogger.setLevel(BMSLogger.INFO);

// Create two logger instances
var logger1 = BMSLogger.getInstance("logger1");
var logger2 = BMSLogger.getInstance("logger2");    

// Log messages with different levels
logger1.debug ("debug message");
logger2.info ("info message");

// Send persisted logs to the {{site.data.keyword.amashort}} service
BMSLogger.send(success, failure);
```
{: codeblock}

### Activation des journaux internes du SDK client de {{site.data.keyword.amashort}}
{: #enable-logger-sdklogs}
Cette fonctionnalité n'est actuellement disponible que dans la version Android du SDK client de {{site.data.keyword.amashort}}.

Le SDK client de {{site.data.keyword.amashort}} offre une meilleure expérience de développement car il n'alourdit pas de manière inutile la sortie Logcat avec des messages de débogage internes. Ainsi, par défaut, les messages de journaux internes de niveau DEBUG générés par le SDK client de {{site.data.keyword.amashort}} ne sont pas imprimés. Vous pouvez activer l'impression de tous les messages de journal internes du SDK client de {{site.data.keyword.amashort}} avec l'API suivante :


```
Logger.setSDKInternalLoggingEnabled(true);
```
{: codeblock}

## Collecte des données d'analyse d'utilisation
{: #usage-analytics}

Vous pouvez configurer l'enregistrement des données d'analyse d'utilisation et leur envoi au service {{site.data.keyword.amashort}} par le SDK client de {{site.data.keyword.amashort}}.
<!--
**Important**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available. -->

**Remarque :** Vous devez avoir activé la capture de la journalisation avant de démarrer l'enregistrement des données d'analyse d'utilisation.

Utilisez les API suivantes pour démarrer l'enregistrement et l'envoi des données d'analyse d'utilisation :

#### Android
{: #usage-analytics-android}

```Java
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.disable();
	
// Enable recording of usage analytics
Analytics.enable();
	
Analytics.log(eventJSONObject);
	
// Send recorded usage analytics to the Mobile Analytics Service
Analytics.send();
```
{: codeblock}

#### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.enabled = false

// Enable recording of usage analytics
Analytics.enabled = true

// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service
Analytics.send()
```
{: codeblock}

#### Cordova
{: #usage-analytics-cordova}

```JavaScript
// Enable usage analytics recording
BMSAnalytics.enable();

// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
BMSAnalytics.send();
```
{: codeblock}

**Remarque :** Lorsque vous développez des applications Cordova, utilisez l'API native pour activer l'enregistrement des événements de leur cycle de vie.
