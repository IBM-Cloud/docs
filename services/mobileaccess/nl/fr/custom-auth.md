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

# Authentification d'utilisateurs à l'aide d'un fournisseur d'identité personnalisé
{: #custom-id}


Vous pouvez créer un fournisseur d'identité personnalisé qui utilise le service {{site.data.keyword.amafull}} et implémente votre propre logique pour la collecte et la validation des données d'identification. Un fournisseur d'identité est une application Web qui expose une interface RESTful. Vous
pouvez héberger le fournisseur d'identité personnalisé sur site ou dans {{site.data.keyword.Bluemix}}. La seule exigence est qu'il soit
accessible depuis l'Internet public afin de pouvoir communiquer avec le service {{site.data.keyword.amashort}}.

## Flux de demande d'identité personnalisée {{site.data.keyword.amashort}}
{: #custom-id-ovr}


### Flux de demande client {{site.data.keyword.amashort}}
 Le diagramme suivant illustre comment {{site.data.keyword.amashort}} intègre un fournisseur d'identité personnalisé.

![Diagramme de flux de demande](images/mca-sequence-custom.jpg)

* Utilisez le SDK {{site.data.keyword.amashort}} pour envoyer une demande à vos ressources de back end qui sont protégées par le SDK serveur de {{site.data.keyword.amashort}}.
* Le SDK serveur de {{site.data.keyword.amashort}} détecte une demande non autorisée et renvoie une demande d'autorisation HTTP 401 et la portée de l'autorisation.
* Le SDK client de {{site.data.keyword.amashort}} détecte automatiquement l'erreur HTTP 401 et lance le processus d'authentification.
* Le SDK client {{site.data.keyword.amashort}} contacte le service {{site.data.keyword.amashort}} et réclame un en-tête d'autorisation.
* Le service {{site.data.keyword.amashort}} communique avec le fournisseur d'identité personnalisé afin de démarrer le processus d'authentification.
* Le fournisseur d'identité renvoie une demande d'authentification au service {{site.data.keyword.amashort}}.
* Le service {{site.data.keyword.amashort}} renvoie la demande d'authentification au SDK client de {{site.data.keyword.amashort}}.
* Le SDK client de {{site.data.keyword.amashort}} délègue l'authentification à une classe personnalisée que vous avez créée. Vous devez collecter les données d'identification et les fournir au SDK client de {{site.data.keyword.amashort}}.
* Les données d'identification fournies au SDK {{site.data.keyword.amashort}} par le développeur sont envoyées au service {{site.data.keyword.amashort}} en tant que réponse à la demande d'authentification.
* Le service {{site.data.keyword.amashort}} valide la réponse à la demande d'authentification auprès du fournisseur d'identité.
* Si la validation aboutit, le service {{site.data.keyword.amashort}} génère un en-tête d'autorisation et le renvoie au SDK client de {{site.data.keyword.amashort}}. L'en-tête d'autorisation contient deux jetons : un jeton qui contient des informations sur les droits d'accès, et un autre jeton qui contient des informations sur l'utilisateur, l'appareil et l'application actuels.
* A partir de ce moment, toutes les demandes faites avec le SDK client de {{site.data.keyword.amashort}} contiennent un nouvel en-tête d'autorisation.
* Le SDK client de {{site.data.keyword.amashort}} renvoie automatiquement la demande d'origine qui avait déclenché le flux d'autorisation.
* Le SDK serveur de {{site.data.keyword.amashort}} extrait l'en-tête d'autorisation de la demande, la valide auprès du service {{site.data.keyword.amashort}}, et donne l'accès à la ressource de back end.

### Flux de demande d'une application Web {{site.data.keyword.amashort}}
{: #mca-custom-web-sequence}

Le flux de demande d'une application Web {{site.data.keyword.amashort}} est similaire à celui d'un client d'une application mobile. Toutefois,
{{site.data.keyword.amashort}} protège l'application et non pas une ressource de back end {{site.data.keyword.Bluemix_notm}}.

  * La requête initiale est envoyée par l'application Web (depuis un formulaire de connexion, par exemple).
  * La redirection finale vise la zone protégée de l'application Web elle-même et non pas une ressource de back end protégée.

## Présentation des fournisseurs d'identité personnalisés
{: #custom-id-about}

Avec un fournisseur d'identité personnalisé, vous pouvez créer des demandes d'authentification personnalisées destinées au client. Il permet de personnaliser l'ensemble du flux d'authentification.

Quand vous créez un fournisseur d'identité personnalisé, vous pouvez :

1. Personnaliser une demande d'authentification à envoyer par le service {{site.data.keyword.amashort}} à l'application
mobile ou au client Web. Une demande d'authentification est un objet JSON qui contient des données personnalisées. Le client peut les utiliser pour
personnaliser les flux d'authentification.

  Exemple de demande d'authentification personnalisée :

	```JavaScript
	{
		status: "challenge",
		challenge: {
			message:"Enter username and password",
			retriesLeft: 2,
			minUsernameLenth: 8
		}
	}
	```
	{: codeblock}

1. Implémentez éventuellement des flux de collecte de données d'identification personnalisés sur le client, notamment l'authentification
multiétape et multiforme. De la même manière que pour la demande d'authentification personnalisée, vous devez créer la structure de la réponse personnalisée.

  Exemple de réponse personnalisée à une demande d'authentification envoyée par le client :

	```JavaScript
	{
		username:"bob.smith",
		password:"abcd1234",
		pincode:"1234"
	}
	```
	{: codeblock}

1. Implémenter la logique personnalisée de la validation fournie par la réponse à la demande d'authentification.

1. Définir un objet identité de l'utilisateur personnalisé contenant les propriétés personnalisées requises. Ci-après figure un exemple d'objet d'identité
utilisateur personnalisé obtenu par le client après aboutissement de l'authentification :

	```JavaScript
	{
		username:"bob.smith",
		displayName:"Bob Smith",
		attributes:{
			age: 30,
			accountNumber: 12345,
			lastLogin: "Sept 1st, 2015"
		}
	}
	```
	{: codeblock}

### Exemple d'implémentation d'un fournisseur d'identité personnalisé
{: #custom-sample}

Vous pouvez utiliser comme référence l'un des exemples d'implémentation Node.js suivants de fournisseur d'identité personnalisé lorsque vous développez votre
fournisseur d'identité personnalisé. Téléchargez le code d'application complet depuis les référentiels
GitHub.

 * [Exemple simple ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
 * [Exemple avancé ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## Communications standard entre le serveur {{site.data.keyword.amashort}} et un fournisseur d'identité personnalisé
{: #custom-id-comm}

1. Le service {{site.data.keyword.amashort}} envoie une demande `startAuthorization` au fournisseur
d'identité personnalisé.
1. Le fournisseur d'identité personnalisé fournit une demande d'authentification personnalisée à renvoyer au client.
1. Le service {{site.data.keyword.amashort}} envoie au client la demande d'authentification personnalisée reçue du fournisseur d'identité
personnalisé et reçoit une réponse du client.
1. Le service {{site.data.keyword.amashort}} envoie au fournisseur d'identité personnalisé une demande `handleChallengeAnswer` avec la réponse
à la demande d'authentification.
1. Le fournisseur d'identité personnalisé vérifie la réponse à la demande d'authentification et répond favorablement en renvoyant les informations d'identité
de l'utilisateur.
1. Facultativement, le fournisseur d'identité personnalisé fournit d'autres demandes d'authentification après avoir reçu la réponse du client. L'envoi de plusieurs demandes d'authentification permet de mettre en oeuvre un processus d'authentification en plusieurs étapes.

## Avec ou sans état
{: #custom-id-state}

Par défaut, le fournisseur d'identité personnalisé est considéré comme une application sans état. Dans certains cas, il peut être amené à stocker l'état associé au
processus d'authentification. L'authentification en plusieurs étapes constitue un exemple de cas d'utilisation dans lequel le fournisseur d'identité personnalisé
a besoin de stocker le résultat de la première étape d'authentification avant de passer à l'étape suivante. Pour prendre en charge les états, un fournisseur d'identité personnalisé doit générer un ID d'état (stateID) et le fournir au service {{site.data.keyword.amashort}} dans sa réponse. Le service {{site.data.keyword.amashort}}
doit transmettre l'ID d'état dans les demandes qui font partie de la suite du processus d'authentification du client.

## Domaine personnalisé
{: #custom-id-custom}

Un fournisseur d'identité personnalisé prend en charge un domaine d'authentification personnalisé. Pour gérer les demandes d'authentification entrantes, créez
et enregistrez une instance `AuthenticationDelegate` / 	`AuthenticationListener` dans votre application client. Définissez le nom du domaine d'authentification personnalisé lorsque vous configurez un fournisseur d'identité personnalisé dans le tableau de bord {{site.data.keyword.amashort}}. Le
domaine identifie l'instance de service {{site.data.keyword.amashort}} spécifique d'une requête entrante.

## Etapes suivantes
{: #next-steps}

* [Création d'un fournisseur d'identité personnalisé](custom-auth-identity-provider.html)
* [Configuration de {{site.data.keyword.amashort}} pour l'authentification personnalisée](custom-auth-config-mca.html)
* [Configuration de l'authentification personnalisée pour Android](custom-auth-android.html)
* [Configuration de l'authentification personnalisée pour iOS (SDK Swift)](custom-auth-ios-swift-sdk.html)
* [Configuration de l'authentification personnalisée pour Cordova](custom-auth-cordova.html)
