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


# Configuration du SDK Swift iOS
{: #getting-started-ios}

Instrumentez votre application Swift iOS avec le SDK {{site.data.keyword.amashort}}, initialisez le  the SDK et envoyez des requêtes à des ressources protégées et
non protégées.

{:shortdesc}


## Avant de commencer
{: #before-you-begin}
Vous devez disposer des éléments suivants :

* Une instance d'une application {{site.data.keyword.Bluemix_notm}}.
* Une instance d'un service {{site.data.keyword.amafull}}.
* Valeur de votre **TenantID**. Ouvrez votre service dans le tableau de bord {{site.data.keyword.amashort}}. Cliquez sur **Options pour application mobile**. Les valeurs `tenantId` (qui portent également le nom d'`appGUID`) sont affichées dans la zone **App GUID / TenantId**. Vous aurez besoin de cette valeur pour initialiser le Gestionnaire des autorisations {{site.data.keyword.amashort}}.
* Votre **Application Route**. Il s'agit de l'URL de votre application back end. Vous avez besoin de cette valeur pour envoyer des demandes à ses noeuds finaux protégés.
* Votre **région** {{site.data.keyword.Bluemix_notm}}.  Vous pouvez trouver votre région {{site.data.keyword.Bluemix_notm}} actuelle dans l'en-tête, en regard de l'icône **Avatar**![icône Avatar](images/face.jpg "icône Avatar"). La valeur de la région qui apparaît doit être l'une des suivantes : `US South`, `Sydney` ou `United Kingdom`, et correspondre aux valeurs SDK requises dans le code : `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` ou `BMSClient.Region.sydney`.  Vous aurez besoin de cette valeur pour initialiser le SDK {{site.data.keyword.amashort}}.
* Un projet Xcode. Pour plus d'informations sur la configuration de votre environnement de développement iOS, accédez au site Web [Apple Developer ![Icône de lien externe ](../../icons/launch-glyph.svg "Icône de lien externe ")](https://developer.apple.com/support/xcode/ "Icône de lien externe"){: new_window}.


## Installation du SDK client de {{site.data.keyword.amashort}}
{: #install-mca-sdk-ios}
Le SDK {{site.data.keyword.amashort}} est distribué avec CocoaPods, un gestionnaire de dépendances pour les projets iOS. CocoaPods télécharge automatiquement
des artefacts depuis les référentiels et les rend disponibles depuis votre application iOS.


### Installation de CocoaPods
{: #install-cocoapods}

1. Depuis une fenêtre de terminal, lancez la commande **pod --version**. Si CocoaPods est déjà installé, le numéro de version est affiché
et vous pouvez passer à la section suivante pour installer le SDK.

1. Si CocoaPods n'est pas installé, exécutez la commande :

```
sudo gem install cocoapods
```
{: codeblock}

Pour plus d'informations, reportez-vous au [site Web CocoaPods ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cocoapods.org/ "Icône de lien externe"){: new_window}.

### Installation du SDK client de {{site.data.keyword.amashort}} avec CocoaPods
{: #install-sdk-cocoapods}

1. Dans une fenêtre de terminal, naviguez jusqu'au répertoire racine de votre projet iOS.

1. Si vous n'avez pas encore initialisé votre espace de travail pour CocoaPods, exécutez la commande `pod init`.<br/>
CocoaPods crée automatiquement un fichier `Podfile`, dans lequel vous définirez les dépendances de votre projet iOS.

1. Editez le fichier `Podfile` et ajoutez la ligne suivante aux cibles requises.

	```
  use_frameworks!
  pod 'BMSSecurity'
	```
	{: codeblock}

  **Astuce :** Vous pouvez ajouter `use_frameworks!` à votre cible Xcode au lieu du Podfile.

1. Enregistrez le fichier `Podfile` et lancez `pod install` depuis la ligne de commande. CocoaPods installe les dépendances
pertinentes et affiche les dépendances et nacelles ajoutées.<br/>

   **Important** : CocoaPods génère un fichier `xcworkspace`.  A partir de ce moment, vous devrez toujours ouvrir ce fichier pour travailler sur votre projet.

1. Ouvrez l'espace de travail de votre projet iOS. Ouvrez le fichier `xcworkspace` qui a été généré par CocoaPods. Exemple : pour `{your-project-name}.xcworkspace`, exécutez

	`open {your-project-name}.xcworkspace`

### Activez le partage de chaîne de certificats pour iOS
{: #enable_keychain}

Activez le partage de chaîne de certificats, `Keychain Sharing`. Accédez à l'onglet `Capabilities` et basculez `Keychain Sharing` sur `On` dans votre projet Xcode.

## Initialisation du logiciel SDK client de {{site.data.keyword.amashort}}
{: #init-mca-sdk-ios}

 Initialisez le logiciel SDK en transmettant le paramètre `tenantId`. En général, vous pouvez placer le code d'initialisation dans la méthode `application:didFinishLaunchingWithOptions` du délégué de l'application, bien que cet emplacement ne soit pas obligatoire.

1. Importez les structures requises dans la classe où vous comptez utiliser le SDK client {{site.data.keyword.amashort}}.

 ```Swift
 import BMSCore
 import BMSSecurity
 ```

1. Initialisez le SDK client {{site.data.keyword.amashort}}.

 ```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: 
		[UIApplicationLaunchOptionsKey: Any]?) -> Bool {

	let mcaAuthManager = MCAAuthorizationManager.sharedInstance
    mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
      // possible values for regionName: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, BMSClient.Region.sydney
	BMSClient.sharedInstance.authorizationManager = mcaAuthManager	
	return true
	}
  ```
  {: codeblock}

* Remplacez la valeur `tenantId` par la valeur que vous avez obtenue depuis **Options pour application mobile**.
* Remplacez `<applicationBluemixRegion>` par la région dans laquelle votre application {{site.data.keyword.Bluemix_notm}} est hébergée.

Pour des informations sur ces valeurs, voir [Avant de commencer](#before-you-begin).


## Envoi d'une demande à votre application back end mobile
{: #request}

Une fois que le SDK client {{site.data.keyword.amashort}} est initialisé, vous pouvez commencer à envoyer des requêtes à votre application back end
mobile.

1. Essayez d'envoyer depuis votre navigateur une requête à un noeud final protégé de votre application back end mobile. Ouvrez l'URL suivante : `{applicationRoute}/protected`, en remplaçant `{applicationRoute}` par la valeur **applicationRoute** extraite depuis **Options pour application mobile** (voir [Initialisation du logiciel SDK client de Mobile Client Access](#init-mca-sdk-ios)). Exemple :

	`http://my-mobile-backend.mybluemix.net/protected
	`

	Un message `Non autorisé` est renvoyé à votre navigateur car ce noeud final n'est
accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}.

1. A l'aide de votre application iOS, envoyez une demande au même noeud final. Ajoutez le code ci-dessous après avoir initialisé `BMSClient` :

 ```Swift
	let customResourceURL = "<your protected resource absolute path>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
 if error == nil {
       	    print ("réponse :\(response?.responseText), aucune erreur")
     } else {
       	    print ("erreur : \(error)")
     }
	}

	request.send(completionHandler: callBack)
 ```
 {: codeblock}

1.  Lorsque votre demande aboutit, la sortie suivante figure dans la console Xcode :

 ```
 response:Optional("Bonjour, ceci est une ressource protégée de l'application back end mobile !"), no error
 ```
{: screen}

## Etapes suivantes
{: #next-steps}
Lorsque vous vous êtes connecté au noeud final protégé, les données d'identification n'ont pas été nécessaires. Pour obliger les utilisateurs à utiliser des données d'identification pour se connecter à votre application, vous devez configurer Facebook, Google ou l'authentification personnalisée.

  * [Facebook](facebook-auth-ios-swift-sdk.html)
  * [Google](google-auth-ios-swift-sdk.html)
  * [Authentification personnalisée](custom-auth-ios-swift-sdk.html)
