---

Copyright : 2015, 2016

---

# Création d'un fournisseur d'identité personnalisé
{: #custom-create}
Pour créer un fournisseur d'identité personnalisé, développez une application Web qui expose une API RESTful :

```
POST <base_url>/apps/<tenant_id>/<realm_name>/<request_type>
```

* `base_url`: URL de base de l'application de fournisseur d'identité personnalisé. L'URL de base est l'adresse URL à enregistrer
dans le tableau de bord {{site.data.keyword.amashort}}.
* `tenant_id` : Identificateur unique du titulaire. Lorsque {{site.data.keyword.amashort}} appelle cette API, il fournit toujours
l'identificateur global unique de l'application {{site.data.keyword.Bluemix}} (`applicationGUID`).
* `realm_name` : Nom de domaine personnalisé défini dans le tableau de bord {{site.data.keyword.amashort}}.
* `request_type` : Un type parmi :
	* `startAuthorization` : Première étape du processus d'authentification. Le fournisseur d'identité personnalisé doit répondre par le statut "challenge", "success" ou "failure".
	* `handleChallengeAnswer` : Gère la réponse à une demande d'authentification d'un client mobile.

## API `startAuthorization`
{: #custom-startauthorization}

`POST <base_url>/apps/<tenant_id>/<realm_name>/startAuthorization`

L'API `startAuthorization` est la première étape du processus d'authentification. Un fournisseur d'identité personnalisé doit répondre par le statut "challenge", "success" ou "failure".

Pour garantir la souplesse maximale du processus d'authentification, un fournisseur d'identité personnalisé a accès à tous les en-têtes HTTP qui sont envoyés par un client mobile dans le corps de la demande. Les en-têtes sont au format suivant :

```JavaScript
{
    "headers" : {
    	"header1": "value1",  
    	"header2" : "value2"
    }
}
```

Le fournisseur d'identité personnalisé peut répondre par une demande d'authentification, ou
par un succès ou un échec immédiat. Le statut de la réponse HTTP doit être `HTTP 200`, et son JSON doit contenir les propriétés suivantes :

* `status` : Statut de la demande : `success`(succès), `challenge` (demande) ou `failure` (échec).
* `stateId` (facultatif) : Identificateur de type chaîne généré de façon aléatoire pour identifier la session auprès du client mobile. Cet attribut peut être omis si le fournisseur d'identité personnalisé ne stocke pas les états.
* `challenge` : Objet JSON qui représente une demande d'authentification à renvoyer au client mobile. Cet attribut n'est envoyé au client que si le statut est défini sur `challenge`.
* `userIdentity` : Objet JSON qui représente l'identité d'un utilisateur.  L'identité de l'utilisateur est constitué de propriétés telles que `userName` (nom d'utilisateur) et `displayName` (nom affiché), et d'attributs.  Pour plus d'informations, voir [Objet identité de l'utilisateur](#custom-user-identity). Cette propriété n'est envoyée au client mobile que si le statut est défini sur `success`.

Exemple :

```
{
	"status":"challenge",
	"stateId":"some-random-guid"
	"challenge":{
		message:"Enter username and password",
		attemptsLeft: 3
	}
}
```

## API `handleChallengeAnswer`
{: #custom-handleChallengeAnswer}

`POST <base_url>/apps/<tenant_id>/<realm_name>/handleChallengeAnswer`

L'API `handleChallengeAnswer` gère la réponse à une demande d'authentification d'un client mobile. Comme l'API `startAuthorization`, l'API `handleChallengeAnswer` répond par le statut `challenge` (demande), `success` (succès) ou `failure` (échec).

Comme pour la demande `startAuthorization`, le fournisseur d'identité personnalisé a accès à tous les en-têtes HTTP qui sont envoyés par un client mobile dans le corps de la demande. Outre les en-têtes de la demande du client mobile, le corps de la demande `handleChallengeAnswer` comprend également les propriétés `stateId` et `challengeAnswer`.

### Exemple de corps d'une demande `handleChallengeAnswer`
{: #custom-handleChallengeAnswer-example}

```JavaScript
{
    "headers" : {
    	"header1": "value1",  
    	"header2" : "value2"
	},
    "stateId" : "123123123",
    "challengeAnswer" : {
    	"pinCode":12345
 	}
}
```

La réponse d'une API `handleChallengeAnswer` doit avoir la même structure que celle de l'API `startAuthorization`.

## Objet identité de l'utilisateur
{: #custom-user-identity}

La réponse à une demande d'authentification qui a abouti doit inclure un objet identité de l'utilisateur, avec les attributs suivants :
* `userName` : Nom unique de l'utilisateur.
* `displayName` : Nom affiché de l'utilisateur.
* `attributes` (facultatif) objet JSON contenant des attributs utilisateur personnalisés.

### Exemple d'objet identité de l'utilisateur
{: #custom-user-identity-example}
```JavaScript
{
    "userName" : "janesmith",
    "displayName" : "Jane Smith",
    "attributes" : {
        "Language" : "French",
        "Country" : "Canada"
    }
}
```

L'objet identité de l'utilisateur est utilisé par le service {{site.data.keyword.amashort}} pour générer un jeton d'ID qui est envoyé au client mobile dans l'en-tête d'autorisation. Une fois l'authentification réussie, le client mobile dispose d'un accès complet à l'objet identité de l'utilisateur.

## Remarques sur la sécurité
{: #custom-security}

Chaque demande du service {{site.data.keyword.amashort}} à un fournisseur d'identité personnalisé contient un en-tête d'autorisation lui permettant de vérifier que la demande provient d'une source autorisée. Même si cette opération n'est pas obligatoire, il est recommandé de valider l'en-tête d'autorisation en instrumentant le fournisseur d'identité personnalisé avec un SDK serveur de {{site.data.keyword.amashort}}. Pour
utiliser ce SDK, votre fournisseur d'identité personnalisé doit être implémenté avec Node.js ou Liberty
for Java&trade;&trade; et s'exécuter sur {{site.data.keyword.Bluemix_notm}}.

L'en-tête d'autorisation contient des informations sur le client mobile et l'appli mobile qui a déclenché le processus d'authentification. Vous pouvez utiliser le contexte de sécurité pour récupérer ces données. Pour plus d'informations, voir [Protection des ressources](protecting-resources.html).

## Exemple d'implémentation d'un fournisseur d'identité personnalisé
{: #custom-sample}
Vous pouvez utiliser comme référence l'un des exemples d'implémentation Node.js suivants de fournisseur d'identité personnalisé lorsque vous
développez votre
fournisseur d'identité personnalisé. Téléchargez le code d'application complet depuis les référentiels GitHub.

* [Exemple simple](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
* [Exemple avancé](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

<!---
 ### JSON structure (simple sample)
{: #custom-sample-json}
This implementation assumes that the supplied authentication challenge answer is a JSON object with the following structure:

```
{
 	username: "my.username",
 	password: "my.password"
 }
 ```

### Custom identity provider sample code (simple sample)
{: #custom-sample-code}
```JavaScript
var express = require('express');
var cfenv = require('cfenv');
var log4js = require('log4js');
var jsonParser = require('body-parser').json();

// Using hardcoded user repository
var userRepository = {
	"john.lennon":      { password: "12345", displayName:"John Lennon", dob:"October 9, 1940"},
	"paul.mccartney":   { password: "67890", displayName:"Paul McCartney", dob:"June 18, 1942"},
	"ringo.starr":      { password: "abcde", displayName:"Ringo Starr", dob: "July 7, 1940"},
	"george.harrison":  { password: "fghij", displayName: "George Harrison", dob:"Feburary 25, 1943"}
}

var app = express();
var logger = log4js.getLogger("CustomIdentityProviderApp");
logger.info("Starting up");

app.post('/apps/:tenantId/:realmName/startAuthorization', jsonParser, function(req, res){
	var tenantId = req.params.tenantId;
	var realmName = req.params.realmName;
	var headers = req.body.headers;

	logger.debug("startAuthorization", tenantId, realmName, headers);

	var responseJson = {
		status: "challenge",
		challenge: {
			text: "Enter username and password"
		}
	};

	res.status(200).json(responseJson);
});

app.post('/apps/:tenantId/:realmName/handleChallengeAnswer', jsonParser, function(req, res){
	var tenantId = req.params.tenantId;
	var realmName = req.params.realmName;
	var challengeAnswer = req.body.challengeAnswer;


	logger.debug("handleChallengeAnswer", tenantId, realmName, challengeAnswer);

	var username = req.body.challengeAnswer["username"];
	var password = req.body.challengeAnswer["password"];

	var userObject = userRepository[username];

	var responseJson = { status: "failure" };

	if (userObject && userObject.password == password ){
		logger.debug("Login success for userId ::", username);
		responseJson.status = "success";
		responseJson.userIdentity = {
			userName: username,
			displayName: userObject.displayName,
			attributes: {
				dob: userObject.dob
			}
		}
	} else {
		logger.debug("Login failure for userId ::", username);
	}

	res.status(200).json(responseJson);
});

app.use(function(req, res, next){
	res.status(404).send("This is not the URL you're looking for");
});

var server = app.listen(cfenv.getAppEnv().port, function () {
	var host = server.address().address;
	var port = server.address().port;
	logger.info('Server listening at %s:%s', host, port);
});
```
--->

## Etapes suivantes
{: #next-steps}
* [Configuration de {{site.data.keyword.amashort}} pour l'authentification personnalisée](custom-auth-config-mca.html)
* [Configuration de l'authentification personnalisée pour Android](custom-auth-android.html)
* [Configuration de l'authentification personnalisée pour iOS](custom-auth-ios.html)
* [Configuration de l'authentification personnalisée pour Cordova](custom-auth-cordova.html)
