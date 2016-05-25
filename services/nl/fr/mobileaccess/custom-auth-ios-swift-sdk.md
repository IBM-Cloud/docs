---

Copyright : 2016

---

# Configuration du SDK client pour iOS (Swift SDK) de {{site.data.keyword.amashort}}
{: #custom-ios}

Configurez votre application iOS qui utilise l'authentification personnalisée de manière qu'elle utilise le SDK client de {{site.data.keyword.amashort}} et connectez-la à {{site.data.keyword.Bluemix}}.

## Avant de commencer
{: #before-you-begin}

Vous devez disposer d'une ressource protégée par une instance du service {{site.data.keyword.amashort}} qui est configuré pour utiliser un fournisseur d'identité personnalisé.  Votre appli mobile doit aussi être instrumentée à l'aide du SDK client de {{site.data.keyword.amashort}}.  Pour plus d'informations, voir les sujets suivants :
 * [Initiation à {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Configuration du SDK Swift iOS](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html)
 * [Utilisation d'un fournisseur d'identité personnalisé](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Création d'un fournisseur d'identité personnalisé](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configuration de {{site.data.keyword.amashort}} pour l'authentification personnalisée](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## Configuration de {{site.data.keyword.amashort}} pour l'authentification personnalisée
 {: #custom-auth-ios-configmca}

 1. Ouvrez votre appli dans le tableau de bord {{site.data.keyword.Bluemix_notm}}.

 1. Cliquez sur **Options pour application mobile** et notez la valeur de **Route** (*applicationRoute*) et
**Identificateur global unique de l'application** (*applicationGUID*). Vous aurez besoin de ces valeurs lors de l'initialisation du SDK.

 1. Cliquez sur la vignette {{site.data.keyword.amashort}}. Le tableau de bord {{site.data.keyword.amashort}} se charge.

 1. Cliquez sur la vignette **Personnalisé**.

 1. Dans **Nom de domaine**, spécifiez votre domaine d'authentification personnalisé.

 1. Dans **URL**, spécifiez votre route d'application (applicationRoute).

 1. Cliquez sur **Sauvegarder**.

## Configuration du SDK client de {{site.data.keyword.amashort}} pour iOS
 {: #custom-auth-ios-sdk}

### Installation de CocoaPods
 {: #custom-auth-cocoapods}

 Le SDK client de {{site.data.keyword.amashort}} est distribué avec CocoaPods, un gestionnaire de dépendances pour les projets iOS. CocoaPods télécharge automatiquement les artefacts à partir des référentiels et les met à la disposition de votre application iOS.

 1. Ouvrez Terminal et lancez la commande `pod --version`. Si CocoaPods est déjà installé, le numéro de version est affiché. Vous pouvez passer à la section suivante de ce tutoriel.

 1. Installez CocoaPods en exécutant `sudo gem install cocoapods`. Reportez-vous au [site Web CocoaPods](https://cocoapods.org/) si vous avez besoin d'autres instructions.

 1. Fermez XCode.

 1. Ouvrez un terminal et utilisez la commande `cd` pour accéder à votre répertoire de projet.

 1.  Exécutez `pod init`.

### Installation du logiciel SDK client avec CocoaPods
{: #custom-ios-sdk-cocoapods}

Utilisez le gestionnaire de dépendances CocoaPods pour installer le SDK client de {{site.data.keyword.amashort}}.

1. Ouvrez Terminal et accédez au répertoire racine de votre projet iOS.

1. Modifiez le fichier `Podfile` en lui ajoutant les lignes suivantes .

 ```
 use_frameworks!
 pod 'BMSSecurity'
 ```
 **Astuce :** Vous pouvez ajouter `use_frameworks!` à votre cible Xcode au lieu du Podfile.

1. Depuis la ligne de commande, exécutez `pod install`.
CocoaPods installe les dépendances qui ont été ajoutées. La progression et les composants ajoutés s'affichent.

 **Important** : A partir de ce moment, vous devrez toujours ouvrir votre projet à l'aide d'un fichier `xcworkspace` généré par CocoaPods. Son nom est généralement `{your-project-name}.xcworkspace`.  

1. Exécutez `open {your-project-name}.xcworkspace` depuis la ligne de commande pour ouvrir l'espace de travail de votre projet iOS.

### Initialisation du logiciel SDK client
{: #custom-ios-sdk-initialize}

Initialisez le SDK en passant les paramètres `applicationRoute` et `applicationGUID`. Bien que ceci ne soit pas obligatoire,
le code d'initialisation est souvent placé dans la méthode `application:didFinishLaunchingWithOptions` de votre délégué d'application

1. Récupérez les valeurs de ces paramètres pour votre application. Ouvrez votre appli dans le tableau de bord {{site.data.keyword.Bluemix_notm}}. Cliquez sur **Options pour application mobile**. Les valeurs `applicationRoute` et `applicationGUID` sont affichées dans les zones **Route** et
**Identificateur global unique de l'application**.

1. Importez les structures requises dans la classe où vous comptez utiliser le SDK client {{site.data.keyword.amashort}}.

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
```

1. Initialisez le SDK client {{site.data.keyword.amashort}}, stipulez MCAAuthorizationManager comme nouveau gestionnaire d'authentification,
définissez un délégué d'authentification et enregistrez-le. Remplacez `<applicationRoute>` et `<applicationGUID>` par
les valeurs de **Route** et **Identificateur global unique de l'application** de la section **Options pour application
mobile** dans le tableau de bord {{site.data.keyword.Bluemix_notm}}.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"
 let customRealm = "<domaine de votre ressource protégée>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

  //Délégué d'authentification pour traitement de demande d'authentification personnalisée
 class MyAuthDelegate : AuthenticationDelegate {
      func onAuthenticationChallengeReceived(authContext: AuthenticationContext, challenge: AnyObject){
          print("onAuthenticationChallengeReceived")
              let answer = <Réponse à la demande d'authentification envoyée par le back-end (Doit être du type  [String:AnyObject])>
              authContext.submitAuthenticationChallengeAnswer(answer)
      }

      func onAuthenticationSuccess(info: AnyObject?) {
           print("onAuthenticationSuccess info = \(info)")
           print("onAuthenticationSuccess")
      }

      func onAuthenticationFailure(info: AnyObject?){
        print("onAuthenticationFailure info = \(info)")
        print("onAuthenticationFailure")
      }
  }

  let delegate = MyAuthDelegate()
  let mcaAuthManager = MCAAuthorizationManager.sharedInstance

 do {
      try mcaAuthManager.registerAuthenticationDelegate(delegate, realm: customRealm)
  } catch {
      print("erreur à l'enregistrement : \(error)")
  }
 return true
 }   
 ```

## Test de l'authentification
{: #custom-ios-testing}

Après avoir initialisé le SDK client et enregistré un délégué d'authentification personnalisé, vous pouvez commencer à envoyer des demandes à votre back end
mobile.

### Avant de commencer
{: #custom-ios-testing-before}

 Vous devez disposer d'une application créée avec un conteneur boilerplate {{site.data.keyword.mobilefirstbp}} et d'une ressource protégée par {{site.data.keyword.amashort}} sur le noeud final `/protected`.

1. Envoyez une demande à un noeud final protégé de votre système de back end mobile dans votre navigateur en ouvrant
`{applicationRoute}/protected`, par exemple : `http://my-mobile-backend.mybluemix.net/protected`.
  Le noeud final `/protected` d'un système de back end mobile qui a été créé avec le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} est protégé par {{site.data.keyword.amashort}}. Ce noeud final n'est accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}. En conséquence, un message `Unauthorized` s'affiche dans le navigateur.

1. A l'aide de votre application iOS, envoyez une demande au même noeud final. Ajoutez le code ci-dessous après avoir initialisé `BMSClient`
et enregistré votre délégué d'authentification personnalisé :

 ```Swift
 let customResourceURL = "<chemin de votre ressource protégée>"
 let request = Request(url: customResourceURL, method: HttpMethod.GET)
 let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) in
 if error == nil {
      print ("response:\(response?.responseText), aucune erreur")
  } else {
      print ("erreur : \(error)")
  }
 }

 request.sendWithCompletionHandler(callBack)
 ```

1. 	Lorsque vos demandes aboutissent, la sortie suivante figure dans la console Xcode :

 ```
 onAuthenticationSuccess info = Optional({
     attributes =     {
     };
     deviceId = don;
     displayName = "Don+Lon";
     isUserAuthenticated = 1;
     userId = don;
 })
 response:Optional("Bonjour Don Lon"), no error
 ```

1. Vous pouvez également ajouter une fonctionnalité de déconnexion en ajoutant le code suivant :

 ```
 MCAAuthorizationManager.sharedInstance.logout(callBack)
 ```  

 Si vous appelez ce code alors qu'un utilisateur est connecté, l'utilisateur est déconnecté. Lorsque l'utilisateur tente de se reconnecter,
il doit à nouveau soumettre ses données d'identification.

 La transmission de `callBack` à la fonction de déconnexion est facultative. Vous pouvez également transmettre la valeur
`nil`.
