---

copyright:
  year: 2016, 2017
lastupdated: "2017-03-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

Le service {{site.data.keyword.amafull}} est remplacé par le service {{site.data.keyword.appid_full}}.

# Activation de l'authentification Google pour les applications Web
{: #google-auth-web}

Utilisation de Google Sign-In pour authentification d'utilisateurs sur votre application Web. Ajoutez une fonctionnalité de sécurité {{site.data.keyword.amafull}}.


## Avant de commencer
{: #before-you-begin}

Vous devez disposer des éléments suivants :

* Une appli Web.
* Une instance d'une application {{site.data.keyword.Bluemix_notm}} qui est protégée par le service {{site.data.keyword.amashort}}. Pour plus d'informations sur la création d'un système de back end {{site.data.keyword.Bluemix_notm}}, voir [Initiation](index.html).
* L'URI de redirection finale (au terme du processus d'autorisation).


## Configuration d'une application Google pour votre site Web
{: #google-auth-config}

Pour commencer à utiliser Google en tant que fournisseur d'identité, créez un projet dans la [console Google Developer ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.developers.google.com){: new_window}. Une
partie de la création d'un  projet consiste à obtenir un **ID client Google** et une **Valeur confidentielle**. L'ID client
Google et la Valeur confidentielle sont les identificateurs uniques de votre application utilisés par l'authentification Google
et sont requis pour la configuration du tableau de bord {{site.data.keyword.amashort}}.

1. Ouvrez votre application dans la console de développeur Google.
3. Ajoutez l'API **Google+**.
3. Créez des données d'identification à l'aide d'OAuth. Sélectionnez Application Web comme type d'application. Entrez l'URI de redirection
{{site.data.keyword.amashort}} dans la zone URI de redirection autorisées. Obtenez l'URI d'autorisation de redirection {{site.data.keyword.amashort}} depuis l'écran de configuration Google du tableau de bord {{site.data.keyword.amashort}}(voir étapes ci-dessous).
4. Enregistrez les changements. Notez l'**ID client Google** et la **Valeur confidentielle de l'application**.


## Configuration de {{site.data.keyword.amashort}} pour l'authentification Google
{: #google-auth-config-ama}

Maintenant que vous disposez d'un ID d'application et d'une valeur confidentielle Google, vous pouvez activer l'authentification Google dans le tableau de bord {{site.data.keyword.amashort}}.

1. Ouvrez le tableau de bord de service {{site.data.keyword.amashort}}.
1. Dans l'onglet **Gérer**, activez **Autorisation**.
1. Développez la section **Google**.
1. Cochez la case **Ajouter Google à une application Web**
4. Dans la section **Configure for Web** :   
    * Notez la valeur dans la zone de texte **Mobile Client Access Redirect URI for Google Developer Console**. Il s'agit de la valeur que vous devez ajouter à la zone relative aux identificateurs **URI de redirection valides** de l'option portant sur les **restrictions dans l'ID client pour l'application Web** du **portail des développeurs Google**.
    * Entrez l'**ID client** et la **Valeur confidentielle du client**.
    * Entrez l'URI de redirection dans **URI de redirection de votre application Web**. Cette valeur est celle de l'URI de redirection à
laquelle accéder à l'aboutissement du processus d'autorisation et est déterminée par le développeur.
5. Cliquez sur **Sauvegarder**.


## Implémentation du flux d'autorisation {{site.data.keyword.amashort}} en utilisant Google comme fournisseur d'identité
{: #google-auth-flow}

La variable d'environnement `VCAP_SERVICES` est créée automatiquement pour chaque instance de service
{{site.data.keyword.amashort}} et contient les propriétés requises pour le processus d'autorisation. Elle se compose d'un objet JSON et vous pouvez la visualiser dans l'onglet **Données d'identification pour le service** du tableau de bord de service de {{site.data.keyword.amashort}}.

Pour démarrer le processus d'autorisation :

1. Identifiez le noeud final d'autorisation (`authorizationEndpoint`) et l'ID client
(`clientId`) dans les données d'identification du service stockées dans la variable d'environnement
`VCAP_SERVICES`.

	`var cfEnv = require("cfenv");`

	`var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;`

	**Remarque :** si vous avez ajouté le service {{site.data.keyword.amashort}} dans votre application avant l'ajout de la prise en charge Web, il se peut que vous n'ayez pas de noeud final de jeton dans les données d'identification pour le service. A la place, utilisez les URL suivantes, selon votre région {{site.data.keyword.Bluemix_notm}} :

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
 });

	function checkAuthentication(req, res, next){
		// Vérifie si l'utilisateur est authentifié
  if (req.session.userIdentity){
			next()
		} else {
			// Si ce n'est pas le cas, redirection vers un serveur d'autorisations
				var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;
				var authorizationEndpoint = mcaCredentials.authorizationEndpoint;
				var clientId = mcaCredentials.clientId;
				var redirectUri = "http://some-server/oauth/callback"; // Your Web application redirect URI
				var redirectUrl = authorizationEndpoint + "?response_type=code";
				redirectUrl += "&client_id=" + clientId;
				redirectUrl += "&redirect_uri=" + redirectUri;
				res.redirect(redirectUrl);
			}
	}
	```
	{: codeblock}

	Notez que le paramètre `redirect_uri` représente l'URI de redirection de votre application Web
et qu'il doit être égal à celui défini dans le tableau de bord {{site.data.keyword.amashort}}.

	Après redirection au noeud final d'autorisation, l'utilisateur reçoit un formulaire de connexion par Google. Une fois que l'utilisateur reçoit les autorisations de connexion après avoir fourni son identité Google, le service {{site.data.keyword.amashort}} appelle l'URI de redirection de votre application Web en soumettant le code d'accord en tant que paramètre de demande.

## Obtention des jetons
{: #google-auth-tokens}

L'étape suivante consiste à obtenir le jeton d'accès et le jeton d'identité à l'aide du code d'accord reçu auparavant .

1. Extrayez le jeton `tokenEndpoint`, `clientId` et `secret` depuis les données d'identification du service, stockées dans la variable d'environnement `VCAP_SERVICES`.

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

2. Envoyez une requête POST à l'URI du serveur de jeton avec les valeurs grant_type
("authorization_code"),
client_id, redirect_uri, et le code en tant que paramètres du masque. Envoyez les éléments `clientId` et `clientSecret` sous forme
de données d'authentification HTTP de base.

	Le code suivant extrait les valeurs requises et les envoie avec une requête Post.

	```Java
  var cfEnv = require("cfenv");
  var base64url = require("base64url ");
  var request = require('request');

	app.get("/oauth/callback", function(req, res, next){
		var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials; 	var tokenEndpoint =
mcaCredentials.tokenEndpoint; 	var formData = {
			grant_type: "authorization_code",
			client_id: mcaCredentials.clientId,
			redirect_uri: "http://some-server/oauth/callback",// URI de redirection de votre application Web
			code: req.query.code
		}

		request.post({
			url: tokenEndpoint,
			formData: formData
		}, function (err, response, body) {
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

	Le paramètre `redirect_uri` est l'URI de redirection après l'aboutissement ou l'échec de l'authentification avec
Google+ et doit correspondre à l'élément `redirect_uri` défini sur le tableau de bord {{site.data.keyword.amashort}}.  

	Prenez soin d'envoyer cette demande POST dans les 10 minutes, qui correspond au délai d'expiration du code d'accord. Au bout de 10 minutes, un nouveau code est requis.

	Le corps de la réponse POST contient les éléments `access_token` et `id_token` codés en base 64.

	Une fois que vous avez obtenu l'accès et reçu les jetons d'identité, vous pouvez marquer la session Web comme authentifiée et, si vous le souhaitez, rendre persistants ces jetons.  


##Utilisation du jeton d'accès et du jeton d'identité obtenus
{: #google-auth-using-token}

Le jeton d'identité contient des informations sur l'identité de l'utilisateur. Dans le cas d'une authentification Google, le jeton contient toutes les informations que
l'utilisateur a accepté de partager, comme son nom complet, l'URL de sa photo de profil, etc.  

Le jeton d'accès active les communications avec les ressources qui sont protégées par des filtres d'autorisation {{site.data.keyword.amashort}}. Voir [Protection des ressources](protecting-resources.html).

Pour soumettre des demandes à des ressources protégées, ajoutez aux demandes un en-tête Authorization doté de la structure suivante :

`Authorization=Bearer <jeton_accès> <jeton_ID>`

####Conseils :
{: #tips}

* Les éléments `jeton_accès` et `jeton_ID`  doivent être séparés par un espace.

* Le paramètre `jeton_accès` est facultatif. Si vous l'omettez, il est possible d'accéder à la ressource protégée, mais aucune information sur l'utilisateur autorisé ne sera transmise.
