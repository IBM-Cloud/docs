---

Copyright : 2015, 2016
  
---

# Configuration du plug-in Cordova
{: #getting-started-cordova}

Instrumentez votre application Cordova avec le SDK client de {{site.data.keyword.amashort}}, initialisez le SDK et envoyez des demandes à des ressources protégées et non protégées.

## Avant de commencer
{: #before-you-begin}

- Vous devez disposer d'une instance d'une application de back end mobile protégée par le service {{site.data.keyword.amashort}}. Pour plus d'informations sur la création d'un système de back end mobile, voir [Initiation](getting-started.html).

- Créez une application Cordova ou utilisez un projet existant. Pour plus d'informations sur la configuration de votre application Cordova, consultez le [site Web Cordova](https://cordova.apache.org/).

## Installation du plug-in Cordova de {{site.data.keyword.amashort}}
{: #getting-started-cordova-plugin}

Le SDK client de {{site.data.keyword.amashort}} pour Cordova est un plug-in Cordova qui encapsule les SDK client natifs de {{site.data.keyword.amashort}}. Il est distribué à l'aide de l'interface de ligne de commande Cordova et de `npmjs`, un référentiel de plug-ins pour les projets Cordova. T'interface de ligne de commande Cordova télécharge automatiquement les plug-ins à partir des référentiels et les met à la disposition de votre application Cordova.

1. Ajoutez les plateformes Android et iOS à votre application Cordova. Exécutez l'une des commandes suivantes ou les deux à partir de la ligne de commande :

	```Bash
	cordova platform add android
	```

	```Bash
	cordova platform add ios
	```

1. Si vous avez ajouté la plateforme Android, vous devez ajouter le niveau d'API minimal pris en charge au fichier `config.xml` de votre application Cordova. Ouvrez le fichier `config.xml` et ajoutez la ligne suivante à l'élément `<platform name="android">` :

	```XML
	<platform name="android">  
		<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
		<!-- add minimum and target Android API level declaration -->
	</platform>
	```

	La valeur de *minSdkVersion* doit être supérieure à `15`. La valeur de *targetSdkVersion* doit être le dernier logiciel SDK Android mis à disposition par Google.

1. Si vous avez ajouté le système d'exploitation iOS, déclarez une cible dans l'élément `<platform name="ios">` :

	```XML
	<platform name="ios">
    <preference name="deployment-target" value="8.0"/>
		<!-- add deployment target declaration -->
	</platform>
	```

1. Installez le plug-in Cordova de {{site.data.keyword.amashort}} :

 	```Bash
	cordova plugin add ibm-mfp-core
	```

1. Configurez votre plateforme pour Android, iOS, ou les deux.

	* **Android**

		Avant d'ouvrir votre projet dans Android Studio, générez votre application Cordova via votre interface de ligne de commande (CLI) pour éviter des erreurs
de génération.

		```
		cordova build android
		```

	* **iOS**

		Configurez comme suit votre projet Xcode pour éviter des erreurs de génération.

		1. Utilisez la version la plus récente de Xcode pour ouvrir votre fichier xcode.proj depuis le répertoire
&lt;*nom_application*&gt;/platforms/ios.

		**Important :** Si vous recevez un message "Convert to Latest Swift Syntax" (Convertir dans la dernière syntaxe Swift), cliquez sur
Cancel (Annuler).

		2. Accédez à **Build Settings (Paramètres de génération) > Swift Compiler (Compilateur Swift) - Code Generation (Génération de code) > Objective-C
Bridging Header (En-tête de pontage Objective-C) ** et ajoutez le chemin suivant :

			```
			<nom_de_votre_projet>/Plugins/ibm-mfp-core/Bridging-Header.h
			```

		3. Accédez à **Build settings (Paramètres de génération) > Linking (Liaison) > Runpath Search Paths (Chemins de recherche de chemins
d'exécution) ** et ajoutez le paramètre Frameworks suivant :

			```
			@executable_path/Frameworks
			```

		4. Générez et exécutez votre application avec Xcode.

1. Vérifiez que le plug-in a été installé correctement à l'aide de la commande suivante :

	```Bash
	cordova plugin list
	```

## Initialisation du plug-in client de {{site.data.keyword.amashort}}
{: #getting-started-cordova-initialize}

Pour pouvoir utiliser le logiciel SDK client de {{site.data.keyword.amashort}}, vous devez l'initialiser en
passant les paramètres suivants : l'identificateur unique global de l'application (*applicationGUID*) et la route de l'application (*applicationRoute*).

1. L'identificateur unique global et la route de l'application figurent sur la page principale du tableau de bord {{site.data.keyword.Bluemix_notm}}. Cliquez sur le nom de votre appli, puis sur **Options pour application mobile** pour afficher les valeurs de **Route de l'application** et d'**Identificateur global unique de l'application** permettant d'initialiser le SDK.

3. Ajoutez l'appel suivant à votre fichier `index.js` pour initialiser le SDK client de {{site.data.keyword.amashort}}. Remplacez
*applicationRoute* et *applicationGUID* par les valeurs de la section **Options pour application mobile** dans le
tableau de bord {{site.data.keyword.Bluemix_notm}}.

	```JavaScript
	BMSClient.initialize("applicationRoute", "applicationGUID");
	```

## Envoi d'une demande au système de back end mobile
{: #getting-started-request}

Lorsque le SDK client de {{site.data.keyword.amashort}} est initialisé, vous pouvez commencer à envoyer des demandes à votre système de back end mobile.

1. Tentez d'envoyer une demande à un noeud final protégé de votre nouveau système de back end mobile. Dans votre navigateur, ouvrez l'URL suivante :
`{applicationRoute}/protected`. Exemple :

	```
	http://my-mobile-backend.mybluemix.net/protected
	```

	Le noeud final `/protected` d'un système de back end mobile créé avec le conteneur boilerplate MobileFirst Services
est protégé par {{site.data.keyword.amashort}}. Un message signalant l'interdiction d'accéder au site (`Unauthorized`) est renvoyé au navigateur. Ce message est renvoyé car ce noeud final n'est accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}.

1. A l'aide de votre application Cordova, envoyez une demande au même noeud final. Ajoutez le code ci-dessous après avoir initialisé `BMSClient` :

	```Javascript
	var success = function(data){
	console.log("succès", data);
	}

	var failure = function(error){
		console.log("échec", error);
	}

	var request = new MFPRequest("/protected", MFPRequest.GET);

	request.send(success, failure);
	```

1. Lorsque votre demande aboutit, la sortie suivante figure dans la console LogCat ou Xcode (selon la plateforme utilisée) :

	![image](images/getting-started-android-success.png)

	## Etapes suivantes
	{: #next-steps}

	Lorsque vous vous êtes connecté au noeud final protégé, les données d'identification n'ont pas été nécessaires. Pour obliger les utilisateurs à utiliser des données d'identification pour se connecter à votre application, vous devez configurer Facebook, Google ou l'authentification personnalisée.
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [Authentification personnalisée](custom-auth-cordova.html)
