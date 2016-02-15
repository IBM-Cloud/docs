# Configuration du SDK client de {{site.data.keyword.amashort}} pour iOS
{: #custom-ios}

Configurez votre application iOS qui utilise l'authentification personnalisée de manière qu'elle utilise le SDK client de {{site.data.keyword.amashort}} et connectez-la à {{site.data.keyword.Bluemix}}.

## Avant de commencer
{: #before-you-begin}
Vous devez disposer d'une ressource protégée par une instance du service {{site.data.keyword.amashort}} qui est configuré pour utiliser un fournisseur d'identité personnalisé. Votre appli mobile doit aussi être instrumentée à l'aide du SDK client de {{site.data.keyword.amashort}}. Pour plus d'informations, voir les sujets suivants :
 * [Initiation à {{site.data.keyword.amashort}}](getting-started.html)
 * [Configuration du SDK iOS](getting-started-ios.html)
 * [Utilisation d'un fournisseur d'identité personnalisé](custom-auth.html)
 * [Création d'un fournisseur d'identité personnalisé](custom-auth-identity-provider.html)
 * [Configuration de {{site.data.keyword.amashort}} pour l'authentification personnalisée](custom-auth-config-mca.html)



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

Initialisez le SDK en passant les paramètres suivants : l'identificateur unique global de l'application (applicationGUID) et la route de l'application (applicationRoute). En général, vous pouvez placer le code d'initialisation dans la méthode `application:didFinishLaunchingWithOptions` du délégué de l'application, bien que cet emplacement ne soit pas obligatoire. 

1. Récupérez les valeurs de ces paramètres pour votre application. Ouvrez votre appli dans le tableau de bord {{site.data.keyword.Bluemix_notm}}. Cliquez sur **Options pour application mobile**. Les valeurs de *Route de l'application* et d'*Identificateur global unique de l'application* sont affichées.

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

1. Initialisez le logiciel SDK client. Remplacez applicationRoute et applicationGUID par les valeurs issues de **Options pour application mobile**.

	Objective-C :

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	Swift :

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("https://abms.mybluemix.net",
	 							backendGUID: "c3f8f2ba-5892-4362-95cf-744692cc7341")
	```


## Délégué IMFAuthenticationHandler
{: #custom-ios-sdk-authhandler}


Le SDK client de {{site.data.keyword.amashort}} fournit l'interface `IMFAuthenticationHandler` permettant d'implémenter un flux d'authentification personnalisé. `IMFAuthenticationHandler` expose trois méthodes qui sont appelées dans différentes phases du processus d'authentification.

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
 						didReceiveAuthenticationChallenge:(NSDictionary*)challenge;
```

Cette méthode est appelée lorsqu'une demande d'authentification personnalisée reçue provient du service {{site.data.keyword.amashort}}. Les arguments sont les suivants : 

* Le protocole `IMFAuthenticationContext` est fourni par le SDK client de {{site.data.keyword.amashort}} pour permettre au développeur de communiquer les réponses aux demandes d'authentification ou les échecs de collecte des données d'identification (par exemple, lorsque l'utilisateur annule la demande d'authentification). 
* `NSDictionary` contient une demande d'authentification personnalisée, renvoyée par un fournisseur d'identité personnalisé.

En appelant la méthode `authenticationContext:didReceiveAuthenticationChallenge`, le SDK client de {{site.data.keyword.amashort}} délègue le contrôle au développeur et se positionne en mode d'attente des données d'identification. Il est de la responsabilité du développeur de collecter les données d'identification et les fournir au SDK client de {{site.data.keyword.amashort}} par l'une des méthodes du protocole `IMFAuthenticationContext` décrites ci-dessous.

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationSuccess:(NSDictionary *)userInfo;
```

Cette méthode est appelée après une authentification réussie. Les arguments sont IMFAuthenticationContext et l'argument facultatif NSDictionary qui contient des informations détaillées sur la réussite de l'authentification.

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationFailure:(NSDictionary*)userInfo;
```

Cette méthode est appelée après un échec d'authentification. Les arguments sont IMFAuthenticationContext et l'argument facultatif NSDictionary qui contient des informations détaillées sur l'échec de l'authentification.

## Protocole IMFAuthenticationContext
{: #custom-ios-sdk-authcontext}


`IMFAuthenticationContext`` est fourni comme argument de la méthode `authenticationContext:didReceiveAuthenticationChallenge` d'une interface `IMFAuthenticationHandler` personnalisée. Le développeur doit collecter les données d'identification et utiliser les méthodes `AuthenticationContext`` pour renvoyer des données d'identification au SDK client de {{site.data.keyword.amashort}} ou pour signaler un incident. Utilisez l'une des méthodes suivantes :

```
-(void) submitAuthenticationChallengeAnswer:(NSDictionary*) answer;

-(void) submitAuthenticationFailure:(NSDictionary*) userInfo;
```

## Exemple d'implémentation d'un délégué d'authentification IMF personnalisé
{: #custom-ios-sdk-sample}


Cet exemple IMFAuthenticationDelegate est conçu pour fonctionner avec l'exemple de fournisseur d'identité personnalisé. Vous pouvez le télécharger depuis le [référentiel Github](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample).

Implémentation Objective-C :

``` Objective-C
CustomAuthenticationDelegate.h
-----------------------------------
#import <Foundation/Foundation.h>

@import IMFCore;
@interface CustomAuthenticationDelegate : NSObject <IMFAuthenticationDelegate>
@end


CustomAuthenticationDelegate.m
-----------------------------------
#import "CustomAuthenticationDelegate.h"

@implementation CustomAuthenticationDelegate

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationChallenge:(NSDictionary *)challenge {

	NSLog(@"didReceiveAuthenticationChallenge :: %@", challenge);

	// In this sample the IMFAuthenticationDelegate immediatelly returns a hardcoded
	// set of credentials. In a real life scenario this is where developer would
	// show a login screen, collect credentials and invoke
	// [context submitAuthenticationChallengeAnswer:] API

	NSDictionary *challengeAnswer = [NSDictionary dictionaryWithObjectsAndKeys:
									 @"john.lennon", @"username",
									 @"12345", @"password", nil];

	[context submitAuthenticationChallengeAnswer:challengeAnswer];

	// In case there was a failure collecting credentials you need to report
	// it back to the IMFAuthenticationContext. Otherwise Mobile Client
	// Access Client SDK will remain in a waiting-for-credentials state
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

		// In this sample the IMFAuthenticationDelegate immediatelly returns a hardcoded
		// set of credentials. In a real life scenario this is where developer would
		// show a login screen, collect credentials and invoke
		// context.submitAuthenticationChallengeAnswer() API

		let challengeAnswer: [String:String] = [
			"username":"john.lennon",
			"password":"12345"
		]

		context.submitAuthenticationChallengeAnswer(challengeAnswer)

		// In case there was a failure collecting credentials you need to report
		// it back to the IMFAuthenticationContext. Otherwise Mobile Client
		// Access Client SDK will remain in a waiting-for-credentials state
		// forever
	}


	func authenticationContext(context: IMFAuthenticationContext!, didReceiveAuthenticationSuccess userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationSuccess")
	}

	func authenticationContext(context: IMFAuthenticationContext!, didReceiveAuthenticationFailure userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationFailure")
	}
}
```

## Enregistrement d'un délégué d'authentification IMF personnalisé

Après avoir créé un IMFAuthenticationDelegate, enregistrez-le avec `IMFClient`.
Le code ci-dessous doit être appelé dans votre application avant l'envoi de demandes à vos ressources protégées. Utilisez le nom de domaine que vous avez défini dans le tableau de bord {{site.data.keyword.amashort}}.

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
Lorsque le SDK client est initialisé et qu'un `IMFAuthenticationDelegate` personnalisé est enregistré, vous pouvez commencer à envoyer des demandes à votre système de back end mobile.

### Avant de commencer
{: #custom-ios-testing-before}
 Vous devez disposer d'une application créée avec un conteneur boilerplate {{site.data.keyword.mobilefirstbp}} et d'une ressource protégée par {{site.data.keyword.amashort}} sur le noeud final `/protected`.


 1. Envoyez une demande à un noeud final protégé de votre système de back end mobile dans votre navigateur en ouvrant
`http://{appRoute}/protected`, par exemple `http://my-mobile-backend.mybluemix.net/protected`.
  Le noeud final `/protected` d'un système de back end mobile qui a été créé avec le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} est protégé par {{site.data.keyword.amashort}}. Ce noeud final n'est accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}. En conséquence, un message `Unauthorized` s'affiche dans le navigateur.
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
