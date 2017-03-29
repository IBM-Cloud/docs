---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Profils utilisateur
{: #user-profile}

Un profil utilisateur est une entité stockée et gérée par {{site.data.keyword.appid_short}}. Le profil contient les attributs et l'identité d'un utilisateur et peut être anonyme ou lié à une identité gérée par un fournisseur d'identité.
{:shortdesc}

{{site.data.keyword.appid_short_notm}} fournit une API pour la connexion, anonyme ou bien avec authentification, via un fournisseur d'identité OpenId Connect (OIDC), Voir [Configuration des fournisseurs d'identité](https://console.stage1.ng.bluemix.net/docs/services/appid/identity-providers.html#setting-up-idp). Le noeud final d'API d'attribut de profil utilisateur est une ressource protégée par le jeton d'accès généré par {{site.data.keyword.appid_short_notm}} au cours du processus de connexion et d'authentification.


## Stockage, lecture et suppression d'attributs utilisateur
{: #storing-data}

{{site.data.keyword.appid_short_notm}} fournit une [API REST](http://mobileclientaccess.stage1.mybluemix.net/swagger-ui/#!/Authorization_Server_V3/authorization) pour réaliser des opérations CRUD sur les attributs d'un utilisateur, ainsi qu'un SDK pour [Android](https://github.com/ibm-cloud-security/appid-clientsdk-android) et pour les clients mobiles [Swift](https://github.com/ibm-cloud-security/appid-clientsdk-swift).


## Identité OAuth
{: #oauth}

Lors de l'appel de l'API de connexion OAuth, {{site.data.keyword.appid_short_notm}} utilise les protocoles OAuth 2.0 et OIDC pour autoriser et authentifier l'appelant avec le fournisseur d'identité sélectionné. Une fois identifiée, l'identité est associée à un enregistrement utilisateur {{site.data.keyword.appid_short_notm}}. {{site.data.keyword.appid_short_notm}} renvoie un  jeton d'accès qui peut être utilisé pour accéder aux attributs de l'utilisateur, et un jeton d'accès contenant les informations d'identité fournies par le fournisseur d'identité. Le même enregistrement utilisateur et ses attributs sont accessibles à nouveau par n'importe quel client qui s'authentifie avec cette même identité.


## Utilisateur anonyme
{: #anonymous}

Lorsque vous vous connectez de manière anonyme, {{site.data.keyword.appid_short_notm}} crée un enregistrement utilisateur qui est marqué comme anonyme. {{site.data.keyword.appid_short_notm}} renvoie des jetons d'accès et d'identité anonyme à l'appelant. En utilisant le jeton d'accès anonyme, l'application utilisateur peut créer, lire, mettre à jour et supprimer des attributs, lesquels sont stockés dans l'enregistrement utilisateur. Par exemple, un développeur peut créer une application dans laquelle un utilisateur peut commencer immédiatement à ajouter des articles à un panier d'achat sans avoir à se connecter.


## Utilisateur identifié
{: #identified}

Un utilisateur anonyme disposant d'une identité émise par un fournisseur d'identité peut devenir un utilisateur identifié. Le flux de passage d'un utilisateur anonyme à un utilisateur connu est décrit dans les étapes suivantes :

* Le développeur transmet le jeton d'accès anonyme à l'API de connexion.
* {{site.data.keyword.appid_short_notm}} authentifie l'utilisateur auprès du fournisseur d'identité.
* {{site.data.keyword.appid_short_notm}} recherche l'enregistrement d'utilisateur anonyme défini par le jeton d'accès et lui affecte l'identité soumise.
    **Remarque** : l'identité ne peut être affectée à l'enregistrement d'utilisateur anonyme que si cette même identité n'a pas déjà été affectée à un autre utilisateur. Si l'identité est déjà associée à un autre utilisateur {{site.data.keyword.appid_short_notm}}, le jeton d'accès et le jeton d'identité contiennent les informations de l'enregistrement de cet autre utilisateur et permettent l'accès à ses attributs. L'utilisateur anonyme précédent et ses attributs ne seront pas accessibles via le nouveau jeton d'accès. Jusqu'à l'expiration du jeton, les informations sont toujours accessibles via le jeton d'accès anonyme. Le développeur peut décider comment fusionner les attributs de l'utilisateur anonyme et de l'utilisateur connu.
* Les nouveaux jetons d'accès et d'identité reçus d'{{site.data.keyword.appid_short_notm}} pointent vers l'utilisateur connu et le jeton d'identité contient les informations publiques reçus du fournisseur d'identité.
* Les jetons anonymes ne sont dès lors plus valides pour l'utilisateur.

Les attributs contenus par cet utilisateur alors qu'il était encore anonyme sont accessibles avec le nouveau jeton d'accès. De nouveaux jetons peuvent être ajoutés, changés ou supprimés. Par la suite, l'utilisateur et ses attributs sont résolus et accessibles lorsqu'il se connecte avec la même identité depuis n'importe quel client.


## Séparation et chiffrement des données
{: #data}

{{site.data.keyword.appid_short_notm}} stocke et chiffre les attributs de profil utilisateur. Etant donné qu'il s'agit d'un service partagé, chaque titulaire est associé à une clé de chiffrement dédiée et les données utilisateur de chaque titulaire sont chiffrées avec sa propre clé.

{{site.data.keyword.appid_short_notm}} garantit que les informations privées soient chiffrées avant leur stockage.
