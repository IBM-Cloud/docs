---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-07"

---

# Configuration du SDK client {{site.data.keyword.amashort}} pour iOS (Objective-C)
{: #custom-ios}


Configurez votre application iOS qui utilise l'authentification personnalisée afin qu'elle se serve du SDK client de {{site.data.keyword.amafull}} et connectez-la à {{site.data.keyword.Bluemix}}.

**Remarque :** si vous développez votre application iOS dans Swift, vous pouvez envisager d'utiliser le SDK Swift client de {{site.data.keyword.amashort}}. Les instructions de cette page s'appliquent au SDK client Objective-C de {{site.data.keyword.amashort}}. Pour les instructions d'utilisation du nouveau SDK Swift, voir [Configuration du SDK client de {{site.data.keyword.amashort}} pour iOS (SDK Swift)](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-ios-swift-sdk.html).

## Avant de commencer
{: #before-you-begin}
Vous devez disposer des éléments suivants :

* Ressource protégée par une instance du service {{site.data.keyword.amashort}} qui est configurée pour utiliser un fournisseur d'identité personnalisé (voir [Configuration de l'authentification personnalisée](https://console.stage1.ng.bluemix.net/docs/services/mobileaccess/custom-auth-config-mca.html)).  
* Valeur de votre **TenantID**. Ouvrez votre service dans le tableau de bord de {{site.data.keyword.amashort}}. Cliquez sur le bouton **Options pour application mobile**. La valeur `tenantId` (qui porte également le nom d'`appGUID`) est affichée dans la zone **App GUID / TenantId**. Vous aurez besoin de cette valeur pour initialiser le Gestionnaire des autorisations.
* Nom de votre **Realm**. Il s'agit de la valeur que vous avez spécifiée dans la zone **Nom du domaine** de la section **Personnalisé** dans l'onglet **Gestion** du tableau de bord de {{site.data.keyword.amashort}} (voir [Configuration de l'authentification personnalisée](https://console.stage1.ng.bluemix.net/docs/services/mobileaccess/custom-auth-config-mca.html)).
* L'URL de votre application back-end (**Route de l'application**). Vous aurez besoin de ces valeurs pour envoyer des requêtes aux noeuds finaux protégés de votre application back end.
* Votre **région** {{site.data.keyword.Bluemix_notm}}. Vous pouvez trouver votre région {{site.data.keyword.Bluemix_notm}} actuelle dans l'en-tête, en regard de l'icône **Avatar**![icône Avatar](images/face.jpg "icône Avatar"). La valeur de la région qui apparaît doit être l'une des suivantes : `US South`, `United Kingdom` ou `Sydney`, et correspondre aux valeurs requises dans le code Javascript de WebView : `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` ou `BMSClient.REGION_SYDNEY`. Vous aurez besoin de cette valeur pour initialiser le client {{site.data.keyword.amashort}}.

Pour plus d'informations, voir les sujets suivants :
 * [Initiation à {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Configuration du SDK Objective-C pour iOS](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html)
 * [Utilisation d'un fournisseur d'identité personnalisé](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Création d'un fournisseur d'identité personnalisé](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configuration de {{site.data.keyword.amashort}} pour l'authentification personnalisée](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## Installation du logiciel SDK client avec CocoaPods
{: #custom-ios-sdk-cocoapods}
Utilisez le gestionnaire de dépendances CocoaPods pour installer le SDK client de {{site.data.keyword.amashort}}.

1. Ouvrez Terminal et accédez au répertoire racine de votre projet iOS.

1. Editez le fichier `Podfile` et ajoutez la ligne suivante.

	```
	pod 'IMFCore'
	```

1. Depuis la ligne de commande, exécutez `pod install`.
CocoaPods installe les dépendances qui ont été ajoutées. La progression et les composants ajoutés s'affichent.

    **Important** : A partir de ce moment, vous devrez toujours ouvrir votre projet à l'aide d'un fichier `xcworkspace` généré par CocoaPods. Son nom est généralement `{your-project-name}.xcworkspace`.

1. Exécutez `open {your-project-name}.xcworkspace` depuis la ligne de commande pour ouvrir l'espace de travail de votre projet iOS.

### Initialisation du logiciel SDK client
{: #custom-ios-sdk-initialize}

Initialisez le SDK en transmettant les paramètres de **App Route** (`applicationRoute`) et **TenantID** (`tenantID`). 

En général, vous pouvez placer le code d'initialisation dans la méthode `application:didFinishLaunchingWithOptions` du délégué de l'application, bien que cet emplacement ne soit pas obligatoire.

1. Importez l'infrastructure `IMFCore` dans la classe qui doit utiliser le SDK client.

	Objective-C :

	```Objective-C
	#import <IMFCore/IMFCore.h>
	```

	Swift :

	Le SDK client de {{site.data.keyword.amashort}} est implémenté avec Objective-C. Il peut être nécessaire d'ajouter un en-tête de pontage à votre projet Swift pour utiliser le logiciel SDK.

	* Cliquez avec le bouton droit sur votre projet dans Xcode, puis sélectionnez **New File... (Nouveau fichier...)**.
	* Dans la catégorie **iOS Source (Source iOS)**, sélectionnez **Header file (Fichier d'en-tête)**. Nommez le fichier `BridgingHeader.h`.
	* Ajoutez `#import <IMFCore/IMFCore.h>` à votre en-tête de pontage.
	* Cliquez sur votre projet dans Xcode et sélectionnez l'onglet **Build Settings (Paramètres de génération)**.
	* Recherchez `Objective-C Bridging Header`.
	* Définissez la valeur sur l'emplacement de votre fichier `BridgingHeader.h`, par exemple : `$(SRCROOT)/MyApp/BridgingHeader.h`
	* Vérifiez que l'en-tête de pontage est prélevé par Xcode lors de la génération de votre projet.

1. Initialisez le logiciel SDK client. Remplacez les paramètres **App Route** (`applicationRoute`) et **TenantID** (`tenantID`) par des valeurs. Pour plus d'informations sur l'obtention de ces valeurs, voir [Avant de commencer](##before-you-begin).

	Objective-C :

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"tenantID"];
	```

	Swift :

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "tenantID")
	```

## Initialisation du gestionnaire AuthorizationManager
Initialisez le gestionnaire AuthorizationManager en transmettant le paramètre `tenantId` du service {{site.data.keyword.amashort}}. 


### Objective-C :

```Objective-
 [[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"tenantId"];
```

### Swift :

```Swift
  IMFAuthorizationManager.sharedInstance().initializeWithTenantId("tenantId")
```


## Délégué IMFAuthenticationHandler
{: #custom-ios-sdk-authhandler}


Le SDK client de {{site.data.keyword.amashort}} fournit l'interface `IMFAuthenticationHandler` permettant d'implémenter un flux d'authentification personnalisé. `IMFAuthenticationHandler` expose trois méthodes qui sont appelées dans différentes phases du processus d'authentification.

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
 						didReceiveAuthenticationChallenge:(NSDictionary*)challenge;
```

Cette méthode est appelée lorsqu'une demande d'authentification personnalisée reçue provient du service {{site.data.keyword.amashort}}. Les arguments sont les suivants :

* Le protocole `IMFAuthenticationContext` est fourni par le SDK client de {{site.data.keyword.amashort}} pour permettre au développeur de communiquer les réponses aux demandes d'authentification ou les échecs de collecte des données d'identification (en cas d'annulation de la part d'un utilisateur, par exemple).
* `NSDictionary` contient une demande d'authentification personnalisée, renvoyée par un fournisseur d'identité personnalisé.

En appelant la méthode `authenticationContext:didReceiveAuthenticationChallenge`, le SDK client de {{site.data.keyword.amashort}} délègue le contrôle au développeur et se positionne en mode d'attente des données d'identification. Il est de la responsabilité du développeur de collecter les données d'identification et de les fournir au SDK client de {{site.data.keyword.amashort}} en utilisant l'une des méthodes du protocole `IMFAuthenticationContext` suivantes :

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationSuccess:(NSDictionary *)userInfo;
```

Cette méthode est appelée après une authentification réussie. Les arguments comprennent `IMFAuthenticationContext` et un élément `NSDictionary` facultatif contenant des informations détaillées sur le succès de l'authentification.

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationFailure:(NSDictionary*)userInfo;
```

Cette méthode est appelée après un échec d'authentification. Les arguments comprennent `IMFAuthenticationContext` et un élément `NSDictionary` facultatif contenant des informations détaillées sur l'échec de l'authentification.

## Protocole IMFAuthenticationContext
{: #custom-ios-sdk-authcontext}


Le protocole `IMFAuthenticationContext` est fourni comme argument de la méthode `authenticationContext:didReceiveAuthenticationChallenge` d'un gestionnaire `IMFAuthenticationHandler` personnalisé. Il est de la responsabilité du développeur de collecter les données d'identification et d'utiliser les méthodes `IMFAuthenticationContext` pour renvoyer des données d'identification au SDK client de {{site.data.keyword.amashort}} ou pour signaler un incident. 
```
-(void) submitAuthenticationChallengeAnswer:(NSDictionary*) answer;

-(void) submitAuthenticationFailure:(NSDictionary*) userInfo;
```

## Exemple d'implémentation d'un délégué d'authentification IMF personnalisé
{: #custom-ios-sdk-sample}


L'exemple IMFAuthenticationDelegate est conçu pour fonctionner avec l'exemple de fournisseur d'identité personnalisé. Vous pouvez le télécharger depuis le [référentiel GitHub](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample).

Objective-C :

``` Objective-C
CustomAuthenticationDelegate.h
-----------------------------------
# import <Foundation/Foundation.h>

@import IMFCore;
@interface CustomAuthenticationDelegate : NSObject <IMFAuthenticationDelegate>
@end


CustomAuthenticationDelegate.m
-----------------------------------
# import "CustomAuthenticationDelegate.h"

@implementation CustomAuthenticationDelegate

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationChallenge:(NSDictionary *)challenge{

	NSLog(@"didReceiveAuthenticationChallenge :: %@", challenge);

	// In this sample, the IMFAuthenticationDelegate immediately returns a hardcoded
	// set of credentials. In a real life scenario, a developer would
	// show a login screen, collect credentials and invoke the
	// [context submitAuthenticationChallengeAnswer:] API

	NSDictionary *challengeAnswer = [NSDictionary dictionaryWithObjectsAndKeys:
									 @"john.lennon", @"username",
									 @"12345", @"password", nil];

	[context submitAuthenticationChallengeAnswer:challengeAnswer];

	// In case there is a failure collecting credentials, report
	// the failure to IMFAuthenticationContext. Otherwise, the Mobile Client
	// Access client SDK remains in a waiting-for-credentials state
	// forever
}

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationSuccess:(NSDictionary *)userInfo{
	NSLog(@"didReceiveAuthenticationSuccess");


}

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationFailure:(NSDictionary *)userInfo{
	NSLog(@"didReceiveAuthenticationFailure");

}

@end
```

Implémentation Swift :

```Swift
import Foundation

class CustomAuthenticationDelegate : NSObject, IMFAuthenticationDelegate{

	func authenticationContext(context: IMFAuthenticationContext!, didReceiveAuthenticationChallenge challenge: [NSObject : AnyObject]!) {

		NSLog("didReceiveAuthenticationChallenge :: %@", challenge)

		// In this sample, the IMFAuthenticationDelegate immediately returns a hardcoded
		// set of credentials. In a real life scenario a developer would
		// show a login screen, collect credentials and invoke the
		// context.submitAuthenticationChallengeAnswer() API

		let challengeAnswer: [String:String] = [
			"username":"john.lennon",
			"password":"12345"
		]

		context.submitAuthenticationChallengeAnswer(challengeAnswer)

		// In case there is a failure collecting credentials, report
		// it back to IMFAuthenticationContext. Otherwise, the Mobile Client
		// Access client SDK remains in a waiting-for-credentials state
		// forever
	}


	func authenticationContext(context: IMFAuthenticationContext!,
					didReceiveAuthenticationSuccess userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationSuccess")
	}

	func authenticationContext(context: IMFAuthenticationContext!, didReceiveAuthenticationFailure userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationFailure")
	}
}
```

## Enregistrement d'un délégué d'authentification IMF personnalisé

Après avoir créé un élément `IMFAuthenticationDelegate` personnalisé, enregistrez-le avec `IMFClient`. Le code ci-dessous doit être appelé dans votre application avant l'envoi de demandes à vos ressources protégées. Utilisez le nom de domaine que vous avez spécifié dans le tableau de bord {{site.data.keyword.amashort}}.

Applications Objective-C :

```Objective-C
[[IMFClient sharedInstance]
				registerAuthenticationDelegate:[CustomAuthenticationDelegate new]
										forRealm:realmName];
```

Applications Swift :
```Swift
IMFClient.sharedInstance().registerAuthenticationDelegate(CustomAuthenticationDelegate(),
									forRealm: realmName)
```


## Test de l'authentification
{: #custom-ios-testing}
Après avoir initialisé le SDK client et enregistré un délégué `IMFAuthenticationDelegate` personnalisé, vous pouvez commencer à envoyer des demandes à votre application back end mobile.

### Avant de commencer
{: #custom-ios-testing-before}
 Vous devez disposer d'une application créée avec un conteneur boilerplate {{site.data.keyword.mobilefirstbp}} et d'une ressource protégée par {{site.data.keyword.amashort}} sur le noeud final `/protected`.

1. Envoyez une demande à un noeud final protégé de votre application de back end mobile dans votre navigateur en ouvrant `{applicationRoute}/protected`, par exemple : `http://my-mobile-backend.mybluemix.net/protected`.
  Le noeud final `/protected` d'une application de back end mobile qui a été créée avec le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} est protégé par {{site.data.keyword.amashort}}. Ce noeud final n'est accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}. En conséquence, un message `Unauthorized` s'affiche dans le navigateur.
1. A l'aide de votre application iOS, envoyez une demande au même noeud final. Ajoutez le code ci-dessous après avoir initialisé `BMSClient` et enregistré votre `IMFAuthenticationDelegate` personnalisé.

	Objective-C :

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
			NSLog(@"%@", [[IMFAuthorizationManager sharedInstance] userIdentity]);
		}
	}];
	```

	Swift :

	```Swift
	let requestPath = IMFClient.sharedInstance().backendRoute + "/protected"

	let request = IMFResourceRequest(path: requestPath, method: "GET");
	request.sendWithCompletionHandler { (response, error) -> Void in
		if (nil != error){
			NSLog("Error :: %@", error.description)
		} else {
			NSLog("Response :: %@", response.responseText)
			NSLog("%@", IMFAuthorizationManager.sharedInstance().userIdentity)
		}
	};

	```
1. 	Lorsque vos demandes aboutissent, la sortie suivante figure dans la console Xcode :

	![image](images/ios-custom-login-success.png)

	Vous pouvez également ajouter une fonctionnalité de déconnexion en ajoutant le code suivant :

	Objective C:

	```Objective-C
	[[IMFAuthorizationManager sharedInstance] logout : callBack]
	```

	Swift :

	```Swift
	IMFAuthorizationManager.sharedInstance().logout(callBack)
	```

 Si vous appelez ce code alors qu'un utilisateur est connecté, l'utilisateur est déconnecté. Lorsque l'utilisateur tente de se reconnecter,
il doit à nouveau soumettre ses données d'identification.

 La transmission de `callBack` à la fonction de déconnexion est facultative. Vous pouvez également transmettre
la valeur `nil`.
