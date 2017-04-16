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

# Activation de l'authentification Google pour les applications iOS (SDK Swift)
{: #google-auth-ios}

Utilisez le mécanisme Google Sign-In pour authentifier les utilisateurs auprès de votre application
{{site.data.keyword.amafull}} Swift iOS .


## Avant de commencer
{: #before-you-begin}

Vous devez disposer des éléments suivants :

* Une instance d'un service {{site.data.keyword.amafull}} et une application {{site.data.keyword.Bluemix_notm}}. Pour plus d'informations sur la création d'un système de back end {{site.data.keyword.Bluemix_notm}}, voir [Initiation](index.html).
* L'URL de votre application back-end (**Route de l'application**). Vous aurez besoin de ces valeurs pour envoyer des requêtes aux noeuds finaux protégés de votre application back end.
* Valeur de votre **TenantID**. Ouvrez votre service dans le tableau de bord de {{site.data.keyword.amashort}}. Cliquez sur le bouton **Options pour application mobile**. La valeur `tenantId` (qui porte également le nom d'`appGUID`) est affichée dans la zone **App GUID / TenantId**. Vous aurez besoin de cette valeur pour initialiser le Gestionnaire des autorisations.
* Votre **région** {{site.data.keyword.Bluemix_notm}}. Vous pouvez trouver votre région {{site.data.keyword.Bluemix_notm}} actuelle dans l'en-tête, en regard de l'icône **Avatar**![icône Avatar](images/face.jpg "icône Avatar"). La valeur de région qui apparaît doit être l'une des suivantes : **US South**, **United Kingdom** ou **Sydney** et correspondre aux valeurs requises dans le code : `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` ou `BMSClient.Region.sydney`.
* Un projet IOS en Xcode. Il n'a pas besoin d'être instrumenté avec le SDK client de {{site.data.keyword.amashort}}.  


## Préparation de votre application pour Google Sign-In
{: #google-sign-in-ios}

Préparez votre application pour le mécanisme de connexion unique Google en suivant les instructions de Google sur le site [Google Sign-In for iOS ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developers.google.com/identity/sign-in/ios/start-integrating "Icône de lien externe"){: new_window}.

Ce processus :

* prépare un nouveau projet sur le site Google Developers,
* crée le fichier `GoogleService-Info.plist` et la valeur `REVERSE_CLIENT_ID` pour ajouter votre projet Xcode, et
* crée l'**ID client Google** pour l'ajouter à votre application de back end {{site.data.keyword.Bluemix_notm}}.

Les étapes suivantes offrent un bref aperçu des tâches nécessaires à la préparation de votre application.

**Remarque :** il n'est pas nécessaire d'ajouter Google Sign-In CocoaPod. Le SDK requis est ajouté par `BMSGoogleAuthentication` CocoaPod.

1. Notez l'identificateur de bundle de votre projet Xcode depuis la section relative à l'identité de l'onglet traitant des dispositions générales de la cible principale. Vous en aurez besoin pour créer votre projet Google Sign-In.

1. Créez un projet pour Google Sign-In for sur le [site Google Developer![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developers.google.com/mobile/add?platform=ios "Icône de lien externe"){: new_window}.

1. Ajoutez l'API Google Sign-In à votre projet.

1. Extrayez `GoogleService-Info.plist`.

   **Important :** Lorsque vous vous êtes procuré le fichier `GoogleService-Info.plist`, ouvrez-le et notez la valeur de
`CLIENT_ID`. Vous en aurez besoin par la suite pour configurer l'application de back end {{site.data.keyword.amashort}}.

1. Ajoutez le fichier `GoogleService-Info.plist` à votre projet Xcode. Pour plus d'informations, voir [Add the configuration file to your project ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config "Icône de lien externe"){: new_window}.

1. Mettez à jour les schémas d'URL dans votre projet Xcode en indiquant votre `REVERSE_CLIENT_ID` et votre identificateur de bundle. Pour plus d'informations, voir [Add URL schemes to your project ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developers.google.com/identity/sign-in/ios/start-integrating#add_a_url_scheme_to_your_project "Icône de lien externe"){: new_window}.

1. Mettez à jour le fichier `project-Bridging-Header.h` de votre application avec le code suivant :

	```
	#import <Google/SignIn.h>
	```
	{: codeblock}

	Pour plus d'informations sur la mise à jour du fichier d'en-tête de pontage, voir [Enable sign-in ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developers.google.com/identity/sign-in/ios/sign-in#enable_sign-in "Icône de lien externe"){: new_window}.

## Configuration de {{site.data.keyword.amashort}} pour l'authentification Google
{: #google-auth-ios-config}

Maintenant que vous disposez d'un ID client iOS, vous pouvez activer l'authentification Google dans le service {{site.data.keyword.amashort}}.

1. Ouvrez votre service dans le tableau de bord {{site.data.keyword.amashort}}.
1. Dans l'onglet **Gérer**, activez **Autorisation**.
1. Développez la section **Google**.
1. Dans **ID application pour iOS**, spécifiez la valeur `CLIENT_ID` que vous avez obtenue dans le fichier
`GoogleService-Info.plist`.
1. Cliquez sur **Sauvegarder**.

## Configuration du SDK client de {{site.data.keyword.amashort}} pour iOS
{: #google-auth-ios-sdk}

### Installation de CocoaPods
{: #install-cocoapods}

1. Ouvrez Terminal et lancez la commande **pod --version**. Si CocoaPods est déjà installé, le numéro de version est affiché. Vous pouvez passer à la section suivante pour installer le SDK.

1. Si CocoaPods n'est pas installé, exécutez la commande :

	```
	sudo gem install cocoapods
	```
	{: codeblock}

Pour plus d'informations, reportez-vous au [site Web CocoaPods ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cocoapods.org/ "Icône de lien externe"){: new_window}.

### Installation du SDK Swift client de {{site.data.keyword.amashort}} avec CocoaPods
{: #facebook-auth-install-swift-cocoapods}

1. Si vous n'avez pas de fichier `Podfile` dans votre projet iOS, exécutez `pod init` pour créer le fichier.

1. Modifiez le fichier `Podfile` en lui ajoutant les lignes suivantes dans la cible appropriée :

	```
	use_frameworks!
	pod 'BMSGoogleAuthentication'
	```
	{: codeblock}

	**Remarque :** si vous avez déjà installé le SDK principal de {{site.data.keyword.amashort}}, vous pouvez retirer la ligne : `pod 'BMSSecurity'`. La
nacelle `BMSGoogleAuthentication` installe toutes les infrastructures nécessaires.

	**Astuce :** Vous pouvez ajouter `use_frameworks!` à votre cible Xcode au lieu du Podfile.

1. Enregistrez le `Podfile` et lancez `pod install` depuis la ligne de commande. CocoaPods installe les dépendances. La progression et les composants ajoutés s'affichent.

	**Important** : Vous devez à présent ouvrir votre projet en utilisant le fichier
`xcworkspace` généré par CocoaPods. Son nom est généralement `{your-project-name}.xcworkspace`.  

1. Exécutez `open {nom_projet}.xcworkspace` depuis la ligne de commande pour ouvrir votre espace de travail de projet iOS.

1. Copiez dans votre répertoire de projet le fichier `GoogleAuthenticationManager.swift` depuis les fichiers pod source
`BMSGoogleAuthentication`.

### Activez le partage de chaîne de certificats pour iOS
{: #enable_keychain}

Activez le partage de chaîne de certificats, `Keychain Sharing`. Accédez à l'onglet `Capabilities` et basculez `Keychain Sharing` sur `On` dans votre projet Xcode.


## Initialisation du SDK Swift client {{site.data.keyword.amashort}}
{: #google-auth-ios-initialize}

Pour utiliser le SDK client de {{site.data.keyword.amashort}}, initialisez-le en lui transmettant le paramètre `tenantID`.

En général, vous pouvez placer le code d'initialisation dans la méthode `application:didFinishLaunchingWithOptions` du délégué de l'application, bien que cet emplacement ne soit pas obligatoire.

1. Importez les structures requises dans la classe où vous comptez utiliser le SDK client {{site.data.keyword.amashort}}. Ajoutez les en-têtes suivants :

	```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: 
		[UIApplicationLaunchOptionsKey: Any]?) -> Bool {

		let mcaAuthManager = MCAAuthorizationManager.sharedInstance
		mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
		//the regionName should be one of the following: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney   
		BMSClient.sharedInstance.authorizationManager = mcaAuthManager
		GoogleAuthenticationManager.sharedInstance.register()
		return true
	}

	// [START openurl]
	    func application(_ application: UIApplication,
			     open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
			return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, sourceApplication: sourceApplication, annotation: annotation)
      }

	@available(iOS 9.0, *)
	func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any]) -> Bool {
		return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, options: options)
  }

	```
	{: codeblock}

	Dans le code :

      * Remplacez `<serviceTenantID>` par la valeur extraite depuis **Options pour application mobile**.
      * Remplacez `<applicationBluemixRegion>` par votre **Région** {{site.data.keyword.Bluemix_notm}}.

	Pour plus d'informations sur l'obtention de ces valeurs, voir [Avant de commencer](#before-you-begin).


## Test de l'authentification
{: #google-auth-ios-testing}

Une fois que le SDK client est initialisé et que le gestionnaire d'authentification Google est enregistré, vous pouvez commencer à envoyer des requêtes
à votre application back end mobile.

### Avant de commencer
{: #google-auth-ios-testing-before}

Vous devez utiliser le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} et disposer au préalable d'une ressource protégée par {{site.data.keyword.amashort}} sur le noeud final `/protected`. Pour configurer un noeud final `/protected`, voir la rubrique [Protection des ressources](protecting-resources.html).

1. Essayez d'envoyer une demande à un noeud final protégé de votre application de back end mobile dans votre navigateur en ouvrant `{applicationRoute}/protected`.  Exemple : `http://my-mobile-backend.mybluemix.net/protected`.

1. Le noeud final `/protected` d'une application back end mobile créée par le conteneur boilerplate MobileFirst Services Boilerplate étant
protégé par {{site.data.keyword.amashort}}, il n'est accessible que par les applications mobiles instrumentées avec le SDK client
{{site.data.keyword.amashort}}. Pour cette raison, le message `Unauthorized` s'affiche dans votre navigateur de bureau.

1. A l'aide de votre application iOS, envoyez une demande au même noeud final.

	```Swift
	let protectedResourceURL = "<your protected resource absolute path>"
	let request = Request(url: protectedResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
 if error == nil {
			print ("response:\(response?.responseText), no error")
 } else {
			print ("erreur : \(error)")
     }
	}

	request.send(completionHandler: callBack)

	```
	{: codeblock}

1. Lancez votre application. Un écran de connexion Google s'affiche :

 ![image](images/ios-google-login.png)

1. Lorsque vous vous connectez et cliquez sur **OK**, vous autorisez {{site.data.keyword.amashort}}
à utiliser votre identité utilisateur Google à des fins d'authentification.

1. Votre demande doit aboutir. La sortie suivante devrait être consignée dans le journal.

	```
	response:Optional("Bonjour, ceci est une ressource protégée de l'application back end mobile !"), no error
	```
	{: screen}

1. Vous pouvez également ajouter une fonctionnalité de déconnexion en ajoutant le code suivant :

	```
	GoogleAuthenticationManager.sharedInstance.logout(callBack)
	```
	{: codeblock}

	Si vous appelez ce code alors que l'utilisateur était connecté via Google et qu'il tente à nouveau de se connecter, il est invité à autoriser
{{site.data.keyword.amashort}} à utiliser Google aux fins d'authentification. A ce stade, l'utilisateur peut cliquer sur un nom d'utilisateur <!--in the upper-right corner of the screen--> pour sélectionner et se connecter sous un autre nom d'utilisateur.

	La transmission de `callBack` à la fonction de déconnexion est facultative. Vous pouvez également transmettre la valeur
`nil`.
