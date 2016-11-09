---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"  
---
{:shortdesc: .shortdesc} 

# Configuration du plug-in Cordova
{: #getting-started-cordova}


Instrumentez votre application Cordova avec le SDK client {{site.data.keyword.amafull}}, initialisez le SDK et envoyez des requêtes à des ressources protégées et
non protégées.

{:shortdesc}

## Avant de commencer
{: #before-you-begin}
Vous devez disposer des éléments suivants :
* Une instance d'une application {{site.data.keyword.Bluemix_notm}} qui est protégée par le service {{site.data.keyword.amashort}}. Pour plus d'informations sur la création d'un système de back end {{site.data.keyword.Bluemix_notm}}, voir [Initiation](index.html).

* Une application Cordova ou un projet existant. Pour plus d'informations sur la configuration de votre application Cordova, consultez le [site Web Cordova](https://cordova.apache.org/).

## Installation du plug-in {{site.data.keyword.amashort}} Cordova
{: #getting-started-cordova-plugin}

Le SDK client de {{site.data.keyword.amashort}} pour Cordova est un plug-in Cordova qui encapsule les SDK client natifs de
{{site.data.keyword.amashort}}. Il est distribué à l'aide de l'interface de ligne de commande Cordova et de `npmjs`, un référentiel de plug-ins pour les projets Cordova. L'interface
CLI de Cordova télécharge automatiquement des plug-ins depuis les référentiels et les rend disponibles depuis votre application Cordova.

1. Ajoutez les plateformes Android et iOS à votre application Cordova. Exécutez l'une des commandes suivantes ou les deux à partir de la ligne de commande :
   	
	###Android
	{: #install-cordova-android}

	```
	cordova platform add android
	```
	
	###iOS
	{: #install-cordova-ios}

	```Bash
	cordova platform add ios
	```

2. Si vous avez ajouté la plateforme Android, vous devez ajouter le niveau d'API minimal pris en charge au fichier `config.xml` de votre application Cordova. Ouvrez
le fichier `config.xml` et ajoutez la ligne suivante à l'élément `<platform
name="android">` :

	```XML
	<platform name="android">  
		<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
		<!-- add minimum and target Android API level declaration -->
	</platform>
	```
	
	La valeur de *minSdkVersion* doit être supérieure ou égale à `15`. La valeur de *targetSdkVersion* doit être le dernier logiciel SDK Android mis à disposition par Google.

3. Si vous avez ajouté le système d'exploitation iOS, déclarez une cible dans l'élément `<platform name="ios">` :

	```XML
	<platform name="ios">
		<preference name="deployment-target" value="8.0"/>
		<!-- add deployment target declaration -->
	 </platform>
	```

4. Installez le plug-in Cordova de {{site.data.keyword.amashort}} :

 	```Bash
	cordova plugin add ibm-mfp-core
	```

5. Configurez votre plateforme pour Android, iOS, ou les deux.

	####Android
	{: #cordova-android}

	Avant d'ouvrir votre projet dans Android Studio, générez votre application Cordova via votre interface de ligne de commande (CLI) pour éviter des erreurs
de génération.
	
	```Bash
	cordova build android
	```
	
	####iOS
	{: #cordova-ios}

	Configurez comme suit votre projet Xcode pour éviter des erreurs de génération.

	1. Utilisez la version Xcode la plus récente pour ouvrir votre fichier `xcode.proj` depuis le répertoire
`<app_name>/platforms/ios`.

		**Important :** si vous recevez un message vous invitant à procéder à une conversion vers la dernière syntaxe Swift, cliquez sur **Annuler**.

	2. Accédez à **Build Settings > Swift Compiler - Code Generation > Objective-C Bridging Header** et ajoutez le chemin d'accès suivant :

		`<your_project_name>/Plugins/ibm-mfp-core/Bridging-Header.h`

	3. Accédez à **Build settings > Linking > Runpath Search Paths** et ajoutez le paramètre Frameworks suivant :

		`@executable_path/Frameworks
			`

	4. Générez et exécutez votre application avec Xcode.

6. Vérifiez que l'installation du plug-in a abouti en exécutant la commande suivante :

	```Bash
	cordova plugin list
	```

## Initialisation du plug-in client de {{site.data.keyword.amashort}}
{: #getting-started-cordova-initialize}

Pour utiliser le SDK client de {{site.data.keyword.amashort}}, initialisez-le en lui transmettant les paramètres *applicationGUID* et *applicationRoute*.

1. L'identificateur unique global et la route de l'application figurent sur la page principale du tableau de bord {{site.data.keyword.Bluemix_notm}}. Cliquez
sur le nom de votre application, puis sur **Options pour application mobile** pour afficher les valeurs **Route de
l'application** et **Identificateur global unique de l'application** pour initialisation du SDK.

3. Ajoutez l'appel suivant à votre fichier `index.js` pour initialiser le SDK client de {{site.data.keyword.amashort}}. 

	```JavaScript
	BMSClient.initialize("applicationRoute", "applicationGUID");
	```

  * Remplacez
`applicationRoute` et `applicationGUID` par les valeurs de la section **Options pour application mobile** dans le
tableau de bord {{site.data.keyword.Bluemix_notm}}.

##Initialisation du gestionnaire AuthorizationManager {{site.data.keyword.amashort}}
{: #initializing-auth-manager}

Utilisez le code JavaScript suivant dans votre application Cordova pour initialiser le gestionnaire AuthorizationManager {{site.data.keyword.amashort}}.

```JavaScript
  MFPAuthorizationManager.initialize("tenantId");
```

Remplacez la valeur `tenantId` par la valeur `tenantId` du service {{site.data.keyword.amashort}}. Cette valeur peut être obtenue en cliquant sur le bouton **Afficher les données d'identification**  sur la vignette du service {{site.data.keyword.amashort}}.

## Envoi d'une demande à l'application back end mobile
{: #getting-started-request}

Une fois que le SDK client {{site.data.keyword.amashort}} est initialisé, vous pouvez commencer à envoyer des requêtes à votre application back end
mobile.

1. Essayez d'envoyer une requête à un noeud final protégé de votre nouvelle application back end
mobile. Dans votre navigateur, ouvrez l'URL suivante : `{applicationRoute}/protected` (`http://my-mobile-backend.mybluemix.net/protected`, par exemple).

	Le noeud final `/protected` d'une application back end mobile créée avec le conteneur boilerplate MobileFirst Services Starter est
protégé par {{site.data.keyword.amashort}}. Un message signalant l'interdiction d'accéder au site (`Unauthorized`) est renvoyé au navigateur. Ce message est renvoyé car ce noeud final n'est accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}.

2. A l'aide de votre application Cordova, envoyez une demande au même noeud final. Ajoutez le code ci-dessous après avoir initialisé `BMSClient` :

	```Javascript
	var success = function(data){
	console.log("success", data);
	}

	var failure = function(error){
	console.log("failure", error);
	}

	var request = new MFPRequest("/protected", MFPRequest.GET);

	request.send(success, failure);
	```

3. Lorsque votre demande aboutit, la sortie suivante figure dans la console LogCat ou Xcode (selon la plateforme utilisée) :

	![image](images/getting-started-android-success.png)

	## Etapes suivantes
	{: #next-steps}

	Lorsque vous vous êtes connecté au noeud final protégé, les données d'identification n'ont pas été nécessaires. Pour obliger les utilisateurs à utiliser des données d'identification pour se connecter à votre application, vous devez configurer Facebook, Google ou l'authentification personnalisée.
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [Authentification personnalisée](custom-auth-cordova.html)
