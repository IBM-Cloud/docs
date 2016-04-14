---

Copyright : 2015, 2016

---

# Configuration du SDK client de {{site.data.keyword.amashort}} pour Cordova
{: #custom-cordova}
Configurez votre application Cordova qui utilise l'authentification personnalisée de manière qu'elle utilise le SDK client de {{site.data.keyword.amashort}} et connectez-la à {{site.data.keyword.Bluemix}}.


## Avant de commencer
{: #before-you-begin}
Vous devez disposer d'une ressource protégée par une instance du service {{site.data.keyword.amashort}} qui est configuré pour utiliser un fournisseur d'identité personnalisé.  Votre appli mobile doit aussi être instrumentée à l'aide du SDK client de {{site.data.keyword.amashort}}.  Pour plus d'informations, voir les sujets suivants :
 * [Initiation à {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Configuration du SDK Cordova](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)
 * [Utilisation d'un fournisseur d'identité personnalisé](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Création d'un fournisseur d'identité personnalisé](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configuration de {{site.data.keyword.amashort}} pour l'authentification personnalisée](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)

## Initialisation du logiciel SDK client de {{site.data.keyword.amashort}}
{: #custom-cordova-sdk}
Initialisez le SDK en passant les paramètres suivants : l'identificateur unique global de l'application (applicationGUID) et la route de l'application (applicationRoute).

1. Récupérez les valeurs de ces paramètres pour votre application. Ouvrez votre appli dans le tableau de bord {{site.data.keyword.Bluemix_notm}}. Cliquez sur **Options pour application mobile**. Les
valeurs **Route** (`applicationRoute`) et **Identificateur global unique de l'application**
(`applicationGUID`) sont affichées.
1. Initialisez le logiciel SDK client.

	```JavaScript
	BMSClient.initialize(applicationRoute, applicationGUID);

	```
 Remplacez *applicationRoute* et *applicationGUID* par les valeurs de **Route** et **Identificateur global
unique de l'application** du panneau **Options pour application mobile** de votre application dans le tableau de bord
{{site.data.keyword.Bluemix_notm}}.

## Interface du programme d'écoute d'authentification
{: #custom-cordva-auth}

Le SDK client de {{site.data.keyword.amashort}} fournit une interface du programme d'écoute d'authentification permettant d'implémenter un flux d'authentification personnalisé. Vous devez ajouter les méthodes suivantes, qui sont appelées dans différentes phases du processus d'authentification.

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...},
	onAuthenticationSuccess: function(info){...},
	onAuthenticationFailure: function(info){...}
}
```

Chaque méthode gère une phase du processus d'authentification.

### Méthode onAuthenticationChallengeReceived
{: #onAuthenticationChallengeReceived}
Cette méthode est appelée lorsqu'une demande d'authentification personnalisée reçue provient du service {{site.data.keyword.amashort}}.
```JavaScript
onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...}
```

#### Arguments
{: #onAuthenticationChallengeReceived-args}
* `authenticationContext` : Fourni par le SDK client de {{site.data.keyword.amashort}} pour permettre au développeur de communiquer les réponses aux demandes d'authentification ou les échecs de collecte des données d'identification (par exemple, lorsque l'utilisateur annule la demande d'authentification).
* `challenge` : Objet JSON qui contient une demande d'authentification personnalisée, renvoyée par un fournisseur d'identité personnalisé.

En appelant la méthode `onAuthenticationChallengeReceived`, le SDK client de {{site.data.keyword.amashort}} délègue le contrôle au développeur. {{site.data.keyword.amashort}} attend les données d'identification. Le développeur doit collecter les données d'identification et les fournir au SDK client de {{site.data.keyword.amashort}} par l'une des méthodes de l'interface `authContext`.

```JavaScript
onAuthenticationSuccess: function(info){...}
```

Cette méthode est appelée après une authentification réussie. Les arguments comprennent un objet JSON facultatif contenant des informations détaillées sur le succès de l'authentification.

```JavaScript
onAuthenticationFailure: function(info){...}
```

Cette méthode est appelée après un échec d'authentification. Les arguments comprennent un objet JSON facultatif contenant des informations détaillées sur l'échec de l'authentification.

## authenticationContext
{: #custom-cordova-authcontext}

La valeur de `authenticationContext`` est fournie comme argument de la méthode `onAuthenticationChallengeReceived` d'un programme d'écoute d'authentification. Le développeur doit collecter les données d'identification et utiliser les méthodes `AuthenticationContext`` pour renvoyer des données d'identification au SDK client de {{site.data.keyword.amashort}} ou pour signaler un incident. Utilisez l'une des méthodes suivantes :

```JavaScript
authenticationContext.submitAuthenticationChallengeAnswer(challengeAnswer);

authenticationContext.submitAuthenticationFailure(info);
```

## Exemple d'implémentation d'un programme d'écoute d'authentification personnalisé
{: #custom-cordova-authlisten-sample}

Cet exemple de programme d'écoute d'authentification est conçu pour fonctionner avec un fournisseur d'identité personnalisé. Vous pouvez télécharger le fournisseur d'identité depuis le [référentiel Github](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample).

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {
		console.log("onAuthenticationChallengeReceived :: ", challenge);

		// Dans cet exemple, le programme d'écoute d'authentification renvoie immédiatement
		// un jeu de données d'identification codé en dur. Dans un scénario réel, c'est ici que le développeur
		// afficherait un écran de connexion, collecterait les données d'identification et appellerait
		// l'API authenticationContext.submitAuthenticationChallengeAnswer()

		var challengeResponse = {
			username: "john.lennon",
			password: "12345"
		}

		authenticationContext.submitAuthenticationChallengeAnswer(challengeResponse);

		// En cas d'échec de la collecte des données d'identification, vous devez le signaler au
		// authenticationContext. Sinon le SDK client d'accès de client mobile
		// demeure indéfiniment à l'état d'attente de données
		// d'identification

	},

	onAuthenticationSuccess: function(info){
		console.log("onAuthenticationSuccess :: ", info);
	},

	onAuthenticationFailure: function(info){
		console.log("onAuthenticationFailure :: ", info);
	}
}
```

## Enregistrement d'un programme d'écoute d'authentification personnalisé
{: #custom-cordova-authreg}

Après avoir créé un programme d'écoute d'authentification personnalisé, enregistrez-le auprès de `BMSClient` avant de commencer à l'utiliser. Ajoutez le code suivant à votre application.  Ce code doit être appelé avant l'envoi de demandes à vos ressources protégées.

```Java
BMSClient.registerAuthenticationListener(realmName, customAuthenticationListener);
```
 Utilisez le nom de domaine que vous avez défini dans le tableau de bord {{site.data.keyword.amashort}}.


## Test de l'authentification
{: #custom-cordova-test}
Lorsque le SDK client est initialisé et qu'un programme d'écoute d'authentification est enregistré, vous pouvez commencer à envoyer des demandes à votre système de back end mobile.

### Avant de commencer
{: #custom-cordova-testing-before}
Vous devez disposer d'une application créée avec un conteneur boilerplate {{site.data.keyword.mobilefirstbp}} et d'une ressource protégée par {{site.data.keyword.amashort}} sur le noeud final `/protected`.


1. Envoyez une demande à un noeud final protégé de votre système de back end mobile dans votre navigateur en ouvrant
`{applicationRoute}/protected`, par exemple : `http://my-mobile-backend.mybluemix.net/protected`.
 Le noeud final `/protected` d'un système de back end mobile qui a été créé avec le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} est protégé par {{site.data.keyword.amashort}}. Ce noeud final n'est accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}. En conséquence, un message `Unauthorized` s'affiche dans le navigateur.

1. A l'aide de votre application Cordova, envoyez une demande au même noeud final. Ajoutez le code ci-dessous après avoir initialisé `BMSClient` et enregistré votre programme d'écoute d'authentification.

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new MFPRequest("/protected", MFPRequest.GET);
	request.send(success, failure);
	```

1. 	Lorsque votre demande aboutit, la sortie suivante figure dans la console LogCat ou Xcode :

	![image](images/android-custom-login-success.png)

	![image](images/ios-custom-login-success.png)
