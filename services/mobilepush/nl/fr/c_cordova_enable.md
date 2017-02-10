---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuration des applications Cordova pour la réception de notifications push
{: #cordova_enable}
Dernière mise à jour : 18 janvier 2017
{: .last-updated}

Cordova est une plateforme permettant de construire des applications hybrides avec JavaScript, CSS et HTML. Le service {{site.data.keyword.mobilepushshort}} prend en charge le développement d'applications iOS et Android reposant sur Cordova.

Vous pouvez activer les applications Cordova pour recevoir des notifications push sur vos appareils.

## Installation du plug-in Cordova Push
{: #cordova_install}

Installez et utilisez le plug-in push client pour développer davantage vos applications Cordova, ce qui a pour effet d'installer aussi le plug-in Cordova core, qui initialise votre connexion à Bluemix.

### Avant de commencer

1. Téléchargez les dernières versions d'Android Studio SDK et Xcode.
1. Configurez votre émulateur. Pour Android Studio, utilisez un émulateur qui prend en charge l'API Google Play.
1. Installez l'outil de ligne de commande Git. Pour Windows, prenez soin de sélectionner l'option **Run Git from the Window Command Prompt**. 
Pour plus d'informations sur le téléchargement et l'installation de cet outil, voir
[Git
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://git-scm.com/downloads "Icône de lien externe"){: new_window}.
1. Installez Node.js et l'outil Node Package Manager (NPM). L'outil de ligne de commande NPM est intégré à Node.js. Pour plus d'informations sur le
téléchargement et l'installation de Node.js, voir [Node.js
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://nodejs.org/en/download/ "Icône de lien externe"){: new_window}.
1. A partir de la ligne de commande, installez les outils de ligne de commande Cordova à l'aide de la commande **npm install -g cordova**. Cette action est requise pour pouvoir utiliser le plug-in push Cordova. Pour
plus d'informations sur l'installation de Cordova et la configuration de votre application Cordova, voir
[Cordova Apache ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lienexterne")](https://cordova.apache.org/#getstarted "Icône de lien externe"){: new_window}. Pour plus d'informations, reportez-vous au

[Fichier
Readme![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push "Icône de lien externe"){: new_window} du plug-in push de Cordova.
1. Placez-vous dans le dossier dans lequel créer votre application Cordova et exécutez la commande ci-dessous pour créer une application Cordova. Si vous possédez déjà une application Cordova, passez à l'étape 3.
```cordova create your_app_name
	cd your_app_name
```
	{: codeblock}
- Facultatif : vous pouvez éditer le fichier **config.xml** et remplacer le nom de l'application dans l'élément <name> par le nom de votre choix, plutôt que d'utiliser le nom par défaut HelloCordova.

Prenez soin de spécifier l'ID de bundle approprié. Les messages d'erreur suivants risquent d'être générés dans Xcode, si un ID de bundle incorrect est spécifié.

* The executable was signed with invalid entitlements.
* The entitlements specified in your application’s Code Signing Entitlements file do not match those specified in your provisioning profile. Pour corriger ce problème, spécifiez l'ID de bundle approprié dans Xcode ou dans le fichier **config.xml** de votre appli Cordova.

1. Ajoutez l'API minimale prise en charge ou la déclaration de cible de déploiement dans le fichier config.xml de votre application Cordova. La valeur de minSdkVersion doit être supérieure à 15. La valeur de targetSdkVersion doit toujours refléter le logiciel SDK Android le plus récent disponible auprès de Google.
	
	* Android - Ouvrez dans votre éditeur le fichier **config.xml** et mettez à jour l'élément
`<platform name="android">` en spécifiant les versions minimum et cible du SDK :

	```
	<platform name="android">
    	<preference name="android-minSdkVersion" value="15" />
    	<preference name="android-targetSdkVersion" value="23" />
    	<!-- add minimum and target Android API level declaration -->
	</platform> 
	```
    	{: codeblock}

   * iOS - Mettez à jour l'élément <platform name="ios"> avec une déclaration cible de déploiement :

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- add deployment target declaration -->
	</platform>
	```
		{: codeblock}

1. A partir de l'interface de ligne de commande Cordova, ajoutez vos plateformes iOS et/ou Android en utilisant la commande suivante :
```
cordova platform add ios
	cordova platform add android
```
	{: codeblock}

1. Depuis le répertoire racine de votre application Cordova, entrez la commande suivante afin d'installer le plug-in push Cordova : **cordova plugin add bms-push**. Selon les plateformes que vous avez ajoutées, vous pouvez voir :
```
Installing "bms-push" for android
Installing "bms-push" for ios
```
	{: codeblock}

1. Depuis votre dossier répertoire_racine_application, vérifiez que les plug-in Cordova core et push ont été installés correctement en entrant la commande suivante : **cordova  plugin list**. Selon les plateformes que vous avez ajoutées, vous pouvez voir :
```
bms-core <version> "BMSCore"
bms-push <version> "BMSPush" 
```
	{: codeblock}

1. Configurez votre environnement de développement iOS.
2. Construisez et exécutez votre application avec Xcode.
1. Téléchargez vos fichiers Firebase `google-services.json` pour Android et placez-les sous le dossier racine de votre projet
Cordova ( `[nom_de_votre_application]/platforms/android.
	1. Accédez au dossier `[nom_de_votre_application]/platforms/android`.
	2. Ouvrez le fichier `build.gradle` (chemin : plateforme > android > build.gradle).
	3. Recherchez le texte `buildscript` dans le fichier `build.gradle`.
	4. Ajoutez la ligne 'com.google.gms:google-services:3.0.0' après celle du chemin de  classes (classpath)
	5. Accédez à la section "dependencies". Sélectionnez les dépendances comportant le texte `compile` et l'endroit marquant la
fin de la
dépendance et ajoutez juste après cette ligne :apply plugin: 'com.google.gms.google-services'.
	6. Préparez et construisez votre projet Cordova Android.
		```
		cordova prepare android
		cordova build android
		```
			{: codeblock}
	**Remarque** : avant d'ouvrir votre projet dans Android Studio, générez votre application Cordova via l'interface CLI Cordova, afin d'éviter des erreurs de génération.

## Initialisation du plug-in Cordova
{: #cordova_initialize}

Pour pouvoir utiliser le plug-in Cordova du service {{site.data.keyword.mobilepushshort}}, vous devez l'initialiser en transmettant la route de l'application et
l'identificateur global unique de l'application. Une fois le plug-in initialisé, vous pouvez vous connecter à l'application serveur que vous avez créée dans le tableau de bord Bluemix. Le plug-in Cordova est l'encapsuleur pour les logiciels SDK de client Android et iOS qui permettent à une application Cordova de communiquer avec les services Bluemix.

1. Initialisez le client BMS en copiant et en collant le fragment de code suivant dans votre fichier JavaScript principal (généralement situé sous le répertoire **www/js**).

```
onDeviceReady: function() {
	app.receivedEvent('deviceready');
	BMSClient.initialize("YOUR APP REGION");
	var category =  {};
	BMSPush.initialize(appGUID,clientSecret,category);
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	BMSPush.registerDevice({}, success, failure);
	var showNotification = function(notif)
	{
	alert(JSON.stringify(notif));
	};
	BMSPush.registerNotificationsCallback(showNotification);
    } 
```
	{: codeblock}

Indiquez la région pour votre application. Les constantes suivantes sont fournies :

```
REGION_US_SOUTH // ".ng.bluemix.net";
REGION_UK //".eu-gb.bluemix.net";
REGION_SYDNEY // ".au-syd.bluemix.net";
```

Par exemple :

```
BMSClient.initialize(BMSClient.REGION_US_SOUTH);
```

**Remarque **: si vous avez créé une application Cordova à l'aide de l'interface CLI de Cordova (par exemple, avec la commande Cordova
create app-name, placez ce code Javascript dans le fichier index.js après la fonction app.receivedEvent dans la fonction onDeviceReady: function()
afin d'initialiser le client `BMSClient`. 


## Enregistrement des appareils
{: #cordova_register}


Pour enregistrer un appareil auprès du service {{site.data.keyword.mobilepushshort}}, appelez la méthode d'enregistrement. Copiez le fragment de code suivant dans votre application Cordova pour enregistrer un appareil.

```
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure);
```
	{: codeblock}

Le fragment de code JavaScript ci-après montre comment initialiser le logiciel SDK de votre client Bluemix Mobile Services, enregistrer un appareil avec le service {{site.data.keyword.mobilepushshort}} et passer en mode écoute sur les notifications push. Incluez ce code dans votre fichier Javascript.

Dans **onDeviceReady: function()**.

```
onDeviceReady: function() {
app.receivedEvent('deviceready');
BMSClient.initialize("YOUR APP REGION");
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure); 
 var showNotification = function(notif)
 {
 alert(JSON.stringify(notif));
 };
BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

Ajoutez le fragment de code Swift suivant à la classe de votre délégué d'application :

```
// Register the device token with Bluemix Push Notification Service
func application(application: UIApplication,
  didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData) {
   CDVBMSPush.sharedInstance().didRegisterForRemoteNotificationsWithDeviceToken(deviceToken)
} 
// Handle error when failed to register device token with APNs
func application(application: UIApplication,
    didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer) {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(error)
} 
```
	{: codeblock}

##Etapes suivantes

{: #cordova_register_next}

Générez votre projet, puis exécutez-le à l'aide des commandes suivantes :

####Android
{: android-next-steps}

```
cordova build android
```
	{: codeblock}

```
cordova run android
```
	{: codeblock}

####iOS
{: ios-next-steps}

```
cordova build ios
```
	{: codeblock}

```
cordova run ios
```
	{: codeblock}

## Réception de notifications push sur les appareils
{: #cordova_receive}

Copiez le fragment de code ci-après pour recevoir des notifications push sur les appareils.

###JavaScript

Ajoutez le fragment de code JavaScript suivant à la partie Web de votre application Cordova :
```
var showNotification = function(notif) {
  alert(JSON.stringify(notif));
        };
        BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

###Propriétés de notification Android

La section suivante répertorie les propriétés de notification Android :

* **message** - Message de notification Push
* **payload** - objet JSON comportant un contenu de notification


###Propriétés de notification iOS

La section suivante répertorie les propriétés de notification iOS :

* **message** - Message de notification Push
* **payload** - Objet JSON comportant un contenu de notification
action-loc-key -  La chaîne est utilisée comme clé pour obtenir une chaîne localisée à l'emplacement actuel, à utiliser comme titre de bouton approprié au lieu de `View`.
* **badge** - numéro à utiliser comme badge de l'icône d'application. Si cette propriété manque, le badge n'est pas changé. Pour supprimer le badge, associez cette propriété à la valeur 0.
* **sound** - Nom d'un fichier son dans le bundle de l'application ou dans le dossier Library/Sounds du conteneur des données d'application.


Ajoutez les fragments de code Swift suivants à la classe de votre délégué d'application :
```
// Handle receiving a remote notification
func application(application: UIApplication,
   didReceiveRemoteNotification userInfo: [NSObject : AnyObject],  fetchCompletionHandler completionHandler: ) {
   CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(userInfo)
}
```
	{: codeblock}

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
  let remoteNotif = launchOptions?[UIApplicationLaunchOptionsKey.remoteNotification] as? NSDictionary
  if remoteNotif != nil {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationOnLaunchWithLaunchOptions(launchOptions)
  }
} 
```
	{: codeblock}

## Envoi de notifications push de base
{: #push-send-notifications}

Une fois que vous avez développé vos applications, vous pouvez envoyer des notifications push de base.

Pour envoyer des notifications push de base, procédez comme suit :

1. Sélectionnez **Envoyer des notifications** et rédigez un message en choisissant une option **Envoyer à**. Les options prises en charge sont **Appareil par étiquette**, **ID de l'appareil**, **ID utilisateur**, **Appareils Android**, **Appareils IOS**, **Notifications Web** et **Tous les appareils**.
**Remarque **: si vous sélectionnez l'option **Tous les appareils**, tous les appareils qui sont abonnés à des notifications de type {{site.data.keyword.mobilepushshort}} recevront les notifications.
![Ecran Notifications](images/tag_notification.jpg)

2. Dans la zone **Message**, composez votre message. Configurez les paramètres facultatifs, selon les besoins.
3. Cliquez sur **Envoyer**.
3. Vérifiez que vos appareils ont reçu votre notification.

Les captures d'écran suivantes présentent une boîte de dialogue d'alerte qui traite une notification de type {{site.data.keyword.mobilepushshort}} s'exécutant au premier plan sur un appareil Android et sur un appareil iOS.

![Notification push qui s'exécute au premier plan sur un appareil Android](images/Android_Screenshot.jpg)

![Notification push qui s'exécute au premier plan sur un appareil iOS](images/iOS_Screenshot.jpg)

   L'image suivante montre {{site.data.keyword.mobilepushshort}} en arrière-plan pour Android.
![Notification push qui s'exécute en arrière-plan sur un appareil Android](images/background.jpg)

## Etapes suivantes
{: #next_steps_tags}

Une fois que vous avez configuré les notifications de base, vous pouvez configurer des notifications basées sur des balises et des options
avancées.

Ajoutez les fonctions du service {{site.data.keyword.mobilepushshort}} à votre application.
Pour utiliser des notifications basées sur les balises, voir [Notifications basées sur les balises](c_tag_basednotifications.html).
Pour utiliser des options de notification avancées, voir [Activation des notifications push avancées](t_advance_badge_sound_payload.html).
