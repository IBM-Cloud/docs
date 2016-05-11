---

Copyright : 2015, 2016
  
---

# Communications de système de back end à système de back end
{: #backend-comm}

Dans certains scénarios avancés, vous pouvez être amené à envoyer des demandes à partir d'une application de back end qui s'exécute sur {{site.data.keyword.Bluemix}} à un autre système de back end qui est protégé par le service {{site.data.keyword.amashort}}, par exemple le service {{site.data.keyword.cloudant}}). Dans ce cas, vous devez ajouter un jeton OAuth à la demande.

Utilisez le module nmpjs `bms-mca-oauth-sdk` pour obtenir et injecter des jetons OAuth dans les demandes.

## Installation du module bms-mca-oauth-sdk
{: #sdk}

Sur une ligne de commande, ouvrez le répertoire de l'application Node.js et lancez la commande suivante :

```Bash
npm install -save bms-mca-oauth-sdk
```

## Utilisation du module bms-mca-oauth-sdk
{: #using-sdk}

Le code suivant illustre l'utilisation du module `bms-mca-oauth-sdk`.


``` JavaScript
var oauthSDK = require('bms-mca-oauth-sdk');

var options = {

	// You can cache tokens to avoid extra roundtrips on every request
	// This property defines the number of tokens to be cached

	cacheSize: 100,

	// All of the below properties are retrieved automatically when your Node.js
	// runs on {{site.data.keyword.Bluemix_notm}} and bound to an instance of {{site.data.keyword.amashort}} Service.
	// Alternatively you can get these properties values by clicking Show Credentials
	// on the {{site.data.keyword.amashort}} Service tile in your {{site.data.keyword.Bluemix_notm}} application dashboard

	appId: "appId",				// Bleumix applicationGUID, a.k.a tenantId
	clientId: "clientId",			
	secret: "secret",
	serverUrl: "serverUrl"
};

oauthSDK.getAuthorizationHeader(options).then(function(authHeader){

	// Dans la demande que vous désirez envoyer à la ressource protégée,
	// ajoutez la valeur authHeader.

	request.headers.Authorization = authHeader;

	// Envoi de la demande

});

```
