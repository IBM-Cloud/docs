---

Copyright :
  Années : 2015, 2016

---

# Instrumentation de votre application pour utiliser les logiciels SDK du client {{site.data.keyword.mobileanalytics_short}}
{: #mobileanalytics_sdk}
*Dernière mise à jour : 27 avril 2016*
{: .last-updated}

Les logiciels SDK de {{site.data.keyword.mobileanalytics_full}} vous permettent d'instrumenter votre application mobile.
{: shortdesc}

{{site.data.keyword.mobileanalytics_short}} vous permet de collecter trois catégories de données, et chacune d'elles nécessite un degré d'instrumentation qui lui est propre :

1.  Données prédéfinies - Cette catégorie inclut des informations sur les périphériques et l'utilisation générique qui s'appliquent à toutes les applications. Cette catégorie comprend les métadonnées de périphérique (système d'exploitation et modèle de périphérique) et les données d'utilisation (utilisateurs actifs et sessions d'application) qui indiquent le volume, la fréquence ou la durée d'utilisation d'une application. Les données prédéfinies sont collectées automatiquement après que vous avez initialisé le logiciel SDK de {{site.data.keyword.mobileanalytics_short}} dans votre application.
2. Evénements personnalisés - Cette catégorie inclut des données que vous définissez vous-même et qui sont propres à votre application. Ces données représentent des événements qui se produisent dans votre application, comme le fait de consulter des pages, de cliquer sur des boutons ou d'effectuer un achat dans l'application. En plus d'initialiser le logiciel SDK de {{site.data.keyword.mobileanalytics_short}} dans votre application, vous devez ajouter une ligne de code pour chaque événement personnalisé que vous souhaitez suivre.
3. Messages de journal client - Cette catégorie permet au développeur d'ajouter des lignes de code dans l'application afin de journaliser des messages personnalisés destinés à faciliter le développement et le débogage. Le développeur affecte un niveau de gravité/détail à chaque message de journal et peut ensuite filtrer les messages en fonction du niveau affecté ou économiser de l'espace de stockage en configurant l'application de telle sorte qu'elle ignore les messages dont le niveau de gravité/détail est inférieur au niveau de journalisation spécifié. Pour collecter des données de journal client, vous devez initialiser le logiciel SDK de {{site.data.keyword.mobileanalytics_short}} dans votre application, mais également ajouter une ligne de code pour chaque message de journal.

Actuellement, les logiciels SDK sont disponibles pour Android, iOS et WatchOS.

## Identification de la valeur de clé de votre client
{: #analytics-clientkey}

Identifiez la valeur de **clé de votre client** avant de configurer le logiciel SDK du client. La clé du client est requise pour initialiser le logiciel SDK du client.
1. Ouvrez votre tableau de bord de service {{site.data.keyword.mobileanalytics_short}}.
2. Cliquez sur l'icône en forme de clé pour ouvrir l'onglet Clés d'API.
3. Dans l'onglet Clés d'API, notez la valeur de clé du client.


## Initialisation de votre application Android pour la collecte d'analyses
{: #initalize-ma-sdk-android}

Initialisez votre application pour qu'elle envoie des journaux au service {{site.data.keyword.mobileanalytics_short}}.

1. Importez le logiciel SDK du client en ajoutant l'instruction `import` suivante au début de votre fichier de projet :

  ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
  ```
  {: codeblock}

2. Initialisez le logiciel SDK de {{site.data.keyword.mobileanalytics_short}} dans votre application Android en ajoutant le code d'initialisation dans la méthode `onCreate` de l'activité principale de votre application Android ou à l'emplacement le plus approprié pour votre projet.

	```Java
	try {
            BMSClient.getInstance().initialize(this.getApplicationContext(), "", "", BMSClient.REGION_US_SOUTH); // Prenez soin de pointer vers votre région
        } catch (MalformedURLException e) {
            Log.e(your_app_name,"URL should not be malformed:  " + e.getLocalizedMessage());
        } 
  ```
  {: codeblock}

  Pour utiliser le logiciel SDK du client {{site.data.keyword.mobileanalytics_short}}, vous devez d'abord initialiser la classe `BMSClient` à l'aide du paramètre **bluemixRegion**. Dans l'initialiseur, la valeur **bluemixRegion** vous permet de spécifier le déploiement {{site.data.keyword.Bluemix_notm}} que vous utilisez, par exemple, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` ou `BMSClient.REGION_SYDNEY`.
  <!-- Set this value with a `BMSClient.REGION` static property. -->

  <!--You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. Initialisez Analytics en utilisant votre objet d'application Android et en lui attribuant le nom de votre application. Vous avez également besoin de la valeur de [**clé du client**](#analytics-clientkey).
	
	```Java
	Analytics.init(getApplication(), "my_app", apiKey, Analytics.DeviceEvent.LIFECYCLE);
	// Dans cet exemple de code, Analytics est configuré pour enregistrer les événements de cycle de vie.
	```
  {: codeblock}

	**Astuce :** Le nom d'application est utilisé pour filtrer la recherche de journaux client dans le tableau de bord. Lorsque vous utilisez le même nom d'application sur plusieurs plateformes (par exemple, Android et iOS), tous les journaux issus de cette application s'affichent sous le même nom, quelle que soit la plateforme à partir de laquelle ils ont été envoyés.

## Initialisation de votre application iOS pour la collecte d'analyses
{: #init-ma-sdk-ios}

Initialisez votre application pour qu'elle envoie des journaux au service {{site.data.keyword.mobileanalytics_short}}. Le logiciel SDK de Swift est disponible pour iOS et watchOS.

1. Importez les infrastructures `BMSCore` et `BMSAnalytics` en ajoutant les instructions `import` suivantes au début de votre fichier de projet `AppDelegate.swift` :

  ```Swift
  import BMSCore
  import BMSAnalytics
  ```
  {: screen}

2. Pour utiliser le logiciel SDK de {{site.data.keyword.mobileanalytics_short}}, vous devez d'abord initialiser la classe `BMSClient` à l'aide du code suivant :

  Placez le code d'initialisation dans la méthode `application(_:didFinishLaunchingWithOptions:)` de votre délégué d'application ou à l'emplacement le plus approprié pour votre projet.

    ```Swift
    BMSClient.sharedInstance.initializeWithBluemixAppRoute(nil, bluemixAppGUID: nil, bluemixRegion: BMSClient.REGION_US_SOUTH)`
    ```
    {: codeblock}

    Pour utiliser le logiciel SDK du client {{site.data.keyword.mobileanalytics_short}}, vous devez d'abord initialiser la classe `BMSClient` à l'aide du paramètre **bluemixRegion**. Dans l'initialiseur, la valeur **bluemixRegion** vous permet de spécifier le déploiement {{site.data.keyword.Bluemix_notm}} que vous utilisez, par exemple, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` ou `BMSClient.REGION_SYDNEY`.
   
   <!-- Set this value with a `BMSClient.REGION` static property. -->

   <!-- You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. Initialisez Analytics en lui attribuant le nom de votre application mobile. Vous avez également besoin de la valeur de [**clé du client**](#analytics-clientkey).

  Le nom d'application est utilisé pour filtrer la recherche de journaux client dans votre tableau de bord {{site.data.keyword.mobileanalytics_short}}. Lorsque vous utilisez le même nom d'application sur plusieurs plateformes (par exemple, Android et iOS), tous les journaux issus de cette application s'affichent sous le même nom, quelle que soit la plateforme à partir de laquelle ils ont été envoyés.

  Un paramètre `deviceEvents` facultatif collecte automatiquement des analyses pour les événements de niveau périphérique.

  ### iOS
    {: #ios-initialize-analytics}

      ```
      Analytics.initializeWithAppName("AppName", apiKey: your_client_key,
      deviceEvents: DeviceEvent.LIFECYCLE)
      ```

  ### watchOS
  {: #watchos-initialize-analytics}

	```
	  Analytics.initializeWithAppName("AppName", apiKey: your_api_key)
	```

  Vous pouvez enregistrer des événements de périphérique sur WatchOS à l'aide des méthodes `Analytics.recordApplicationDidBecomeActive()` et `Analytics.recordApplicationWillResignActive()`.
  
  Ajoutez la ligne suivante à la méthode `applicationDidBecomeActive()` de la classe ExtensionDelegate :

	```
	Analytics.recordApplicationDidBecomeActive()
	```
  {: codeblock}

  Ajoutez la ligne suivante à la méthode applicationWillResignActive() de la classe ExtensionDelegate :
	```
	Analytics.recordApplicationWillResignActive()
	```
  {: codeblock}

## Collecte des données d'analyse d'utilisation
{: #app-monitoring-gathering-analytics}

  Vous pouvez configurer l'enregistrement des données d'analyse d'utilisation et leur envoi au service {{site.data.keyword.mobileanalytics_short}} par le SDK client de {{site.data.keyword.mobileanalytics_short}}.

  Utilisez les API suivantes pour démarrer l'enregistrement et l'envoi des données d'analyse d'utilisation :

#### Android
{: #android-usage-api}
	
```
// Désactivez l'enregistrement des analyses d'utilisation (par exemple, pour économiser de l'espace disque)
// L'enregistrement est activé par défaut
Analytics.disable();
	
// Activez l'enregistrement des analyses d'utilisation
Analytics.enable();
	
Analytics.log(eventJSONObject);
	
// Envoyez des analyses d'utilisation enregistrées au service Mobile Analytics
Analytics.send();
```
	
Exemple d'analyse d'utilisation pour la journalisation d'un événement :
	
```
// Journalisez un événement d'analyse personnalisé pour des graphiques personnalisés, qui est représenté par un objet JSON :
JSONObject eventJSONObject = new JSONObject();
	
eventJSONObject.put("customProperty" , "propertyValue");
```

#### iOS - Swift
{: #ios-usage-api}

```
// Désactivez l'enregistrement des analyses d'utilisation (par exemple, pour économiser de l'espace disque)
// L'enregistrement est activé par défaut
Analytics.enabled = false

// Activez l'enregistrement des analyses d'utilisation
Analytics.enabled = true

// Envoyez des analyses d'utilisation enregistrées au service {{site.data.keyword.mobileanalytics_short}}
Analytics.send()
```

Exemple d'analyse d'utilisation pour la journalisation d'un événement :

```
// Journalisez un événement d'analyse personnalisé pour des graphiques personnalisés
let eventObject = ["customProperty": "propertyValue"]
Analytics.log(eventObject)
```

  <!--Removing Cordova for experimental-->
  <!--### Cordova-->
  <!--{: #usage-analytics-cordova}-->

  <!--```JavaScript-->
  <!--// Enable usage analytics recording-->
  <!--Analytics.enable();-->

  <!--// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service-->
  <!--Analytics.send();-->
  <!--```-->
  <!--**Note:** When you are developing Cordova applications, use the native API to enable application lifecycle event recording.-->

## Activation, configuration et utilisation du journal d'événements
{: #app-monitoring-logger}

  Le logiciel SDK du client {{site.data.keyword.mobileanalytics_full}} fournit une
infrastructure de journalisation similaire à d'autres infrastructures que vous pouvez connaître, telles que `java.util.logging` ou `log4j`. L'infrastructure de journalisation prend en charge plusieurs instances de journal d'événements par module, différents niveaux de journalisation, la capture de traces de pile pour une panne d'application, etc.

  Vous pouvez également configurer les données journalisées à stocker sur le périphérique sur lequel l'application s'exécute et envoyer ultérieurement ces journaux de périphérique au service {{site.data.keyword.mobileanalytics_short}}.

  <!-- Initialization has to happen first to be able to collect logs and send them to the {{site.data.keyword.mobileanalytics_short}} service. -->

  L'infrastructure de journalisation du logiciel SDK du client {{site.data.keyword.mobileanalytics_short}} prend en charge les niveaux de journalisation suivants, répertoriés dumoins prolixe au plus prolixe et accompagnés de recommandations d'utilisation :

  * `FATAL` - Pour les pannes ou les blocages irrémédiables. Le niveau `FATAL` est réservé aux erreurs irrémédiables de journalisation, qui se matérialisent pour l'utilisateur sous la forme d'une panne de l'application.
  * `ERROR` : Pour les exceptions inattendues ou les erreurs de protocole de réseau inattendues.
  * `WARN` : Pour journaliser des avertissements d'utilisation qui ne sont pas considérés comme des erreurs critiques, par exemple, l'utilisation d'API obsolètes ou un ralentissement des réponses du réseau.
  * `INFO` : Pour communiquer des événements d'initialisation et d'autres données qui peuvent être importants, mais non urgents.
  * `DEBUG` - Pour communiquer des informations de débogage permettant aux développeurs de résoudre les défauts de l'application.

    #### Scénario de niveau de journalisation
    {: #log-level-scenario}

    Lorsque le niveau du journal d'événements a pour valeur `FATAL`, ce dernier capture les exceptions non interceptées, mais pas les journaux qui produisent l'événement de panne. Vous pouvez définir un niveau de journal plus prolixe, de sorte que les journaux susceptibles de produire une entrée `FATAL`, telle que `WARN` ou `ERROR`, soient également capturés.

  <!--**Note:** Find full Logger API references for each platform at [SDKs, samples, API reference](sdks-samples-apis.html). The Logger API is part of the--> <!--{{site.data.keyword.mobileanalytics_short}} Client SDK Core.-->

  <!--### Cordova-->


  <!--```JavaScript-->

  <!--var logger = MFPLogger.getInstance("myLogger");-->

  <!--logger.debug("debug info");-->
  <!--logger.info("info message");-->
  <!--logger.warn("warning message");-->
  <!--logger.fatal("fatal message");-->

  <!--```-->


### Exemple d'utilisation de journal d'événements
{: #sample-logger-usage}

**Remarque :** Prenez soin d'instrumenter votre application pour qu'elle utilise le [logiciel SDK du client{{site.data.keyword.mobileanalytics_short}} ](sdk.html) avant d'utiliser l'infrastructure de journalisation.
 
  Le fragment de code suivant est un exemple d'utilisation du journal d'événements :

#### Android
{: #android-logger-sample}

```
// Configurez le journal d'événements de manière à sauvegarder les journaux sur le périphérique afin de pouvoir
// les envoyer ultérieurement au service {{site.data.keyword.mobileanalytics_short}}
// Désactivé par défaut ; affectez la valeur true pour l'activer
Logger.storeLogs(true);

// Changez le niveau minimum de journalisation (facultatif)
// La valeur définie par défaut est Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);

// Envoyez des journaux au service {{site.data.keyword.mobileanalytics_short}}
Logger.send();
```

Scénarios de journal d'événements :

```
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
```

#### iOS - Swift
{: ios-logger-sample}

```
// Configurez le journal d'événements de manière à sauvegarder les journaux sur le périphérique afin de pouvoir les envoyer ultérieurement au service {{site.data.keyword.mobileanalytics_short}}
// Désactivé par défaut ; affectez la valeur true pour l'activer
Logger.logStoreEnabled = true

// Changez le niveau minimum de journalisation (facultatif)
// La valeur définie par défaut est LogLevel.Debug
Logger.logLevelFilter = LogLevel.Info

// Envoyez des journaux au service {{site.data.keyword.mobileanalytics_short}}
Logger.send()
```

Scénarios de journal d'événements :
    
```
// Créez deux instances de journal d'événements
// Vous pouvez créer plusieurs instances de journal pour organiser vos journaux
let logger1 = Logger.logger(forName: "feature1Logger")
let logger2 = Logger.logger(forName: "feature2Logger")
	
// Journalisez les messages avec différents niveaux
logger1.debug("debug message for feature 1") 
//Le message logger1.debug n'est pas journalisé car logLevelFilter a pour valeur Info
logger2.info("info message for feature 2")
```

**Astuce** : Pour des raisons de confidentialité, vous pouvez désactiver la génération de la sortie du journal d'événements pour les applications créées en mode édition. Par défaut, la classe du journal d'événements imprime les journaux sur la console Xcode. Dans les paramètres de création de votre cible, ajoutez un indicateur `-D RELEASE_BUILD` à la section **Other Swift Flags** de la configuration de création d'édition.
    

  <!-- ### Cordova-->
  <!--{: #enable-logger-sample-cordova}-->

  <!--// Enable persisting logs-->
  <!--MFPLogger.setCapture(true);-->

  <!--// Set the minimum log level to be printed and persisted-->
  <!--MFPLogger.setLevel(MFPLogger.INFO);-->

  <!--var logger1 = MFPLogger.getInstance("logger1");-->
  <!--var logger2 = MFPLogger.getInstance("logger2");   -->

  <!--// Log messages with different levels-->
  <!--logger1.debug ("debug message");-->
  <!--logger2.info ("info message");-->

  <!--// Send persisted logs to the {{site.data.keyword.mobileanalytics_short}} Service-->
  <!--```-->

<!--## Enabling the {{site.data.keyword.mobileanalytics_short}} Client SDK internal logs
{: #enable-logger-sdklogs}

  The {{site.data.keyword.mobileanalytics_short}} Client SDK provides a better development experience by not unnecessarily increasing the console output with its internal debug messages. Therefore, by default, internal log messages that are produced by the {{site.data.keyword.mobileanalytics_short}} SDK with the DEBUG level are not printed. You can enable printing of all internal log messages of the {{site.data.keyword.mobileanalytics_short}} Client SDK with the following API:

#### Android
{: #enable-logger-print-android}

```
Logger.setSDKDebugLoggingEnabled(true);
```

#### iOS - Swift
{: #enable-logger-print-swift}

```
Logger.sdkDebugLoggingEnabled = true
```
-->

## Suivi des utilisateurs actifs
{: #trackingusers}
Vous pouvez éventuellement suivre le nombre de personnes qui utilisent votre application de manière active en communiquant le nom d'utilisateur de ces utilisateurs actifs à {{site.data.keyword.mobileanalytics_short}}.

#### Android
{: #android-tracking-users}

Ajoutez le code suivant qui correspond au moment où l'utilisateur se connecte :

```
Analytics.setUserIdentity("username");
```

Ajoutez le code suivant qui correspond au moment où l'utilisateur se déconnecte :

```
Analytics.clearUserIdentity();
```

#### iOS - Swift
{: #ios-tracking-users}

Ajoutez le code suivant qui correspond au moment où l'utilisateur se connecte :

```
Analytics.userIdentity = "username"
```

Ajoutez le code suivant qui correspond au moment où l'utilisateur se déconnecte :

```
Analytics.userIdentity = nil
```

<!--## Configuring MobileFirst Platform Foundation servers to use the {{site.data.keyword.mobileanalytics_short}} service (optional)
{: #configmfp}
  If you are using MobileFirst Platform Foundation Server V7 and higher, you can configure it to use the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} service to store analytics and logged data. 
  
  Configure MobileFirst Platform V7.0, V7.1, and V8.0 Beta servers to send analytics data to the {{site.data.keyword.mobileanalytics_short}} service on {{site.data.keyword.Bluemix_notm}}.

  1. Visit the dashboard for the {{site.data.keyword.mobileanalytics_short}} service where you want to send analytics data and note the browser URL for the dashboard.
  2. Determine the value for reporting analytics, as follows:
  	1. Get the {{site.data.keyword.mobileanalytics_short}} service route from the dashboard URL. The {{site.data.keyword.mobileanalytics_short}} service route is the part of the URL before `/analytics/console/dashboard`.  

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
    {: #mfp70}

        The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/data?tenant=<Client API Key>`
        {: screen}

        The `wl.analytics.console.url` JNDI property is the Analytics service dashboard URL.

        #### Example of MobileFirst Platform V7.0 JNDI property values
        {: #example-mfp70-jndi-values}

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
    {: #mfp71}

      The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/v2/<Client API Key>`
      {: screen}

      #### Example of MobileFirst Platform JNDI V7.1 property values
      {: #example-mfp71-jndi-values}

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
      {: #mfp80}

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
{: #ignored-events}
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

# rellinks

## Référence pour l'API
{: #api}
* [API REST](https://mobile-analytics-dashboard.eu-gb.bluemix.net/analytics-service/){:new_window}
