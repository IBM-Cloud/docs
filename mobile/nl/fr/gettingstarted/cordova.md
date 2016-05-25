---

copyright:
  années : 2015, 2016

---
<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Initiation à l'exemple HelloWorld
{: #gettingstarted-cordova}
*Dernière mise à jour : 17 mars 2016*

Si vous voulez débuter avec une nouvelle application Cordova, vous pouvez utiliser l'application HelloWorld. Elle explique comment se connecter à
votre système de back end mobile dans {{site.data.keyword.Bluemix}} depuis une application mobile sans authentification. Le logiciel SDK est déjà installé pour l'application. Une fois prêt, vous pouvez vous procurer les bibliothèques spécifiques que vous voulez utiliser dans
votre application.

1. Créez votre application de back end mobile dans {{site.data.keyword.Bluemix_notm}}.

	1. Dans la section Conteneurs boilerplate du catalogue {{site.data.keyword.Bluemix_notm}}, cliquez sur MobileFirst Services Starter.
	1. Entrez un nom et un hôte pour votre application et cliquez sur **Créer**.
	1. Cliquez sur **Terminer**.

2. Obtenez le projet depuis GitHub. Vous pouvez utiliser la commande git clone pour obtenir le projet. Depuis votre ordinateur, ouvrez le
terminal, puis entrez la commande suivante :

	```Bash
	git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld
	```

3. Exécutez les commandes suivantes depuis votre répertoire de projet afin d'ajouter les environnements de plateforme Android et iOS :

	### Android

	```Bash
	cordova platform add android
	```

	### iOS

	```Bash
	cordova platform add ios
	```

4. Ajoutez le plug-in Cordova avec la commande suivante :

	```Bash
	cordova plugin add ibm-mfp-core
	```

5. Configurez l'exemple HelloWorld.

	* Placez-vous dans le répertoire dans lequel vous avez cloné le projet.
	* Ouvrez le fichier *&lt;rép_de_votre_app&gt;*/www/js/index.js et remplacez *&lt;APPLICATION_ROUTE&gt;* et
*&lt;APPLICATION_ID&gt;* par votre ID d'application Bluemix et votre route.

		**Remarque :** assurez-vous que votre route utilise le protocole https pour la sécurité.

		```Javascript
		// Données d'identification Bluemix
		route: "<APPLICATION_ROUTE>",
		GUID: "<APPLICATION_GUID>",
		```

6. Configurez votre appli Cordova pour iOS. La plateforme Android ne nécessite pas de configuration supplémentaire.

	### iOS
  Configurez votre projet Xcode comme suit afin d'éviter toute erreur de génération.

	1. Utilisez la version la plus récente de Xcode pour ouvrir votre fichier `xcode.proj` dans le répertoire *&lt;nom_app&gt;*/platforms/ios.

		**Important :** si vous recevez le message "Convert to Latest Swift Syntax", cliquez sur **Cancel**.

	2. Accédez à **Build Settings > Swift Compiler - Code Generation > Objective-C Bridging Header** et ajoutez le chemin suivant :

		```
		<nom_de_votre_projet>/Plugins/ibm-mfp-core/Bridging-Header.h
		```

	3. Accédez à **Build settings > Linking > Runpath Search Paths** et ajoutez le paramètre Frameworks suivant :

		```
		@executable_path/Frameworks
		```

7. Créez et exécutez l'exemple sur votre émulateur ou périphérique mobile. 

  ### Android
	1. Générez l'appli Cordova avec la commande suivante : 

    **Important :** Avant d'ouvrir votre projet dans Android Studio, vous devez d'abord générer votre appli Cordova via l'interface de ligne de commande Cordova (CLI). Si vous ne le faites pas, vous des erreurs de génération se produisent.

	```Bash
	cordova build android
	```

	2. Exécutez l'exemple dans Android Studio.

  ### iOS
  1. Générez l'appli Cordova dans Xcode.

    **Astuce :** La génération dans Xcode permet d'avoir accès à d'autres options, telles que le débogage et la configuration des projets.

  2. Exécutez l'exemple dans Xcode.

Une application avec une vue unique comportant un bouton **PING BLUEMIX** s'affiche. Si vous tapez sur ce bouton, l'application teste
la connexion du client à l'application {{site.data.keyword.Bluemix_notm}} de back end. La connexion est testée avec la route d'application que
vous avez spécifiée dans le fichier `index.js`.


![Application Hello World
connectée à Bluemix](images/yayconnected.jpg "Figure 1. Application Hello World connectée à Bluemix")


Si vous parvenez à vous connecter à {{site.data.keyword.Bluemix_notm}} depuis votre application mobile, le message "Yay! You are connected" s'affiche.


<!--![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")-->

Si la connexion échoue, un message d'erreur s'affiche. Ce dernier inclut des informations supplémentaires sur l'erreur. Vous pouvez vérifier les éléments suivants afin de traiter votre erreur :

- Assurez-vous d'avoir collé correctement les valeurs de route et d'identificateur global unique.
- Affichez le journal de débogage de Xcode ou Android.
- Vérifiez le statut de votre application dans {{site.data.keyword.Bluemix_notm}}.

## Etapes suivantes :
{: #next}
Pour des informations sur l'obtention du logiciel SDK et son intégration à votre application mobile, voir :
* [Mobile Client Access : Configuration du plug-in Cordova](../../services/mobileaccess/getting-started-cordova.html)
* [Push Notifications : Configuration du plug-in Cordova](../../services/mobilepush/enablepush_cordova.html#setup_sdk_cordova)

# rellinks

## samples
   * [HelloWorld (Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld)

## sdk
   * [bms-clientsdk-cordova-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

<!--## api
   * [Core API](https://classicdocs.{DomainName}/docs/api/content/api/mobilefirst/cordova/core-api-doc/overview-summary.html)
-->
