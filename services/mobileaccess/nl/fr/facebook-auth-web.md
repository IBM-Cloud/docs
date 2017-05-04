---

copyright:
  year: 2016, 2017
lastupdated: "2017-04-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

**Important : Le service {{site.data.keyword.amafull}} est remplacé par le service {{site.data.keyword.appid_full}}.**

# Activation de l'authentification Facebook pour les applications Web
{: #facebook-auth-web}

Utilisez Facebook pour authentifier les utilisateurs sur votre application Web {{site.data.keyword.amafull}}. Ajoutez une fonctionnalité de sécurité {{site.data.keyword.amashort}}.

## Avant de commencer
{: #facebook-auth-android-before}
Vous devez disposer des éléments suivants :

* Une appli Web.
* Un service {{site.data.keyword.amashort}}. Pour plus d'informations, voir [Initiation](index.html).
* L'URI de redirection finale (au terme du processus d'autorisation).


## Configuration d'une application sur le site Facebook for Developers
{: #facebook-auth-config}

Pour utiliser Facebook comme fournisseur d'identité dans votre site Web, vous devez ajouter et configurer la plateforme de site Web sur votre application 
Facebook.

1. Connectez-vous à votre compte sur le site [Facebook for Developers](https://developers.facebook.com).
	Pour plus d'informations sur la création d'une nouvelle appli, voir [Création d'une application sur le site Web Facebook for Developers](facebook-auth-overview.html#facebook-appID).
1. Notez les valeurs des zones **ID application** et **Valeur confidentielle de l'application**. Vous en aurez besoin pour configurer votre projet Web
pour l'authentification Facebook dans le tableau de bord de Mobile Client Access.
1. Dans **Products List**, sélectionnez **Facebook Login**.
4. Ajoutez la plateforme **Web**, si elle n'existe pas.
6. Entrez l'URI de noeud final de rappel du serveur d'autorisation dans la zone **URI de redirection OAuth
valides**. Vous pouvez ajouter cette valeur après avoir configuré votre service {{site.data.keyword.amashort}} dans les étapes suivantes.
7. Enregistrez les changements.


## Configuration de {{site.data.keyword.amashort}} pour l'authentification Facebook
{: #facebook-auth-config-ama}

Une fois que vous disposez de votre ID d'application et de la valeur confidentielle Facebook et que votre application Facebook for Developers a été configurée pour servir les clients Web, vous pouvez activer l'authentification Facebook dans le tableau de bord {{site.data.keyword.amashort}}.

1. Ouvrez le tableau de bord de service {{site.data.keyword.amashort}}.
1. Dans l'onglet **Gérer**, activez **Autorisation**.
1. Développez la section **Facebook**.
1. Sélectionnez **Ajouter Facebook à une application Web**.
5. Notez la valeur de la zone de texte **URI de redirection Mobile Client Access pour Facebook for Developers**. Vous devez ajouter cette valeur à la zone relative aux **URI de redirection OAuth valides** dans la **connexion Facebook** du portail des développeurs Facebook.
6. Entrez l'**ID application** et la **Valeur confidentielle de l'application** obtenus sur le site Web Facebook for Developers.
7. Entrez l'URI de redirection dans **URI de redirection de votre application Web**. Cette valeur est celle de l'URI de redirection à laquelle accéder
à l'aboutissement du processus d'autorisation et est déterminée par le développeur.
8. Cliquez sur **Sauvegarder**.


## Implémentation du flux d'autorisation {{site.data.keyword.amashort}} en utilisant Facebook comme fournisseur d'identité
{: #facebook-auth-flow}

La variable d'environnement `VCAP_SERVICES` est créée automatiquement pour chaque instance de service {{site.data.keyword.amashort}}
et contient les propriétés requises pour le processus d'autorisation. Elle se compose d'un objet JSON et vous pouvez la visualiser dans l'onglet **Données d'identification pour le service** du tableau de bord de service de {{site.data.keyword.amashort}}.

Pour démarrer le processus d'autorisation :

1. Extrayez le noeud final d'autorisation (`authorizationEndpoint`) et l'ID client
(`clientId`) depuis les données d'identification du service stockées dans la variable
d'environnement `VCAP_SERVICES`.

	`var cfEnv = require("cfenv");`

	**Remarque :** si vous avez ajouté le service {{site.data.keyword.amashort}} dans votre application avant l'ajout de la prise en charge Web, il se peut que vous n'ayez pas de noeud final de jeton dans les **Données d'identification pour le service**. A la place, utilisez les URL suivantes, selon votre région {{site.data.keyword.Bluemix_notm}} :

	Sud des Etats-Unis :

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization`

	Londres :

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization`

	Sydney :

	`  https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization 
  `

2. Construisez l'URI du serveur d'autorisation en utilisant `response_type("code")`, `client_id` et
`redirect_uri` en tant que paramètres de requête.

3. Redirigez l'utilisateur depuis votre application Web vers l'URI généré.

	L'exemple suivant extrait les paramètres depuis la variable `VCAP_SERVICES`, construit l'URL et envoie la demande de redirection.

	```Java
  var cfEnv = require("cfenv");

	app.get("/protected", checkAuthentication, function(req, res, next){  
		res.send("Bonjour, ceci est un noeud final protégé");
  }
	);

	function checkAuthentication(req, res, next){
		// Check if user is authenticated

		if (req.session.userIdentity){   
			next()
     } else {   
			// If not - redirect to authorization server   
			var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;   
			var authorizationEndpoint = mcaCredentials.authorizationEndpoint;   
			var clientId = mcaCredentials.clientId;   
			var redirectUri = "http://some-server/oauth/callback"; 
			// Your Web application redirect URI   

			var redirectUrl = authorizationEndpoint + "?response_type=code";
        redirectUrl += "&client_id=" + clientId;
        redirectUrl += "&redirect_uri=" + redirectUri;   

			res.redirect(redirectUrl);

      }
	}
	```
	{: codeblock}

	Le paramètre `redirect_uri` est l'URI de redirection après l'aboutissement ou l'échec de l'authentification avec
Facebook.   

	Après redirection au noeud final d'autorisation, l'utilisateur reçoit un formulaire de connexion par
Facebook. Une fois que Facebook confirme l'identité de l'utilisateur, le service {{site.data.keyword.amashort}} appelle l'URI de redirection de votre
application Web en soumettant le code d'accord en tant que paramètre de requête.  


## Obtention des jetons
{: #facebook-auth-tokens}

L'étape suivante consiste à obtenir le jeton d'accès et le jeton d'identité à l'aide du code d'accord reçu auparavant :

1.  Extrayez le jeton `tokenEndpoint`, `clientId` et `secret` depuis les données d'identification du
service stockées dans la variable d'environnement `VCAP_SERVICES`.

	**Remarque :** si vous avez utilisé {{site.data.keyword.amashort}} avant l'ajout de la prise en charge Web, il se peut que vous n'ayez pas de noeud final de jeton dans les données d'identification pour le service. A la place, utilisez les URL suivantes, selon votre région Bluemix :

	Sud des Etats-Unis :

	`     https://mobileclientaccess.ng.bluemix.net/oauth/v2/token   
 `

	Londres :

	`     https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token
 `

	Sydney :

	`     https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token 
 `

2. Envoyez une demande POST à l'URI du serveur de jeton avec le type d'autorisation ("authorization_code"), l'élément `clientId` et votre URI de redirection comme paramètres de masque. Envoyez les éléments `clientId` et
`secret` sous forme de données d'authentification HTTP de base.

	Le code suivant extrait les valeurs requises et les envoie avec une demande POST.

	```Java
  var cfEnv = require("cfenv");
  var base64url = require("base64url ");
  var request = require('request');

	app.get("/oauth/callback", function(req, res, next){
		var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;
    var tokenEndpoint = mcaCredentials.tokenEndpoint;
    var formData = {
			grant_type: "authorization_code", 
			client_id: mcaCredentials.clientId, 
			redirect_uri: "http://some-server/oauth/callback",
			// Your web application redirect uri 
			code: req.query.code 
		} 

		request.post( {
			url: tokenEndpoint,
    formData: formData
    }, function (err, response, body){
			var parsedBody = JSON.parse(body); 			req.session.accessToken =
parsedBody.access_token; 			req.session.idToken = parsedBody.id_token; 			var idTokenComponents = parsedBody.id_token.split("."); // [header, payload, signature] 
			var decodedIdentity= base64url.decode(idTokenComponents[1]);
			req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"]; 
			res.redirect("/"); 
		}
		).auth(mcaCredentials.clientId, mcaCredentials.secret);
   }
	);
	```
	{: codeblock}

	Notez que le paramètre `redirect_uri` doit correspondre au paramètre `redirect_uri` utilisé dans la demande d'autorisation
précédente. La valeur du paramètre `code` doit être le code d'accord dans la réponse de la demande d'autorisation. Le code d'accord est valide pendant 10 minutes, après quoi un nouveau code doit être obtenu.

	Le corps de la réponse contiendra le code d'accès et l'ID du jeton au format JWT (voir le [site Web JWT ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://jwt.io/){: new_window}.

	Une fois que vous avez obtenu l'accès et reçu les jetons d'identité, vous pouvez marquer la session Web comme authentifiée et, si vous le désirez,
rendre
persistants ces jetons.  

##Utilisation du jeton d'accès et du jeton d'identité obtenus
{: #facebook-auth-using-token}

Le jeton d'identité contient des informations sur l'identité de l'utilisateur. Dans le cas d'une authentification Facebook, le jeton contiendra toutes les informations que
l'utilisateur a accepté de partager, comme son nom complet, son groupe d'âge, l'URL de sa photo de profil, etc.  

Le jeton d'accès active les communications avec les ressources protégées par les filtres d'autorisation de
{{site.data.keyword.amashort}}. Voir [Protection des ressources](protecting-resources.html).

Pour soumettre des demandes à des ressources protégées, ajoutez aux demandes un en-tête Authorization doté de la structure suivante :

`Authorization=Bearer <jeton_accès> <jeton_ID>`

#### Conseils
{: #tips}

* Vous devez séparer les éléments `accessToken` et `idToken` par un espace.

* Le paramètre `jeton_accès` est facultatif. Si vous l'omettez, il est possible d'accéder à la ressource protégée, mais sans recevoir
d'informations sur l'utilisateur autorisé.
