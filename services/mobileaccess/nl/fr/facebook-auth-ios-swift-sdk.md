---

copyright:
  years: 2016

---
{:screen: .screen}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}

# Activation de l'authentification Facebook pour les applications iOS (SDK Swift)
{: #facebook-auth-ios}

Dernière mise à jour : 1er août 2016
{: .last-updated}

Pour utiliser Facebook comme fournisseur d'identité dans vos applications iOS, ajoutez et configurez la plateforme iOS pour votre application Facebook.
{:shortdesc}

## Avant de commencer
{: #facebook-auth-ios-before}
 Vous devez disposer des éléments suivants :
* Un projet iOS qui est configuré pour fonctionner avec CocoaPods. Pour plus d'informations, voir **Installation de CocoaPods** dans [Configuration du SDK Swift iOS](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html).  
   **Remarque :** il n'est pas nécessaire d'installer le SDK client de {{site.data.keyword.amashort}} principal avant de poursuivre.
* Une instance d'une application {{site.data.keyword.Bluemix_notm}} qui est protégée par le service {{site.data.keyword.amashort}}. Pour plus d'informations sur la création d'un système de back end {{site.data.keyword.Bluemix_notm}}, voir [Initiation](index.html).
* Une application Facebook sur le site Facebook for Developers. 


**Important :** il n'est pas nécessaire d'installer séparément le SDK Facebook (`com.facebook.FacebookSdk`). Celui-ci s'installe automatiquement avec {{site.data.keyword.amashort}} `BMSFacebookAuthentication`. Vous pouvez sauter l'étape relative à l'**ajout du SDK Facebook à votre projet Xcode** quand
vous ajoutez ou configurez votre application sur le site Facebook for Developers.

**Remarque :** Bien que que le SDK Objective-C reste complètement pris en charge et soit toujours considéré comme le SDK principal pour
{{site.data.keyword.Bluemix_notm}} Mobile Services, il est envisagé de le retirer plus tard dans l'année et de le remplacer par le nouveau
SDK
Swift.
## Configuration d'une application Facebook pour la plateforme iOS
{: #facebook-auth-ios-config}
Sur le site Facebook for Developers :

1. Connectez-vous à votre compte.
1. Vérifiez que la plateforme iOS a été ajoutée à votre application. Lorsque vous ajoutez ou configurez la plateforme iOS, d'autres informations sont fournies
sur les étapes suivantes.

1. Entrez l'ID de bundle (*bundleId*) de votre application iOS. Pour trouver l'ID *bundleId*, recherchez la valeur de **Bundle Identifier (ID de bundle)** dans le fichier `info.plist` ou dans l'onglet **General** du projet Xcode.

  **Astuce** : Vous pouvez activer le suffixe de schéma d'URL et l'authentification unique (SSO) si vous prévoyez d'utiliser ces fonctions.

1. Cliquez sur **Save Settings (Sauvegarder les paramètres)**.

## Configuration de {{site.data.keyword.amashort}} pour l'authentification Facebook
{: #facebook-auth-ios-configmca}

Après avoir configuré l'ID d'application Facebook et votre application Facebook pour traiter des clients iOS, vous pouvez activer
l'authentification Facebook dans {{site.data.keyword.amashort}}.

1. Ouvrez votre appli dans le tableau de bord {{site.data.keyword.Bluemix}}.

1. Cliquez sur **Options pour application mobile** et notez la valeur de **Route** (*applicationRoute*) et
**Identificateur global unique de l'application** (*applicationGUID*). Vous aurez besoin de ces valeurs lors de l'initialisation du SDK.

1. Cliquez sur la vignette {{site.data.keyword.amashort}}. Le tableau de bord {{site.data.keyword.amashort}} se charge.

1. Cliquez sur le bouton **Configurer** dans le panneau **Facebook**.

1. Entrez l'ID d'application Facebook et cliquez sur **Sauvegarder**.

## Configuration du SDK client de {{site.data.keyword.amashort}} pour iOS
{: #facebook-auth-ios-sdk}

### Installation de CocoaPods
{: #install-cocoapods}

1. Ouvrez Terminal et lancez la commande **pod --version**. Si CocoaPods est déjà installé, son numéro de version est affiché. Vous pouvez passer à la section suivante pour installer le SDK.

1. Si CocoaPods n'est pas installé, exécutez la commande :
```
sudo gem install cocoapods
```
Pour plus d'informations, reportez-vous au [site Web CocoaPods](https://cocoapods.org/).

### Installation du SDK Swift client de {{site.data.keyword.amashort}} avec CocoaPods
{: #facebook-auth-install-swift-cocoapods}

1. Si vous n'avez pas de fichier `Podfile` dans votre projet iOS, exécutez `pod init` pour créer ce fichier.

1. Modifiez le fichier `Podfile` en lui ajoutant les lignes suivantes :

 ```
use_frameworks!
pod 'BMSFacebookAuthentication'

	```

   **Remarque :** si votre fichier Pod comporte la ligne : `pod 'BMSSecurity'`, vous devez la retirer. La nacelle
`BMSFacebookAuthentication` installe toutes les infrastructures requises.

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
	<key>CFBundleURLTypes</key>
	<array>
		<dict>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>fb{votre_ID_d'application_Facebook}</string>
			</array>
		</dict>
	</array>
	<key>FacebookAppID</key>
	<string>{votre_ID_d'application_Facebook}</string>
	<key>FacebookDisplayName</key>
	<string>{votre_nom_d'application_Facebook}</string>
	<key>LSApplicationQueriesSchemes</key>
	<array>
		<string>fbauth</string>
		<string>fbauth2</string>
	</array>
	<key>NSAppTransportSecurity</key>
	<dict>
	    <key>NSExceptionDomains</key>
	    <dict>
	        <key>facebook.com</key>
	        <dict>
	            <key>NSIncludesSubdomains</key>
	            <true/>
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

Initialisez le SDK client en passant les paramètres suivants : l'identificateur unique global de l'application `(applicationGUID) ` et la route de l'application `applicationRoute`.

Bien que ceci ne soit pas obligatoire, le code d'initialisation est souvent placé dans la méthode `application:didFinishLaunchingWithOptions`
de votre délégué d'application

1. Récupérez les valeurs de ces paramètres pour votre application. Ouvrez votre appli dans le tableau de bord {{site.data.keyword.Bluemix_notm}}. Cliquez sur **Options pour application mobile**. Les
valeurs `applicationRoute` et `applicationGUID` sont affichées dans les zones
**Route** et **Identificateur global unique de l'application**.

1. Importez la structure requise dans la classe devant utiliser le SDK client {{site.data.keyword.amashort}} en ajoutant les en-têtes suivants :

 ```swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```
2. Initialisez le SDK client.	Remplacez `<applicationRoute>` et
`<applicationGUID>` par les valeurs de **Route** et **Identificateur global unique de l'application**
de la section **Options pour application mobile** dans le tableau de bord {{site.data.keyword.Bluemix_notm}}.
Remplacez `<applicationBluemixRegion>` par la région dans laquelle votre application {{site.data.keyword.Bluemix_notm}} est hébergée. Pour afficher votre région {{site.data.keyword.Bluemix_notm}}, cliquez sur l'icône **Avatar**  ![icône Avatar](images/face.jpg "icône Avatar")  dans la barre de menu pour ouvrir le widget **Compte et support**.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<applicationBluemixRegion>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 FacebookAuthenticationManager.sharedInstance.register()
 ```

1. Avisez le SDK Facebook de l'activation de l'application et enregistrez le gestionnaire d'authentification Facebook en ajoutant le code suivant à la méthode
`application:didFinishLaunchingWithOptions` dans votre délégué d'application. Ajoutez ce code après avoir initialisé l'instance BMSClient et enregistré Facebook comme gestionnaire d'authentification.

 ```Swift
  return FacebookAuthenticationManager.sharedInstance.onFinishLaunching(application, withOptions: launchOptions)
 ```

1. Copiez le fichier `FacebookAuthenticationManager.swift` depuis les fichiers source de la nacelle `BMSFacebookAuthentication`
vers votre répertoire de projet.

1. Ajoutez le code suivant au délégué de votre appli.

 ```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		return FacebookAuthenticationManager.sharedInstance.onOpenURL(application, url: url, sourceApplication: sourceApplication, annotation: annotation)

	}
 ```

## Test de l'authentification
{: #facebook-auth-ios-testing}

Une fois que le SDK client est initialisé et que le gestionnaire d'authentification Facebook est enregistré, vous pouvez commencer à envoyer des requêtes à
votre application back end mobile.

### Avant de commencer
{: #facebook-auth-ios-testing-before}

Vous devez utiliser le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} et disposer au préalable d'une ressource protégée par {{site.data.keyword.amashort}} sur le noeud final `/protected`. Pour configurer un noeud final `/protected`, voir la rubrique [Protection des ressources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Essayez d'envoyer depuis votre navigateur une requête à un noeud final protégé de votre nouvelle application back end mobile. Ouvrez l'URL suivante :
`http://{applicationRoute}/protected`.
Par exemple : `http://my-mobile-backend.mybluemix.net/protected`
<br/>Le noeud final `/protected` d'une application back end mobile créée avec le conteneur boilerplate MobileFirst Services Starter est
protégé par {{site.data.keyword.amashort}}. Un message signalant l'interdiction d'accéder au site (`Unauthorized`) est renvoyé au navigateur. Ce message est renvoyé car ce noeud final n'est accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}.

1. A l'aide de votre application iOS, envoyez une demande au même noeud final.

	```Swift
  let protectedResourceURL = "<URL_de_votre_ressource_protégée>" // any protected resource
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
  {: screen}

1. Vous pouvez également ajouter une fonctionnalité de déconnexion en ajoutant le code suivant :

 ```
FacebookAuthenticationManager.sharedInstance.logout(callBack)
```

 Si vous appelez ce code après qu'un utilisateur se soit connecté à Facebook et qu'il tente à nouveau de s'y connecter,
il est invité à autoriser {{site.data.keyword.amashort}} à utiliser Facebook à des fins d'authentification.

 Pour changer d'utilisateur, vous devez appeler ce code et l'utilisateur doit se déconnecter de Facebook dans son navigateur.

 La transmission de `callBack` à la fonction de déconnexion est facultative. Vous pouvez également transmettre la valeur
`nil`.
