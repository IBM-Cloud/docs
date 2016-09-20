---

Copyright :
  Années : 2015, 2016

---

# Installation du plug-in Cordova Push
{: #cordova_install}

Installez et utilisez le plug-in Push client pour développer davantage vos applications Cordova. Elle installe
également le plug-in Cordova Core, qui initialise votre connexion à Bluemix.

### Avant de commencer

1. Téléchargez les dernières versions d'Android Studio SDK et Xcode.
1. Configurez votre émulateur. Pour Android Studio, utilisez un émulateur qui prend en charge l'API Google Play.
1. Installez l'outil de ligne de commande Git. Pour Windows, prenez soin de sélectionner l'option **Run Git from the Window Command Prompt**. Pour plus d'informations sur le téléchargement et l'installation de cet outil, voir [Git](https://git-scm.com/downloads).

1. Installez Node.js et l'outil Node Package Manager (NPM). L'outil de ligne de commande NPM est intégré à Node.js. Pour plus d'informations sur le téléchargement et l'installation de cet outil, voir [Node.js](https://nodejs.org/en/download/).
1. A partir de la ligne de commande, installez les outils de ligne de commande Cordova à l'aide de la commande **npm install -g cordova**. Vous en aurez besoin pour pouvoir utiliser le plug-in Cordova Push. Pour obtenir des informations sur l'installation de Cordova et la configuration de votre appli Cordova, voir [Cordova Apache](https://cordova.apache.org/#getstarted).

	**Remarque** : Pour afficher le fichier Readme du plug-in Cordova Push, accédez à [https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push)


## Installation du plug-in Cordova Push
1. Placez-vous dans le dossier dans lequel créer votre application Cordova et exécutez la commande ci-dessous pour créer une application Cordova. Si vous possédez déjà une application Cordova, passez à l'étape 3.


	cordova create your_app_name
	cd your_app_name
	```
1. Facultatif : Editez le fichier **config.xml** et remplacez le nom de l'application dans l'élément <name> par le
nom de votre choix, plutôt que d'utiliser le nom HelloCordova par défaut.

	**Remarque** : Prenez soin de spécifier l'ID de bundle approprié. A défaut, les messages d'erreur suivants s'afficheront dans Xcode :
	* The executable was signed with invalid entitlements.
	* The entitlements specified in your application’s Code Signing Entitlements file do not match those specified in your provisioning profile.

	Pour corriger ce problème, spécifiez l'ID de bundle approprié dans Xcode ou dans le fichier **config.xml** de votre appli Cordova.

1. Ajoutez l'API minimale prise en charge ou la déclaration de cible de déploiement dans le fichier config.xml de votre application Cordova. La valeur de minSdkVersion doit être supérieure à 15. La valeur de targetSdkVersion doit toujours refléter le logiciel SDK Android le plus récent disponible auprès de Google.
	* **Android** - A l'aide de votre éditeur, ouvrez le fichier config.xml et mettez à jour
l'élément ```<platform name="android">``` avec les versions minimum et cible de SDK :

	```
	<!-- add deployment target declaration -->
	<platform name="android">  
			  <preference name="android-minSdkVersion" value="15" />
			  <preference name="android-targetSdkVersion" value="23" />
			</platform>
	```
   * **iOS** - Mettez à jour l'élément <platform name="ios"> avec une déclaration cible de déploiement :

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- other properties -->
	</ platform>
	```

1. A partir de l'interface de ligne de commande Cordova, ajoutez vos plateformes iOS et/ou Android à l'aide des commandes suivantes :

	```
	cordova platform add ios
	cordova platform add android
	```
1. Depuis le répertoire principal de votre application Cordova, entrez la commande suivante pour installer le plug-in Cordova Push : **cordova plugin add ibm-mfp-push**.

	Selon les plateformes que vous avez ajoutées, la sortie peut ressembler à l'exemple suivant :

	```
	Installing "ibm-mfp-push" for android
	Installing "ibm-mfp-push" for ios
	```
1. Depuis *your-app-root-folder*, vérifiez que les plug-ins Cordova Core et Push ont été installés correctement en entrant la
commande suivante : **cordova plugin list**.

	Selon les plateformes que vous avez ajoutées, la sortie peut ressembler à l'exemple suivant :

	```
	ibm-mfp-core 1.0.0 "MFPCore"
	ibm-mfp-push 1.0.0 “MFPPush"
	```
1. (iOS uniquement) - Configurez votre environnement de développement iOS.
	a. Ouvrez votre fichier your-app-name.xcodeproj dans le répertoire *your-app-name***/platforms/ios** à l'aide de Xcode.

	b. Ajoutez l'en-tête de pontage. Accédez à **Build settings > Swift Compiler - Code Generation > Objective-C Bridging Header** et ajoutez le chemin suivant :*your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	c. Ajoutez le paramètre Frameworks. Accédez à **Build Settings > Linking > Runpath Search Paths** et ajoutez le paramètre suivant :
	```
	@executable_path/Frameworks
	```
	d. Supprimez la mise en commentaire des instructions d'importation Push suivantes dans votre en-tête de pontage. Accédez à *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	```
	//#import <IMFPush/IMFPush.h>
	//#import <IMFPush/IMFPushClient.h>
	//#import <IMFPush/IMFResponse+IMFPushCategory.h>
	```
	e. Générez et exécutez votre application à l'aide de Xcode.
1. (Android uniquement) - Générez votre projet Android à l'aide de la commande suivante :
**cordova build android**.

	**Remarque** : Avant d'ouvrir votre projet dans Android Studio, vous devez d'abord générer votre application Cordova via l'interface CLI Cordova. A défaut, des erreurs de génération seront émises.

1. Etape suivante. [Initialisation du plug-in Cordova](t_cordova_initalize.html).
