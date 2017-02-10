---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

#Activation de l'envoi de {{site.data.keyword.mobilepushshort}} par les applications iOS
{: #enable-push-ios-notifications}
Dernière mise à jour : 16 janvier 2017
{: .last-updated}

Vous pouvez permettre aux applications iOS d'envoyer des {{site.data.keyword.mobilepushshort}} à vos appareils.


##Installation de CocoaPods
{: #enable-push-ios-notifications-install}

Pour un projet Xcode existant, vous pouvez configurer le logiciel SDK client des services Bluemix Mobile en utilisant l'outil de gestion des dépendances CocoaPods. Vous pouvez aussi installer le logiciel SDK manuellement.

Pour consulter le fichier Readme de Swift Push, accédez au site
[Readme ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}.



1. Installez CocoaPods en exécutant la commande suivante sur votre terminal Mac :
```$ sudo gem install cocoapods
```
	{: codeblock}
2. Entrez la commande `pod init` dans le terminal pour initialiser CocoaPods. Assurez-vous de bien exécuter la commande depuis le répertoire où se trouve votre projet Xcode. La commande `pod init` crée un fichier Pod.  
3. Dans le fichier Pod généré, ajoutez les dépendances de logiciel SDK requises. Copiez le fichier Pod suivant :
   
	```
	source 'https://github.com/CocoaPods/Specs.git'
	// Copiez la liste suivante telle quelle et supprimez les dépendances superflues.
	use_frameworks!
	target 'MyApp' do
	    platform :ios, '8.0'
	pod 'BMSCore'
	    pod 'BMSPush'
      pod 'BMSAnalyticsAPI'
	end
	```
		{: codeblock}

3. Depuis le terminal, accédez au dossier de votre projet et installez des dépendances avec la commande `pod update`.

Cette commande installe vos dépendances et crée un nouvel espace de travail Xcode.  
**Remarque** : Prenez soin de toujours ouvrir le nouvel espace de travail Xcode au
lieu du fichier de projet Xcode d'origine :
```
$ open App.xcworkspace
```
	{: codeblock}

Cet espace de travail contient votre projet d'origine et le projet Pods contenant vos dépendances. Pour modifier le dossier source des services mobiles Bluemix, vous le trouverez dans votre projet Pods, sous `Pods/yourImportedSourceFolder`. Exemple : `Pods/BMSPush`.

##Ajout d'infrastructures à l'aide de Carthage
{: #carthage}

Ajoutez des infrastructures à votre projet à l'aide de
[Carthage ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window}. Notez que Carthage dans Xcode8 n'est pas pris en charge.

1. Ajoutez des infrastructures `BMSPush` à votre fichier Cartfile :
```
github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
```
	{: codeblock}
2. Exécutez la commande `carthage update`. Lorsque la construction est terminée, faites glisser `BMSPush.framework`, `BMSCore.framework` et `BMSAnalyticsAPI.framework` dans votre projet Xcode.
3. Suivez les instructions du site [Carthage ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window} pour compléter

l'intégration.

##Configuration du logiciel SDK pour iOS
{: ios-sdk}

Installez le kit de développement de logiciels (SDK) iOS et ajoutez le code suivant au fichier **AppDelegate.swift** dans votre application. Notez
que ceci effectue également un enregistrement auprès des APN.  
```
func application(_ application: UIApplication,
didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool 
 {  
 BMSPushClient.sharedInstance.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE")
  }
```
    {: codeblock}

##Utilisation d'infrastructures et de dossiers source importés
{: using-imported-frameworks}

Référencez le logiciel SDK dans votre code. Vérifiez que les prérequis suivants sont en place.
	- iOS 8.0 ou version ultérieure	
	- Xcode 7

Ecrivez des directives `#import` pour les en-têtes pertinents, par exemple :
	```
	//swift
	import BMSCore
	import BMSPush
	```
		{: codeblock}

Pour consulter le fichier Readme de Swift Push, accédez au site
[Readme ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}.

**Remarque** : La mise à jour de votre projet Pods via les commandes CocoaPods `pod install` ou `pod update` peut remplacer les dossiers source des services Bluemix Mobile. Si
vous voulez conserver vos versions personnalisées des fichiers d'origine, prenez soin de les sauvegarder avant d'entrer l'une de ces commandes.


##Paramètres de génération
{: build-settings}

Accédez à **Xcode > Build Settings > Build Options** et affectez à l'option Set Enable Bitcode la valeur **No**.

**Attention** : Depuis iOS 9, des modifications apportées à la fonction App Transport Security (ATS) peuvent avoir un impact sur la façon dont vous gérez le processus d'authentification. Les
articles de blogue suivants fournissent des informations supplémentaires sur les modifications :
[ATS and Bitcode in iOS 9 ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/){: new_window} et
[Connect your iOS 9 app to Bluemix today ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/){: new_window}.

## Initialisation du logiciel SDK Push pour les applications iOS
{: #enable-push-ios-notifications-initialize}

Le code d'initialisation se trouve généralement dans le délégué d'application de l'application iOS. Cliquez sur le lien **Options pour application mobile** dans votre tableau de bord Push pour obtenir la route de l'application et l'identificateur global unique.

###Initialisation du logiciel SDK de base
{: Initializing-the-core-sdk}


```
// Initialisation du SDK Core pour Swift avec le GUID IBM Bluemix, la route et la région
let myBMSClient = BMSClient.sharedInstance
myBMSClient.initialize(bluemixRegion: "Location where your app is hosted.")
```
	{: codeblock}

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

- BMSClient.Region.usSouth 
- BMSClient.Region.unitedKingdom
- BMSClient.Region.sydney

####AppGUID
{: ios-AppGUID}

Spécifie la clé AppGUID unique qui a été affectée au service {{site.data.keyword.mobilepushshort}} que vous avez créé dans Bluemix.

###Initialisation du logiciel SDK Push du client
{: initializing-the-client-Push-SDK}

```
//Initialisation du SDK Push client pour Swift
let push = BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


## Enregistrement d'applications et d'appareils iOS
{: #enable-push-ios-notifications-register}


Une application doit être enregistrée auprès d'APNS pour pouvoir recevoir des notifications distantes, après installation sur un appareil. Une fois que le jeton d'appareil généré par APNS est reçu par l'application, il doit être transmis au service {{site.data.keyword.mobilepushshort}}.

Pour enregistrer les applications et les appareils iOS, vous devez :

1. Créez une application d'arrière plan.
2. Passer le jeton à {{site.data.keyword.mobilepushshort}}.


###Créez une application d'arrière plan
{: create-a-backend-app}

Créez une application d'arrière plan dans la section Boilerplates du catalogue Bluemix® , ce qui lie automatiquement le service {{site.data.keyword.mobilepushshort}} à cette application. Si
vous avez déjà créé une application dorsale, prenez soin de la lier au service {{site.data.keyword.mobilepushshort}}.


###Passage de jetons à {{site.data.keyword.mobilepushshort}}
{: pass-token-push-notifications}

Une fois que le jeton envoyé par APNS a été reçu, transmettez-le à {{site.data.keyword.mobilepushshort}} dans le cadre de la méthode `registerWithDeviceToken`.

Une fois que le jeton envoyé par APNS a été reçu, transmettez-le au service de notifications push dans le cadre de la méthode `didRegisterForRemoteNotificationsWithDeviceToken`.

```
func application (_application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data){
   let push =  BMSPushClient.sharedInstance
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
	{: codeblock}


## Réception de notifications push sur des appareils iOS
{: #enable-push-ios-notifications-receiving}


Pour recevoir des notifications push sur des appareils iOS, ajoutez la méthode Swift suivante au délégué d'application de votre application :

```
// Pour Swift
func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void)
{ //Le dictionnaire UserInfo contiendra des données envoyées depuis le serveur }
```
	{: codeblock}

## Suivi des applications push sur les unités iOS
{: ios-monitoring}

Pour surveiller le statut actuel de la notification, ajoutez la méthode Swift suivante au délégué d'application de votre
application.

```
// Envoi du statut de la notification lorsque l'application est ouverte en cliquant sur les notifications
func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any]) {
 let push =  BMSPushClient.sharedInstance
 let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 let data = respJson.data(using: String.Encoding.utf8)
 let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 let messageId:String = jsonResponse.value(forKey: "nid") as! String
    push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
      print("Send message status to the Push server")
     }
}
```
	{: codeblock}

```
// Envoi du statut de notification lorsque l'application est en mode arrière-plan.
func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
 let payLoad = ((((userInfo as NSDictionary).value(forKey: "aps") as! NSDictionary).value(forKey: "alert") as! NSDictionary).value(forKey: "body") as! NSString)
 self.showAlert(title: "Recieved Push notifications", message: payLoad)
 let push =  BMSPushClient.sharedInstance
 let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 let data = respJson.data(using: String.Encoding.utf8)
 let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 let messageId:String = jsonResponse.value(forKey: "nid") as! String
 push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
       completionHandler(UIBackgroundFetchResult.newData)
   }
}
```
	{: codeblock}


## Envoi de notifications push de base
{: #send}

Une fois que vous avez développé vos applications, vous pouvez envoyer des notifications push de base.

Pour envoyer des notifications push de base, procédez comme suit :

1. Sélectionnez **Envoyer des notifications** et rédigez un message en choisissant une option **Envoyer à**. Les options prises en charge sont **Appareil par étiquette**, **ID de l'appareil**, **ID utilisateur**, **Appareils Android**, **Appareils IOS**, **Notifications Web** et **Tous les appareils**.  
**Remarque **: si vous sélectionnez l'option **Tous les appareils**, tous les appareils qui sont abonnés à des notifications de type {{site.data.keyword.mobilepushshort}} recevront les notifications.
![Ecran Notifications](images/tag_notification.jpg)

2. Dans la zone **Message**, composez votre message. Configurez les paramètres facultatifs, selon les besoins.
3. Cliquez sur **Envoyer**.
3. Vérifiez que vos appareils ont reçu votre notification.

L'image suivante présente une boîte de dialogue d'alerte qui traite une notification de type {{site.data.keyword.mobilepushshort}} sur un appareil iOS.

![Notification push qui s'exécute au premier plan sur un appareil iOS](images/iOS_Screenshot.jpg) 

### Paramètres facultatifs pour l'envoi de notifications
{: #send_ios_otpional_setting}

Vous pouvez personnaliser les paramètres de type {{site.data.keyword.mobilepushshort}} pour l'envoi de notifications vers des appareils iOS. Les options de personnalisation facultative suivantes sont prises en charge.

- **Badge** : indique le nombre qui s'affiche sur le badge d'application. La valeur par défaut, zéro (0), n'affiche pas de badge. 
- **Son** : indique le clip audio à exécuter à réception d'une notification. Prend en charge le fichier par défaut ou utilise le nom de la ressource audio intégré dans l'application.
- **Contenu supplémentaire** : spécifie les valeurs de contenu personnalisées pour vos notifications.

##Activation des notifications interactives

Vous pouvez à présent enrichir vos notifications iOS en leur ajoutant plus de détails, comme une image, une mappe ou un bouton de réponse en activant les notifications interactives. Ceci
fournit des informations de contexte supplémentaires aux utilisateurs, ainsi que la possibilité de lancer une action immédiate sans quitter le contexte en cours.  

Pour activer les notifications interactives, utilisez le code suivant :

```
// Ceci définit l'action du bouton.
let actionOne = BMSPushNotificationAction(identifierName: "ACCEPT", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
 let actionTwo = BMSPushNotificationAction(identifierName: "DECLINE", buttonTitle: "Decline", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
```
	{: codeblock}
```
// Ceci définit la catégorie pour les boutons
let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
```
	{: codeblock}
```
// Ceci met à jour l'enregistrement en incluant le buttonsPass de la catégorie définie dans iOS BMSPushClientOptions
let notificationOptions = BMSPushClientOptions(categoryName: [category])
let push = BMSPushClient.sharedInstance
push.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE", options: notificationOptions)
```
	{: codeblock}

Pour envoyer une notification interactive, procédez comme suit :

1. Dans la section Compose, pour la liste déroulante Envoyer à, sélectionnez **Appareils IOS**.
2. Entrez le message de notification que vous voudrez peut-être envoyer.
3. Dans la section Paramètres facultatifs, sélectionnez **Mobile** et cliquez sur **iOS**.
4. Dans la liste déroulante Type, sélectionnez **Mixte**.
5. Dans la zone Catégorie, spécifiez le type de notification que vous avez défini dans votre application. 

![Notification interactive pour iOS](images/push_ios_notification_interactive.jpg) 

## Etapes suivantes
{: #next_steps_tags}

Une fois que vous avez configuré les notifications de base, vous pouvez configurer des notifications basées sur des balises et des options
avancées.

Ajoutez ces fonctions du service de notifications push à votre application.
Pour utiliser des notifications basées sur les balises, voir [Notifications basées sur les balises](c_tag_basednotifications.html).
Pour utiliser des options de notification avancées, voir [Activation des notifications push avancées](t_advance_badge_sound_payload.html).
