---

copyright:
  years: 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Initiation à {{site.data.keyword.mobileanalytics_short}} (bêta)  

{: #gettingstartedtemplate}
*Dernière mise à jour : 17 mai 2016*
{: .last-updated}

Utilisez le service {{site.data.keyword.mobileanalytics_full}} pour mesurer l'état, le comportement et le contexte de vos applications mobiles, utilisateurs mobiles et périphériques mobiles.
{: shortdesc}

Pour être rapidement opérationnel avec le service {{site.data.keyword.mobileanalytics_short}}, procédez comme suit :

1. Après avoir [créé une instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance) du service {{site.data.keyword.mobileanalytics_short}}, vous pouvez accéder à la console {{site.data.keyword.mobileanalytics_short}} en cliquant sur la vignette dans la section Services du tableau de bord {{site.data.keyword.Bluemix}}.

  **Important :** Lorsque vous ouvrez pour la première fois le service Mobile Analytics que vous venez de créer, une fenêtre s'affiche pour vous permettre de confirmer que vous autorisez {{site.data.keyword.Bluemix_notm}} à fournir au service les informations nécessaires vous concernant, de sorte que ce dernier puisse valider votre identité. Cliquez sur **Confirmer** pour passer à la console {{site.data.keyword.mobileanalytics_short}}. Si vous annulez l'opération, la console {{site.data.keyword.mobileanalytics_short}} ne s'ouvre pas.

2. Installez les [logiciels SDK du client](install-client-sdk.html) {{site.data.keyword.mobileanalytics_short}}.

3. Importez les logiciels SDK du client et initialisez-les à l'aide du fragment de code suivant pour enregistrer les analyses d'utilisation.

	#### Android
	{: #android-initialize}
	1. Importez le logiciel SDK du client :

		```
		import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
		import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
		```
	2. Initialisez le logiciel SDK du client au sein de votre code d'application pour enregistrer les analyses d'utilisation et les sessions d'application, à l'aide de la valeur de [clé du client](sdk.html#analytics-clientkey).

		```Java
			try {
			     BMSClient.getInstance().initialize(this.getApplicationContext(), "", "", BMSClient.REGION_US_SOUTH);
			}
			catch (MalformedURLException e) {
	            //The Bluemix region provided is invalid
	        }
				Analytics.init(getApplication(), your_app_name, your_client_key, Analytics.DeviceEvent.LIFECYCLE);
		```
    Le paramètre **bluemixRegion** vous permet de spécifier le déploiement Bluemix que vous utilisez, par exemple, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` ou `BMSClient.REGION_SYDNEY`.

  #### iOS
  {: #ios-initialize}
  1. Importez les infrastructures `BMSCore` et `BMSAnalytics` :
  ```
    import BMSCore
    import BMSAnalytics
    ```
  2. Initialisez le logiciel SDK du client au sein de votre code d'application pour enregistrer les analyses d'utilisation et les sessions d'application, à l'aide de la valeur de [clé du client](sdk.html#analytics-clientkey).
 
	```Swift
	BMSClient.sharedInstance.initializeWithBluemixAppRoute(nil, bluemixAppGUID: nil, bluemixRegion: BMSClient.REGION_US_SOUTH) //You can change the region
	Analytics.initializeWithAppName(your_app_name, apiKey: your_client_key, deviceEvents: DeviceEvent.LIFECYCLE)
	```
  Le paramètre **bluemixRegion** vous permet de spécifier le déploiement Bluemix que vous utilisez, par exemple, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` ou `BMSClient.REGION_SYDNEY`.

4. Envoyez des analyses d'utilisation enregistrées au service Mobile Analytics. Une méthode simple pour tester votre analyse consiste à exécuter le code suivant au démarrage de l'application :

	#### Android
	{: #android-send}

	Vous pouvez ajouter la méthode `Analytics.send()` dans la méthode `onCreate` de l'activité principale de votre application Android ou à l'emplacement le plus approprié pour votre projet.

	```
	Analytics.send();
	```

	#### iOS
	{: #ios-send}

	Utilisez la méthode `Analytics.send` pour envoyer des données d'analyse au serveur. Placez la méthode `Analytics.send` dans la méthode `application(_:didFinishLaunchingWithOptions:)` de votre délégué d'application ou à l'emplacement le plus approprié pour votre projet.

	```
	Analytics.send()
	```

	Reportez-vous à la rubrique [Instrumentation de votre application](sdk.html).
5. Compilez et exécutez l'application sur votre émulateur ou périphérique.

6. Accédez au **tableau de bord** {{site.data.keyword.mobileanalytics_short}} pour voir les analyses d'utilisation, telles que les nouveaux périphériques et le nombre total de périphériques qui utilisent l'application. Vous pouvez également surveiller votre application en [créant des graphiques personnalisés](app-monitoring.html#custom-charts), [définissant des alertes](app-monitoring.html#alerts) et en [surveillant des pannes d'application](app-monitoring.html#monitor-app-crash).


# rellinks

## Logiciel SDK
* [Logiciel SDK Android](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [Logiciel SDK iOS](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
