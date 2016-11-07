---

copyright:
 years: 2015, 2016

---

# Configuration des applications Cordova pour la réception de notifications push
{: #cordova_enable}
Dernière mise à jour : 17 octobre 2016
{: .last-updated}

Cordova est une plateforme permettant de construire des applications hybrides avec JavaScript, CSS et HTML. Le service {{site.data.keyword.mobilepushshort}} prend en charge le développement d'applications iOS et Android reposant sur Cordova.

Vous pouvez activer les applications Cordova pour recevoir des notifications push sur vos appareils.

## Installation du plug-in push Cordova
{: #cordova_install}

Installez et utilisez le plug-in push client pour développer davantage vos applications Cordova, ce qui a pour effet d'installer aussi le plug-in Cordova core, qui initialise votre connexion à Bluemix.

### Avant de commencer

1. Téléchargez les dernières versions d'Android Studio SDK et Xcode.
1. Configurez votre émulateur. Pour Android Studio, utilisez un émulateur qui prend en charge l'API Google Play.
1. Installez l'outil de ligne de commande Git. Pour Windows, prenez soin de sélectionner l'option **Run Git from the Window Command Prompt**. Pour plus d'informations sur le téléchargement et l'installation de cet outil, voir [Git](https://git-scm.com/downloads).
1. Installez Node.js et l'outil Node Package Manager (NPM). L'outil de ligne de commande NPM est intégré à Node.js. Pour plus d'informations sur le téléchargement et l'installation de cet outil, voir [Node.js](https://nodejs.org/en/download/).
1. A partir de la ligne de commande, installez les outils de ligne de commande Cordova à l'aide de la commande **npm install -g cordova**. Cette action est requise pour pouvoir utiliser le plug-in push Cordova. Pour obtenir des informations sur l'installation de Cordova et la configuration de votre appli Cordova, voir [Cordova Apache](https://cordova.apache.org/#getstarted). Pour plus d'informations, voir le [fichier readme](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push) du plug-in push Cordova.
1. Placez-vous dans le dossier dans lequel créer votre application Cordova et exécutez la commande ci-dessous pour créer une application Cordova. Si vous possédez déjà une application Cordova, passez à l'étape 3.
```
cordova create your_app_name
	cd your_app_name
```
	{: codeblock}
- Facultatif : vous pouvez éditer le fichier **config.xml** et remplacer le nom de l'application dans l'élément <name> par le nom de votre choix, plutôt que d'utiliser le nom par défaut HelloCordova.

Prenez soin de spécifier l'ID de bundle approprié. Les messages d'erreur suivants risquent d'être générés dans Xcode, si un ID de bundle incorrect est spécifié.

* The executable was signed with invalid entitlements.
* The entitlements specified in your application’s Code Signing Entitlements file do not match those specified in your provisioning profile. Pour corriger ce problème, spécifiez l'ID de bundle approprié dans Xcode ou dans le fichier **config.xml** de votre appli Cordova.

1. Ajoutez l'API minimale prise en charge ou la déclaration de cible de déploiement dans le fichier config.xml de votre application Cordova. La valeur de minSdkVersion doit être supérieure à 15. La valeur de targetSdkVersion doit toujours refléter le logiciel SDK Android le plus récent disponible auprès de Google.
	
	* Android - avec votre éditeur, ouvrez le fichier config.xml et mettez à jour l'élément `<platform name="android">` avec les versions SDK minimum et cible :

```
< !-- add deployment target declaration --> 
add deployment target declaration <preference name="android-minSdkVersion" value="15" />
  <preference name="android-targetSdkVersion" value="23" />
</platform>
```
    {: codeblock}

   * iOS - Mettez à jour l'élément <platform name="ios"> avec une déclaration cible de déploiement :

```
<platform name ="ios">
<preference name=deployment-target" value="8.0" /> <!-- other properties -->
</ platform>
```
	{: codeblock}

1. A partir de l'interface de ligne de commande Cordova, ajoutez vos plateformes iOS et/ou Android en utilisant la commande suivante :
```
cordova platform add ios
	cordova platform add android
```
	{: codeblock}

1. Depuis le répertoire principal de votre application Cordova, entrez la commande suivante pour installer le plug-in push Cordova : **cordova plugin add ibm-mfp-push**. Selon les plateformes que vous avez ajoutées, vous pouvez voir :
```
Installing "ibm-mfp-push" for android
	Installing "ibm-mfp-push" for ios
```
	{: codeblock}

1. Depuis *your-app-root-folder*, vérifiez que les plug-ins Cordova core et push ont été installés correctement en entrant la commande suivante : **cordova plugin list**. Selon les plateformes que vous avez ajoutées, vous pouvez voir :
```
ibm-mfp-core 1.0.0 "MFPCore"
	ibm-mfp-push 1.0.0 “MFPPush"
```
	{: codeblock}

1. (iOS uniquement) - Configurez votre environnement de développement iOS.
2. Exécutez les sous-procédures suivantes :

 a. Ouvrez votre fichier your-app-name.xcodeproj dans le répertoire *your-app-name***/platforms/ios** à l'aide de Xcode.

 b. Ajoutez l'en-tête de pontage. Accédez à **Build settings > Swift Compiler - Code Generation > Objective-C Bridging Header** et ajoutez le chemin suivant :*your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

 c. Ajoutez le paramètre Frameworks. Accédez à **Build Settings > Linking > Runpath Search Paths** et ajoutez le paramètre `@executable_path/Frameworks`.

 d. Supprimez la mise en commentaire des instructions d'importation Push suivantes dans votre en-tête de pontage. Accédez à *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

```
//#import <IMFPush/IMFPush.h>
	//#import <IMFPush/IMFPushClient.h>
	//#import <IMFPush/IMFResponse+IMFPushCategory.h>
```
	{: codeblock}

 e. Générez et exécutez votre application à l'aide de Xcode.

1. (Android uniquement) - Générez votre projet Android à l'aide de la commande suivante :
**cordova build android**.

	**Remarque** : avant d'ouvrir votre projet dans Android Studio, générez votre application Cordova via l'interface CLI Cordova, afin d'éviter des erreurs de génération.


## Initialisation du plug-in Cordova
{: #cordova_initialize}

Pour pouvoir utiliser le plug-in Cordova du service {{site.data.keyword.mobilepushshort}}, vous devez l'initialiser en transmettant la route de l'application et
l'identificateur global unique de l'application. Une fois le plug-in initialisé, vous pouvez vous connecter à l'application serveur que vous avez créée dans le tableau de bord Bluemix. Le plug-in Cordova est l'encapsuleur pour les logiciels SDK de client Android et iOS qui permettent à une application Cordova de communiquer avec les services Bluemix.

1. Initialisez le client BMS en copiant et en collant le fragment de code suivant dans votre fichier JavaScript principal (généralement situé sous le répertoire **www/js**).

```
BMSClient.initialize("https://myapp.mybluemix.net","App GUID");
```
	{: codeblock}

1. Modifiez le fragment de code pour qu'il utilise vos paramètres de route et d'identificateur global unique Bluemix. Cliquez sur le lien **Options pour application mobile** dans votre tableau de bord Push pour obtenir la route et l'identificateur global unique de l'application ainsi que la valeur confidentielle du client. Utilisez les valeurs Route et Identificateur global unique de l'application comme paramètres dans votre fragment de code `BMSClient.initialize`.

	**Remarque** : Si vous avez créé une appli Cordova à l'aide de l'interface CLI Cordova, par exemple, la commande Cordova create app-name, placez ce code Javascript dans le fichier **index.js**, après la fonction `app.receivedEvent` dans la fonction `onDeviceReady: function()` afin d'initialiser le client BMS.

```
onDeviceReady: function() {
app.receivedEvent('deviceready');
BMSClient.initialize("https://myapp.mybluemix.net","App GUID");
    },
```
	{: codeblock}

## Enregistrement des appareils
{: #cordova_register}


Pour enregistrer un appareil auprès du service {{site.data.keyword.mobilepushshort}}, appelez la méthode d'enregistrement. Copiez le fragment de code suivant dans votre application Cordova pour enregistrer un appareil.

```
var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	MFPPush.registerDevice({}, success, failure);
```
	{: codeblock}

### Android
{: #cordova_register_android}
Android n'utilise pas le paramètre settings. Si vous ne générez qu'une application Android, passez un objet vide, par exemple :

```
MFPPush.registerDevice({}, success, failure);
	MFPPush.unregisterDevice(success, failure);
```
	{: codeblock}

### iOS
{: #cordova_register_ios}
Pour personnaliser les propriétés d'alerte, de badge et de son, ajoutez le fragment de code JavaScript suivant
à la partie Web de votre application Cordova.

```
var settings = {
   ios: {
      alert: true,
	       badge: true,
	       sound: true
	   }
}
	MFPPush.registerDevice(settings, success, failure);
```
	{: codeblock}


### JavaScript
{: #cordova_register_js}

```
MFPPush.registerDevice({}, success, failure);
```
	{: codeblock}

Vous pouvez accéder au contenu du paramètre de réponse success dans Javascript à l'aide de JSON.parse : **var token = JSON.parse(response).token**


Les clés disponibles sont les suivantes : `token` et `deviceId`.

Le fragment de code JavaScript ci-après montre comment initialiser votre logiciel SDK du client Bluemix Mobile Services, enregistrer un appareil avec le service {{site.data.keyword.mobilepushshort}} et passer en mode écoute sur les notifications push. Incluez ce code dans votre fichier Javascript.

```
//Register device token with Bluemix Push Notification Service
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
  CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
```
	{: codeblock}

```
//Handle error when failed to register device token with APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```
	{: codeblock}
Dans **onDeviceReady: function()**.

```
onDeviceReady: function() {
app.receivedEvent('deviceready');
     BMSClient.initialize("https://http://myroute_mybluemix.net","my_appGuid");
     var success = function(message) { console.log("Success: " + message); };
     var failure = function(message) { console.log("Error: " + message); };
     var settings = {
     ios: {
         alert: true,
	       badge: true,
	       sound: true
	   }
  };
   MFPPush.registerDevice(settings, success, failure);
   var notification = function(notif){
       alert (notif.message);
    };
    MFPPush.registerNotificationsCallback(notification);
	 }
```
	{: codeblock}

### Objective-C
{: #cordova_register_objective}
Ajoutez le fragment de code Objective-C suivant à la classe de votre délégué d'application :

```
// Register the device token with Bluemix Push Notification Service
	- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
  [[CDVMFPPush sharedInstance] didRegisterForRemoteNotifications:deviceToken];
	}
// Handle error when failed to register device token with APNs
	- (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error {
   [[CDVMFPPush sharedInstance] didFailToRegisterForRemoteNotificationsWithError:error];
	}
```
	{: codeblock}

###Swift
{: #cordova_register_swift}
Ajoutez le fragment de code Swift suivant à la classe de votre délégué d'application :

```
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
// Handle error when failed to register device token with APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
   CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
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
var notification = function(notification){
    // la notification est un objet JSON.
alert(notification.message);
};
MFPPush.registerNotificationsCallback(notification);
```
	{: codeblock}

###Propriétés de notification Android

La section suivante répertorie les propriétés de notification Android :

* message - Message de notification push
* payload - Objet JSON comportant un contenu de notification


###Propriétés de notification iOS

La section suivante répertorie les propriétés de notification iOS :

* message - Message de notification push
* payload - Objet JSON comportant un contenu de notification JSON action-loc-key - La chaîne est utilisée comme clé pour obtenir une chaîne localisée à l'emplacement actuel, à utiliser comme titre de bouton approprié au lieu de `View`.
* badge - Numéro à afficher comme badge de l'icône d'application. Si cette propriété manque, le badge n'est pas changé. Pour supprimer le badge, associez cette propriété à la valeur 0.
* sound - Nom d'un fichier son dans le regroupement d'applications ou dans le dossier Library/Sounds du conteneur des données d'application.

###Objective-C

Ajoutez les fragments de code Objective-C suivants à la classe de votre délégué d'application :

```
// Handle receiving a remote notification
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler {
 [[CDVMFPPush sharedInstance] didReceiveRemoteNotification:userInfo];
}
```
	{: codeblock}


```
// Handle receiving a remote notification on launch
		- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
    [[CDVMFPPush sharedInstance] didReceiveRemoteNotificationOnLaunch:launchOptions];
	}
```
	{: codeblock}

###Swift

Ajoutez les fragments de code Swift suivants à la classe de votre délégué d'application :
```
// Handle receiving a remote notification
funcapplication(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: ){
  CDVMFPPush.sharedInstance().didReceiveRemoteNotification(userInfo)
	}
```
	{: codeblock}

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
  CDVMFPPush.sharedInstance().didReceiveRemoteNotificationOnLaunch(launchOptions)
	}
```
	{: codeblock}

## Envoi de notifications push de base
{: #push-send-notifications}

Une fois que vous avez développé vos applications, vous pouvez envoyer des notifications push de base.

Pour envoyer des notifications push de base, procédez comme suit :

1. Sélectionnez **Envoyer des notifications** et rédigez un message en choisissant une option **Envoyer à**. Les options prises en charge sont **Appareil par étiquette**, **ID de l'appareil**, **ID utilisateur**, **Appareils Android**, **Appareils IOS**, **Notifications Web** et **Tous les appareils**.
**Remarque **: quand vous sélectionnez l'option **Tous les appareils**, tous les appareils qui sont abonnés à des notifications de type {{site.data.keyword.mobilepushshort}} recevront les notifications.
![Ecran Notifications](images/tag_notification.jpg)

2. Dans la zone **Message**, composez votre message. Configurez les paramètres facultatifs, selon les besoins.
3. Cliquez sur **Envoyer**.
3. Vérifiez que vos appareils ont reçu votre notification.

La capture d'écran suivante présente une boîte de dialogue d'alerte qui traite une notification de type {{site.data.keyword.mobilepushshort}} s'exécutant au premier plan sur un appareil Android et iOS.

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
