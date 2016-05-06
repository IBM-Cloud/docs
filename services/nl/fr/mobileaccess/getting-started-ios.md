---

Copyright : 2015, 2016

---

# Configuration du SDK Objective-C pour iOS
{: #getting-started-ios}

Instrumentez votre application iOS avec le SDK {{site.data.keyword.amashort}}, initialisez le SDK et envoyez des demandes à des ressources protégées et non protégées.

**Astuce :** Si vous développez votre application iOS dans Swift, vous pouvez envisager d'utiliser le SDK Swift client de
{{site.data.keyword.amashort}}. Pour plus d'informations, voir [Configuration du SDK Swift pour
iOS](getting-started-ios-swift-sdk.html)

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
	pod 'IMFCore'
	```

1. Sauvegardez le fichier `Podfile` et exécutez `pod install` à partir de la ligne de commande. <br/>Cocoapods installe les dépendances qui ont été ajoutées. La progression et les composants ajoutés s'affichent.<br/>
**Important** : CocoaPods génère un fichier `xcworkspace`.  A partir de ce moment, vous devrez toujours ouvrir ce fichier pour travailler sur votre projet.

1. Ouvrez l'espace de travail de votre projet iOS. Ouvrez le fichier `xcworkspace` qui a été généré par CocoaPods. Par exemple : `{your-project-name}.xcworkspace`. Exécutez `open {your-project-name}.xcworkspace`.

## Initialisation du logiciel SDK client de {{site.data.keyword.amashort}}
{: #init-mca-sdk-ios}

Pour pouvoir utiliser le SDK client de {{site.data.keyword.amashort}}, vous devez l'initialiser en transmettant les paramètres
**Route** (`applicationRoute`) et **App GUID** (`applicationGUID`).


1. Dans la page principale du tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur votre appli. Cliquez sur **Options pour application mobile**. Vous
aurez besoin des valeurs de **Route** et de **Identificateur global unique de l'application** pour initialiser le SDK.

1. Importez l'infrastructure `IMFCore` dans la classe qui doit utiliser
le SDK client de {{site.data.keyword.amashort}} en ajoutant l'en-tête suivant :

	**Objective-C:**
	 ```Objective-C
	#import <IMFCore/IMFCore.h>
	```

	**Swift :**

	Le SDK client de {{site.data.keyword.amashort}} est implémenté avec Objective-C. Il peut être nécessaire d'ajouter un en-tête de pontage à votre projet Swift :

	1. Cliquez avec le bouton droit sur votre projet dans Xcode, puis sélectionnez **New File... (Nouveau fichier...)**.
	1. Dans la catégorie **iOS Source (Source iOS)**, cliquez sur **Header file (Fichier d'en-tête)**. Nommez le fichier `BridgingHeader.h`.
	1. Ajoutez la ligne suivante à votre en-tête de pontage : `#import <IMFCore/IMFCore.h>`
	1. Cliquez sur votre projet dans Xcode et sélectionnez l'onglet **Build Settings (Paramètres de génération)**.
	1. Recherchez `Objective-C Bridging Header`.
	1. Définissez la valeur sur l'emplacement de votre fichier `BridgingHeader.h`, par exemple : `$(SRCROOT)/MyApp/BridgingHeader.h`.
	1. Vérifiez que l'en-tête de pontage est prélevé par Xcode lors de la génération de votre projet. Vous ne devez voir aucun message d'erreur.

1. Utilisez le code suivant pour initialiser le SDK client de {{site.data.keyword.amashort}}.  En général, vous pouvez placer le code d'initialisation dans la méthode `application:didFinishLaunchingWithOptions` du délégué de l'application, bien que cet emplacement ne soit pas obligatoire. <br/>Remplacez *applicationRoute* et *applicationGUID* par les valeurs de la section **Options pour application mobile** du tableau de bord {{site.data.keyword.Bluemix_notm}}.

	**Objective-C :**

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	**Swift :**

	```Swift
IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",backendGUID: "applicationGUID")
	```

## Envoi d'une demande au système de back end mobile
{: #request}

Lorsque le SDK client de {{site.data.keyword.amashort}} est initialisé, vous pouvez commencer à envoyer des demandes à votre système de back end mobile.

1. Depuis votre navigateur, tentez d'envoyer une demande à un noeud final protégé de votre système de back end mobile. Ouvrez l'URL suivante :
`{applicationRoute}/protected`. Par exemple : `http://my-mobile-backend.mybluemix.net/protected`
<br/>Le noeud final `/protected` d'un système de back end mobile qui a été créé avec le conteneur boilerplate MobileFirst Services Starter est protégé par {{site.data.keyword.amashort}}. Un message `Unauthorized` est renvoyé à votre navigateur car ce noeud final n'est accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}.

1. A l'aide de votre application iOS, envoyez une demande au même noeud final. Ajoutez le code ci-dessous après avoir initialisé `IMFClient` :

	**Objective-C :**

	```Objective-C
	NSString *requestPath = [NSString stringWithFormat:@"%@/protected",
								[[IMFClient sharedInstance] backendRoute]];

	IMFResourceRequest *request =  [IMFResourceRequest requestWithPath:requestPath
																method:@"GET"];

	[request sendWithCompletionHandler:^(IMFResponse *response, NSError *error) {
		if (error){
			NSLog(@"Error :: %@", [error description]);
		} else {
			NSLog(@"Response :: %@", [response responseText]);
		}
	}];
	```

	**Swift :**

	```Swift
	let requestPath = IMFClient.sharedInstance().backendRoute + "/protected"

	let request = IMFResourceRequest(path: requestPath, method: "GET");
	request.sendWithCompletionHandler { (response, error) -> Void in
		if (nil != error){
			NSLog("Error :: %@", error.description)
		} else {
			NSLog("Response :: %@", response.responseText)
		}
	};

	```

1.  Lorsque votre demande aboutit, la sortie suivante figure dans la console Xcode :

	![image](images/getting-started-ios-success.png)

## Etapes suivantes
{: #next-steps}
Lorsque vous vous êtes connecté au noeud final protégé, les données d'identification n'ont pas été nécessaires. Pour obliger les utilisateurs à utiliser des données d'identification pour se connecter à votre application, vous devez configurer Facebook, Google ou l'authentification personnalisée.
  * [Facebook](facebook-auth-ios.html)
  * [Google](google-auth-ios.html)
  * [Authentification personnalisée](custom-auth-ios.html)
