---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

Le service {{site.data.keyword.amafull}} est remplacé par le service {{site.data.keyword.appid_full}}.

# Configuration d'une authentification personnalisée pour votre application {{site.data.keyword.amashort}} Cordova
{: #custom-cordova}

Instrumentez votre application Cordova pour utiliser l'authentification personnalisée et le SDK client d'{{site.data.keyword.amafull}} pour accéder à votre application protégée.

## Avant de commencer
{: #before-you-begin}
* Ressource protégée par une instance du service {{site.data.keyword.amashort}} qui est configurée pour utiliser un fournisseur d'identité personnalisé (voir [Configuration de l'authentification personnalisée](custom-auth-config-mca.html)).  
* Valeur de votre **TenantID**. Ouvrez votre service dans le tableau de bord de {{site.data.keyword.amashort}}. Cliquez sur le bouton **Options pour application mobile**. La valeur `tenantId` (qui porte également le nom d'`appGUID`) est affichée dans la zone **App GUID / TenantId**. Vous aurez besoin de cette valeur pour initialiser le Gestionnaire des autorisations.
* Nom de votre **Realm**. Il s'agit de la valeur que vous avez spécifiée dans la zone **Nom du domaine** de la section **Personnalisé** dans l'onglet **Gestion** du tableau de bord de {{site.data.keyword.amashort}}.
* Votre **région** {{site.data.keyword.Bluemix_notm}}. Vous pouvez trouver votre région {{site.data.keyword.Bluemix_notm}} actuelle dans l'en-tête, en regard de l'icône **Avatar**![icône Avatar](images/face.jpg "icône Avatar"). La valeur de région doit être l'une des suivantes : `US South`, `United Kingdom` ou `Sydney`. La syntaxe exacte des constantes SDK correspondantes est donnée dans les exemples de code.

Pour plus d'informations, voir les sujets suivants :

 * [Configuration de {{site.data.keyword.amashort}} pour l'authentification personnalisée](custom-auth-config-mca.html). Cet exemple montre comment configurer le service {{site.data.keyword.amashort}} pour l'authentification personnalisée. Ici, vous définissez la valeur de **Domaine**.
 * [Configuration du SDK Cordova](getting-started-cordova.html). Informations sur la configuration de l'appli client Cordova.
 * [Utilisation d'un fournisseur d'identité personnalisé](custom-auth.html). Comment authentifier des utilisateurs avec un fournisseur d'identité personnalisé.
 * [Création d'un fournisseur d'identité personnalisé](custom-auth-identity-provider.html). Exemples de fonctionnement d'un fournisseur d'identité personnalisé.

## Configurez votre code WebView Cordova
### Initialisation du SDK client {{site.data.keyword.amashort}} dans le WebView Cordova
{: #custom-cordova-sdk}
Initialisez le logiciel SDK en transmettant le paramètre `<applicationBluemixRegion>` dans le fichier `index.js`.

```JavaScript
BMSClient.initialize("<applicationBluemixRegion>");
```
{: codeblock}

Remplacez `<applicationBluemixRegion>` par votre région (voir [Avant de commencer](#before-you-begin)).


### Interface du programme d'écoute d'authentification
{: #custom-cordva-auth}

Le SDK client de {{site.data.keyword.amashort}} fournit une interface du programme d'écoute d'authentification permettant  d'implémenter un flux d'authentification personnalisé. Vous devez ajouter les méthodes suivantes, qui sont appelées dans différentes phases du processus d'authentification.

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...},
	onAuthenticationSuccess: function(info){...},
	onAuthenticationFailure: function(info){...}
}
```
{: codeblock}

Chaque méthode gère une phase du processus d'authentification.

### Méthode onAuthenticationChallengeReceived
{: #onAuthenticationChallengeReceived}
Cette méthode est appelée lorsqu'une demande d'authentification personnalisée reçue provient du service {{site.data.keyword.amashort}}.
```JavaScript
onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...}
```
{: codeblock}

* `authenticationContext` : Fourni par le SDK client de {{site.data.keyword.amashort}} pour permettre au développeur de communiquer les réponses aux demandes d'authentification ou les échecs de collecte des données d'identification (par exemple, lorsque l'utilisateur annule la demande d'authentification).
* `challenge` : Objet JSON qui contient une demande d'authentification personnalisée, renvoyée par un fournisseur d'identité personnalisé.

En appelant la méthode `onAuthenticationChallengeReceived`, le SDK client de {{site.data.keyword.amashort}} délègue le contrôle au développeur. {{site.data.keyword.amashort}} attend les données d'identification. Le développeur doit collecter les données d'identification et les fournir au SDK client de {{site.data.keyword.amashort}} par l'une des méthodes de l'interface `authContext`.

```JavaScript
onAuthenticationSuccess: function(info){...}
```
{: codeblock}

Cette méthode est appelée après une authentification réussie. Les arguments comprennent un objet JSON facultatif contenant des informations détaillées sur le succès de l'authentification.

```JavaScript
onAuthenticationFailure: function(info){...}
```
{: codeblock}

Cette méthode est appelée après un échec d'authentification. Les arguments comprennent un objet JSON facultatif contenant des informations détaillées sur l'échec de l'authentification.

### authenticationContext
{: #custom-cordova-authcontext}

La valeur de `authenticationContext` est fournie comme argument de la méthode `onAuthenticationChallengeReceived` d'un programme d'écoute d'authentification. Le développeur doit collecter les données d'identification et utiliser les méthodes `authenticationContext` pour renvoyer des données d'identification au SDK client de {{site.data.keyword.amashort}} ou pour signaler un incident. Utilisez l'une des méthodes suivantes :

```JavaScript
authenticationContext.submitAuthenticationChallengeAnswer(challengeAnswer);
```
{: codeblock}

```JavaScript
authenticationContext.submitAuthenticationFailure(info);
```
{: codeblock}

Le code suivant montre comment un programme d'écoute d'authentification client peut recueillir des informations d'identification, traiter des problèmes et fournir des réponses d'authentification.

## Exemple d'implémentation du workflow d'un programme d'écoute d'authentification personnalisé
{: #custom-cordova-authlisten-sample}

Cet exemple de programme d'écoute d'authentification est conçu pour fonctionner avec un fournisseur d'identité personnalisé. Vous pouvez télécharger le fournisseur d'identité personnalisé depuis ce [référentiel Github ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}.

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {
		console.log("onAuthenticationChallengeReceived :: ", challenge);

		// In this sample the authentication listener immediatelly returns a hardcoded
		// set of credentials. In a real life scenario this is where developer would
		// show a login screen, collect credentials and invoke
		// authenticationContext.submitAuthenticationChallengeAnswer() API

		var challengeResponse = {
			username: "john.lennon",
			password: "12345"
		}

		authenticationContext.submitAuthenticationChallengeAnswer(challengeResponse);

		// In case there was a failure collecting credentials you need to report
		// it back to the authenticationContext. Otherwise Mobile Client
		// Access client SDK will remain in a waiting-for-credentials state
		// forever

	},

	onAuthenticationSuccess: function(info){
		console.log("onAuthenticationSuccess :: ", info);
	},

	onAuthenticationFailure: function(info){
		console.log("onAuthenticationFailure :: ", info);
	}
}
```
{: codeblock}

## Enregistrement d'un programme d'écoute d'authentification personnalisé dans le WebView Cordova
{: #custom-cordova-authreg}

Après avoir créé un programme d'écoute d'authentification personnalisé, vous devez l'enregistrer auprès de `BMSClient` avant de commencer à l'utiliser. Ajoutez le code suivant à votre application.  Ce code doit être appelé avant l'envoi de demandes à vos ressources protégées.

```Java
BMSClient.registerAuthenticationListener(<realmName>, customAuthenticationListener);
```
{: codeblock}
 Utilisez le nom de domaine, `realmName`, que vous avez spécifié dans le tableau de bord {{site.data.keyword.amashort}}.

## Définissez le Gestionnaire d'autorisations dans le code natif

Le Gestionnaire d'autorisations {{site.data.keyword.amashort}} doit être enregistré dans votre code de plateforme natif.

**Android** (ajouter à `onCreate` dans l'activité principale)

```
String tenantId = "<tenantId>";
MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
```
{: codeblock}

**iOS Objective-C** (ajouter à `AppDelegate.m`)

Enregistrez votre Gestionnaire d'autorisations selon votre version de Xcode.

```
#import "<your_module_name>-Swift.h"

- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

{  

    //[CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];
 }
```
{: codeblock}

Remarque : Pour utiliser le fichier d'en-tête Swift correct, remplacez `your_module_name` par le nom de module de votre projet (par
exemple, si votre module se nomme `Cordova`, remplacez-le par `#import "Cordova-Swift.h"`). Pour trouver le nom du module, allez à **Build Settings > Packagin` > Product Module Name**.

**Remarque :** remplacez votre `tenantId` par votre identifiant de locataire situé sur le bouton **Mobile Options** du tableau de bord du service de {{site.data.keyword.amashort}}.


## Activez le partage de chaîne de certificats pour iOS

Activez `Keychain Sharing` en allant à l'onglet `Capabilities` et basculez `Keychain Sharing` sur `On` dans votre projet Xcode.


## Test de l'authentification
{: #custom-cordova-test}
Une fois que le SDK client est initialisé et qu'un programme `AuthenticationListener` est enregistré, vous pouvez commencer à envoyer des demandes à votre application de back end mobile.

### Avant de commencer
{: #custom-cordova-testing-before}
Vous devez disposer d'une application créée avec un conteneur boilerplate {{site.data.keyword.mobilefirstbp}} et d'une ressource protégée par {{site.data.keyword.amashort}} sur le noeud final `/protected`.


1. Envoyez une demande à un noeud final protégé de votre application de back end mobile dans votre navigateur en ouvrant `{applicationRoute}/protected`, par exemple : `http://my-mobile-backend.mybluemix.net/protected`.
 Le noeud final `/protected` d'une application de back end mobile qui a été créée avec le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} est protégé par {{site.data.keyword.amashort}}. Ce noeud final n'est accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}. En conséquence, un message `Unauthorized` s'affiche dans le navigateur.

1. A l'aide de votre application Cordova, envoyez une demande au même noeud final. Ajoutez le code ci-dessous après avoir initialisé `BMSClient` et enregistré votre programme d'écoute d'authentification.

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new BMSRequest("<your-application-route>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}

	Remplacez `<your-application-route>` par votre URL d'application back end (voir [Avant de commencer](#before-you-begin)).

1. 	Lorsque votre demande aboutit, la sortie suivante figure dans la console `LogCat` ou Xcode :

	![image](images/android-custom-login-success.png)

	![image](images/ios-custom-login-success.png)
