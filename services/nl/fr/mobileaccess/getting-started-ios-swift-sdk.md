---

Copyright : 2016

---

# Configuration du SDK Swift iOS
{: #getting-started-ios}

Instrumentez votre application iOS avec le SDK {{site.data.keyword.amashort}}, initialisez le SDK et envoyez des demandes à des ressources protégées et non protégées.

## Avant de commencer
{: #before-you-begin}
* Vous devez disposer d'une instance d'une application de back end mobile protégée par le service {{site.data.keyword.amashort}}. Pour plus d'informations sur la création d'un système de back end mobile, voir [Initiation](getting-started.html).
* Vérifiez que Xcode est correctement configuré. Pour plus d'informations sur la configuration de votre environnement de développement iOS, consultez le [site Web Apple Developer](https://developer.apple.com/support/xcode/).


## Installation du SDK client de {{site.data.keyword.amashort}}
{: #install-mca-sdk-ios}
Le SDK {{site.data.keyword.amashort}} est distribué avec CocoaPods, un gestionnaire de dépendances pour les projets iOS. CocoaPods télécharge automatiquement les artefacts à partir des référentiels et les met à la disposition de votre application iOS.


### Installation de CocoaPods
{: #install-cocoapods}
1. Ouvrez Terminal et lancez la commande **pod --version**. Si CocoaPods est déjà installé, le numéro de version est affiché. Vous pouvez passer à la section suivante pour installer le SDK.

1. Si CocoaPods n'est pas installé, exécutez la commande :
```
sudo gem install cocoapods
```
Pour plus d'informations, reportez-vous au [site Web CocoaPods](https://cocoapods.org/).

### Installation du logiciel SDK client de {{site.data.keyword.amashort}} avec CocoaPods
{: #install-sdk-cocoapods}

1. Dans Terminal, naviguez jusqu'au répertoire racine de votre projet iOS.

1. Si vous n'avez pas encore initialisé votre espace de travail pour CocoaPods, exécutez la commande `pod init`.<br/>
CocoaPods crée automatiquement un fichier `Podfile`, dans lequel vous définirez les dépendances de votre projet iOS.

1. Editez le fichier `Podfile` et ajoutez la ligne suivante aux cibles requises.

	```
  use_frameworks!
	pod 'BMSSecurity'
	```
  **Astuce :** Vous pouvez ajouter `use_frameworks!` à votre cible Xcode au lieu du Podfile.

1. Sauvegardez le fichier `Podfile` et exécutez `pod install` à partir de la ligne de commande. <br/>Cocoapods installe les dépendances qui ont été ajoutées. La progression et les composants ajoutés s'affichent.<br/>
**Important** : CocoaPods génère un fichier `xcworkspace`.  A partir de ce moment, vous devrez toujours ouvrir ce fichier pour travailler sur votre projet.

1. Ouvrez l'espace de travail de votre projet iOS. Ouvrez le fichier `xcworkspace` qui a été généré par CocoaPods. Par exemple : `{your-project-name}.xcworkspace`. Exécutez `open {your-project-name}.xcworkspace`.

## Initialisation du logiciel SDK client de {{site.data.keyword.amashort}}
{: #init-mca-sdk-ios}

 Initialisez le SDK en passant les paramètres `applicationRoute` et `applicationGUID`. En général, vous pouvez placer le code d'initialisation dans la méthode `application:didFinishLaunchingWithOptions` du délégué de l'application, bien que cet emplacement ne soit pas obligatoire.

1. Récupérez les valeurs de ces paramètres pour votre application. Ouvrez votre appli dans le tableau de bord {{site.data.keyword.Bluemix_notm}}. Cliquez sur **Options pour application mobile**. Les valeurs `applicationRoute` et `applicationGUID` sont affichées dans les zones **Route** et
**Identificateur global unique de l'application**.

1. Importez les structures requises dans la classe où vous comptez utiliser le SDK client {{site.data.keyword.amashort}}.

 ```Swift
 import BMSCore
 import BMSSecurity
 ```  

1. Initialisez le SDK client {{site.data.keyword.amashort}}. Remplacez `<applicationRoute>` et
`<applicationGUID>` par les valeurs de **Route** et **Identificateur global unique de l'application** de
la section **Options pour application mobile** dans le tableau de bord {{site.data.keyword.Bluemix_notm}}.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 // Initialisez le SDK client.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 return true
      }
 ```

## Envoi d'une demande au système de back end mobile
{: #request}

Lorsque le SDK client de {{site.data.keyword.amashort}} est initialisé, vous pouvez commencer à envoyer des demandes à votre système de back end mobile.

1. Depuis votre navigateur, tentez d'envoyer une demande à un noeud final protégé de votre système de back end mobile. Ouvrez l'URL suivante :
`http://{applicationRoute}/protected`. Par exemple : `http://my-mobile-backend.mybluemix.net/protected`
<br/>Le noeud final `/protected` d'un système de back end mobile qui a été créé avec le conteneur boilerplate MobileFirst Services Starter est protégé par {{site.data.keyword.amashort}}. Un message `Unauthorized` est renvoyé à votre navigateur car ce noeud final n'est accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}.

1. A l'aide de votre application iOS, envoyez une demande au même noeud final. Ajoutez le code ci-dessous après avoir initialisé `BMSClient` :

 ```Swift
 let customResourceURL = "<chemin de votre ressource protégée>"
 let request = Request(url: customResourceURL, method: HttpMethod.GET)
 let callBack:MfpCompletionHandler = {(response: Response?, error: NSError?) in
     if error == nil {
         print ("réponse :\(response?.responseText), aucune erreur")
     } else {
         print ("erreur : \(error)")
     }
 }

 request.sendWithCompletionHandler(callBack)
 ```

1.  Lorsque votre demande aboutit, la sortie suivante figure dans la console Xcode :

 ```
 response:Optional("Bonjour, ceci est une ressource protégée de l'application back end mobile !"), no error
 ```

## Etapes suivantes
{: #next-steps}
Lorsque vous vous êtes connecté au noeud final protégé, les données d'identification n'ont pas été nécessaires. Pour obliger les utilisateurs à utiliser des données d'identification pour se connecter à votre application, vous devez configurer Facebook, Google ou l'authentification personnalisée.
  * [Facebook](facebook-auth-ios-swift-sdk.html)
  * [Google](google-auth-ios-swift-sdk.html)
  * [Authentification personnalisée](custom-auth-ios-swift-sdk.html)
