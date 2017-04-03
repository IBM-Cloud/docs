---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---

{:shortdesc: .shortdesc}
{:codeblock:.codeblock}

Le service {{site.data.keyword.amafull}} est remplacé par le service {{site.data.keyword.appid_full}}.

# Protection des ressources de back-end avec le service {{site.data.keyword.amashort}}
{: #protecting-resources}


Le service {{site.data.keyword.amafull}} permet de protéger les applications de back end Node.js et Java qui s'exécutent sur {{site.data.keyword.Bluemix_notm}} via des fonctions de surveillance et de sécurité OAuth pour appareils mobiles.
{:shortdesc}

## Avant de commencer
{: #before-you-begin}
Avant de commencer, vérifiez que le service Node.js existe dans votre application de back end {{site.data.keyword.Bluemix_notm}}.


## Filtre d'autorisation
{: #auth-filter}
Le SDK serveur de {{site.data.keyword.amashort}} contient des filtres d'autorisation qui peuvent vous servir à protéger vos applications de back end.  Le filtre d'autorisation intercepte les demandes entrantes et vérifie la présence d'un en-tête d'autorisation. En cas d'absence ou d'invalidité de l'en-tête d'autorisation, le filtre renvoie une réponse d'erreur HTTP 401. Le
SDK client {{site.data.keyword.amashort}} sait comment intercepter une réponse HTTP 401 renvoyée par le SDK serveur
{{site.data.keyword.amashort}} et déclencher le flux d'authentification.
## En-tête d'autorisation
{: #auth-header}
L'en-tête d'autorisation de la demande entrante se compose de trois parties : Bearer, le jeton d'accès et le jeton d'ID, qui sont
séparées par des espaces. Le `jeton d'accès` est un composant nécessaire, alors que le `jeton d'ID est facultatif`.

L'en-tête d'autorisation entrant est traité par le filtre d'autorisation correspondant. Le filtre valide les signatures, la date d'expiration, et l'intégrité structurelle des jetons d'accès et d'ID. Une fois que la validation a abouti, un objet de contexte de sécurité est ajouté à l'objet demande. Vous
pouvez établir une référence au contexte de sécurité à l'aide de l'API pertinente.

Le contexte de sécurité contient les informations sur le sujet, l'utilisateur, l'unité et l'application, selon la structure suivante :
```JSON
{
    "imf.sub":"myclientid",
    "imf.user": {
        "id":"user-name",
        "authBy":"myrealm",
        "displayName":"display-name"
    },
    "imf.device": {
        "id":"device-id",
        "platform":"iOSnative",
        "model":"device-model",
        "osVersion":"device-os"
    },
    "imf.application": {
        "id":"ios.bundle.id",
        "version":"1.0"
    }
}
```
{: codeblock}

* `imf.sub` : Sujet du jeton d'ID ou ID unique du client s'il n'existe pas de jeton d'ID.
* `imf.user` : Identité de l'utilisateur qui est extraite du jeton d'ID. S'il n'existe pas de jeton d'ID, cette zone contient un objet vide.
* `imf.device` : Identité de l'appareil qui est extraite du jeton d'ID. S'il n'existe pas de jeton d'ID, cette zone contient un objet vide.
* `imf.application` : Identité de l'application qui est extraite du jeton d'ID. S'il n'existe pas de jeton d'ID, cette zone contient un objet vide.

## Etapes suivantes
{: #next-steps}
* [Protection des ressources Node.js](protecting-resources-nodejs.html)
* [Protection des ressources Liberty for Java&trade;](protecting-resources-java.html)
* [Développement local](protecting-resources-local.html)
