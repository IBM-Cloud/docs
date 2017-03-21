# Initialisation du logiciel SDK Push pour les applications iOS
{: #enable-push-ios-notifications-install}

Pour un projet Xcode existant, vous pouvez configurer le logiciel SDK du client Bluemix Mobile Services à l'aide de l'outil de gestion des dépendances CocoaPods. Vous pouvez aussi installer le logiciel SDK manuellement.

**Remarque** : Pour afficher le fichier Readme Swift Push, accédez à https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master

##Installation de CocoaPods

1. Installez CocoaPods en exécutant la commande suivante sur votre terminal Mac :
```
$ sudo gem install cocoapods
```
2. Entrez la commande ci-dessous dans le terminal pour initialiser CocoaPods. Prenez soin d'exécuter cette commande dans le répertoire où se trouve votre Xcode. La commande `pod init` permet de créer un titre de fichier.  
```
$ pod init
```
3. Dans le fichier Pod généré, ajoutez les dépendances de logiciel SDK dont vous avez besoin. Copiez le fichier Pod suivant :

   Objective-C

    ```
    source 'https://github.com/CocoaPods/Specs.git'
	Copiez la liste suivante en l'état et supprimez les dépendances dont vous n'avez pas besoin
	pod 'IMFCore'
	pod 'IMFPush'
	```

   Swift

	```
	source 'https://github.com/CocoaPods/Specs.git'
	// Copy the following list as is and remove the dependencies you do not need.
	use_frameworks!

	target 'MyApp' do
	    platform :ios, '8.0'
	    pod 'BMSCore'
	    pod 'BMSPush'
	end
	```
3. Depuis le terminal, accédez au dossier de votre projet et installez des dépendances avec la commande suivante :
```
$ pod update
```
Cette commande installe vos dépendances et crée un espace de travail Xcode.  **Remarque** : Prenez soin de toujours ouvrir le nouvel espace de travail Xcode au lieu du fichier de projet Xcode d'origine :
	```
	$ open App.xcworkspace
	```
Cet espace de travail contient votre projet d'origine et le projet Pods contenant vos dépendances. Si
vous voulez modifier un dossier source Bluemix Mobile Services, vous le trouverez dans votre projet
Pods, sous `Pods/yourImportedSourceFolder`. Par exemple :`Pods/IMFGoogleAuthentication`.

##Utilisation d'infrastructures et de dossiers source importés

Référencez le logiciel SDK dans votre code.


### Objective-C

Ecrivez des directives #import pour les en-têtes pertinents, par exemple :

```
//Objective-C
#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**Remarque** : La mise à jour de votre projet Pods à l'aide des commandes CocoaPods `pod install` ou `pod update` peut remplacer les dossiers source Bluemix Mobile Services. Si
vous voulez conserver vos versions personnalisées des fichiers d'origine, prenez soin de les sauvegarder avant d'entrer l'une de ces commandes.

###Swift

**Eléments prérequis**

- iOS 8.0 ou version ultérieure
- Xcode 7


Ecrivez des directives #import pour les en-têtes pertinents, par exemple :

```
//swift
import BMSCore
import BMSPush
```


##Paramètres de génération

Accédez à **Xcode > Build Settings > Build Options** et affectez à l'option Set Enable Bitcode la valeur **No**.

**Attention** : Depuis iOS 9, des modifications apportées à la fonction App Transport Security (ATS) peuvent avoir un impact sur la façon dont vous gérez le processus d'authentification. Les articles de blogue suivants contiennent d'autres informations sur les modifications : [ATS and Bitcode in iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) et [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)




# Initialisation du logiciel SDK Push pour les applications iOS
{: #enable-push-ios-notifications-initialize}

Le code d'initialisation se trouve généralement dans le délégué d'application de l'application iOS.
Cliquez sur le lien **Options pour application mobile** dans le tableau de bord de votre application Bluemix pour obtenir la route
de l'application et l'identificateur global unique.

##Initialisation du logiciel SDK de base

###Objective-C

```
// Initialize the SDK for Object-C with IBM Bluemix GUID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```

###Swift

```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstance

myBMSClient.initializeWithBluemixAppRoute("BluemixAppRoute", bluemixAppGUID: "APPGUID", bluemixRegion:"Location where your app Hosted")
myBMSClient.defaultRequestTimeout = 10.0 // Timput in seconds
```


##Initialisation du logiciel SDK Push du client

###Objective-C

```
//Initialize client Push SDK for Objective-C
IMFPushClient _pushService = [IMFPushClient sharedInstance];
```

###Swift

```
//Initialize client Push SDK for Swift
let push = BMSPushClient.sharedInstance
```

## Route, identificateur global unique et région Bluemix

**appRoute**

Spécifie la route qui a été affectée à l'application serveur que vous avez créée dans Bluemix.

**GUID**

Spécifie la clé unique qui a été affectée à l'application que vous avez créée dans Bluemix. Cette
valeur est sensible à la casse.

**bluemixRegionSuffix**

Indique l'emplacement où l'appli est hébergée. Le paramètre `bluemixRegion` spécifie le déploiement Bluemix que vous utilisez. ous pouvez définir cette valeur avec une propriété statique `BMSClient.REGION` et utiliser l'une des trois valeurs suivantes :

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY




# Enregistrement d'applications et d'appareils iOS
{: #enable-push-ios-notifications-register}


Une application doit être enregistrée auprès d'APNS pour pouvoir recevoir des notifications distantes. Cet
enregistrement s'effectue généralement après l'installation de l'application sur un appareil. Une fois que le jeton d'appareil généré par APNS a
été reçu par l'application, il doit être transmis au service Push Notifications.

Pour enregistrer les applications et les appareils iOs :

1. Créez une application de back end
2. Transmettez le jeton au service de notifications push


##Créez une application de back end

Créez une application de back end dans la section Conteneurs boilerplate du catalogue Bluemix, qui lie automatiquement le service Push à cette application. Si vous avez déjà créé une application de
back end, veillez à lier l'application au service de notifications push.

###Objective-C

```
	//Pour Objective-C
	- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	if ([[[UIDevice currentDevice] systemVersion] floatValue] >= 8.0){
	    [[UIApplication sharedApplication] registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge) categories:categories]];
	    [[UIApplication sharedApplication] registerForRemoteNotifications];
	    }
	    else{
	    [[UIApplication sharedApplication] registerForRemoteNotificationTypes:
	    (UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)];
	    }
	    return YES;
	}
```

###Swift

```
	//For Swift
	func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
		let notificationTypes: UIUserNotificationType = UIUserNotificationType.Badge | UIUserNotificationType.Alert | UIUserNotificationType.Sound
		let notificationSettings: UIUserNotificationSettings = UIUserNotificationSettings(forTypes: notificationTypes, categories: categories)
		application.registerUserNotificationSettings(notificationSettings)
		application.registerForRemoteNotifications()
	}
```

##Transmettez le jeton au service de notifications push

Une fois reçu le jeton envoyé par le service APNS, transmettez-le au service de notifications push par le biais de la méthode `registerDevice:withDeviceToken`.

###Objective-C

```
//Pour Objective-C
-( void) application:( UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:( NSData *)deviceToken{

   IMFClient *client = [IMFClient sharedInstance];

 [client initializeWithBackendRoute: @"your-backend-route-here" backendGUID: @"Your-backend-GUID-here"];


 // get Push instance
IMFPushClient* push = [IMFPushClient sharedInstance];
[push registerDeviceToken:deviceToken completionHandler:^(IMFResponse *response,  NSError *error) {
   if (error){
     [ self  updateMessage:error .description];
  }  else {
    [ self updateMessage:response .responseJson .description];
}
}];
```

###Swift

Une fois reçu le jeton envoyé par le service APNS, transmettez-le au service de notifications push par le biais de la méthode `didRegisterForRemoteNotificationsWithDeviceToken`.

```
func application (application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   let push =  BMSPushClient.sharedInstance
   push.registerDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
        if error.isEmpty {
            print( "Response during device registration : \(response)")
            print( "status code during device registration : \(statusCode)")
        }
        else{
            print( "Error during device registration \(error) ")
            Print( "Error during device registration \n  - status code: \(statusCode) \n Error :\(error) \n")
        }
    }

}
```



# Réception de notifications push sur des appareils iOS
{: #enable-push-ios-notifications-receiving}

Recevez des notifications push sur des appareils iOS.

##Objective-C
Pour recevoir des notifications push sur des appareils iOS, ajoutez la méthode Objective-C suivante au délégué d'application de votre application :

```
// For Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
}
```

##Swift
Pour recevoir des notifications push sur des appareils iOS, ajoutez la méthode Swift suivante au délégué d'application de votre application :

```
 // For Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       //UserInfo dictionary will contain data sent from the server
   }

```



# Envoi de notifications push de base
{: #push-send-notifications}

Une fois que vous avez développé vos applications, vous pouvez envoyer des notifications push de base (sans utiliser de balise, de badge, de
contenu supplémentaire ou de fichier son).


Envoi de notifications push de base.

1. Dans **Sélectionner les utilisateurs concernés**, sélectionnez l'une des options suivantes : **Tous les terminaux**, ou par plateforme : **Les appareils iOS uniquement** ou **Les appareils Android uniquement**.

	**Remarque** : Lorsque vous sélectionnez l'option **Tous les terminaux**, tous les appareils qui ont été abonnés à des notifications push reçoivent votre notification.

	![Ecran Notifications](images/tag_notification.jpg)

2. Dans la zone **Créez votre notification**, entrez votre message, puis cliquez sur **Envoyer**.
3. Vérifiez que vos appareils ont reçu votre notification.

	La capture d'écran suivante présente une boîte d'alerte relative à une notification push s'exécutant au premier plan sur un appareil Android et iOS.
	![Notification push qui s'exécute au premier plan sur un appareil Android](images/Android_Screenshot.jpg)

	![Notification push qui s'exécute au premier plan sur un appareil iOS](images/iOS_Screenshot.jpg)

	La capture d'écran suivante présente une notification push qui s'exécute en arrière-plan sur un appareil Android.
	![Notification push qui s'exécute en arrière-plan sur un appareil Android](images/background.jpg)




# Etapes suivantes
{: #next_steps_tags}

Une fois que vous avez configuré les notifications de base, vous pouvez configurer des notifications basées sur des balises et des options
avancées.

Ajoutez ces fonctions du service de notifications push à votre application.
Pour utiliser des notifications basées sur les balises, voir [Notifications basées sur les balises](c_tag_basednotifications.html).
Pour utiliser des options de notification avancées, voir [Notifications push avancées](t_advance_notifications.html).
