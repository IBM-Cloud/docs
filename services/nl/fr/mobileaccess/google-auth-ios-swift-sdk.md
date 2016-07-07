 ---

copyright:
  years: 2016

---
{:screen:  .screen}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}

# Activation de l'authentification Google pour les applications iOS (SDK Swift)
{: #google-auth-ios}
Utilisez Google Sign-In pour authentifier les utilisateurs sur votre application iOS Swift {{site.data.keyword.amashort}}. Le nouveau SDK Swift {{site.data.keyword.amashort}} qui vient de sortir améliore les fonctionnalités fournies par le SDK Mobile Client Access Objective-C existant et en ajoute de nouvelles.

**Remarque :** alors que le SDK Objective-C reste complètement pris en charge et est toujours considéré comme le SDK principal pour {{site.data.keyword.Bluemix_notm}} Mobile Services, il est prévu qu'il soit interrompu plus tard dans l'année et remplacé par le nouveau SDK Swift.



## Avant de commencer
{: #google-auth-ios-before}
Vous devez disposer des éléments suivants :

* Un projet IOS en Xcode. Il n'a pas besoin d'être instrumenté avec le SDK client de {{site.data.keyword.amashort}}.  
* Une instance d'une application {{site.data.keyword.Bluemix_notm}} qui est protégée par le service {{site.data.keyword.amashort}}. Pour plus d'informations sur la création d'un système de back end {{site.data.keyword.Bluemix_notm}}, voir [Initiation](index.html).


## Préparation de votre application pour Google Sign-In
{: #google-sign-in-ios}

Préparez votre application pour Google Sign-In en suivant les instructions fournies par Google sur le site [Google Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start-integrating). 

Ce processus :
* prépare un nouveau projet sur le site Google Developers, 
* crée le fichier `GoogleService-Info.plist` et la valeur `REVERSE_CLIENT_ID` pour ajouter votre projet Xcode, et
* crée l'**ID client Google** pour l'ajouter à votre application de back end {{site.data.keyword.Bluemix_notm}}.

Les étapes suivantes offrent un bref aperçu des tâches nécessaires à la préparation de votre application. 

**Remarque :** il n'est pas nécessaire d'ajouter `Google/SignIn` CocoaPod. Le SDK requis est ajouté par `BMSGoogleAuthentication` CocoaPod.

1. Notez l'identificateur de bundle de votre projet Xcode depuis la section relative à l'identité de l'onglet traitant des dispositions générales de la cible principale. Vous en aurez besoin pour créer votre projet Google Sign-In.

1. Créez un projet sur Google Developers pour Google Sign-In for iOS, à l'adresse https://developers.google.com/mobile/add?platform=ios. 

2. Ajoutez le service Google Sign-In à votre projet.

3. Extrayez `GoogleService-Info.plist`.

  **Important :** Lorsque vous vous êtes procuré le fichier `GoogleService-Info.plist`, ouvrez-le et notez la valeur de
`CLIENT_ID`. Vous en aurez besoin par la suite pour configurer l'application de back end {{site.data.keyword.amashort}}.

1. Ajoutez le fichier `GoogleService-Info.plist` à votre projet Xcode. Pour plus d'informations, voir [Add the configuration file to your project](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config).

1. Mettez à jour les schémas d'URL dans votre projet Xcode en indiquant votre `REVERSE_CLIENT_ID` et votre identificateur de bundle. Pour plus d'informations, voir [Add URL schemes to your project](https://developers.google.com/identity/sign-in/ios/start-integrating#add_a_url_scheme_to_your_project).


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
{: #install-cocoapods}

1. Ouvrez Terminal et lancez la commande **pod --version**. Si CocoaPods est déjà installé, le numéro de version est affiché. Vous pouvez passer à la section suivante pour installer le SDK.

1. Si CocoaPods n'est pas installé, exécutez la commande :
```
sudo gem install cocoapods
```
Pour plus d'informations, reportez-vous au [site Web CocoaPods](https://cocoapods.org/).

### Installation du SDK Swift client de {{site.data.keyword.amashort}} avec CocoaPods
{: #facebook-auth-install-swift-cocoapods}

1. Si vous n'avez pas de fichier `Podfile` dans votre projet iOS, exécutez `pod init` pour créer le fichier.

1. Modifiez le fichier `Podfile` en lui ajoutant les lignes suivantes dans la cible appropriée :

 ```
 use_frameworks!
 pod 'BMSGoogleAuthentication'
 ```
 
 **Remarque :** si vous avez déjà installé le SDK principal de {{site.data.keyword.amashort}}, vous pouvez retirer la ligne : `pod 'BMSSecurity'`. Le pod `BMSGoogleAuthentication` installe toutes les infrastructures nécessaires.
	
 **Astuce :** Vous pouvez ajouter `use_frameworks!` à votre cible Xcode au lieu du Podfile.

1. Enregistrez le `Podfile` et lancez `pod install` depuis la ligne de commande. CocoaPods installe les dépendances. La progression et les composants ajoutés s'affichent.

 **Important** : Vous devez à présent ouvrir votre projet en utilisant le fichier
`xcworkspace` généré par CocoaPods. Son nom est généralement `{your-project-name}.xcworkspace`.  

1. Exécutez `open {nom_projet}.xcworkspace` depuis la ligne de commande pour ouvrir votre espace de travail de projet iOS.

1. Copiez dans votre répertoire de projet le fichier `GoogleAuthenticationManager.swift` depuis les fichiers pod source
`BMSGoogleAuthentication`.

## Initialisation du SDK Swift client {{site.data.keyword.amashort}}
{: #google-auth-ios-initialize}

Pour utiliser le SDK client de {{site.data.keyword.amashort}}, initialisez-le en lui transmettant les paramètres `applicationGUID` et `applicationRoute`.

En général, vous pouvez placer le code d'initialisation dans la méthode `application:didFinishLaunchingWithOptions` du délégué de l'application, bien que cet emplacement ne soit pas obligatoire.

1. Récupérez les valeurs de ces paramètres pour votre application. Ouvrez votre appli dans le tableau de bord {{site.data.keyword.Bluemix_notm}}. Cliquez sur **Options pour application mobile**. Les
valeurs `applicationRoute` et `applicationGUID` sont affichées dans les zones
**Route** et **Identificateur global unique de l'application**.

1. Importez les structures requises dans la classe où vous comptez utiliser le SDK client {{site.data.keyword.amashort}}. Ajoutez les en-têtes suivants :

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```

1. Utilisez le code suivant pour initialiser le SDK client. Remplacez `<applicationRoute>` et `<applicationGUID>` par les valeurs de **Route** et **Identificateur global unique de l'application** que vous avez obtenues depuis la section **Options pour application mobile** du tableau de bord {{site.data.keyword.Bluemix_notm}}. Remplacez `<applicationBluemixRegion>` par la région dans laquelle votre application {{site.data.keyword.Bluemix_notm}} est hébergée. Pour afficher votre région {{site.data.keyword.Bluemix_notm}}, cliquez sur l'icône face (![Face](/face.png "Face")) dans l'angle supérieur gauche du tableau de bord. 

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 // Initialisez le SDK client.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUId, bluemixRegion: BMSClient.<applicationBluemixRegion>)

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
{: screen}

1. Vous pouvez également ajouter une fonctionnalité de déconnexion en ajoutant le code suivant :

 ```
 GoogleAuthenticationManager.sharedInstance.logout(callBack)
 ```

  Si vous appelez ce code alors que l'utilisateur était connecté via Google et qu'il tente à nouveau de se connecter, il est invité à autoriser
{{site.data.keyword.amashort}} à utiliser Google aux fins d'authentification. A ce stade, l'utilisateur peut cliquer sur un nom d'utilisateur à l'angle
supérieur droit de l'écran pour sélectionner et se connecter sous un autre nom d'utilisateur.

   La transmission de `callBack` à la fonction de déconnexion est facultative. Vous pouvez également transmettre la valeur
`nil`.
