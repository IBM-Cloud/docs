---

copyright:
  years: 2016
lastupdated: "2016-10-19"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Initiation à {{site.data.keyword.mobileanalytics_short}}
{: #gettingstartedtemplate}


Dernière mise à jour : 19 octobre 2016
{: .last-updated}

{{site.data.keyword.mobileanalytics_full}} fournit aux développeurs, aux administrateurs informatiques et aux parties prenantes des informations relatives aux performances et à l'utilisation de leurs applications mobiles. Vous pouvez surveiller les performances et l'utilisation de toutes vos applications depuis votre bureau ou votre tablette. Vous pouvez identifier rapidement les tendances et les anomalies, accéder aux détails pour résoudre les problèmes et déclencher des alertes lorsque des mesures clés dépassent des seuils critiques. 
{: shortdesc}

Pour être rapidement opérationnel avec le service {{site.data.keyword.mobileanalytics_short}}, procédez comme suit :

1. Après avoir créé une instance
<!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->du service
{{site.data.keyword.mobileanalytics_short}}, vous pouvez accéder à la console de {{site.data.keyword.mobileanalytics_short}}
en cliquant sur votre vignette dans la section **Services** du tableau de bord {{site.data.keyword.Bluemix}}.

 Le service {{site.data.keyword.mobileanalytics_short}} se lance avec le **mode démo** activé. Ce mode remplit des graphiques sur les pages **Données d'application** et **Alertes**, ce qui vous permet de voir de quelle façon vos données seront affichées. Vous pouvez désactiver le mode démo lorsque vous possédez vos propres données. La console {{site.data.keyword.mobileanalytics_short}} est accessible en lecture seule lorsque le mode démo est activé, et vous ne pouvez pas créer de nouvelles définitions d'alerte. 

2. Installez les [logiciels SDK du client](install-client-sdk.html) {{site.data.keyword.mobileanalytics_short}}. Si vous le
souhaitez, vous pouvez utiliser l'[API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window} de {{site.data.keyword.mobileanalytics_short}}.

3. Importez les logiciels SDK du client et initialisez-les à l'aide du fragment de code suivant pour enregistrer les analyses d'utilisation.

	#### Android
	{: #android-initialize}
	1. Importez le logiciel SDK du client :

		```
		import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
		import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
		```
		{: codeblock}
		
	2. Initialisez le logiciel SDK du client dans votre code d'application pour enregistrer les analyses d'utilisation et les sessions d'application
avec votre valeur de [clé d'API](sdk.html#analytics-clientkey).

		```Java
			BMSClient.getInstance().initialize(this.getApplicationContext(), BMSClient.REGION_US_SOUTH); // Vous pouvez changer la région
			
			Analytics.init(getApplication(), "your_app_name_here", "your_api_key_here", hasUserContext, Analytics.DeviceEvent.LIFECYCLE);
		```
		{: codeblock}
		
    Le nom que vous sélectionnez pour votre application (`your_app_name_here`) s'affiche dans la console {{site.data.keyword.mobileanalytics_short}} comme nom d'application. Le nom d'application est utilisé pour filtrer la recherche des journaux d'application dans votre tableau de bord.
Lorsque vous utilisez le même nom d'application sur plusieurs plateformes (par exemple, Android et iOS), tous les journaux issus de cette application s'affichent sous le même nom, quelle que soit la plateforme à partir de laquelle ils ont été envoyés.
    
    Le paramètre **bluemixRegion** spécifique le déploiement {{site.data.keyword.Bluemix_notm}} que vous utilisez, par exemple, `BMSClient.REGION_US_SOUTH` et `BMSClient.REGION_UK`. 
    <!-- , or `BMSClient.REGION_SYDNEY`.-->
    
    **Remarque :** définissez la valeur **true** ou **false** pour `hasUserContext`. Si la valeur est false
(valeur par défaut), chaque périphérique est comptabilisé comme un utilisateur actif. La méthode
[`Analytics.setUserIdentity("username");`](sdk.html#android-tracking-users) ne fonctionne pas si
`hasUserContext` a pour valeur false. Si la valeur est true, chaque utilisation d'[`Analytics.setUserIdentity("username");`](sdk.html#android-tracking-users) est comptabilisée comme un utilisateur
actif. Il n'y a pas d'identité d'utilisateur par défaut lorsque `hasUserContext` a pour valeur true ; par conséquent, celle-ci doit être définie
pour remplir les graphiques d'utilisateurs actifs.

  #### iOS
  {: #ios-initialize}
  
  1. Importez les infrastructures `BMSCore` et `BMSAnalytics` :
	```
	import BMSCore
    import BMSAnalytics
	```
	{: codeblock}
    
  2. Initialisez le logiciel SDK du client dans votre code d'application pour enregistrer les analyses d'utilisation et les sessions d'application
avec votre valeur de [clé d'API](sdk.html#analytics-clientkey).
 
	Swift :
	
	```Swift
	BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Vous pouvez changer la région
	Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: DeviceEvent.lifecycle)	
	```
	{: codeblock}
		
	Le nom que vous sélectionnez pour votre application (`your_app_name_here`) s'affiche dans la console {{site.data.keyword.mobileanalytics_short}} comme nom d'application. Le nom d'application est utilisé pour filtrer la recherche des journaux d'application dans votre tableau de bord.
Lorsque vous utilisez le même nom d'application sur plusieurs plateformes (par exemple, Android et iOS), tous les journaux issus de cette application s'affichent sous le même nom, quelle que soit la plateforme à partir de laquelle ils ont été envoyés.
	
	Le paramètre **bluemixRegion** spécifie le déploiement Bluemix que vous utilisez, par exemple
`BMSClient.REGION_US_SOUTH` ou `BMSClient.REGION_UK`.
	<!-- , or `BMSClient.REGION_SYDNEY`. -->
	
	**Remarque :** définissez la valeur **false** pour `hasUserContext`. Si la valeur est false
(valeur par défaut), chaque périphérique est comptabilisé comme un utilisateur actif. La méthode [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) ne fonctionne pas si `hasUserContext` a pour valeur false. Si la valeur est true, chaque utilisation d'[`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) est comptabilisée comme un utilisateur actif. Il n'y a pas d'identité d'utilisateur par défaut lorsque `hasUserContext` a pour valeur true ; par conséquent, celle-ci doit être définie
pour remplir les graphiques d'utilisateurs actifs.

4. Envoyez des analyses d'utilisation enregistrées au service Mobile Analytics. Une méthode simple pour tester votre analyse consiste à exécuter le code suivant au démarrage de l'application :

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

	Lisez la rubrique [Instrumentation de votre application](sdk.html) pour en savoir plus sur les fonctions {{site.data.keyword.mobileanalytics_short}}.
5. Compilez et exécutez l'application sur votre émulateur ou périphérique.

6. Accédez à la {{site.data.keyword.mobileanalytics_short}} **console** pour voir l'analyse de l'utilisation de votre application. Vous pouvez également surveiller votre application en <!--[creating custom charts](app-monitoring.html#custom-charts),-->[définissant des alertes](app-monitoring.html#alerts) et en [surveillant les pannes d'application](app-monitoring.html#monitor-app-crash).


# rellinks

## Logiciel SDK
* [Logiciel SDK Android](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [Logiciel SDK iOS](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## Référence d'API
{: #api}
* [API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
