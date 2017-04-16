---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"

---
{:shortdesc: .shortdesc}

# Configuration du SDK iOS Objective-C
{: #getting-started-ios}

Instrumentez votre application iOS avec le SDK {{site.data.keyword.amafull}}, initialisez le SDK et envoyez des requêtes à des ressources protégées et
non protégées.

{:shortdesc}

**Important :** Bien que le SDK Objective-C reste complètement pris en charge et soit toujours considéré comme le SDK principal pour
{{site.data.keyword.Bluemix_notm}} Mobile Services, il est envisagé de le retirer plus tard dans l'année et de le remplacer par le nouveau SDK Swift. Pour les nouvelles applications, il est vivement recommandé d'utiliser le SDK Swift (voir [Configuration du SDK Swift iOS](getting-started-ios-swift-sdk.html)).

## Avant de commencer
{: #before-you-begin}
Vous devez disposer des éléments suivants :
* Une instance d'une application {{site.data.keyword.Bluemix_notm}} protégée par le service
{{site.data.keyword.amashort}}. Pour plus d'informations sur la création d'un système de back end {{site.data.keyword.Bluemix_notm}}, voir [Initiation](index.html).
* Valeur de votre **TenantID**. Ouvrez votre service dans le tableau de bord de {{site.data.keyword.amashort}}. Cliquez sur **Options pour application mobile**. Les valeurs `tenantId` (qui portent également le nom d'`appGUID`) sont affichées dans la zone **App GUID / TenantId**. Vous aurez besoin de cette valeur pour initialiser le Gestionnaire des autorisations {{site.data.keyword.amashort}}.
* Votre **Application Route**. Il s'agit de l'URL de votre application back end. Vous avez besoin de cette valeur pour envoyer des demandes à ses noeuds finaux protégés.
* Un projet Xcode.  


## Installation du SDK client de {{site.data.keyword.amashort}}
{: #install-mca-sdk-ios}
Le SDK {{site.data.keyword.amashort}} est distribué avec CocoaPods, un gestionnaire de dépendances pour les projets iOS. CocoaPods télécharge automatiquement
des artefacts depuis les référentiels et les rend disponibles depuis votre application iOS.


### Installation de CocoaPods
{: #install-cocoapods}

1. Ouvrez Terminal et lancez la commande **pod --version**. Si CocoaPods est déjà installé, le numéro de version est affiché. Passez à la section suivante pour installer le SDK.

1. Si CocoaPods n'est pas installé, exécutez la commande :

```
sudo gem install cocoapods
```

Pour plus d'informations, reportez-vous au [site Web CocoaPods](https://cocoapods.org/).

### Installation du SDK client de {{site.data.keyword.amashort}} avec CocoaPods
{: #install-sdk-cocoapods}

1. Dans Terminal, naviguez jusqu'au répertoire racine de votre projet iOS.

1. Si vous n'avez pas encore initialisé votre espace de travail pour CocoaPods, exécutez la commande `pod init`.<br/>
CocoaPods crée automatiquement un fichier `Podfile`, dans lequel vous définirez les dépendances de votre projet iOS.

1. Editez le fichier `Podfile` en lui ajoutant la ligne suivante vers les cibles requises et exécutez :


	`pod 'IMFCore'`

1. Enregistrez le fichier `Podfile` et lancez `pod install` depuis la ligne de commande. <br/>Cocoapods installe les
dépendances ajoutées et affiche les composants ajoutés.<br/>

	**Important** : CocoaPods génère un fichier `xcworkspace`.  A partir de ce moment, vous devrez toujours ouvrir ce fichier pour travailler sur votre projet.

1. Ouvrez l'espace de travail de votre projet iOS. Ouvrez le fichier `xcworkspace` qui a été généré par CocoaPods. Par exemple : `{your-project-name}.xcworkspace`. Exécutez `open {your-project-name}.xcworkspace`.

## Initialisation du logiciel SDK client de {{site.data.keyword.amashort}}
{: #init-mca-sdk-ios}

1. Importez l'infrastructure `IMFCore` dans la classe qui doit utiliser le SDK client de {{site.data.keyword.amashort}} en ajoutant l'en-tête suivant :

	####Objective-C
	{: #imfcore-objc}

	```Objective-C
	  #import <IMFCore/IMFCore.h>
	```

	####Swift
	{: #sdk-swift}

	Le SDK client de {{site.data.keyword.amashort}} est implémenté avec Objective-C. Il peut être nécessaire d'ajouter un en-tête de pontage à votre projet Swift :
	1. Cliquez avec le bouton droit sur votre projet dans Xcode et sélectionnez **New File**.
	1. Dans la catégorie **iOS Source (Source iOS)**, cliquez sur **Header file (Fichier d'en-tête)**. Nommez le fichier `BridgingHeader.h`.
	1. Ajoutez la ligne suivante à votre en-tête de pontage : `#import <IMFCore/IMFCore.h>`.
	1. Cliquez sur votre projet dans Xcode et sélectionnez l'onglet **Build Settings (Paramètres de génération)**.
	1. Recherchez `Objective-C Bridging Header`.
	1. Définissez la valeur sur l'emplacement de votre fichier `BridgingHeader.h`, par exemple : `$(SRCROOT)/MyApp/BridgingHeader.h`.
	1. Vérifiez que l'en-tête de pontage est prélevé par Xcode lors de la génération de votre projet. Vous ne devez voir aucun message d'erreur.

1. Utilisez le code suivant pour initialiser le SDK client de {{site.data.keyword.amashort}}.  En général, vous pouvez placer le code d'initialisation dans la méthode `application:didFinishLaunchingWithOptions` du délégué de l'application, bien que cet emplacement ne soit pas obligatoire. <br/>
Pour plus d'informations sur l'obtention des valeurs `applicationRoute` et `applicationGUID`, voir [Avant de commencer](#before-you-begin). 

	####Objective-C
	{: #sharedinstance-objc}

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	####Swift
	{: #sharedinstance-swift}
	```Swift
 		MFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",backendGUID: "applicationGUID")
	```

## Initialisation du gestionnaire AuthorizationManager
Initialisez le gestionnaire `AuthorizationManager` en transmettant le paramètre `tenantId` du service {{site.data.keyword.amashort}}. Pour des informations sur l'obtention de ces valeurs, voir [Avant de commencer](#before-you-begin). 

#### Objective-C

```Objective-C
[[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"<tenantId>"];
```

#### Swift

```Swift
IMFAuthorizationManager.sharedInstance().initializeWithTenantId("<tenantId>")
```

	
## Envoi d'une demande à votre application back end mobile
{: #request}

Une fois que le SDK client {{site.data.keyword.amashort}} est initialisé, vous pouvez commencer à envoyer des requêtes à votre application back end
mobile.

1. Essayez d'envoyer depuis votre navigateur une requête à un noeud final protégé de votre application back end mobile. Ouvrez l'URL suivante :
`{applicationRoute}/protected`. Par exemple : `http://my-mobile-backend.mybluemix.net/protected`
<br/>Le noeud final `/protected` d'une application back end mobile créée avec le conteneur boilerplate MobileFirst Services Starter est protégé par {{site.data.keyword.amashort}}. Un
message `Non autorisé` est renvoyé à votre navigateur car ce noeud final n'est accessible qu'aux applications mobiles instrumentées
avec le SDK client de {{site.data.keyword.amashort}}.

1. A l'aide de votre application iOS, envoyez une demande au même noeud final. Ajoutez le code ci-dessous après avoir initialisé `IMFClient` :

	####Objective-C
	{: #nsstring-objc}

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

	####Swift
	{: #imfclientrequestpath-swift}

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
Lors de la connexion au noeud final protégé, aucune donnée d'identification ne vous a été réclamée. Pour obliger les utilisateurs à utiliser des données d'identification pour se connecter à votre application, vous devez configurer Facebook, Google ou l'authentification personnalisée.
  * [Facebook](facebook-auth-ios.html)
  * [Google](google-auth-ios.html)
  * [Authentification personnalisée](custom-auth-ios.html)
