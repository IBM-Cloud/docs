---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Activation de l'authentification Facebook pour les applications iOS (SDK Swift)
{: #facebook-auth-ios}

Pour utiliser Facebook comme fournisseur d'identité dans vos applications iOS {{site.data.keyword.amafull}}, ajoutez et configurez la plateforme iOS pour votre application Facebook.
{: shortdesc}

## Avant de commencer
{: #before-you-begin}

Vous devez disposer des éléments suivants :

* Une instance d'un service {{site.data.keyword.amafull}} et une application {{site.data.keyword.Bluemix_notm}}. Pour plus d'informations sur la création d'un système de back end {{site.data.keyword.Bluemix_notm}}, voir [Initiation](index.html).
* L'URL de votre application back-end (**Route de l'application**). Vous aurez besoin de ces valeurs pour envoyer des requêtes aux noeuds finaux protégés de votre application back end.
* Valeur de votre **TenantID**. Ouvrez votre service dans le tableau de bord de {{site.data.keyword.amashort}}. Cliquez sur le bouton **Options pour application mobile**. La valeur `tenantId` (qui porte également le nom d'`appGUID`) est affichée dans la zone **App GUID / TenantId**. Vous aurez besoin de cette valeur pour initialiser le Gestionnaire des autorisations.
* Votre **région** {{site.data.keyword.Bluemix_notm}}. Vous pouvez trouver votre région {{site.data.keyword.Bluemix_notm}} actuelle dans l'en-tête, en regard de l'icône **Avatar**![icône Avatar](images/face.jpg "icône Avatar"). La valeur de région qui apparaît doit être l'une des suivantes : `US South`, `United Kingdom` ou `Sydney` et correspondre aux valeurs SDK requises dans le SDK Swift : `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` ou `BMSClient.Region.sydney`. Vous aurez besoin de cette valeur pour initialiser le client {{site.data.keyword.amashort}}.
* Un projet iOS qui est configuré pour fonctionner avec CocoaPods.  Pour plus d'informations, voir **Installation de CocoaPods** dans [Configuration du SDK Swift iOS](getting-started-ios-swift-sdk.html).  
   **Remarque :** il n'est pas nécessaire d'installer le SDK client de {{site.data.keyword.amashort}} principal avant de poursuivre.
* Une application Facebook sur le site Web [Facebook for Developers ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developers.facebook.com "Icône de lien externe"){: new_window}.

**Important :** il n'est pas nécessaire d'installer séparément le SDK Facebook (`com.facebook.FacebookSdk`). Celui-ci s'installe automatiquement avec {{site.data.keyword.amashort}} `BMSFacebookAuthentication`. Vous pouvez sauter l'étape relative à l'**ajout du SDK Facebook à votre projet Xcode** quand
vous ajoutez ou configurez votre application sur le site Facebook for Developers.

## Configuration d'une application Facebook pour la plateforme iOS
{: #facebook-auth-ios-config}

Sur le site Facebook for Developers :

1. Connectez-vous à votre compte sur le site [Facebook for Developers ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developers.facebook.com "Icône de lien externe"){: new_window}.

1. Assurez-vous que la plateforme iOS a été ajoutée à votre appli. Lorsque vous ajoutez ou configurez la plate-forme iOS, vous devez fournir le **bundleId** de votre application iOS. Pour trouver l'ID **bundleId**, recherchez la valeur de **Bundle Identifier (ID de bundle)** dans le fichier `info.plist` ou dans l'onglet **General** du projet Xcode.

  **Astuce** : Vous pouvez activer le suffixe de schéma d'URL et l'authentification unique (SSO) si vous prévoyez d'utiliser ces fonctions.

1. Cliquez sur **Save Settings (Sauvegarder les paramètres)**.

## Configuration de {{site.data.keyword.amashort}} pour l'authentification Facebook
{: #facebook-auth-ios-configmca}

Après avoir configuré l'ID d'application Facebook et votre application Facebook pour servir les clients iOS, vous pouvez activer l'authentification Facebook dans votre service {{site.data.keyword.amashort}}.

1. Ouvrez votre service dans le tableau de bord {{site.data.keyword.amashort}}.
1. Dans l'onglet **Gérer**, activez **Autorisation**.
1. Développez la section **Facebook**.
1. Ajoutez l'**ID d'application Facebook** et cliquez sur **Sauvegarder**.

## Configuration du SDK client de {{site.data.keyword.amashort}} pour iOS
{: #facebook-auth-ios-sdk}

### Installation de CocoaPods
{: #install-cocoapods}

1. Ouvrez Terminal et lancez la commande **pod --version**. Si CocoaPods est déjà installé, son numéro de version est affiché. Vous pouvez passer à la section suivante pour installer le SDK.

1. Si CocoaPods n'est pas installé, exécutez la commande :

   ```
   sudo gem install cocoapods
   ```
   {: codeblock}

Pour plus d'informations, reportez-vous au [site Web CocoaPods ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cocoapods.org/ "Icône de lien externe"){: new_window}.

### Installation du SDK Swift client de {{site.data.keyword.amashort}} avec CocoaPods
{: #facebook-auth-install-swift-cocoapods}

1. Si vous n'avez pas de fichier `Podfile` dans votre projet iOS, exécutez `pod init` pour créer le fichier.

1. Modifiez le fichier `Podfile` en lui ajoutant les lignes suivantes :

   ```
   use_frameworks!
   pod 'BMSFacebookAuthentication'
   ```
   {: codeblock}

   **Remarque :** si votre fichier Pod comporte la ligne : `pod 'BMSSecurity'`, vous devez la retirer. La nacelle
`BMSFacebookAuthentication` installe toutes les infrastructures requises.

   **Astuce :** Vous pouvez ajouter `use_frameworks!` à votre cible Xcode au lieu du Podfile.

1. Sauvegardez le fichier `Podfile` et exécutez la commande `pod install` à partir de la ligne de commande. CocoaPods installe les dépendances. La progression et les composants ajoutés s'affichent.

   **Important** : Vous devez à présent ouvrir votre projet en utilisant le fichier `xcworkspace` généré par CocoaPods. Son nom est généralement `{your-project-name}.xcworkspace`.  

1. Exécutez `open {your-project-name}.xcworkspace` depuis la ligne de commande pour ouvrir l'espace de travail de votre projet iOS.

### Activez le partage de chaîne de certificats pour iOS
{: #enable_keychain}

Activez le partage de chaîne de certificats, `Keychain Sharing`. Accédez à l'onglet `Capabilities` et basculez `Keychain Sharing` sur `On` dans votre projet Xcode.

### Configuration de votre projet iOS pour authentification Facebook
{: #facebook-auth-ios-configproject}

1. Localisez le fichier `info.plist`, généralement situé sous le dossier `Supporting files` de votre projet Xcode.

1. Configurez l'intégration Facebook en ajoutant les propriétés suivantes à votre fichier `info.plist` :

   ![image](images/ios-facebook-infoplist-settings.png)

   Mettez à jour les propriétés de schéma d'URL et FacebookAppID avec votre ID d'application Facebook.

   Vous pouvez aussi mettre à jour le fichier `info.plist` en cliquant avec le bouton droit, en sélectionnant **Open as (Ouvrir en tant que) > Source Code (Code source)** et en ajoutant le code XML suivant :

   ```XML
   <key>CFBundleURLTypes</key>
   <array>
      <dict>
         <key>CFBundleURLSchemes</key>
         <array>
            <string>fb{your-facebook-application-id}</string>
         </array>
      </dict>
   </array>
   <key>FacebookAppID</key>
   <string>{your-facebook-application-id}</string>
   <key>FacebookDisplayName</key>
   <string>{your-faceebook-application-name}</string>
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
   {: codeblock}

   Mettez à jour les propriétés `CFBundleURLSchemes` et `FacebookappID` avec votre ID d'application Facebook. Mettez à jour `FacebookDisplayName` avec le nom de votre application Facebook.

   **Important** : Veillez à ne pas remplacer les propriétés existantes du fichier `info.plist`. Si certaines propriétés se chevauchent, vous devez les fusionner manuellement. Pour plus d'informations, voir [Configure Xcode Project ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developers.facebook.com/docs/ios/getting-started/ "Icône de lien externe"){: new_window} et [Preparing Your Apps for iOS9 ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developers.facebook.com/docs/ios/ios9 "Icône de lien externe"){: new_window}.

## Initialisation du SDK Swift client {{site.data.keyword.amashort}}
{: #facebook-auth-ios-initalize-swift}

Initialisez le logiciel SDK client en transmettant le paramètre `tenantId`.

En général, vous pouvez placer le code d'initialisation dans la méthode `application:didFinishLaunchingWithOptions` du délégué de l'application, bien que cet emplacement ne soit pas obligatoire.

1. Importez la structure requise dans la classe devant utiliser le SDK client {{site.data.keyword.amashort}} en ajoutant les en-têtes suivants :

   ```swift
 import UIKit
 import BMSCore
 import BMSSecurity
   ```
   {: codeblock}

1. Initialisez le logiciel SDK client.

   ```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

   func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: 
		[UIApplicationLaunchOptionsKey: Any]?) -> Bool {
      let mcaAuthManager = MCAAuthorizationManager.sharedInstance
      mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
      //the regionName should be one of the following: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney
      BMSClient.sharedInstance.authorizationManager = mcaAuthManager
      FacebookAuthenticationManager.sharedInstance.register()
   }
   ```
   {: codeblock}

   Dans le code :

   * Remplacez `<applicationBluemixRegion>` par la région dans laquelle votre application {{site.data.keyword.Bluemix_notm}} est hébergée.
   * Remplacez `tenantId` par la valeur **TenantId/App GUID**.

   Pour plus d'informations sur ces valeurs, voir [Avant de commencer](#before-you-begin).

1. Avisez le SDK Facebook de l'activation de l'application et enregistrez le gestionnaire d'authentification Facebook en ajoutant le code suivant à la méthode
`application:didFinishLaunchingWithOptions` dans votre délégué d'application. Ajoutez ce code après avoir initialisé l'instance BMSClient et enregistré Facebook comme gestionnaire d'authentification.

   ```Swift
  return FacebookAuthenticationManager.sharedInstance.onFinishLaunching(application, withOptions: launchOptions)
   ```
   {: codeblock}

1. Copiez le fichier `FacebookAuthenticationManager.swift` depuis les fichiers source de la nacelle `BMSFacebookAuthentication`
vers votre répertoire de projet.

1. Ajoutez le code suivant au délégué de votre appli.

   ```Swift
   func application(_ app: UIApplication,
      open url: URL,
      options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool{
         return FacebookAuthenticationManager.sharedInstance.onOpenURL(app, open: url, options: options)
      }
   ```
   {: codeblock}

## Test de l'authentification
{: #facebook-auth-ios-testing}

Une fois que le SDK client est initialisé et que le gestionnaire d'authentification Facebook est enregistré, vous pouvez commencer à envoyer des requêtes à
votre application back end mobile.

### Avant de commencer
{: #facebook-auth-ios-testing-before}

Vous devez utiliser le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} et disposer au préalable d'une ressource protégée par {{site.data.keyword.amashort}} sur le noeud final `/protected`. Pour configurer un noeud final `/protected`, voir la rubrique [Protection des ressources](protecting-resources.html).

1. Essayez d'envoyer depuis votre navigateur une requête à un noeud final protégé de votre nouvelle application back end mobile. Ouvrez l'URL suivante : `{applicationRoute}/protected`, en remplaçant `{applicationRoute}` par la valeur extraite depuis **Options pour application mobile** (voir [Configuration de Mobile Client Access pour l'authentification personnalisée](#facebook-auth-ios-configmca)).
Par exemple : `http://my-mobile-backend.mybluemix.net/protected`
<br/>Le noeud final `/protected` d'une application back end mobile créée avec le conteneur boilerplate MobileFirst Services Starter est
protégé par {{site.data.keyword.amashort}}. Un message signalant l'interdiction d'accéder au site (`Unauthorized`) est renvoyé au navigateur. Ce message est renvoyé car ce noeud final n'est accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}.

1. A l'aide de votre application iOS, envoyez une demande au même noeud final.

   ```Swift
	let protectedResourceURL = "<your protected resource absolute path>"
	let request = Request(url: protectedResourceURL, method: HttpMethod.GET)

   let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
 if error == nil {
         print ("response:\(response?.responseText), no error")
 } else {
         print ("error: \(error)")
 }
   }

	request.send(completionHandler: callBack)
   ```
   {: codeblock}

1. Lancez votre application. Un écran de connexion à Facebook s'affiche.

   ![image](images/ios-facebook-login.png)

   Cet écran peut être légèrement différent si vous n'êtes pas connecté actuellement à Facebook.

1. Cliquez sur **OK** pour autoriser {{site.data.keyword.amashort}} à utiliser votre ID utilisateur Facebook pour l'authentification.

1. 	Lorsque votre demande aboutit, la sortie suivante figure dans la console Xcode :

   ```
   response:Optional("Bonjour, ceci est une ressource protégée de l'application back end mobile !"), no error
   ```
   {: screen}

1. Vous pouvez également ajouter une fonctionnalité de déconnexion en ajoutant le code suivant :

   ```
   FacebookAuthenticationManager.sharedInstance.logout(callBack)
   ```
   {: codeblock}

   Si vous appelez ce code après qu'un utilisateur se soit connecté à Facebook et qu'il tente à nouveau de s'y connecter,
il est invité à autoriser {{site.data.keyword.amashort}} à utiliser Facebook à des fins d'authentification.

   Pour changer d'utilisateur, vous devez appeler ce code et l'utilisateur doit se déconnecter de Facebook dans son navigateur.

   La transmission de `callBack` à la fonction de déconnexion est facultative. Vous pouvez également transmettre la valeur
`nil`.
