---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# A propos d'{{site.data.keyword.appid_short_notm}}
{: #about}

{{site.data.keyword.appid_full}} permet aux développeurs de sécuriser et d'ajouter une authentification à leurs applications {{site.data.keyword.Bluemix}} via seulement quelques lignes de code. Les développeurs peuvent également gérer les données spécifiques à l'utilisateur pour construire des applications personnalisées.
{:shortdesc}


Vous pouvez utiliser le service d'une des manières suivantes :

* Pour ajouter une authentification à vos applications mobiles et Web
* Pour accorder un accès aux ressources de back-end et aux applications Web protégées
* Pour protéger les applications Node.js et Swift hébergées sur {{site.data.keyword.Bluemix_notm}}
* Pour stocker des données utilisateur, telles que les préférences d'application ou des informations de leur profil social public
* Pour utiliser des données stockées afin de construire des applications personnalisées
* Pour protéger les ressources tant face aux utilisateurs authentifiés qu'aux utilisateurs anonymes

**Remarque** : les protocoles implémentés sont totalement compatibles avec Open Connect (OIDC).


## Composants
{: #components}

* Tableau de bord - Permet de télécharger des exemples fonctionnels, de consulter les journaux d'activité, de configurer divers types d'authentification et de fournisseurs d'identité
* SDK client - Permet de construire des applications mobiles et Web utilisant le service pour implémenter l'authentification d'utilisateur
    * Prérequis pour Android : API 25 (ou version ultérieure), Java 8.x, Android SDK Tools 25.2.5 (ou versions ultérieure), Android SDK Platform Tools 25.0.3 (ou version ultérieure), Android Build Tools version 25.0.2
    * Prérequis pour iOS : iOS9 (ou version ultérieure), MacOS 10.11.5, Xcode 8.2
* SDK serveur - Permet de protéger des ressources hébergées sur {{site.data.keyword.Bluemix_notm}}
    * Contextes d'exécution pris en charge : Node.js et Swift

## Présentation de l'architecture

Diagramme de l'architecture ![{{site.data.keyword.appid_short_notm}}](/images/appid_architecture.png)

Figure 1. Diagramme de l'architecture {{site.data.keyword.appid_short_notm}}

Vous pouvez protéger vos ressources de cloud à l'aide du SDK serveur d'{{site.data.keyword.appid_short_notm}}. Utilisez la catégorie de demande fournie par le SDK client d'{{site.data.keyword.appid_short_notm}} pour communiquer avec vos ressources de cloud protégées.

* Le SDK client détecte les demandes non autorisées et renvoie une demande d'authentification HTTP 401.
* Le SDK client détecte les demandes authentification HTTP 401 et lance automatiquement le processus d'authentification conformément à la configuration des fournisseurs d'identité.
* Une tentative d'authentification est lancée en fonction des fournisseurs d'identité actuellement configurés.
* Si l'authentification aboutit, le service renvoie des jetons d'authentification et d'identité.
* Le SDK client ajoute automatiquement le jeton d'autorisation à la demande d'origine et réachemine la demande à la ressource de cloud.
* Le SDK serveur extrait de la demande le jeton d'accès et le valide auprès d'{{site.data.keyword.appid_short_notm}}.
L'accès est accordé et la réponse est renvoyée à l'application.


## Flux de demandes
{: #request}

Le diagramme ci-dessous illustre un flux de demandes depuis le SDK client vers votre application de back-end et les fournisseurs d'identité.

![Flux de demandes {{site.data.keyword.appid_short_notm}}](/images/appidflow.png)


* Utilisez le SDK client {{site.data.keyword.appid_short_notm}} pour soumettre une demande à vos ressources de back-end protégées par le SDK serveur {{site.data.keyword.appid_short_notm}}.
* Le SDK serveur {{site.data.keyword.appid_short_notm}} détecte les demandes dépourvues d'autorisation et renvoie une réponse HTTP 401 une portée d'autorisation.
* Le SDK client détecte automatiquement la réponse HTTP 401 et lance la procédure d'autorisation.
* Lorsque le SDK client contacte le service, le SDK serveur renvoie le widget de connexion si plusieurs fournisseurs d'identité ont été configurés. {{site.data.keyword.appid_short_notm}} appelle le fournisseur d'identité et lui présente son formulaire d'identification ou renvoie un code d'acceptation qui lui permet de s'authentifier si aucun fournisseur d'identité n'a été configuré.
* {{site.data.keyword.appid_short_notm}} demande à l'application client de s'authentifier en répondant à une demande d'authentification.
* Si Facebook ou Google sont configurés et que l'utilisateur se connecte, l'authentification est traitée par le flux du protocole d'autorisation OAuth du fournisseur d'identité correspondant.
* Si l'authentification se conclut par le même code d'accord, celui-ci est envoyé au noeud final du jeton. Le noeud final renvoie deux jetons : un code d'accès et un jeton d'identification. Dès lors, toutes les demandes effectuées avec le SDK client ont le nouvel en-tête d'autorisation obtenu.
* Le SDK client renvoie automatiquement la demande d'origine ayant déclenché le flux d'autorisation.
* Le SDK serveur extrait l'en-tête de l'autorisation depuis la demande, le valide auprès du service et octroie l'accès à une ressource de back-end.

## Jetons d'accès et d'identité
{: #access-and-identity}

{{site.data.keyword.appid_short}} utilise deux types de jetons : jeton d'accès et jeton d'identité. Les jetons sont au format <a href="https://jwt.io/introduction/" target="_blank">Jeton Web JSON<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.


### Jeton d'accès
{: #access-tokens notoc}

Le jeton d'accès permet la communication avec des ressources protégées par des filtres d'autorisation d'{{site.data.keyword.appid_short_notm}}. Voir [Protection des ressources de back-end](/docs/services/appid/protecting-resources.html).
Le jeton est conforme aux spécifications JOSE (JavaScript Object Signing and Encryption) et adopte le format suivant :

```
Header: {

    "typ": "JOSE", // type d'en-tête, conformément à la spécification

    "alg": "RS256", // algorithme, conformément à la spécification

}
Payload: {

    "iss": "", // émetteur, indique le serveur AppID ayant émis ce jeton. StringOrURL

    "sub": "", // sujet, indique à qui ce jeton a été émis. Très probablement à un ID utilisateur

    "aud": "", // public, indique à qui ce jeton est destiné. ID_client OAuth2.

    "exp: "", // horodatage de l'expiration, date et heure

    "iat": "", // horodatage de l'émission, date et heure

    "tenant": "xxx", indique l'ID titulaire AppID pour lequel le jeton a été émis

    "auth_by": "appid_anon / appid_facebook / appid_google",

    "scope": "", // indique la ou les portées pour lesquelles le jeton a été émis

}
```
{:screen}

### Jeton d'identité
{: #identity-tokens notoc}

Le jeton d'identité contient des informations sur l'utilisateur, notamment son nom, son adresse électronique, son sexe, sa photo et son emplacement.

```
Header: {

    "typ": "JOSE", // type d'en-tête, conformément à la spécification

    "alg": "RS256", // algorithme, conformément à la spécification

}
Payload: {

    "iss": "", // émetteur, indique le serveur AppID ayant émis ce jeton. StringOrURL

    "sub": "", // sujet, indique à qui ce jeton a été émis. ID utilisateur AppIDm.

    "aud": "", // public, indique à qui ce jeton est destiné. ID_client OAuth2.

    "exp: "", // horodatage de l'expiration, date et heure

    "iat": "", // horodatage de l'émission, date et heure

    "tenant": "xxx", // indique l'ID titulaire AppID pour lequel le jeton a été émis

    "name": "John Smith", // nom complet de l'utilisateur tel qu'indiqué par l'IDP, obligatoire,

    "email": "js@mail.com", // adresse électronique telle qu'indiquée par l'IDP, uniquement si disponible,

    "gender", "male", // sexe de l'utilisateur tel qu'indiqué par l'IDP, uniquement si disponible,

    "locale": "en", // environnement local de l'utilisateur tel qu'indiqué par l'IDP, uniquement si disponible

    "picture": "https://url.to.photo", // URL pointant sur la photo de l'utilisateur, uniquement si disponible

    "auth_by": "appid_facebook/appid_google", // nom de l'IDP (fournisseur d'identité) utilisé pour l'authentification, obligatoire

    "identities": [

        "provider: "appid_facebook/appid_google", // obligatoire

        "id": "ID utilisateur unique tel qu'indiqué par l'IDP", // obligatoire

        "profile": { ... } // objet JSON renvoyé par l'IDP, obligatoire

      },

      {...}, {...} // autres identités liées

    ],

    "oauth_client":{

      "type": "serverapp/mobileapp de l'enregistrement du client", // obligatoire

      "name": "client_name (nom du client) tel qu'indiqué lors de l'enregistrement du client", // obligatoire

      "software_id": "software_id (ID logiciel) tel qu'indiqué lors de l'enregistrement du client", // obligatoire

      "software_version": "version du logiciel telle qu'indiquée lors de l'enregistrement du client", // obligatoire

      "device_id": "device_id (ID de périphérique) d'après l'enregistrement client", // uniquement pour mobile

      "device_model": "device_model (modèle du périphérique) d'après l'enregistrement du client", // uniquement pour mobile

      "device_os": "device_os (système d'exploitation du périphérique) d'après l'enregistrement du client", // uniquement pour mobile

    }

}
```
{:screen}


## Présentation des fournisseurs d'identité
{: #identity-providers-overview}

Vous pouvez utiliser les fournisseurs d'identité suivants dans vos applications mobiles et Web :

* **Facebook** - Vos utilisateurs se connectent à l'application mobile ou Web avec leurs données d'identification Facebook.
* **Google** -  Vos utilisateurs se connectent à l'application mobile ou Web avec leurs données d'identification Google+.
<!--* **Custom** - Bring your own identity provider. The identity providers should be compliant with OIDC. -->

## Utilisation de la configuration par défaut
{: #default-configuration}

{{site.data.keyword.appid_short_notm}} fournit une configuration par défaut lorsque vous mettez en place initialement vos fournisseurs d'identité. Vous ne pouvez utiliser la configuration par défaut qu'en mode développement. Pour chaque fournisseur d'identité, ces données d'identification sont limitées à 100 utilisations par instance {{site.data.keyword.appid_short_notm}} et par jour. Avant de publier votre application, mettez à jour la configuration par défaut en spécifiant vos propres données d'identification. Pour mettre à jour votre configuration, voir [Configuration des fournisseurs d'identité](/docs/services/appid/identity-providers.html).
