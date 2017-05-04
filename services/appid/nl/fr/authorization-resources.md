---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Filtres d'autorisation et en-têtes
{: #auth}

Le SDK serveur d'{{site.data.keyword.appid_short}} fournit des stratégies pour protéger deux types de ressources : API et applications Web.
{:shortdesc}


## Filtres d'autorisation
{: #auth-filter}

La stratégie de protection de l'API renvoie une réponse HTTP 401 avec une liste de portées afin d'obtenir une autorisation pour un client non authentifié. La stratégie de protection d'application Web renvoie une réponse HTTP 302 suggérant une redirection. La redirection envoie un client non authentifié à la page de connexion hébergée par le service {{site.data.keyword.appid_short_notm}} ou directement à la page de connexion d'un fournisseur d'identité, selon votre configuration.



### Stratégie d'API
{: #api}

La stratégie d'API s'attend à ce que les demandes contiennent un en-tête d'autorisation avec un jeton d'accès valide. La réponse peut également contenir un jeton d'identité, mais ceci n'est pas obligatoire. Voir [Jetons d'accès et d'identité](/docs/services/appid/access-identity.html#access-and-identity).

Si un jeton n'est pas valide ou a expiré, la stratégie d'API renvoie une erreur HTTP 401 contenant les informations suivantes : Www-Authenticate=Bearer scope="{scope}" error="{error}". Le composant `error` est facultatif.

Si la demande renvoie un jeton valide, le contrôle passe au middleware suivant et la propriété `appIdAuthorizationContext` est injectée dans l'objet de demande. Cette propriété contient les jetons d'accès et d'identité originaux, ainsi que les informations de contenu décodées sous forme d'objets JSON ordinaires.


### Stratégie d'application Web
{: #web}

Lorsque la classe de stratégie d'application Web détecte des tentatives non authentifiées d'accès à une ressource protégée, elle redirige automatiquement le navigateur de l'utilisateur vers la page d'authentification. Si l'authentification aboutit, l'utilisateur est ramené à l'URL de rappel de l'application Web. Le service utilise la classe de stratégie d'application Web pour obtenir les jetons d'accès et d'identité. Après avoir obtenu ces jetons, la classe de stratégie d'application Web les stocke dans une session HTTP sous `WebAppStrategy.AUTH_CONTEXT`. La décision de stocker ou non les jetons d'accès et d'identité dans la base de données de l'application relève de l'utilisateur.

## En-tête d'autorisation
{: #auth-header}

L'en-tête d'autorisation dans la demande entrante est composé de trois parties séparées par des espaces : Bearer, Access Token et ID Token. Access Token (jeton d'accès) est un composant obligatoire et ID Token (jeton d'identité) est facultatif. La structure d'en-tête attendue est la suivante : Authorization=Bearer {jeton_d'accès} [jeton_d'identité}]
