---

Copyright : 2016

---

# Activation de l'authentification Google dans les applications iOS (SDK Swift)
{: #google-auth-ios}

## Avant de commencer
{: #google-auth-ios-before}

* Vous devez disposer d'une ressource protégée par {{site.data.keyword.amashort}} et d'un projet iOS instrumenté avec le SDK client de {{site.data.keyword.amashort}}.  Pour plus d'informations, voir [Initiation à {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) et [Configuration du SDK Swift iOS](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html).  
* Protégez manuellement votre application de back end avec le SDK serveur de {{site.data.keyword.amashort}}. Pour plus d'informations, voir [Protection des ressources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

## Préparation de votre application pour connexion Google
{: #google-sign-in-ios}

Préparez votre application pour connexion Google en suivant les instructions fournies par Google sur le site [Google Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start-integrating). Les étapes suivantes offrent un bref aperçu des tâches que vous devez effectuer pour préparer votre application.

1. Activez la connexion Google pour iOS pour votre application. Pour plus d'informations, voir
[Try Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start?ver=swift).

1. Procurez-vous un fichier de configuration (`GoogleService-Info.plist`) pour votre projet. Pour obtenir le fichier, voir
[Enable Google services for your app](https://developers.google.com/mobile/add?platform=ios).

 **Important :** Lorsque vous vous êtes procuré le fichier `GoogleService-Info.plist`, ouvrez-le et notez la valeur de
`CLIENT_ID`. Vous en aurez besoin par la suite pour configurer {{site.data.keyword.amashort}}.

1. Ajoutez le fichier `GoogleService-Info.plist` à votre projet Xcode. Pour plus d'informations, voir
[Add the configuration file to your project](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config)

1. Mettez à jour les schémas d'URL dans votre projet Xcode en indiquant votre `REVERSE_CLIENT_ID` et votre identificateur de bundle. Pour plus d'informations, voir [Add URL schemes to your project](https://developers.google.com/identity/sign-in/ios/start-integrating#add_url_schemes_to_your_project).

1. Mettez à jour le fichier project-Bridging-Header.h de votre application avec le code suivant :

 ```
 #import <Google/SignIn.h>
 ```

 Pour plus d'informations sur la mise à jour du fichier d'en-tête de pontage, reportez-vous à l'étape 1 dans
[Enable sign-in](https://developers.google.com/identity/sign-in/ios/sign-in#enable_sign-in).

## Configuration de {{site.data.keyword.amashort}} pour l'authentification Google
{: #google-auth-ios-config}

Maintenant que vous disposez d'un ID client iOS, vous pouvez activer l'authentification Google dans le tableau de bord {{site.data.keyword.Bluemix}}.

1. Ouvrez votre appli dans le tableau de bord {{site.data.keyword.Bluemix_notm}}.

1. Cliquez sur **Options pour application mobile** et notez la valeur de **Route** (*applicationRoute*) et **Identificateur global unique de l'application** (*applicationGUID*). Vous aurez besoin de ces valeurs lors de l'initialisation du SDK.

1. Cliquez sur la vignette {{site.data.keyword.amashort}}. Le tableau de bord {{site.data.keyword.amashort}} se charge.

1. Cliquez sur la vignette **Google** .

1. Dans **ID application pour iOS**, spécifiez la valeur `CLIENT_ID` figurant dans le fichier
`GoogleService-Info.plist` que vous vous êtes procuré auparavant et cliquez sur **Sauvegarder**.

## Configuration du SDK client de {{site.data.keyword.amashort}} pour iOS
{: #google-auth-ios-sdk}

### Installation de CocoaPods
{: #google-auth-cocoapods}

Le SDK client de {{site.data.keyword.amashort}} est distribué avec CocoaPods, un gestionnaire de dépendances pour les projets iOS. CocoaPods télécharge automatiquement les artefacts à partir des référentiels et les met à la disposition de votre application iOS.

1. Ouvrez Terminal et lancez la commande `pod --version`. Si CocoaPods est déjà installé, le numéro de version est affiché. Vous pouvez passer à la section suivante de ce tutoriel.

1. Installez CocoaPods en exécutant `sudo gem install cocoapods`. Reportez-vous au [site Web CocoaPods](https://cocoapods.org/) si vous avez besoin d'autres instructions.

1. Fermez XCode.

1. Ouvrez un terminal et utilisez la commande `cd` pour accéder à votre répertoire de projet.

1.  Exécutez `pod init`.

### Installation du {{site.data.keyword.amashort}} SDK Swift client à l'aide de CocoaPods
{: #google-auth-ios-sdk-cocoapods}

1. Accédez à votre projet iOS.

1. Modifiez le fichier `Podfile` en lui ajoutant les lignes suivantes :

 ```
 use_frameworks!
 pod 'BMSGoogleAuthentication'
 ```
 **Astuce :** Vous pouvez ajouter `use_frameworks!` à votre cible Xcode au lieu du Podfile.

1. Enregistrez le `Podfile` et lancez `pod install` depuis la ligne de commande. CocoaPods installe les dépendances. La progression et les composants ajoutés s'affichent.

 **Important** : Vous devez à présent ouvrir votre projet en utilisant le fichier
`xcworkspace` généré par CocoaPods. Son nom est généralement `{your-project-name}.xcworkspace`.  

1. Exécutez `open {nom_projet}.xcworkspace` depuis la ligne de commande pour ouvrir votre espace de travail de projet iOS.

1. Copiez dans votre répertoire de projet le fichier `GoogleAuthenticationManager.swift` depuis les fichiers pod source
`BMSGoogleAuthentication`.

## Initialisation du SDK Swift client {{site.data.keyword.amashort}}
{: #google-auth-ios-initialize}

Pour utiliser le SDK client de {{site.data.keyword.amashort}}, initialisez-le en lui transmettant les paramètres
`applicationGUID` et `applicationRoute`.

En général, vous pouvez placer le code d'initialisation dans la méthode `application:didFinishLaunchingWithOptions` du délégué de l'application, bien que cet emplacement ne soit pas obligatoire.

1. Récupérez les valeurs de ces paramètres pour votre application. Ouvrez votre appli dans le tableau de bord {{site.data.keyword.Bluemix_notm}}. Cliquez sur **Options pour application mobile**. Les
valeurs `applicationRoute` et `applicationGUID` sont affichées dans les zones
**Route** et **Identificateur global unique de l'application**.

1. Importez les structures requises dans la classe où vous comptez utiliser le SDK client
{{site.data.keyword.amashort}}. Ajoutez les en-têtes suivants :

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```

1. Utilisez le code suivant pour initialiser le SDK client. Remplacez `<applicationRoute>` et
`<applicationGUID>` par les valeurs de **Route** et **Identificateur global unique de l'application**
de la section **Options pour application mobile** dans le tableau de bord {{site.data.keyword.Bluemix_notm}}.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 // Initialisez le SDK client.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUId, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 GoogleAuthenticationManager.sharedInstance.register()
      return true
      }

 // [START openurl]
      func application(application: UIApplication,
          openURL url: NSURL, sourceApplication: String?, annotation: AnyObject) -> Bool {
             return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, sourceApplication: sourceApplication, annotation: annotation)
      }

 @available(iOS 9.0, *)
 func application(app: UIApplication, openURL url: NSURL, options: [String : AnyObject]) -> Bool {
 return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, options: options)
  }
 ```

## Test de l'authentification
{: #google-auth-ios-testing}

Une fois que le SDK client est initialisé et que le gestionnaire d'authentification Google est enregistré, vous pouvez commencer à envoyer des
demandes à votre back end mobile.

### Avant de commencer
{: #google-auth-ios-testing-before}

Vous devez utiliser le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} et disposer au préalable d'une ressource protégée par {{site.data.keyword.amashort}} sur le noeud final `/protected`. Pour configurer un noeud final `/protected`, voir la rubrique [Protection des ressources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Essayez d'envoyer une demande à un noeud final protégé de votre back end mobile dans votre navigateur de bureau en ouvrant
`{applicationRoute}/protected`, par exemple : `http://my-mobile-backend.mybluemix.net/protected`

1. Le noeud final `/protected` d'un système de back end mobile créé avec le conteneur boilerplate MobileFirst Services est protégé par {{site.data.keyword.amashort}}, par conséquent, seules les applications mobiles instrumentées avec le logiciel SDK client de {{site.data.keyword.amashort}} peuvent y accéder. Pour cette raison, le message `Unauthorized` s'affiche dans votre navigateur de bureau.

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

1. Lancez votre application. Un écran de connexion Google s'affiche :

 ![image](images/ios-google-login.png)

1. Lorsque vous vous connectez et cliquez sur **OK**, vous autorisez {{site.data.keyword.amashort}}
à utiliser votre identité utilisateur Google à des fins d'authentification.

1. 	Votre demande doit aboutir. La sortie suivante devrait figurer dans le journal.

 ```
 onAuthenticationSuccess info = Optional({attributes = {};
     deviceId = 105747725068605084657;
     displayName = "donlonqwerty@gmail.com";
     isUserAuthenticated = 1;
     userId = 105747725068605084657;
 })
 response:Optional("Bonjour, cette ressource est protégée !"), no error
 ```

1. Vous pouvez également ajouter une fonctionnalité de déconnexion en ajoutant le code suivant :

 ```
 GoogleAuthenticationManager.sharedInstance.logout(callBack)
 ```

  Si vous appelez ce code alors que l'utilisateur était connecté via Google et qu'il tente à nouveau de se connecter, il est invité à autoriser
{{site.data.keyword.amashort}} à utiliser Google aux fins d'authentification. A ce stade, l'utilisateur peut cliquer sur un nom d'utilisateur à l'angle
supérieur droit de l'écran pour sélectionner et se connecter sous un autre nom d'utilisateur.

   La transmission de `callBack` à la fonction de déconnexion est facultative. Vous pouvez également transmettre la valeur
`nil`.
