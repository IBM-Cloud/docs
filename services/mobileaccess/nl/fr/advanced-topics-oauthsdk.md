---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-08"

---

{:codeblock:.codeblock}

# Communication entre applications de back end et services
{: #backend-comm}

Dans certains scénarios, vous pouvez être amené à envoyer des demandes à partir d'une application de back end qui s'exécute sur {{site.data.keyword.Bluemix}} à un autre système de back end qui est protégé par le service {{site.data.keyword.amafull}} (le service {{site.data.keyword.cloudant}}, par exemple). Dans ce cas, vous devez ajouter un jeton OAuth à la demande.

Utilisez le module `bms-mca-oauth-sdk npmjs` pour obtenir et injecter des jetons OAuth dans les demandes.

## Installation du module bms-mca-oauth-sdk
{: #sdk}

Sur une ligne de commande, ouvrez le répertoire de l'application Node.js et lancez la commande suivante :

```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## Utilisation du module bms-mca-oauth-sdk
{: #using-sdk}

Le code suivant illustre l'utilisation du module `bms-mca-oauth-sdk`.


``` JavaScript
var oauthSDK = require('bms-mca-oauth-sdk');

var options = {

	// You can cache tokens to avoid extra roundtrips on every request
	// This property defines the number of tokens to be cached

	cacheSize: 100,

	// The following properties are retrieved automatically when your Node.js
	// runs on {{site.data.keyword.Bluemix_notm}} and bound to an instance of {{site.data.keyword.amashort}} Service.
	// Alternatively, you can get these property values by clicking Show Credentials
	// on the {{site.data.keyword.amashort}} Service tile in your {{site.data.keyword.Bluemix_notm}} application dashboard

	appId: "tenantID",				// a.k.a. Bluemix applicationGUID
	clientId: "clientId",			
	secret: "secret",
	serverUrl: "serverUrl"
};

oauthSDK.getAuthorizationHeader(options).then(function(authHeader){

	// In the request that you want to send to the protected resource, 
	// add the authHeader value.

	request.headers.Authorization = authHeader;

	// Send request

});

```
{: codeblock}
