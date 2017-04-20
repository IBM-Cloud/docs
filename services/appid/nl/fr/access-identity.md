---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Jetons d'accès et d'identité
{: #access-and-identity}

{{site.data.keyword.appid_short}} utilise deux types de jetons : jeton d'accès et jeton d'identité. Les jetons sont au format <a href="https://jwt.io/introduction/" target="_blank">Jeton Web JSON<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
{:shortdesc}


## Jeton d'accès
{: #access-tokens}

Le jeton d'accès permet la communication avec des [ressources de back-end](/docs/services/appid/protecting-resources.html) qui sont protégées par les filtres d'autorisation
d'{{site.data.keyword.appid_short_notm}}. Le jeton est conforme aux spécifications JOSE (JavaScript Object Signing and Encryption) et adopte le format suivant :

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

## Jeton d'identité
{: #identity-tokens}

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
