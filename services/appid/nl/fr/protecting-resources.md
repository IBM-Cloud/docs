---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Protection des ressources de back-end
{: #protecting-resources}

Le SDK serveur d'{{site.data.keyword.appid_short}} fournit des stratégies pour protéger deux types de ressources : API et applications Web.
{:shortdesc}


## Accès aux ressources protégées depuis des SDK client
{: #accessing}

L'appel d'une ressource protégée lance, en cas de besoin, le widget de connexion. Si un jeton d'accès valide a déjà été obtenu, le widget de connexion n'est pas lancé et l'accès direct à la ressource est autorisé.


### Utilisation du SDK Swift
{: #requesting-swift notoc}

1. Importez BMSCore.

  ```swift
  import BMSCore
  ```
  {:pre}

2. Invocation d'une demande de ressource protégée.

  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<URL_de_votre_ressource_protégée>")
  request.send(completionHandler: {(response:Response?, error:Error?) 
      //code gérant la réponse
  })
  ```
  {:pre}


### Utilisation du SDK Android
{: #requesting-android notoc}

1. Invocation d'une demande de ressource protégée.

  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<URL_de_votre_ressource protégée>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
		public void onSuccess (Response response) {
     //code gérant la réponse
  }
  @Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
      //code gérant la réponse
  });
  ```
  {:pre}



## Filtres d'autorisation
{: #auth-filter}

La stratégie de protection de l'API renvoie une réponse HTTP 401 avec une liste de portées afin d'obtenir une autorisation pour un client non authentifié. La stratégie de protection d'application Web renvoie une réponse HTTP 302 suggérant une redirection. La redirection envoie un client non authentifié à la page de connexion hébergée par le service {{site.data.keyword.appid_short_notm}} ou directement à la page de connexion d'un fournisseur d'identité, selon votre configuration.



### Stratégie d'API
{: #api notoc}

La stratégie d'API s'attend à ce que les demandes contiennent un en-tête d'autorisation avec un jeton d'accès valide. La réponse peut également contenir un jeton d'identité, mais ceci n'est pas obligatoire. Voir [Jetons d'accès et d'identité](/docs/services/appid/about.html#acess-and-identity).

Si un jeton n'est pas valide ou a expiré, la stratégie d'API renvoie une erreur HTTP 401 contenant les informations suivantes : Www-Authenticate=Bearer scope="{scope}" error="{error}". Le composant `error` est facultatif.

Si la demande renvoie un jeton valide, le contrôle passe au middleware suivant et la propriété `appIdAuthorizationContext` est injectée dans l'objet de demande. Cette propriété contient les jetons d'accès et d'identité originaux, ainsi que les informations de contenu décodées sous forme d'objets JSON ordinaires.


### Stratégie d'application Web
{: #web notoc}

Lorsque la classe de stratégie d'application Web détecte des tentatives non authentifiées d'accès à une ressource protégée, elle redirige automatiquement le navigateur de l'utilisateur vers la page d'authentification. Si l'authentification aboutit, l'utilisateur est ramené à l'URL de rappel de l'application Web. Le service utilise la classe de stratégie d'application Web pour obtenir les jetons d'accès et d'identité. Après avoir obtenu ces jetons, la classe de stratégie d'application Web les stocke dans une session HTTP sous `WebAppStrategy.AUTH_CONTEXT`. La décision de stocker ou non les jetons d'accès et d'identité dans la base de données de l'application relève de l'utilisateur.

## En-tête d'autorisation
{: #auth-header}

L'en-tête d'autorisation dans la demande entrante est composé de trois parties séparées par des espaces : Bearer, Access Token et ID Token. Access Token (jeton d'accès) est un composant obligatoire et ID Token (jeton d'identité) est facultatif. La structure d'en-tête attendue est la suivante : Authorization=Bearer {jeton_d'accès} [jeton_d'identité}]
