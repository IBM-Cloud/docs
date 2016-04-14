---

Copyright : 2015, 2016

---

{:shortdesc: .shortdesc}

# Protection des ressources de cloud à l'aide de {{site.data.keyword.amashort}}
{: #protecting-resources}
Le service {{site.data.keyword.amashort}} permet de protéger les applications de back end Node.js et Java qui s'exécutent sur {{site.data.keyword.Bluemix_notm}} à l'aide des fonctions de sécurité OAuth pour les mobiles et de surveillance.
{:shortdesc}
## Filtre d'autorisation
{: #auth-filter}
Le SDK serveur de {{site.data.keyword.amashort}} contient des filtres d'autorisation qui peuvent vous servir à protéger vos applications de back end.  Le filtre d'autorisation intercepte les demandes entrantes et vérifie la présence d'un en-tête d'autorisation. En cas d'absence ou d'invalidité de l'en-tête d'autorisation, le filtre renvoie une réponse d'erreur HTTP 401. Le SDK serveur de {{site.data.keyword.amashort}} sait intercepter une réponse HTTP 401 renvoyée par le SDK serveur de {{site.data.keyword.amashort}} et déclenche le flux d'authentification.
## En-tête d'autorisation
{: #auth-header}
L'en-tête d'autorisation de la demande entrante se compose de trois parties : Bearer, le jeton d'accès et le jeton d'ID, qui sont
séparées par des espaces. Le `jeton d'accès` est un composant nécessaire, alors que le `jeton d'ID est facultatif`.

L'en-tête d'autorisation entrant est traité par le filtre d'autorisation correspondant. Le filtre valide les signatures, la date d'expiration, et l'intégrité structurelle des jetons d'accès et d'ID. Une fois que la validation a abouti, un objet de contexte de sécurité est ajouté à l'objet demande. Vous pouvez établir une référence au contexte de sécurité à l'aide d'une API.

Le contexte de sécurité contient les informations sur le sujet, l'utilisateur, le périphérique et l'application, selon la structure suivante :
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
* `imf.sub` : Sujet du jeton d'ID ou ID unique du client s'il n'existe pas de jeton d'ID.
* `imf.user` : Identité de l'utilisateur qui est extraite du jeton d'ID. S'il n'existe pas de jeton d'ID, cette zone contient un objet vide.
* `imf.device` : Identité du périphérique qui est extraite du jeton d'ID. S'il n'existe pas de jeton d'ID, cette zone contient un objet vide.
* `imf.application` : Identité de l'application qui est extraite du jeton d'ID. S'il n'existe pas de jeton d'ID, cette zone contient un objet vide.

## Etapes suivantes
{: #next-steps}
* [Protection des ressources Node.js](protecting-resources-nodejs.html)
* [Protection des ressources Liberty for Java&trade;](protecting-resources-java.html)
* [Développement local](protecting-resources-local.html)
