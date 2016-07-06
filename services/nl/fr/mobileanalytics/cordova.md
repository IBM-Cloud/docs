<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Initiation à l'exemple HelloWorld
{: #gettingstarted-cordova}

Si vous voulez débuter avec une nouvelle application Cordova, vous pouvez utiliser l'application HelloWorld. Elle explique comment se connecter à votre système de back end Bluemix depuis une application mobile sans authentification. Le logiciel SDK est déjà installé pour l'application. Une fois prêt, vous pouvez vous procurer les bibliothèques spécifiques que vous voulez utiliser dans
votre application.

1. Créez votre application de back end mobile dans Bluemix.
<ol>
	<li>Dans la section Conteneurs boilerplate du catalogue Bluemix, cliquez sur MobileFirst Services Starter.</li>
    	<li>Entrez un nom et un hôte pour votre application et cliquez sur **Créer**.</li>
    	<li>Cliquez sur **Terminer**. </li>
</ol>
2. Obtenez le projet depuis GitHub. Si vous le souhaitez, vous pouvez utiliser la commande git clone pour obtenir le projet. Depuis votre ordinateur, ouvrez le
terminal, puis entrez la commande suivante :
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld
```

3. Exécutez les commandes suivantes depuis votre répertoire de projet afin d'ajouter les environnements de plateforme Android et iOS :

Android :
```
cordova platform add android
```

iOS :
```
cordova platform add ios
```

4. Ajoutez le plug-in Cordova à l'aide de la commande suivante :
```
cordova plugin add ibm-mfp-core
```

5. Configurez votre application Cordova pour Android, iOS ou les deux.

 * Android

	 Avant d'ouvrir votre projet dans Android Studio, générez et exécutez votre application Cordova via votre interface de ligne de commande afin d'éviter toute erreur de génération.

	 ```
	 cordova build android
	 ```

	 ```
	 cordova run android
	 ```

 * iOS

	 Configurez votre projet Xcode comme suit, afin d'éviter toute erreur de génération.

	    1. Utilisez la version la plus récente de Xcode pour ouvrir votre fichier xcode.proj depuis le répertoire
&lt;nom_application&gt;/platforms/ios.

			**Important :** Si vous recevez un message "Convert to Latest Swift Syntax" (Convertir dans la dernière syntaxe Swift), cliquez sur
Cancel (Annuler).

		2. Accédez à **Build Settings > Swift Compiler - Code Generation > Objective-C Bridging Header** et ajoutez le chemin suivant :

		```
		<votre_nom_de_projet>/Plugins/ibm-mfp-core/Bridging-Header.h
		```
		3. Accédez à **Build settings > Linking > Runpath Search Paths** et ajoutez le paramètre Frameworks suivant :

		```
		@executable_path/Frameworks
		```
		4. Générez et exécutez votre application avec Xcode.

6. Configurez l'exemple HelloWorld
<ol>
	<li>Accédez au répertoire dans lequel vous avez cloné le projet.</li>
	<li>Ouvrez le fichier &lt;répertoire_de_votre_application&gt;/www/js/index.js et remplacez &lt;APPLICATION_ROUTE&gt; et &lt;APPLICATION_ID&gt; par la route et l'ID de votre application Bluemix.</li>
</ol>

Remarque : vérifiez que votre route &lt;APPLICATION_ROUTE&gt; utilise le protocole https.

```
// Bluemix credentials
route: "<APPLICATION_ROUTE>",
GUID: "<APPLICATION_GUID>",
```

7. Exécutez l'exemple sur votre émulateur ou périphérique mobile.

   Générez l'application Cordova avec les commandes suivantes :
	 ```
	 cordova build ios
	 ```
	 ```
	 cordova build android
	 ```

   Exécutez le modèle d'application avec les commandes suivantes :
	 ```
	 cordova run ios
	 ```
   ```
	 cordova run android
	 ```


Une application avec une vue unique comportant un bouton **PING BLUEMIX** s'affiche. Lorsque vous sélectionnez le bouton, l'application teste la connexion entre le client et l'application de backend Bluemix. La connexion est testée à l'aide de la route d'application que vous spécifié dans le fichier index.js.


![Application Hello World
connectée à Bluemix](images/yayconnected.jpg "Figure 1. Application Hello World connectée à Bluemix")

Lorsque vous parvenez à vous connecter à Bluemix depuis l'application mobile, le message suivant s'affiche : "Yay! You are connected".
8. Corrigez les problèmes éventuels.

<!--![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")-->

Si la connexion échoue, le message suivant s'affiche : "Bummer Something went wrong". Des informations supplémentaires sur l'erreur sont incluses.
Vérifiez les points suivants :
 * Assurez-vous d'avoir collé correctement les valeurs de route et d'identificateur global unique.
 * Affichez le journal de débogage de Xcode ou Android.
 * Vérifiez l'état de votre application dans Bluemix.

## Etapes suivantes :
{: #next}
Pour obtenir des informations sur l'obtention du logiciel SDK et son intégration à votre application mobile, voir Configuration du logiciel SDK du client Cordova.

# rellinks

## Exemples
   * [HelloWorld (Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld)

## sdk
   * [bms-clientsdk-cordova-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

<!--## api
   * [Core API](https://www.{DomainName}/docs/api/content/api/mobilefirst/cordova/core-api-doc/overview-summary.html)
-->
