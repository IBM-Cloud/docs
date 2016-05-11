---

Copyright : 2016

---

# Activation de l'authentification Facebook dans les applications iOS (SDK Swift)
{: #facebook-auth-ios}

Pour utiliser Facebook comme fournisseur d'identité dans vos applications iOS, ajoutez et configurez la plateforme iOS pour votre application Facebook.

## Avant de commencer
{: #facebook-auth-ios-before}

* Vous devez disposer d'une ressource protégée par {{site.data.keyword.amashort}} et d'un projet iOS instrumenté avec le SDK client de {{site.data.keyword.amashort}}.  Pour plus d'informations, voir [Initiation à {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) et [Configuration du SDK Swift iOS](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html).  
* Protégez manuellement votre application de back end avec le SDK serveur de {{site.data.keyword.amashort}}. Pour plus d'informations, voir [Protection des ressources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).
* Créez un ID d'application Facebook. Pour plus d'informations, voir [Acquisition d'un ID d'application Facebook sur le portail Facebook Developer](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).

## Configuration d'une application Facebook pour la plateforme iOS
{: #facebook-auth-ios-config}

1. Connectez-vous au [tableau de bord de votre application Facebook](https://developers.facebook.com/apps/).

1. Notez la valeur de **ID application** pour votre application. Vous en aurez besoin pour configurer votre projet iOS pour authentification Facebook.

1. Cliquez sur **Paramètres > Ajouter une plateforme > iOS**.

1. Entrez l'ID de bundle (*bundleId*) de votre application iOS. Pour trouver l'ID *bundleId*, recherchez la valeur de **Bundle Identifier (ID de bundle)** dans le fichier `info.plist` ou dans l'onglet **General** du projet Xcode.
**Astuce** : Vous pouvez activer le suffixe de schéma d'URL et l'authentification unique (SSO) si vous prévoyez d'utiliser ces fonctions.

1. Cliquez sur **Save Settings (Sauvegarder les paramètres)**.

## Configuration de {{site.data.keyword.amashort}} pour l'authentification Facebook
{: #facebook-auth-ios-configmca}

Après avoir configuré l'ID d'application Facebook, ainsi que votre application Facebook de manière qu'elle puisse répondre aux demandes des clients iOS, vous pouvez activer l'authentification Facebook dans {{site.data.keyword.amashort}}.

1. Ouvrez votre appli dans le tableau de bord {{site.data.keyword.Bluemix}}.

1. Cliquez sur **Options pour application mobile** et notez la valeur de **Route** (*applicationRoute*) et
**Identificateur global unique de l'application** (*applicationGUID*). Vous aurez besoin de ces valeurs lors de l'initialisation du SDK.

1. Cliquez sur la vignette {{site.data.keyword.amashort}}. Le tableau de bord {{site.data.keyword.amashort}} se charge.

1. Cliquez sur la vignette **Facebook** .

1. Entrez l'ID d'application Facebook et cliquez sur **Sauvegarder**.

## Configuration du SDK client de {{site.data.keyword.amashort}} pour iOS
{: #facebook-auth-ios-sdk}

### Installation de CocoaPods
{: #facebook-auth-cocoapods}

Le SDK client de {{site.data.keyword.amashort}} est distribué avec CocoaPods, un gestionnaire de dépendances pour les projets iOS. CocoaPods télécharge automatiquement les artefacts à partir des référentiels et les met à la disposition de votre application iOS.

1. Ouvrez Terminal et lancez la commande `pod --version`. Si CocoaPods est déjà installé, le numéro de version est affiché. Vous pouvez passer à la section suivante de ce tutoriel.

1. Installez CocoaPods en exécutant `sudo gem install cocoapods`. Reportez-vous au [site Web CocoaPods](https://cocoapods.org/) si vous avez besoin d'autres instructions.

1. Fermez XCode.

1. Ouvrez un terminal et utilisez la commande `cd` pour accéder à votre répertoire de projet.

1.  Exécutez `pod init`.

### Installation du SDK Swift client {{site.data.keyword.amashort}} avec CocoaPods
{: #facebook-auth-install-swift-cocoapods}

1. Dans votre projet iOS, modifiez le fichier `Podfile` en lui ajoutant les lignes suivantes :

 ```
use_frameworks!
pod 'BMSFacebookAuthentication'
	```
 **Astuce :** Vous pouvez ajouter `use_frameworks!` à votre cible Xcode au lieu du Podfile.

1. Sauvegardez le fichier `Podfile` et exécutez la commande `pod install` à partir de la ligne de commande. CocoaPods installe les dépendances. La progression et les composants ajoutés s'affichent.

 **Important** : Vous devez à présent ouvrir votre projet en utilisant le fichier `xcworkspace` généré par CocoaPods. Son nom est généralement `{your-project-name}.xcworkspace`.  

1. Exécutez `open {your-project-name}.xcworkspace` depuis la ligne de commande pour ouvrir l'espace de travail de votre projet iOS.

### Configuration de votre projet iOS pour authentification Facebook
{: #facebook-auth-ios-configproject}

1. Localisez le fichier `info.plist`, généralement situé sous le dossier `Supporting files` de votre projet Xcode.

1. Configurez l'intégration Facebook en ajoutant les propriétés suivantes à votre fichier `info.plist` :

   ![image](images/ios-facebook-infoplist-settings.png)

   Mettez à jour les propriétés de schéma d'URL et d'ID d'appli Facebook avec votre ID d'application Facebook.

   Vous pouvez aussi mettre à jour le fichier `info.plist` en cliquant avec le bouton droit, en sélectionnant **Open as (Ouvrir en tant que) > Source Code (Code source)** et en ajoutant le code XML suivant :

   ```XML
	<key>CFBundleURLTypes</key> 	<array> 		<dict> 			<key>CFBundleURLSchemes</key> 			<array>
				<string>fb{votre_ID_application_facebook}</string> 			</array> 		</dict> 	</array>
	<key>FacebookAppID</key> 	<string>{votre_ID_application_facebook}</string> 	<key>FacebookDisplayName</key>
	<string>{votre_nom_application_facebook}</string> 	<key>LSApplicationQueriesSchemes</key> 	<array>
		<string>fbauth</string> 		<string>fbauth2</string> 	</array>
	<key>NSAppTransportSecurity</key> 	<dict> 	    <key>NSExceptionDomains</key> 	    <dict> 	
<key>facebook.com</key> 	        <dict> 	            <key>NSIncludesSubdomains</key> 	            <true/>                
	            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
	            <false/>
	        </dict>
	        <key>fbcdn.net</key>
	        <dict>
	            <key>NSIncludesSubdomains</key>
	            <true/>
	            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
	            <false/>
	        </dict>
	        <key>akamaihd.net</key>
	        <dict>
	            <key>NSIncludesSubdomains</key>
	            <true/>
	            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
	            <false/>
	        </dict>
	    </dict>
	</dict>
```
   Mettez à jour les propriétés de schéma d'URL et d'ID d'appli Facebook avec votre ID d'application Facebook. Mettez à jour le nom d'affichage
Facebook (FacebookDisplayName) avec le nom de votre application Facebook.

    **Important** : Veillez à ne pas remplacer les propriétés existantes du fichier `info.plist`. Si certaines propriétés se chevauchent, vous devez les fusionner manuellement. Pour plus d'informations, voir [Configure Xcode Project](https://developers.facebook.com/docs/ios/getting-started/) et [Preparing Your Apps for iOS9](https://developers.facebook.com/docs/ios/ios9).

## Initialisation du SDK Swift client {{site.data.keyword.amashort}}
{: #facebook-auth-ios-initalize-swift}

Initialisez le SDK en passant les paramètres suivants : l'identificateur unique global de l'application (`applicationGUID`) et la route de l'application (`applicationRoute`).

Bien que ceci ne soit pas obligatoire, le code d'initialisation est souvent placé dans la méthode
`application:didFinishLaunchingWithOptions` de votre délégué d'application

1. Récupérez les valeurs de ces paramètres pour votre application. Ouvrez votre appli dans le tableau de bord {{site.data.keyword.Bluemix_notm}}. Cliquez sur **Options pour application mobile**. Les valeurs `applicationRoute` et `applicationGUID` sont affichées dans les zones **Route** et
**Identificateur global unique de l'application**.

1. Importez l'infrastructure requise dans la classe qui doit utiliser le SDK client de {{site.data.keyword.amashort}} en ajoutant les en-têtes suivants :

 ```swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```
2. Initialisez le logiciel SDK client.	Remplacez `<applicationRoute>` et `<applicationGUID>` par les valeurs de
**Route** et **Identificateur global unique de l'application** de la section **Options pour application
mobile** dans le tableau de bord {{site.data.keyword.Bluemix_notm}}.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 FacebookAuthenticationManager.sharedInstance.register()
 ```

1. Signalez au SDK Facebook l'activation de l'application et enregistrez le gestionnaire d'authentification Facebook en ajoutant le code suivant à la méthode
`application:didFinishLaunchingWithOptions` dans votre délégué d'application. Ajoutez ce code juste après avoir initialisé l'instance
BMSClient et enregistré Facebook comme gestionnaire d'authentification.

 ```Swift
  return FacebookAuthenticationManager.sharedInstance.onFinishLaunching(application, withOptions: launchOptions)
 ```

1. Copiez dans votre répertoire de projet le fichier `FacebookAuthenticationManager.swift` depuis les fichiers pod source
`BMSFacebookAuthentication`.

1. Ajoutez le code suivant au délégué de votre appli.

 ```Swift
	func application(application: UIApplication, openURL url: NSURL, 					sourceApplication: String?, annotation: AnyObject) -> Bool {

		return FacebookAuthenticationManager.sharedInstance.onOpenURL(application, url: url, sourceApplication: sourceApplication, annotation: annotation)

	}
 ```

## Test de l'authentification
{: #facebook-auth-ios-testing}

Lorsque le SDK client est initialisé et que le gestionnaire d'authentification Facebook est enregistré, vous pouvez commencer à envoyer des demandes à votre système de back end mobile.

### Avant de commencer
{: #facebook-auth-ios-testing-before}

Vous devez utiliser le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} et disposer au préalable d'une ressource protégée par {{site.data.keyword.amashort}} sur le noeud final `/protected`. Pour configurer un noeud final `/protected`, voir la rubrique [Protection des ressources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Depuis votre navigateur, tentez d'envoyer une demande à un noeud final protégé de votre nouveau système de back end mobile. Ouvrez l'URL suivante :
`http://{applicationRoute}/protected`.
Par exemple : `http://my-mobile-backend.mybluemix.net/protected`
<br/>Le noeud final `/protected` d'un système de back end mobile qui a été créé avec le conteneur boilerplate MobileFirst Services Starter est protégé par {{site.data.keyword.amashort}}. Un message signalant l'interdiction d'accéder au site (`Unauthorized`) est renvoyé au navigateur. Ce message est renvoyé car ce noeud final n'est accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}.

1. A l'aide de votre application iOS, envoyez une demande au même noeud final.

	```Swift
 let protectedResourceURL = "<URL de votre ressource protégée>" // ressource protégée de votre choix
 let request = Request(url: protectedResourceURL , method: HttpMethod.GET)
 let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) in

  if error == nil {
     print ("response:\(response?.responseText), no error")
 } else {
     print ("error: \(error)")
 }
  }

  request.sendWithCompletionHandler(callBack)
 ```

1. Lancez votre application. Un écran de connexion à Facebook s'affiche.

   ![image](images/ios-facebook-login.png)

   Cet écran peut être légèrement différent si vous n'êtes pas connecté actuellement à Facebook.

1. Cliquez sur **OK** pour autoriser {{site.data.keyword.amashort}} à utiliser votre ID utilisateur Facebook pour l'authentification.

1. 	Lorsque votre demande aboutit, la sortie suivante figure dans la console Xcode :

 ```
 "onAuthenticationSuccess info = Optional({
     attributes =     {
     };
     deviceId = 218227041863639;
     displayName = "Don+Lon";
     isUserAuthenticated = 1;
     userId = 218227041863639;
 })
 response:Optional("Bonjour, ceci est une ressource protégée de l'application back end mobile !"), no error
 ```

1. Vous pouvez également ajouter une fonctionnalité de déconnexion en ajoutant le code suivant :

 ```
FacebookAuthenticationManager.sharedInstance.logout(callBack)
```

 Si vous appelez ce code alors que l'utilisateur était connecté via Facebook et qu'il tente à nouveau de se connecter, il est invité à autoriser
{{site.data.keyword.amashort}} à utiliser Facebook aux fins d'authentification. 

 Les utilisateurs de switch doivent appeler ce code et l'utilisateur doit se déconnecter de Facebook
dans son navigateur.

 La transmission de `callBack` à la fonction de déconnexion est facultative. Vous pouvez également transmettre la valeur
`nil`.
