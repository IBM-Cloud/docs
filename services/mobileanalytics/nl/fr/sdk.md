---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Instrumentation de votre application pour utiliser les logiciels SDK du client {{site.data.keyword.mobileanalytics_short}}
{: #mobileanalytics_sdk}

Les logiciels SDK de {{site.data.keyword.mobileanalytics_full}} vous permettent d'instrumenter votre application mobile.
{: shortdesc}

{{site.data.keyword.mobileanalytics_short}} vous permet de collecter deux <!--three--> catégories de données, et chacune d'elles nécessite un degré d'instrumentation qui lui est propre :

1. Données prédéfinies - Cette catégorie inclut des informations sur les périphériques et l'utilisation générique qui s'appliquent à toutes les applications. Cette catégorie comprend les métadonnées de périphérique (système d'exploitation et modèle de périphérique) et les données d'utilisation (utilisateurs actifs et sessions d'application) qui indiquent le volume, la fréquence ou la durée d'utilisation d'une application. Les données prédéfinies sont collectées automatiquement après que vous avez initialisé le logiciel SDK de {{site.data.keyword.mobileanalytics_short}} dans votre application.

2. Messages de journal d'application - Cette catégorie permet au développeur d'ajouter des lignes de code dans l'application afin de journaliser des messages personnalisés destinés à faciliter le développement et le débogage. Le développeur affecte un niveau de gravité/détail à chaque message de journal et peut ensuite filtrer les messages en fonction du niveau affecté ou économiser de l'espace de stockage en configurant l'application de telle sorte qu'elle ignore les messages dont le niveau de gravité/détail est inférieur au niveau de journalisation spécifié. Pour collecter des données de journal d'application, vous devez initialiser le logiciel SDK de {{site.data.keyword.mobileanalytics_short}} dans votre application, mais également ajouter une ligne de code pour chaque message de journal.

3. Evénements personnalisés - Cette catégorie inclut des données que vous définissez vous-même et qui sont spécifiques à votre application. Ces données représentent des événements qui se produisent dans votre application, comme des vues de page, des clics sur des boutons, ou des achats depuis l'application. Outre l'initialisation du SDK {{site.data.keyword.mobileanalytics_short}} dans votre application, vous devez aussi ajouter une ligne de code pour chaque événement personnalisé
devant faire l'objet d'un suivi. 

Actuellement, des logiciels SDK sont disponibles pour Android, iOS, WatchOS et Cordova.

## Identification de votre valeur de clé d'API pour les données d'identification de service
{: #analytics-clientkey}

Identifiez votre valeur de **clé d'API** avant de configurer le logiciel SDK du client. La clé d'API est requise pour initialiser le logiciel SDK du client.

1. Ouvrez votre tableau de bord de service {{site.data.keyword.mobileanalytics_short}}.
2. Développez **Afficher les données d'identification** pour révéler votre valeur de clé d'API. Vous aurez besoin de la valeur de clé d'API pour initialiser le logiciel SDK client de {{site.data.keyword.mobileanalytics_short}}.


## Initialisation de votre application pour la collecte d'analyses
{: #initalize-ma-sdk}

Initialisez votre application pour qu'elle envoie des journaux au service {{site.data.keyword.mobileanalytics_short}}.

1. Importez le logiciel SDK du client.

	### Android
	{: #android-import notoc}

	Ajoutez les instructions `import` suivantes au début de votre fichier de projet :
	
	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
	```
	{: codeblock}
  
	### iOS
	{: #ios-import notoc}
	
	**Remarque :** Le logiciel SDK de Swift est disponible pour iOS et watchOS.
	
	Importez les infrastructures `BMSCore` et `BMSAnalytics` en ajoutant les instructions `import` suivantes au début de votre fichier de projet `AppDelegate.swift` :

	```Swift
	import BMSCore
	import BMSAnalytics
	```
	{: codeblock}  
   
	### Cordova
	{: #cordova-import notoc}
		
	Ajoutez le plug-in Cordova en exécutant la commande suivante depuis le répertoire racine de votre application Cordova :

	```Javascript
	cordova plugin add bms-core
	```
	{: codeblock}  

2. Initialisez le SDK client {{site.data.keyword.mobileanalytics_short}} dans votre application.

	### Android
	{: #android-init notoc}
	
	Initialisez le logiciel SDK de {{site.data.keyword.mobileanalytics_short}} dans votre application Android en ajoutant le code d'initialisation dans la méthode `onCreate` de l'activité principale de votre application Android ou à l'emplacement le plus approprié pour votre projet.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // Make sure that you point to your region
	```
	{: codeblock}

	Vous devez initialiser la classe `BMSClient` à l'aide du paramètre **bluemixRegion**. Dans l'initialiseur, la valeur **bluemixRegion** spécifie le déploiement {{site.data.keyword.Bluemix_notm}} que vous utilisez, par exemple, `BMSClient.REGION_US_SOUTH` et `BMSClient.REGION_UK`.
     
    <!-- , or `BMSClient.REGION_SYDNEY`.--> 
    
	### iOS
	{: #ios-init notoc}
    
	Initialisez d'abord la classe `BMSClient` à l'aide du code suivant. Placez le code d'initialisation dans la méthode `application(_:didFinishLaunchingWithOptions:)` de votre délégué d'application ou à l'emplacement le plus approprié pour votre projet.
	
	```Swift
    BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Prenez soin de pointer sur votre région
	```
	{: codeblock}

	Vous devez initialiser la classe `BMSClient` à l'aide du paramètre **bluemixRegion**. Dans l'initialiseur, la valeur **bluemixRegion** spécifie le déploiement {{site.data.keyword.Bluemix_notm}} que vous utilisez, par exemple `BMSClient.Region.usSouth` ou `BMSClient.Region.unitedKingdom`.
    <!-- , or `BMSClient.Region.Sydney`. -->
    
	### Cordova
	{: #cordova-init notoc}
    
	Initialisez **BMSClient** et **BMSAnalytics**. Vous devez aussi connaître la valeur de la [**clé d'API**](#analytics-clientkey).

	```Javascript
  var applicationName = "HelloWorld";
  var apiKey =  "your_api_key_here";
  var hasUserContext = true;
  var deviceEvents = [BMSAnalytics.ALL];

	BMSClient.initialize(BMSClient.REGION_US_SOUTH); //Make sure you point to your region	
  BMSAnalytics.initialize(applicationName, apiKey, hasUserContext, deviceEvents)
	```
	{: codeblock}

	Pour utiliser le logiciel SDK du client {{site.data.keyword.mobileanalytics_short}}, vous devez d'abord initialiser la classe `BMSClient` à l'aide du paramètre **bluemixRegion**. Dans l'initialiseur, la valeur **bluemixRegion** spécifie le déploiement {{site.data.keyword.Bluemix_notm}} que vous utilisez, par exemple `BMSClient.REGION_US_SOUTH` ou `BMSClient.REGION_UK`.
    <!-- , or `BMSClient.REGION_SYDNEY`. -->
    
3. Initialisez Analytics en utilisant votre objet d'application et en lui attribuant le nom de votre application. 

	Le nom que vous sélectionnez pour votre application (`your_app_name_here`) s'affiche dans la console {{site.data.keyword.mobileanalytics_short}} comme nom d'application. Le nom d'application est utilisé pour filtrer la recherche des journaux d'application dans votre tableau de bord. Lorsque vous utilisez le même nom d'application sur plusieurs plateformes (par exemple, Android et iOS), tous les journaux issus de cette application s'affichent sous le même nom, quelle que soit la plateforme à partir de laquelle ils ont été envoyés.

	Vous devez aussi connaître la valeur de la [**clé d'API**](#analytics-clientkey).

	### Android
	{: #android-init-analytics notoc}
	
	```Java
	// Dans cet exemple de code, Analytics est configuré pour enregistrer les événements de cycle de vie.
	Analytics.init(getApplication(), "your_app_name_here", apiKey, hasUserContext, Analytics.DeviceEvent.ALL);
	```
	{: codeblock}
	
	**Remarque :** définissez la valeur **true** ou **false** pour `hasUserContext`. Si la valeur est false (valeur par défaut), chaque périphérique est comptabilisé comme un utilisateur actif. La méthode [`Analytics.setUserIdentity("username")`](sdk.html#android-tracking-users), qui vous permet de suivre le nombre d'utilisateurs par périphérique qui utilisent activement votre application, ne fonctionne pas si `hasUserContext` a pour valeur false. Si la valeur est true, chaque utilisation d'[`Analytics.setUserIdentity("username")`](sdk.html#android-tracking-users) est comptabilisée comme un utilisateur actif. Il n'y a pas d'identité d'utilisateur par défaut lorsque `hasUserContext` a pour valeur true ; par conséquent, celle-ci doit être définie pour remplir les graphiques d'utilisateurs actifs.
	
	### iOS
	{: #ios-initialize-analytics notoc}
	
	```Swift 
	Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: .lifecycle, .network)
	```
	{: codeblock}
 	
	### watchOS
	{: #watchos-initialize-analytics notoc}
	 	
	```Swift
 	Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", deviceEvents: .network)
	```
	{: codeblock}
 	
	Un paramètre `deviceEvents` facultatif collecte automatiquement des analyses pour les événements de niveau périphérique.
	
	**Remarque :** définissez la valeur **true** ou **false** pour `hasUserContext`. Si la valeur est false (valeur par défaut), chaque périphérique est comptabilisé comme un utilisateur actif. La méthode [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users), qui vous permet de suivre le nombre d'utilisateurs par périphérique qui utilisent activement votre application, ne fonctionne pas si `hasUserContext` a pour valeur false. Si `hasUserContext` a pour valeur true, chaque utilisation d'[`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) est comptabilisée comme un utilisateur actif. Il n'y a pas d'identité d'utilisateur par défaut lorsque `hasUserContext` a pour valeur true ; par conséquent, celle-ci doit être définie pour remplir les graphiques d'utilisateurs actifs.

	#### watchOS
	{: #watchos-record-device notoc}

	Vous pouvez enregistrer des événements de périphérique sur WatchOS à l'aide des méthodes `Analytics.recordApplicationDidBecomeActive()` et `Analytics.recordApplicationWillResignActive()`.
  
	Ajoutez la ligne suivante à la méthode `applicationDidBecomeActive()` de la classe ExtensionDelegate :
 
	```
	Analytics.recordApplicationDidBecomeActive()
	```
	{: codeblock}

	Ajoutez la ligne suivante à la méthode `applicationWillResignActive()` de la classe ExtensionDelegate :
 
	```
	Analytics.recordApplicationWillResignActive()
	```
	{: codeblock}	
		
4. Vous avez maintenant initialisé votre application pour collecter des analyses. Ensuite, vous pouvez [envoyer des données d'analyse](sdk.html#app-monitoring-gathering-analytics) au service {{site.data.keyword.mobileanalytics_short}}.


## Collecte des données d'analyse d'utilisation
{: #app-monitoring-gathering-analytics}

Vous pouvez configurer l'enregistrement des données d'analyse d'utilisation et leur envoi au service {{site.data.keyword.mobileanalytics_short}} par le SDK client de {{site.data.keyword.mobileanalytics_short}}.

Utilisez les API suivantes pour démarrer l'enregistrement et l'envoi des données d'analyse d'utilisation :


### Android
{: #android-usage-api notoc}
	
```
// Désactivez l'enregistrement des analyses d'utilisation (par exemple, pour économiser de l'espace disque)
// L'enregistrement est activé par défaut
Analytics.disable();
	
// Activez l'enregistrement des analyses d'utilisation
Analytics.enable();
		
// Envoyez des analyses d'utilisation enregistrées à Mobile Analytics Service
Analytics.send(new ResponseListener() {
            @Override
            public void onSuccess(Response response) {
                // Gérez ici le succès de l'envoi des analyses.
            }

            @Override
            public void onFailure(Response response, Throwable throwable, JSONObject jsonObject) {
                // Gérez ici l'échec de l'envoi des analyses.
            }
        });
```
{: codeblock}
	
Exemple d'analyse d'utilisation pour consignation d'un événement :
	
```
// Log a custom analytics event
JSONObject eventJSONObject = new JSONObject();
	
eventJSONObject.put("customProperty" , "propertyValue");

Analytics.log(eventJSONObject);
```
{: codeblock}


### iOS - Swift
{: #ios-usage-api notoc}

```
// Désactivez l'enregistrement des analyses d'utilisation (par exemple, pour économiser de l'espace disque)
// L'enregistrement est activé par défaut
Analytics.isEnabled = false

// Activez l'enregistrement des analyses d'utilisation
Analytics.isEnabled = true

// Envoyez des analyses d'utilisation enregistrées à Mobile Analytics Service
Analytics.send(completionHandler: { (response: Response?, error: Error?) dans

    if let response = response {
        // Gérez ici le succès de l'envoi des analyses.
            }
    if let error = error {
        // Gérez ici l'échec de l'envoi des analyses.
    }
})
```
{: codeblock}

Exemple d'analyse d'utilisation pour consignation d'un événement :

```Swift
// Log a custom analytics event
let eventObject = ["customProperty": "propertyValue"]
Analytics.log(metadata: eventObject)
```
{: codeblock}

### Cordova
{: #usage-analytics-cordova notoc}

```JavaScript
  // Enable usage analytics recording
  BMSAnalytics.enable();
  
// Disable usage analytics recording
  BMSAnalytics.disable();

// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service
  BMSAnalytics.send(
	function(response) {
		console.log('success: ' + response);
		},
	function (err) {
		console.log('fail: ' + err);
		});
```
{: codeblock}

Exemple d'analyse d'utilisation pour consignation d'un événement :

```JavaScript
// Log a custom analytics event
var eventObject = {"customProperty": "propertyValue"}
BMSAnalytics.log(eventObject)
```
{: codeblock}

**Remarque :** Lorsque vous développez des applications Cordova, utilisez l'API native pour activer l'enregistrement des événements de leur cycle de vie.
  
## Activation, configuration et utilisation du journal d'événements
{: #app-monitoring-logger}

Le logiciel SDK du client {{site.data.keyword.mobileanalytics_full}} fournit une infrastructure de journalisation similaire à d'autres infrastructures que vous pouvez connaître, telles que `java.util.logging` ou `log4j`. L'infrastructure de journalisation prend en charge plusieurs instances de journal d'événements par module, différents niveaux de journalisation, la capture de traces de pile pour une panne d'application, etc.

Vous pouvez également configurer les données journalisées à stocker sur le périphérique sur lequel l'application s'exécute et envoyer ultérieurement ces journaux de périphérique au service {{site.data.keyword.mobileanalytics_short}}.

<!-- Initialization has to happen first to be able to collect logs and send them to the {{site.data.keyword.mobileanalytics_short}} service. -->

L'infrastructure de journalisation du logiciel SDK du client {{site.data.keyword.mobileanalytics_short}} prend en charge les niveaux de journalisation suivants, répertoriés du moins prolixe au plus prolixe et accompagnés de recommandations d'utilisation :

  * `FATAL` : Pour les pannes ou les blocages irrémédiables. Le niveau `FATAL` est réservé aux erreurs irrémédiables de journalisation, qui se matérialisent pour l'utilisateur sous la forme d'une panne de l'application.
  * `ERROR` : Pour les exceptions inattendues ou les erreurs de protocole de réseau inattendues.
  * `WARN` : Pour journaliser des avertissements d'utilisation qui ne sont pas considérés comme des erreurs critiques, par exemple, l'utilisation d'API obsolètes ou un ralentissement des réponses du réseau.
  * `INFO` : Pour communiquer des événements d'initialisation et d'autres données qui peuvent être importants, mais non urgents.
  * `DEBUG` : Pour communiquer des informations de débogage permettant aux développeurs de résoudre les défauts de l'application.


### Scénario de niveau de journalisation
{: #log-level-scenario notoc}

Lorsque le niveau du journal d'événements a pour valeur `FATAL`, ce dernier capture les exceptions non interceptées, mais pas les journaux qui produisent l'événement de panne. Vous pouvez définir un niveau de journal plus prolixe, de sorte que les journaux susceptibles de produire une entrée `FATAL`, telle que `WARN` ou `ERROR`, soient également capturés.

Lorsque le niveau du consignateur est défini sur `DEBUG`, vous obtenez également les journaux SDK de Mobile Analytics Client, inclus lors de l'envoi des journaux.

<!-- **Note:** Find full Logger API references for each platform at [SDKs, samples, API reference](sdks-samples-apis.html). The Logger API is part of the--> <!--{{site.data.keyword.mobileanalytics_short}} Client SDK Core. -->


### Exemple d'utilisation de journal d'événements
{: #sample-logger-usage notoc}

**Remarque :** assurez-vous d'avoir instrumenté votre application en vue de l'utilisation du logiciel SDK du client {{site.data.keyword.mobileanalytics_short}} avant d'utiliser l'infrastructure de journalisation.
 
Le fragment de code suivant est un exemple d'utilisation du journal d'événements :


#### Android
{: #android-logger-sample notoc}

```
// Configurez le journal d'événements de manière à sauvegarder les journaux sur le périphérique afin de pouvoir
// les envoyer ultérieurement au service Mobile Analytics
// Désactivé par défaut ; affectez la valeur true pour l'activer
Logger.storeLogs(true);

// Changez le niveau minimum de journalisation (facultatif)
// La valeur définie par défaut est Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);

// Créez deux instances de journal d'événements
// Vous pouvez créer plusieurs instances de journal pour organiser vos journaux
Logger logger1 = Logger.getLogger("logger1");
Logger logger2 = Logger.getLogger("logger2");

// Journalisez les messages avec différents niveaux
// Message Debug pour la fonction 1
// Message Info pour la fonction 2
logger1.debug("debug message");
//Le message logger1.debug n'est pas journalisé car logLevelFilter a pour valeur Info
logger2.info("info message");

// Envoyez des journaux à Mobile Analytics Service
        Logger.send(new ResponseListener() {
	@Override
            public void onSuccess(Response response) {
		// Gérez ici le succès de l'envoi du journal d'événements.
                    }

	@Override
            public void onFailure(Response response, Throwable throwable, JSONObject jsonObject) {
		// Gérez ici l'échec de l'envoi du journal d'événements.
                    }
});        
```
{: codeblock}


#### iOS - Swift
{: #ios-logger-sample-swift2 notoc}

```
// Configure Logger to save logs to the device so that they 
// can later be sent to the Mobile Analytics service
// Disabled by default; set to true to enable
Logger.isLogStorageEnabled = true

// Changez le niveau minimum de journalisation (facultatif)
// La valeur définie par défaut est LogLevel.debug
Logger.logLevelFilter = LogLevel.info

// Créez deux instances de journal d'événements
// Vous pouvez créer plusieurs instances de journal pour organiser vos journaux
let logger1 = Logger.logger(name: "feature1Logger")
let logger2 = Logger.logger(name: "feature2Logger")

// Journalisez les messages avec différents niveaux
logger1.debug(message: "debug message for feature 1") 
// Le message logger1.debug n'est pas journalisé car
//logLevelFilter a pour valeur info
logger2.info(message: "info message for feature 2")

// Envoyez des journaux à Mobile Analytics Service
Logger.send(completionHandler: { (response: Response?, error: Error?) dans
    
    if let response = response {
        logger.debug(message: "Status code: \(response.statusCode)")
        logger.debug(message: "Response: \(response.responseText)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
})
```
{: codeblock}

**Astuce :** pour des raisons de confidentialité, vous pouvez désactiver la génération de la sortie du journal d'événements pour les applications créées en mode édition. Par défaut, la classe du journal d'événements imprime les journaux sur la console Xcode. Dans les paramètres de création de votre cible, ajoutez un indicateur `-D RELEASE_BUILD` à la section **Other Swift Flags** de la configuration de création d'édition.
    

#### Cordova
{: #enable-logger-sample-cordova notoc}

```
// Enable persisting logs
  BMSLogger.storeLogs(true);

// Set the minimum log level to be printed and persisted
  BMSLogger.setLogLevel(BMSLogger.INFO);

var logger1 = BMSLogger.getLogger("logger1");
  var logger2 = BMSLogger.getLogger("logger2");   

// Log messages with different levels
  logger1.debug ("debug message");
  logger2.info ("info message");

// Send persisted logs to the {{site.data.keyword.mobileanalytics_short}} Service
  BMSLogger.send();
  BMSAnalytics.send();
```
{: codeblock}


<!--## Enabling the {{site.data.keyword.mobileanalytics_short}} Client SDK internal logs
{: #enable-logger-sdklogs notoc}

The {{site.data.keyword.mobileanalytics_short}} Client SDK provides a better development experience by not unnecessarily increasing the console output with its internal debug messages. Therefore, by default, internal log messages that are produced by the {{site.data.keyword.mobileanalytics_short}} SDK with the DEBUG level are not printed. You can enable printing of all internal log messages of the {{site.data.keyword.mobileanalytics_short}} Client SDK with the following API:

#### Android
{: #enable-logger-print-android notoc}

```
{: codeblock}
Logger.setSDKDebugLoggingEnabled(true);
```
{: codeblock}

#### iOS - Swift
{: #enable-logger-print-swift notoc}

```
Logger.sdkDebugLoggingEnabled = true
```
{: codeblock}
-->

## Soumission d'une demande réseau
{: #network-requests}

Vous pouvez configurer le SDK client de {{site.data.keyword.mobileanalytics_short}} pour [effectuer une demande réseau](/docs/mobile/sdk_network_request.html). Vérifiez que vous avez bien initialisé et configuré `BMSClient` et `BMSAnalytics` et importé les SDK client.

<!--
#### Android
{: #android-network-requests notoc}

**Note:** This code snippet assumes that you have [imported the Client SDKs](#android-import).

```
public void makeGetCall(){
    Thread thread = new Thread(new Runnable() {
        @Override
        public void run() {
            try  {
                Request request = new Request("http://httpbin.org/get", "GET");
                    request.send(null, null);
            } catch (Exception e) {
                // Handle failure here.
            }
        }
    });
    thread.start();
}
```
{: codeblock}

-->

<!-- 
#### Swift 3.0
{: #ios-network-requests notoc}

 ```Swift
 	// Make a network request
	let customResourceURL = "<your resource URL>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
   	if error == nil {
       	    print ("response:\(response?.responseText), no error")
    	  } else {
       	    print ("error: \(error)")
    	}
	}
	request.send(completionHandler: callBack)
 ```
 {: codeblock}
 
 -->

<!-- Commenting out bmsurlsession
```
// Make a network request
let urlSession = BMSURLSession(configuration: .default, delegate: nil, delegateQueue: nil)
var request = URLRequest(url: URL(string: "http://httpbin.org/get")!)
request.httpMethod = "GET"
request.allHTTPHeaderFields = ["foo":"bar"]

urlSession.dataTask(with: request) { (data: Data?, response: URLResponse?, error: Error?) in
    if let httpResponse = response as? HTTPURLResponse {
        logger.info(message: "Status code: \(httpResponse.statusCode)")
    }
    if data != nil, let responseString = String(data: data!, encoding: .utf8) {
        logger.info(message: "Response data: \(responseString)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
}.resume()
```
{: codeblock}
-->

<!--
#### Swift 2.2
{: ios-swift22-network-requests}

```Swift
 	// Make a network request
	let customResourceURL = "<your resource URL>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: NSError?) in
   	if error == nil {
       	    print ("response:\(response?.responseText), no error")
    	  } else {
       	    print ("error: \(error)")
    	}
	}
	request.send(completionHandler: callBack)
 ```
 {: codeblock}
-->
<!--
```
// Make a network request
let urlSession = BMSURLSession(configuration: .defaultSessionConfiguration(), delegate: nil, delegateQueue: nil)
let request = NSMutableURLRequest(URL: NSURL(string: "http://httpbin.org/get")!)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = ["foo":"bar"]

urlSession.dataTaskWithRequest(request) { (data: NSData?, response: NSURLResponse?, error: NSError?) in
    if let httpResponse = response as? NSHTTPURLResponse {
        logger.info(message: "Status code: \(httpResponse.statusCode)")
    }
    if data != nil, let responseString = NSString(data: data!, encoding: NSUTF8StringEncoding) {
        logger.info(message: "Response data: \(responseString)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
}.resume()
```
{: codeblock}
-->
<!--
#### Cordova
{: #cordova-network-requests notoc}

```
var success = function(data){
     console.log("success", data);
 }
 var failure = function(error)
     {console.log("failure", error);
 }
 var request = new BMSRequest("<your application route>", BMSRequest.GET);
 request.send(success, failure);
```
{: codeblock}

-->


## Génération de rapports relatifs à l'analyse des pannes
{: #report-crash-analytics}

Vous pouvez visualiser les [données de panne d'application](app-monitoring.html#monitor-app-crash) en envoyant des informations d'analyse et de journal à {{site.data.keyword.mobileanalytics_short}}.

La méthode `Analytics.send()` remplit les tableaux **Vue d'ensemble des pannes** et **Pannes** de la page **Pannes**. Les graphiques de cette section sont activés à l'aide du processus d'initialisation et d'envoi des analyses ; aucune configuration spéciale n'est requise.

La méthode `Logger.send()` remplit les tableaux **Récapitulatif des pannes** et **Détails des pannes** de la page **Traitement des incidents**. Vous devez activer votre application pour le stockage et l'envoi de journaux dans le but de remplir les graphiques dans cette section, en ajoutant une instruction supplémentaire dans votre code d'application.


### Android
{: #android-crash-statement notoc}

* `Logger.storeLogs(true);`
<!-- * `Logger.setLogLevel(Logger.LEVEL.FATAL); // or greater` -->

Voir [Exemple d'utilisation de journal d'événements](sdk.html#android-logger-sample)


### iOS
{: #ios-crash-statement notoc}

* `Logger.isLogStorageEnabled = true`
<!-- * `Logger.logLevelFilter = LogLevel.Fatal // or greater` -->

Voir [Exemple d'utilisation de journal d'événements](sdk.html##ios-logger-sample-swift2)


### Cordova
{: #cordova-crash-statement notoc}

* `BMSLogger.storeLogs(true);`
<!-- * `Logger.logLevelFilter = LogLevel.Fatal // or greater` -->

Voir [Exemple d'utilisation de journal d'événements](sdk.html##ios-logger-sample-swift2)


## Suivi des utilisateurs actifs
{: #trackingusers}

Si votre application peut reconnaître des utilisateurs uniques sur un périphérique, vous pouvez éventuellement suivre le nombre d'utilisateurs qui utilisent activement votre application en communiquant le nom de l'utilisateur actif à {{site.data.keyword.mobileanalytics_short}}. 

Activez le suivi des utilisateurs en initialisant {{site.data.keyword.mobileanalytics_short}} avec `hasUserContext=true`. Sinon, {{site.data.keyword.mobileanalytics_short}} ne capture qu'un seul utilisateur par périphérique. 


### Android
{: #android-tracking-users notoc}

Ajoutez le code suivant pour savoir à quel moment l'utilisateur se connecte :

```
Analytics.setUserIdentity("username");
```
{: codeblock}

<!--Add the following code for when the user logs out:

```
Analytics.clearUserIdentity();
```
{: codeblock}
-->

### iOS - Swift
{: #ios-tracking-users notoc}

Ajoutez le code suivant pour savoir à quel moment l'utilisateur se connecte :

```
Analytics.userIdentity = "username"
```
{: codeblock}

<!--
Add the following code for when the user logs out:

```
Analytics.userIdentity = nil
```
{: codeblock}
-->


### Cordova
{: #cordova-tracking-users notoc}

Ajoutez le code suivant pour savoir à quel moment l'utilisateur se connecte :

```
BMSAnalytics.setUserIdentity("username");
```
{: codeblock}


<!--## Configuring MobileFirst Platform Foundation servers to use the {{site.data.keyword.mobileanalytics_short}} service (optional)
{: #configmfp notoc}
  If you are using MobileFirst Platform Foundation Server V7 and higher, you can configure it to use the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} service to store analytics and logged data. 
  
  Configure MobileFirst Platform V7.0, V7.1, and V8.0 Beta servers to send analytics data to the {{site.data.keyword.mobileanalytics_short}} service on {{site.data.keyword.Bluemix_notm}}.

  1. Visit the dashboard for the {{site.data.keyword.mobileanalytics_short}} service where you want to send analytics data and note the browser URL for the dashboard.
  2. Determine the value for reporting analytics, as follows:
  	1. Get the {{site.data.keyword.mobileanalytics_short}} service route from the dashboard URL. The {{site.data.keyword.mobileanalytics_short}} service route is the part of the URL before ``/analytics/console/dashboard``.  

  		For example, if the dashboard URL is: `http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde`
      {: screen}

  		then the Analytics Service Route is
      `http://mobile-analytics-dashboard.ng.bluemix.net`
      {: screen}

  	2. Get the [Client API Key](#analytics-clientkey) value from the Analytics dashboard.

  	You will use the {{site.data.keyword.mobileanalytics_short}} service route and API Key to construct a URL to report analytics data, depending on the version of your MobileFirst Platform server. -->

<!--  3. Copy the URL for your {{site.data.keyword.mobileanalytics_short}} service dashboard. Include the `instanceId` query parameter, for example:
      `http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=1212345abcde`
      {: screen}

  4. Configure the values for the MobileFirst Platform server JNDI properties, as follows:-->

<!--    ### MobileFirst Platform V7.0
    {: #mfp70 notoc}

        The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/data?tenant=<Client API Key>`
        {: screen}

        The `wl.analytics.console.url` JNDI property is the Analytics service dashboard URL.

        #### Example of MobileFirst Platform V7.0 JNDI property values
        {: #example-mfp70-jndi-values notoc}

        For a MobileFirst Platform project named `Myproj7000`, based on the examples in steps 2 and 3, replace the current JNDI property values in the `server.xml` file with:
        ```
        <jndiEntry jndiName="MyProj7000/wl.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data?tenant=12345abcde"'/>
        ```
        {: screen}
        ```
        <jndiEntry jndiName="MyProj7000/wl.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
        ```
        {: screen}

    ### MobileFirst Platform V7.1
    {: #mfp71 notoc}

      The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/v2/<Client API Key>`
      {: screen}

      #### Example of MobileFirst Platform JNDI V7.1 property values
      {: #example-mfp71-jndi-values notoc}

      For a MobileFirst Platform project named `MyProj7101`, replace the current JNDI property values in the `server.xml` file with:
      ```
      <jndiEntry jndiName="MyProj7101/wl.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/v2/data?tenant=12345abcde"'/>
      ```
      {: screen}
      ```
      <jndiEntry jndiName="MyProj7101/wl.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
      ```
      {: screen}

      ### MobileFirst Platform V8.0
      {: #mfp80 notoc}

      The format of the `mfp.analytics.url` JNDI property is:
      `<Analytics Service Route>/analytics-service/rest/v2/<Client API Key>`  

    #### Example MobileFirst Platform V8.0 Beta JNDI property values
      {: example-mfp80b-jndi-values}

      For a MobileFirst Platform project named `mfp`, which is the default, replace the current JNDI property values in the `server.xml` file with:
      ```
      <jndiEntry jndiName="mfp/mfp.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data?tenant=12345abcde"'/>
      ```
      {: screen}
      ```
      <jndiEntry jndiName="mfp/mfp.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
      ```
      {: screen}
-->
<!-- #### Ignored events and event retention
{: #ignored-events notoc}
The {{site.data.keyword.mobileanalytics_short}} service saves the following data for ignored events and event retention:
  
<dl>	
<dt>Ignored events</dt>
	<dd>`ANALYTICS_SDK_CFG_IGNORE_AppPushAction: true`
		  `ANALYTICS_SDK_CFG_IGNORE_ServerLog: true`
		  `ANALYTICS_SDK_CFG_IGNORE_NetworkTransaction: true`
		  `ANALYTICS_SDK_CFG_IGNORE_NetworkTransactionSummarizedHourly: true`
		  `ANALYTICS_SDK_CFG_IGNORE_PushNotification: true`
		  `ANALYTICS_SDK_CFG_IGNORE_PushSubscription: true`</dd>
</dt>
<dt>Event retention</dd>
<dd>
`ANALYTICS_TTL_AlertNotification: 14d`<br>
`ANALYTICS_TTL_CustomData: 7d`<br>
`ANALYTICS_TTL_Device: 90d`<br>
`ANALYTICS_TTL_AppLog: 3d`<br>
`ANALYTICS_TTL_AppSession: 7d`
</dd>
</dt>
</dl>
  
-->


## Opération suivante
{: #what-to-do-next notoc}

Vous pouvez à présent accéder à la console {{site.data.keyword.mobileanalytics_short}} pour voir les analyses d'utilisation, telles que les nouveaux périphériques et le nombre total de périphériques qui utilisent l'application. Vous pouvez également surveiller votre application en <!--[creating custom charts](app-monitoring.html#custom-charts),-->[définissant des alertes](app-monitoring.html#alerts) et en [surveillant les pannes d'application](app-monitoring.html#monitor-app-crash).


# Liens connexes
{: #rellinks notoc}

## Référence d'API
{: #api notoc}

* [API REST ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
