---

copyright:
 years: 2015, 2016

---

# Configuration des applications iOS pour la réception de notifications push
{: #enable-push-ios-notifications}
Dernière mise à jour : 16 août 2016
{: .last-updated}

Vous pouvez activer les applications iOS pour recevoir et envoyer des notifications push à vos périphériques.


##Installation de CocoaPods
{: #enable-push-ios-notifications-install}

Pour un projet Xcode existant, vous pouvez configurer le logiciel SDK du client Bluemix Mobile Services à l'aide de l'outil de gestion des dépendances CocoaPods. Vous pouvez aussi installer le logiciel SDK manuellement.

**Remarque** : pour afficher le fichier Readme Swift Push, accédez à https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master.



1. Installez CocoaPods en exécutant la commande suivante sur votre terminal Mac :
```
$ sudo gem install cocoapods
```
2. Entrez la commande ci-dessous dans le terminal pour initialiser CocoaPods. Assurez-vous de bien exécuter la commande depuis le répertoire où se trouve votre projet Xcode. La commande `pod init` permet de créer un titre de fichier.  
```
$ pod init
```
3. Dans le fichier Pod généré, ajoutez les dépendances de logiciel SDK requises. Copiez l'un des fichiers Pod suivants, selon vos préférences.

###Objective-C
   {: objc-sdkdependencies}

    ```
    source 'https://github.com/CocoaPods/Specs.git'
	# Copy the following list as is and remove the dependencies you do not need
	pod 'IMFCore'
	pod 'IMFPush'
	```

####Swift
   {: swift-sdkdependencies}

	```
	source 'https://github.com/CocoaPods/Specs.git'
	# Copy the following list as is and remove the dependencies you do not need.
	use_frameworks!

	target 'MyApp' do
	    platform :ios, '8.0'
	    pod 'BMSCore'
	    pod 'BMSPush'
      pod 'BMSAnalyticsAPI'
	end
	```
3. Depuis le terminal, accédez au dossier de votre projet et installez des dépendances avec la commande suivante :
```
$ pod update
```
Cette commande installe vos dépendances et crée un espace de travail Xcode.  **Remarque** : Prenez soin de toujours ouvrir le nouvel espace de travail Xcode au
lieu du fichier de projet Xcode d'origine :

	```
	$ open App.xcworkspace
	```
Cet espace de travail contient votre projet d'origine et le projet Pods contenant vos dépendances. Si
vous voulez modifier un dossier source Bluemix Mobile Services, vous le trouverez dans votre projet
Pods, sous `Pods/yourImportedSourceFolder`. Exemple : `Pods/BMSPush`.

##Carthage
{: #carthage}

Ajoutez des infrastructures à votre projet à l'aide de [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos). (https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos%29.)

1. Ajoutez des infrastructures `BMSPush` à votre fichier Cartfile :
```
github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
```
2. Exécutez la commande `carthage update`. Lorsque la construction est terminée, faites glisser `BMSPush.framework`, `BMSCore.framework` et `BMSAnalyticsAPI.framework` dans votre projet Xcode.
3. Suivez les instructions du site [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) pour terminer l'intégration.

##Utilisation d'infrastructures et de dossiers source importés
{: using-imported-frameworks}

Référencez le logiciel SDK dans votre code.


####Objective-C
{: objc-import-directives}

Ecrivez des directives #import pour les en-têtes pertinents, par exemple :

```
 //Objective-C
#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**Remarque** : La mise à jour de votre projet Pods à l'aide des commandes CocoaPods `pod install` ou `pod update` peut remplacer les dossiers source Bluemix Mobile Services. Si
vous voulez conserver vos versions personnalisées des fichiers d'origine, prenez soin de les sauvegarder avant d'entrer l'une de ces commandes.

####Swift
{: swift-import-directives}

####Prérequis
{: prerequisites}

- iOS 8.0 ou version ultérieure
- Xcode 7


Ecrivez des directives #import pour les en-têtes pertinents, par exemple :

```
//swift
import BMSCore
import BMSPush
```
**Attention** : our afficher le fichier Readme Swift Push, accédez à  [Readme](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master)

##Paramètres de génération
{: build-settings}

Accédez à **Xcode > Build Settings > Build Options** et affectez à l'option Set Enable Bitcode la valeur **No**.

**Attention** : Depuis iOS 9, des modifications apportées à la fonction App Transport Security (ATS) peuvent avoir un impact sur la façon dont vous gérez le processus d'authentification. Les articles de blogue suivants contiennent d'autres informations sur les modifications : [ATS and Bitcode in iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) et [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)




## Initialisation du logiciel SDK Push pour les applications iOS
{: #enable-push-ios-notifications-initialize}

Le code d'initialisation se trouve généralement dans le délégué d'application de l'application iOS. Cliquez sur le lien **Options pour application mobile** dans votre tableau de bord Push pour obtenir la route de l'application et l'identificateur global unique.

###Initialisation du logiciel SDK de base
{: Initializing-the-core-sdk}

####Objective-C
{: objc-initialize-core-sdk}

```
// Initialize the SDK for Object-C with IBM Bluemix GUID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```

####Swift
{: swift-initialize-core-sdk}

```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstance
myBMSClient.initializeWithBluemixAppRoute("BluemixAppRoute", bluemixAppGUID: "APPGUID", bluemixRegion:"Location where your app Hosted")
myBMSClient.defaultRequestTimeout = 10.0 // Timput in seconds
```

### Route, identificateur global unique et région Bluemix
{: route-guid-bluemix-region}

####appRoute
{: ios-approute}

Spécifie la route qui a été affectée à l'application serveur que vous avez créée dans Bluemix.

####identificateur_global_unique
{: ios-guid}

Spécifie la clé unique qui a été affectée à l'application que vous avez créée dans Bluemix. Cette
valeur est sensible à la casse.

####bluemixRegionSuffix
{: ios-bluemixRegionSuffix}

Indique l'emplacement où l'appli est hébergée. Le paramètre `bluemixRegion` spécifie le déploiement Bluemix que vous utilisez. ous pouvez définir cette valeur avec une propriété statique `BMSClient.REGION` et utiliser l'une des trois valeurs suivantes :

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

####AppGUID
{: ios-AppGUID}

Spécifie la clé AppGUID unique qui a été affectée au service Push Notifications que vous avez créé dans Bluemix.

###Initialisation du logiciel SDK Push du client
{: initializing-the-client-Push-SDK}

####Objective-C
{: objc-initialize-push-sdk}

```
//Initialize client Push SDK for Objective-C
IMFPushClient *push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID"];

```

####Swift
{: swift-initialize-push-sdk}

```
//Initialize client Push SDK for Swift
let push = BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID")

```



## Enregistrements d'applications et de périphériques iOS
{: #enable-push-ios-notifications-register}


Une application doit être enregistrée auprès d'APNS pour pouvoir recevoir des notifications distantes, après installation sur un périphérique. Une fois que le jeton de périphérique généré par APNs est reçu par l'application, il doit être transmis au service {{site.data.keyword.mobilepushshort}}.

Pour enregistrer les applications et les périphériques iOS :

1. Créez une application de back end
2. Transmettez le jeton à {{site.data.keyword.mobilepushshort}}


###Créez une application de back end
{: create-a-backend-app}

Créez une application de back end dans la section Conteneurs boilerplate du catalogue Bluemix®, qui lie automatiquement le service {{site.data.keyword.mobilepushshort}} à cette application. Si vous avez déjà créé une application de backend, veillez à lier l'application au service {{site.data.keyword.mobilepushshort}}.

####Objective-C
{: objc-backendapp-code}

```
	//For Objective-C
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

####Swift
{: swift-backendapp-code}

```
	//For Swift
	func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
		let settings = UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound], categories: nil) UIApplication.sharedApplication().registerUserNotificationSettings(settings) UIApplication.sharedApplication().registerForRemoteNotifications()
	}
```

###Passage de jetons à {{site.data.keyword.mobilepushshort}}
{: pass-token-push-notifications}

Une fois que le jeton envoyé par APNs a été reçu, transmettez-le à {{site.data.keyword.mobilepushshort}} dans le cadre de la méthode `registerWithDeviceToken`.

####Objective-C
{: objc-token}

```
//For Objective-C
-( void) application:( UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:( NSData *)deviceToken{

   IMFClient *client = [IMFClient sharedInstance];

 [client initializeWithBackendRoute: @"your-backend-route-here" backendGUID: @"Your-backend-GUID-here"];


 // get Push instance
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID"];
[push registerWithDeviceToken:deviceToken completionHandler:^(IMFResponse *response,  NSError *error) {
   if (error){
     NSLog(@"%@",error.description);
  }  else {
    NSLog(@"%@",response.responseJson.description);
}
}];
```

####Swift
{: swift-token}

Une fois que le jeton envoyé par APNS a été reçu, transmettez-le au service de notification push dans le cadre de la méthode `didRegisterForRemoteNotificationsWithDeviceToken`.

```
func application (application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   let push =  BMSPushClient.sharedInstance
  push.initializeWithAppGUID("appGUID")
  push.registerWithDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
  push.initializeWithPushAppGUID("pushAppGUID")
   push.registerWithDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
        if error.isEmpty {
            print( "Response during device registration : \(response)")
            print( "status code during device registration : \(statusCode)")
        }
        else{
            print( "Error during device registration \(error) ")
            print( "Error during device registration \n  - status code: \(statusCode) \n Error :\(error) \n")
        }
    }

}
```



## Réception de notifications push sur des périphériques iOS
{: #enable-push-ios-notifications-receiving}

Recevez des notifications push sur des périphériques iOS.

####Objective-C
{: objc-receive-push-notifications}

Pour recevoir des notifications push sur des périphériques iOS, ajoutez la méthode Objective-C suivante au délégué d'application de votre application :

```
// For Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
}
```

####Swift
{: swift-receive-push-notifications}
Pour recevoir des notifications push sur des périphériques iOS, ajoutez la méthode Swift suivante au délégué d'application de votre application :

```
 // For Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       //UserInfo dictionary will contain data sent from the server
   }

```



## Envoi de notifications push de base
{: #send}

Une fois que vous avez développé vos applications, vous pouvez envoyer des notifications push de base (sans utiliser de balise, de badge, de
contenu supplémentaire ou de fichier son).


1. Dans la zone **Choisir des destinataires**, sélectionnez l'un des publics suivants :
**Tous les terminaux** ou par plateforme : **Terminaux iOS seulement** ou
**Terminaux Android seulement**. 

	**Remarque** : Lorsque vous sélectionnez l'option **Tous les périphériques**, tous les périphériques qui sont abonnés à des notifications push recevront votre notification.

![Ecran Notifications](images/tag_notification.jpg)

2. Dans la zone **Create your Notification**, entrez votre message, puis cliquez sur **Send**.
3. Vérifiez que vos périphériques ont reçu la notification. L'image suivante présente une boîte de dialogue d'alerte qui traite une notification de type {{site.data.keyword.mobilepushshort}} qui s'exécute au premier plan et en arrière-plan sur un périphérique iOS.

	![Notification push qui s'exécute au premier plan sur un périphérique Android](images/iOS_Foreground.jpg)

![Notification push qui s'exécute au premier plan sur un périphérique iOS](images/iOS_Screenshot.jpg)




## Etapes suivantes
{: #next_steps_tags}

Une fois que vous avez configuré des notifications de base, vous pouvez configurer des notifications basées sur les balises et des options
avancées.

Ajoutez ces fonctions du service Notifications push à votre application.
Pour utiliser des notifications basées sur les balises, voir [Notifications basées sur les balises](c_tag_basednotifications.html).
Pour utiliser des options de notification avancées, voir [Notifications push avancées](t_advance_notifications.html).
