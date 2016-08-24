---

copyright:
  year: 2016

---

# Activation de l'authentification Facebook pour les applications Web

*Dernière mise à jour : 18 juillet 2016*
{: .last-updated}

Utilisez Facebook pour authentifier les utilisateurs sur votre application Web.

## Avant de commencer
{: #facebook-auth-android-before}
Vous devez disposer des éléments suivants :
* Une application Web. 
* Une instance d'une application {{site.data.keyword.Bluemix_notm}} protégée par le service
{{site.data.keyword.amashort}}. Pour plus d'informations sur la création d'un système de back end {{site.data.keyword.Bluemix_notm}}, voir [Initiation](index.html).
* L'URI de redirection finale (au terme du processus d'autorisation).


## Configuration d'une application Facebook pour votre site Web
Pour utiliser Facebook comme fournisseur d'identité dans votre site Web, vous devez ajouter et configurer la plateforme de site Web sur votre application 
Facebook.

1. Connectez-vous au portail de développeurs Facebook (https://developers.facebook.com).
2. Ouvrez ou créez votre application.
1. Notez les valeurs de **Application ID** et de **App Secret**. Vous en aurez besoin pour configurer votre projet Web
pour authentification Facebook dans le tableau de bord {{site.data.keyword.amashort}}.
1. Ajoutez la plateforme de site Web si elle n'existe pas.
1. Ajoutez ou ouvrez la **Connexion Facebook** depuis la liste des produits.
1. Entrez l'URI de noeud final de rappel du serveur d'autorisation dans la zone **URI de redirection OAuth
valides**. Vous pouvez identifier cet URI de redirection d'autorisation dans les étapes de configuration du tableau de bord
{{site.data.keyword.amashort}} ci-dessous.
2. Enregistrez les changements.




# Configuration de {{site.data.keyword.amashort}} pour l'authentification Facebook
Une fois que vous disposez de votre ID d'application et de la valeur confidentielle Facebook, et que votre application Facebook a été configurée pour servir les clients Web, vous pouvez activer l'authentification Facebook dans le tableau de bord {{site.data.keyword.Bluemix_notm}}.

1. Ouvrez le tableau de bord {{site.data.keyword.Bluemix_notm}}.
1. Cliquez sur la vignette de l'application pertinente. L'application est chargée.
2. Cliquez sur la vignette du service {{site.data.keyword.amashort}}.
1. Cliquez sur le bouton **Configurer** dans le panneau **Facebook**.
2. Notez la valeur de la zone de texte **URI de redirection Mobile Client Access pour la console développeur Facebook **. Cette valeur
est celle que vous devrez ajouter à la zone **URI de redirection OAuth valides** dans la **Connexion Facebook** du portail
de développeurs Facebook à l'étape 6 plus haut.
1. Entrez l'**ID d'application** et la **Valeur confidentielle de l'application** Facebook.
2. Entrez l'URI de redirection dans **URI de redirection de votre application Web**. Cette valeur est celle de l'URI de redirection à laquelle accéder
à l'aboutissement du processus d'autorisation et est déterminée par le développeur.
3. Cliquez sur **Sauvegarder**.




## Implémentation du flux d'autorisation {{site.data.keyword.amashort}} en utilisant Facebook comme fournisseur d'identité

La variable d'environnement `VCAP_SERVICES` est créée automatiquement pour chaque instance de service {{site.data.keyword.amashort}}
et contient les propriétés requises pour le processus d'autorisation. Elle est constituée d'un objet JSON et peut être affichée en cliquant sur **Variables
d'environnement** dans le navigateur sur le côté gauche de votre application.

Pour démarrer le processus d'autorisation :

1. Extrayez le noeud final d'autorisation (`authorizationEndpoint`) et l'ID client
(`clientId`) depuis les données d'identification du service stockées dans la variable
d'environnement `VCAP_SERVICES`. 

    **Remarque :** Si vous avez créé le service {{site.data.keyword.amashort}} avant l'ajout de la prise en charge Web,
il se peut que vous ne disposiez pas de noeuds finaux d'autorisation dans les données d'identification pour le service. Dans
ce cas, utilisez le noeud final d'autorisation ci-dessous correspondant à votre région Bluemix :
  
  Sud des Etats-Unis : 
  ```
  https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization
   ```
  Londres :
   ``` 
 https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization
   ```
  Sydney : 
    ```
 https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization
  ```
2. Construisez l'URI du serveur d'autorisation en utilisant `response_type("code")`, `client_id` et
`redirect_uri` en tant que paramètres de requête. 
3. Redirigez l'utilisateur depuis votre application Web vers l'URI généré.



L'exemple ci-dessous extrait les paramètres depuis la variable `VCAP_SERVICES`, construit l'URL et envoie la demande de redirection.

  ```Java
  var cfEnv = require("cfenv");
  app.get("/protected", checkAuthentication, function(req, res, next){
      res.send("Bonjour, ceci est un noeud final protégé");
  }
); 
  
  function checkAuthentication(req, res, next){
  // Vérifie si l'utilisateur est authentifié

    if (req.session.userIdentity){
       next()
     } else {
  // Sinon, redirection au serveur d'autorisation
        var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;
        var authorizationEndpoint = mcaCredentials.authorizationEndpoint;
        var clientId = mcaCredentials.clientId;
        var redirectUri = "http://some-server/oauth/callback";
         // URI de redirection de votre application Web

        var redirectUrl = authorizationEndpoint + "?response_type=code";
        redirectUrl += "&client_id=" + clientId;
        redirectUrl += "&redirect_uri=" + redirectUri;

        res.redirect(redirectUrl);

      }
  }
  
 ```

   Le paramètre `redirect_uri` est l'URI de redirection après l'aboutissement ou l'échec de l'authentification avec
Facebook.
   

 Après redirection au noeud final d'autorisation, l'utilisateur reçoit un formulaire de connexion par
Facebook. Une fois que Facebook confirme l'identité de l'utilisateur, le service {{site.data.keyword.amashort}} appelle l'URI de redirection de votre
application Web en soumettant le code d'accord en tant que paramètre de requête.  
## Obtention des jetons

L'étape suivante consiste à obtenir le jeton d'accès et le jeton d'identité à l'aide du code d'accord reçu auparavant : 

 1.  Extrayez le jeton `tokenEndpoint`, `clientId` et `secret` depuis les données d'identification du
service stockées dans la variable d'environnement `VCAP_SERVICES`. 
 
    **Remarque :** Si vous avez utilisé Mobile Client Access avant l'ajout de la prise en charge Web,
il se peut que vous n'ayez pas de noeud final de jeton dans les données d'identification pour le service. 
Dans ce cas, utilisez à la place l'URL ci-dessous correspondant à votre région Bluemix : 

    Sud des Etats-Unis : 
    ```
    https://mobileclientaccess.ng.bluemix.net/oauth/v2/token
     ```
    Londres :
      ```
    https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token
     ```
    Sydney : 
      ```
    https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token
    ```

 1. Envoyez une demande POST à l'URI du serveur de jeton avec le type d'autorisation ("authorization_code"), l'élément
`clientId` et votre URI de redirection comme paramètres de masque. Envoyez les éléments `clientId` et
`secret` sous forme de données d'authentification HTTP de base.
 
Le code suivant extrait les valeurs requises et les envoie avec une requête Post.

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
     // URI de redirection d'application Web
      code: req.query.code
   }


    request.post({
        url: tokenEndpoint,
        formData: formData
      }, function (err, response, body){
        var parsedBody = JSON.parse(body);
        req.session.accessToken = parsedBody.access_token;
        req.session.idToken = parsedBody.id_token;
        var idTokenComponents = parsedBody.id_token.split(".");
        // [header, payload, signature]
        var decodedIdentity= base64url(idTokenComponents[1]);
        req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"];
        res.redirect("/");
        }
   ).auth(mcaCredentials.clientId, mcaCredentials.secret);
   }
  ); 
   
  ```
 
 Notez que le paramètre `redirect_uri` doit correspondre au paramètre `redirect_uri` utilisé dans la demandee d'autorisation
précédente. La valeur du paramètre `code` doit être le code d'accord dans la réponse  de la demandee d'autorisation . 
Le code d'accord est valide pendant 10 minutes, après quoi un nouveau code doit être obtenu.

Le corps de la réponse contiendra le code d'accès et le jeton d'ID au format JWT (https://jwt.io/).

Une fois que vous avez obtenu l'accès et reçu les jetons d'identité, vous pouvez marquer la session Web comme authentifiée et, si vous le désirez,
rendre
persistants ces jetons.  

##Utilisation du jeton d'accès et du jeton d'identité obtenus 

Le jeton d'identité contient des informations sur l'identité de l'utilisateur. Dans le cas d'une authentification Facebook, le jeton contiendra toutes les informations que
l'utilisateur a accepté de partager, comme son nom complet, son groupe d'âge, l'URL de sa photo de profil, etc.  

Le jeton d'accès active les communications avec les ressources protégées par les filtres d'autorisation de
{{site.data.keyword.amashort}}. Voir [Protection des ressources](protecting-resources.html).


Pour soumettre des demandes à des ressources protégées, ajoutez aux demandes un en-tête Authorization doté de la structure suivante : 

`Authorization=Bearer <jeton_accès> <jeton_ID>`

**Remarque :** 

* Les éléments `jeton_accès` et `jeton_ID`  doivent être séparés par un espace. 

* Le paramètre `jeton_accès` est facultatif. Si vous l'omettez, il est possible d'accéder à la ressource protégée, mais sans recevoir
d'informations sur l'utilisateur autorisé. 
 



