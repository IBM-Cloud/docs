---

copyright:
  years: 2016
lastupdated: "2016-11-30"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Initiation à {{site.data.keyword.mobileanalytics_short}} (Bêta)

{: #gettingstartedtemplate}

{{site.data.keyword.mobileanalytics_full}} fournit aux développeurs, aux administrateurs informatiques et aux parties prenantes des informations relatives aux performances et à l'utilisation de leurs applications mobiles. Vous pouvez surveiller les performances et l'utilisation de toutes vos applications depuis votre bureau ou votre tablette. Vous pouvez identifier rapidement les tendances et les anomalies, accéder aux détails pour résoudre les problèmes et déclencher des alertes lorsque des mesures clés dépassent des seuils critiques. 
{: shortdesc}

Pour être rapidement opérationnel avec le service {{site.data.keyword.mobileanalytics_short}}, procédez comme suit :

1. Après avoir créé une instance
<!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->du service
{{site.data.keyword.mobileanalytics_short}}, vous pouvez accéder à la console de {{site.data.keyword.mobileanalytics_short}}
en cliquant sur votre vignette dans la section **Services** du tableau de bord {{site.data.keyword.Bluemix}}.

 Le service {{site.data.keyword.mobileanalytics_short}} se lance avec le **mode démo** activé. Ce mode remplit des graphiques sur les pages **Données d'application** et **Alertes**, ce qui vous permet de voir de quelle façon vos données seront affichées. Vous pouvez désactiver le mode démo lorsque vous possédez vos propres données. La console {{site.data.keyword.mobileanalytics_short}} est accessible en lecture seule lorsque le mode démo est activé, et vous ne pouvez pas créer de nouvelles définitions d'alerte.

2. Installez les [logiciels SDK du client](/docs/services/mobileanalytics/install-client-sdk.html) {{site.data.keyword.mobileanalytics_short}}. Si vous le
souhaitez, vous pouvez utiliser l'[API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window} de {{site.data.keyword.mobileanalytics_short}}.

3. Importez les SDK client et initialisez-les avec le fragment de code suivant pour enregistrer les analyses de l'utilisation :

	#### Android
	{: #android-import}

	Ajoutez les instructions `import` suivantes au début de votre fichier de projet :
	
    ```
    import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
    ```
    {: codeblock}
  
 #### iOS
 {: #ios-import}
	
 **Remarque :** Le logiciel SDK de Swift est disponible pour iOS et watchOS.
	
 Importez les infrastructures `BMSCore` et `BMSAnalytics` en ajoutant les instructions `import` suivantes au début de votre fichier de projet `AppDelegate.swift` :

   ```Swift
  import BMSCore
  import BMSAnalytics
   ```
   {: codeblock}  
   
 #### Cordova
 {: #cordova-import}
		
 Ajoutez le plug-in Cordova en exécutant la commande suivante depuis le répertoire racine de votre application Cordova :

 ```Javascript
 cordova plugin add bms-core
 ```
 {: codeblock}  

4. Initialisez le SDK client {{site.data.keyword.mobileanalytics_short}} dans votre code d'application pour enregistrer les analyses de
l'utilisation et les sessions d'application, en utilisant la valeur de votre [Clé d'API](/docs/services/mobileanalytics/sdk.html#analytics-clientkey).	
	
 #### Android
 {: #android-initialize}	

  ```
  BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // You can change the region
  Analytics.init(getApplication(), "your_app_name_here", "your_api_key_here", hasUserContext, Analytics.DeviceEvent.ALL);
  ```
  {: codeblock}
    
 Le paramètre **bluemixRegion** spécifique le déploiement {{site.data.keyword.Bluemix_notm}} que vous utilisez, par exemple, `BMSClient.REGION_US_SOUTH` et `BMSClient.REGION_UK`. 
    <!-- , or `BMSClient.Region.Sydney`.-->

 #### iOS
 {: #ios-initialize}
  
  Initialisez le logiciel SDK du client dans votre code d'application pour enregistrer les analyses d'utilisation et les sessions d'application
avec votre valeur de [clé d'API](/docs/services/mobileanalytics/sdk.html#analytics-clientkey).
	
  ```Swift
		BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // You can change the region
		Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: deviceEvents: .lifecycle, .network)
  ```
  {: codeblock}
			
   Le paramètre **bluemixRegion** spécifie le déploiement Bluemix que vous utilisez, par exemple `BMSClient.Region.usSouth` ou `BMSClient.Region.unitedKingdom`.
	<!-- , or `BMSClient.REGION_SYDNEY`. -->
	
 #### Cordova
 {: #cordova-initialize}
	
 Initialisez le logiciel SDK du client dans votre code d'application pour enregistrer les analyses d'utilisation et les sessions d'application
avec votre valeur de [clé d'API](/docs/services/mobileanalytics/sdk.html#analytics-clientkey).
	
  ```
  var appName = "your_app_name_here";
  var apiKey = "your_api_key_here";
	
  BMSClient.initialize(BMSClient.REGION_US_SOUTH); // You can change the region
  BMSAnalytics.initialize(appName, apiKey, false, [BMSAnalytics.ALL])
  ```
  {: codeblock}
  
  Le paramètre **bluemixRegion** spécifique le déploiement {{site.data.keyword.Bluemix_notm}} que vous utilisez, par exemple, `BMSClient.REGION_US_SOUTH` et `BMSClient.REGION_UK`.
  
 **Remarque :** le nom que vous sélectionnez pour votre application (`your_app_name_here`)
est affiché dans la console {{site.data.keyword.mobileanalytics_short}} en tant que nom de l'application. Le nom d'application est utilisé pour filtrer la recherche des journaux d'application dans votre tableau de bord. Lorsque vous utilisez le même nom d'application sur plusieurs plateformes (par exemple, Android et iOS), tous les journaux issus de cette application s'affichent sous le même nom, quelle que soit la plateforme à partir de laquelle ils ont été envoyés.

5. Envoyez des analyses d'utilisation enregistrées au service Mobile Analytics. Une méthode simple pour tester votre analyse consiste à exécuter le code suivant au démarrage de l'application :

	#### Android
	{: #android-send}

	Utilisez la méthode `Analytics.send()` pour envoyer des données d'analyse au serveur. Vous pouvez placer la méthode `Analytics.send()` n'importe où dans la méthode `onCreate` de l'activité principale de votre application Android ou à l'emplacement le plus approprié pour votre projet. 
	
	Vous pouvez insérer `Analytics.send()` n'importe où.

	```
	Analytics.send();
	```
	{: codeblock}

	#### iOS
	{: #ios-send}

	Utilisez la méthode `Analytics.send` pour envoyer des données d'analyse au serveur. Vous pouvez placer la méthode `Analytics.send` n'importe où dans la méthode `application(_:didFinishLaunchingWithOptions:)` de votre délégué d'application ou à l'emplacement le plus approprié pour votre projet. 

	```
	Analytics.send()
	```
	{: codeblock}
	
	#### Cordova
	{: #cordova-send}
	
	Utilisez la méthode `BMSAnalytics.send` pour envoyer des données d'analyse au serveur. Placez la méthode `BMSAnalytics.send` dans le meilleur emplacement pour votre projet.
	
	```
	BMSAnalytics.send
	```
	{: codeblock}
	
	Lisez la rubrique [Instrumentation de votre application](/docs/services/mobileanalytics/sdk.html) pour connaître les fonctionnalités {{site.data.keyword.mobileanalytics_short}} supplémentaires, telles que la [consignation ](/docs/services/mobileanalytics/sdk.html#app-monitoring-logger), les [demandes de réseau](/docs/services/mobileanalytics/sdk.html#network-requests) et l'[analyse des pannes](/docs/services/mobileanalytics/sdk.html#report-crash-analytics).
	
6. Compilez et exécutez l'application sur votre émulateur ou périphérique.

7. Accédez à la console {{site.data.keyword.mobileanalytics_short}} pour voir l'analyse de l'utilisation de votre application. Vous pouvez également surveiller votre application en <!--[creating custom charts](app-monitoring.html#custom-charts),-->[définissant des alertes](/docs/services/mobileanalytics/app-monitoring.html#alerts) et en [surveillant les pannes d'application](/docs/services/mobileanalytics/app-monitoring.html#monitor-app-crash).


# rellinks

## Logiciel SDK
* [Logiciel SDK Android](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [Logiciel SDK iOS](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
* [Logiciel SDK de base du plug-in Cordova](https://www.npmjs.com/package/bms-core){: new_window}

## Référence d'API
{: #api}
* [API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
