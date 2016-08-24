---

copyright:
  years: 2015, 2016
  
---

# Configuration des communications de système back end à système back end
{: #backend-comm}

*Dernière mise à jour : 16 juin 2016*
{: .last-updated}

Dans certains scénarios, vous pouvez être amené à envoyer des demandes à partir d'une application de back end qui s'exécute sur {{site.data.keyword.Bluemix}} à un autre système de back end qui est protégé par le service {{site.data.keyword.amashort}} (le service {{site.data.keyword.cloudant}}, par exemple). Dans ce cas, vous devez ajouter un jeton OAuth à la demande.

Utilisez le module `bms-mca-oauth-sdk npmjs` pour obtenir et injecter des jetons OAuth dans les demandes.

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

	// Toutes les propriétés ci-dessous sont extraites automatiquement lorsque votre Node.js
	// s'exécute sur {{site.data.keyword.Bluemix_notm}} et est lié à une instance du service {{site.data.keyword.amashort}}.
	// Vous pouvez également obtenir ces valeurs de propriétés en cliquant sur Afficher les données d'identification
	// sur la vignette du service {{site.data.keyword.amashort}} dans le tableau de bord de votre application {{site.data.keyword.Bluemix_notm}}

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
