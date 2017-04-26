---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-17"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# IBM Cloud Identity and Access Management (IAM)
{: #iam_overview}

IBM Cloud IAM permet de gérer de manière sécurisée les identités des utilisateurs et des services, ainsi que l'accès aux ressources pour ces identités. Vous pouvez visualiser et gérer les utilisateurs à travers le compte ou l'organisation, en fonction des options d'accès que vous êtes habilité à gérer. Vous pouvez effectuer toutes les opérations concernant les utilisateurs, notamment les inviter et les gérer, ainsi que les rôles auxquels ils sont affectés, et les comptes et les organisations, ou bien les deux, auxquels ils peuvent accéder. En tant que propriétaire du compte, vous pouvez gérer les options d'accès dont vous et les utilisateurs sont tous deux membres, quel que soit le rôle, dans le compte actuel.

La gestion des identités couvre les aspects suivants :
 * Gestion des utilisateurs 
   * Création, suppression et mise à jour des informations sur les utilisateurs
   * Gestion de clé d'API
   * Création, actualisation et échange de jeton
   * Authentification de l'identité d'un utilisateur
 * Gestion de l'ID du service
   * Création, suppression et mise à jour des informations sur les utilisateurs
   * Gestion de clé d'API
   * Création, actualisation et échange de jeton
   * Authentification de l'identité du service
   
   
La gestion des accès couvre les aspects suivants :
 * Gestion des règles
   * Création, suppression et mise à jour de règles
 * Décisions concernant l'accès aux ressources
 
## Présentation de l'identité
{: #identity}

Le service de jeton Cloud IAM Token Service est le service d'authentification pour IBM Cloud et repose sur les normes ouvertes spécifiées par [OAuth 2.0]( https://tools.ietf.org/html/rfc6749), [JWT](https://tools.ietf.org/html/rfc7519), [JWT Profile](https://tools.ietf.org/html/rfc7523) et [JWKS](https://tools.ietf.org/html/rfc7517).

Un des pôles du service Token Service est l'authentification des développeurs, des opérateurs et des administrateurs de la plateforme IBM Cloud. Pour cette authentification, le service Token Service est connecté au système IBMid afin d'authentifier les utilisateurs et, dans les environnements dédiés et locaux, peut être connecté à un système d'authentification choisi par le client, comme LDAP. 

Pour extraire un jeton IAM, vous pouvez utiliser les types d'octroi OAuth 2.0 standards tels que `password` (mot de passe). Par exemple :
```
curl
    -u "<clientid>:<valeur secrète du client>"
    –H "Content-Type: application/x-www-form-urlencoded"
    –d "grant_type=password&username=<IBMid>&password=<mot de passe IBMid>
       [&ims_account=<compte IMS>][&bss_account=<compte BSS>]
       [&response_type=cloud_iam,uaa,ims_portal]"
    "https://iam.ng.bluemix.net/oidc/token[?pretty=true]"
```
{: codeblock}

En extension d'OAuth 2.0, vous devez soumettre des informations de compte pour rendre le jeton spécifique au compte. Vous pouvez également répertorier différents types de réponse pour obtenir des jetons `UAA` ou `IMS` pour interactions avec les API CloudFoundry ou IMS.

Le service Cloud IAM Token Service vous permet de créer, de mettre à jour, de supprimer et d'utiliser des clés d'API pour les utilisateurs. Ces clés d'API peuvent être créées via des appels d'API ou la console Bluemix. Pour exploiter une clé d'API, un utilisateur peut utiliser le type d'octroi étendu suivant :
```
curl
    -u "<clientid>:<valeur secrète du client>"
    –H "Content-Type: application/x-www-form-urlencoded"
    –d "grant_type=urn:ibm:params:oauth:grant-type:apikey&
       apikey=<valeur clé d'API>[&response_type=cloud_iam,uaa,ims_portal]"
    "https://iam.ng.bluemix.net/oidc/token[?pretty=true]"
```
{: codeblock}

Le jeton résultant peut être utilisé de la même manière qu'un jeton extrait via un octroi de mot de passe ou une connexion à l'interface utilisateur.

Autre variation, le service Cloud IAM Token Service vous permet de vous connecter interactivement à l'interface utilisateur. Ceci est implémenté en utilisant le type d'octroi OAuth 2.0 `authorization_code` (code d'autorisation), également dénommé `OAuth Dance`, vu qu'il entraîne de multiples redirections du navigateur Web lors de la phase d'authentification.

L'autre pôle du service Token Service est la possibilité de créer des ID de service et des clés d'API pour les ID de service. Un ID de service est similaire à un "ID fonctionnel" ou un "ID d'application" et il est utilisé pour s'authentifier auprès de services, et non pas pour représenter un utilisateur.

Les utilisateurs peuvent créer des ID de service et les lier à des portées telles qu'un compte Bluemix, une organisation CloudFoundry ou un espace CloudFoundry. Cette liaison est effectuée pour attribuer à l'ID de service un conteneur dans lequel exister. Ce conteneur définit également qui peut mettre à jour et supprimer l'ID de service  et qui peut créer, mettre à jour, lire et supprimer des clés d'API associées à cet ID de service. Un ID de service n'est PAS associé à un utilisateur.

Pour mieux comprendre comment utiliser les ID de service, vous pouvez essayer notre [Application de démonstration](https://iam.ng.bluemix.net/demo), laquelle illustre les API.

## Présentation de la gestion des accès
{: #access_management}

IAM est un système de contrôle d'accès basé attributs (Attribute Based Access Control system - ABAC) incluant des conditions inspirées par la publication [NIST](http://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.sp.800-162.pdf).  

IAM utilise une combinaison d'attributs pour déterminer l'accès aux ressources. Les stratégies IAM comportent des règles qui sont appliquées au rôles, attributs d'utilisateur/d'ID de service, attributs de ressources, et des conditions. Ceci permet une approche souple et puissante pour définir des accès pour des utilisateurs et des ID de service.

Par exemple, dans le cas d'une machine virtuelle, VM123 pourrait avoir les attributs suivants : 
```
    resource: {
      'serviceName': 'virtual-machine',
      'region': 'us-south',
      'resourceType': 'vm',
      'resource': 'vm123'
    }
```
{: codeblock}
  
N'importe quelle combinaison de ces attributs de ressource peut être utilisée pour créer une règle.

Pour des exemples plus détaillés, voir [Exemples de règle IAM](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/policy_examples.html#iam_policy_examples).

ABAC est différent du contrôle d'accès basé rôles (Role Based Access Control - RBAC), dans lequel des rôles prédéfinis sont affectés aux utilisateurs. Ces rôles prédéfinis ont des prérogatives spécifiques et les utilisateurs affectés à ce rôle jouissent de toutes les prérogatives définies par ce rôle. 
 
Par exemple, un rôle `Administrateur` de la machine virtuelle. Ce rôle englobe toutes les prérogatives de type Administrateur sur n'importe quelle ressource de machine virtuelle. 

Représentation plus simple d'ABAC :

1. ABAC combine des utilisateurs, des ressources, des contextes et des actions.
1. Chaque instance d'un Utilisateur, d'une Ressource, d'un Contexte et d'une Action a un identificateur unique.
1. Chaque instance reçoit des attributs.
   Essentiellement, ceci signifie : "Ce qui est avéré pour l'instance du point de vue de l'autorisation".
   Exemples : 
   1. L'utilisateur est du signe Poisson et né dans les années 60.
   1. La ressource est une liste d'une équipe de Baseball.
   1. Le contexte est 9h00 à 17h00 (heure de l'est des Etats-Unis).
   1. L'action est "peut mettre à jour".
1. Des règles sont créées pour déterminer quel jeu d'attributs accorde à l'utilisateur la permission d'effectuer l'action sur la ressource.
1. Lorsqu'un utilisateur demande à effectuer une action sur une ressource, les règles sont consultées pour savoir si cette demande est permise.

L'image ci-après offre une vue détaillée de la séquence d'autorisation.

![Séquence d'autorisation](auth_sequence.png)

## Configuration du contrôle des accès à votre service
{: #setup_access_mgmt}

L'intégration d'un service dans {{site.data.keyword.Bluemix_notm}} implique un ensemble d'opérations différent de son intégration avec Cloud IAM. Du point de vue technique, vous pouvez intégrer indépendamment le service avec {{site.data.keyword.Bluemix_notm}} et Cloud IAM, et dans n'importe quel ordre. L'équipe Cloud IAM collabore avec l'équipe d'intégration de service {{site.data.keyword.Bluemix_notm}} afin que le processus d'intégration de service {{site.data.keyword.Bluemix_notm}} puisse inclure également Cloud IAM.

Pour configurer le contrôle d'accès pour votre service, vous devez inclure les étapes suivantes dans le cadre de votre processus d'intégration :

### Etape 1 : Créez un ID de service via cette requête HTTP :
```
  POST https://iam.ng.bluemix.net/serviceids
  Authorization: <jeton Bluemix>
  Content-Type: application/json

  {
    "name": "<nom ID service>",
    "description": "<description ID service>",
    "boundTo": "<crn>"
  }
```
{: codeblock}

Commande Curl :
```  
curl -X POST -H 'Authorization: <jeton Bluemix>' -H 'Content-Type: application/json' -d '{"name": "<nom ID service>", "description": "<description ID service>", "boundTo": "<crn>"}' 'https://iam.ng.bluemix.net/serviceids'
```
{: codeblock}

La section ci-dessous décrit plus en détail les valeurs `Service id` et `Service crn` utilisées dans la commande `curl` :
  
#### ID service 
  
Le nom de l'ID de service peut être le même que le nom de service qui apparaît dans les crns pour votre service.
  
Votre ID de service doit être lié à un compte, une organisation, ou un espace. Cette liaison détermine qui est habilité à gérer votre ID de service. Par exemple, l'administrateur de l'entité à laquelle est lié votre ID de service peut mettre à jour ou supprimer cet ID. Votre jeton {{site.data.keyword.Bluemix_notm}} doit pouvoir accéder au compte, à l'organisation et à l'espace auquel vous liez l'ID. Pour lier l'ID à un compte, le crn `boundTo` doit être similaire à ceci : 

`crn:v1:::<nom service>::a/<ID compte>:::` 
  
S'il s'agit d'une organisation, il doit être similaire à ceci :
`crn:v1:<cname>:<ctype>:<nom service>:<region>:o/<ID organisation>:::` 
  
S'il s'agit d'un espace, il doit être similaire à ceci :
`crn:v1:<cname>:<ctype>:<nom service>:<région>:s/<ID espace>:::`  
  
La valeur `boundTo` spécifiée n'affecte pas les ressources auxquelles votre ID de service peut accéder.  
  
Les règles d'accès IAM déterminent à quelles ressources votre ID de service peut accéder. Bien que votre ID de service soit lié à une organisation IBM, des règles IAM peuvent être créées pour permettre à votre ID de service un accès à des ressources hors de cette organisation. Lors de l'intégration avec IAM, la première règle d'accès créée par l'équipe IAM permet à l'ID de service de créer des règles pour n'importe quelle ressource dont votre service est propriétaire.

Voir [createServiceid](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/) pour plus d'informations sur cette API et les API connexes.

#### crn du service

La valeur de service-name dans le crn `boundTo` doit correspondre au nom de service qui figure dans le crn pour votre service.
  
Consultez les [spécifications CRN](https://github.ibm.com/ibmcloud/builders-guide/blob/master/specifications/crn/CRN.md) pour savoir comment renseigner ces zones.

Notez dans la réponse les valeurs de metadata->uuid et de metadata->crn, lesquelles indiquent votre ID de service et le crn de l'ID de service.


### Etape 2 : Contactez l'équipe AccessControl sur le site [#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 
Le rôle Administrateur des règles a été attribué à votre ID du service sur les ressources du service.

Utilisez le format suivant :
```
Infos du service d'utilisateur IAM

service id: uuid issu de l'étape 1
service name: nom du service tel qu'il apparaît dans les crns pour votre service
```
{: codeblock}

### Etape 3 : Vous devez créer un clé d'API (api-key) depuis votre ID de service. Utilisez la requête HTTP suivante :
```
  POST https://iam.ng.bluemix.net/apikeys
  Authorization: <jeton Bluemix>
  Content-Type: application/json

  {
    "boundTo": "<crn ID service>",
    "name": "<nom clé API>",
    "description": "<description clé API>"
  }
```
{: codeblock}

Commande Curl : 
```
  curl -X POST -H 'Authorization: <jeton Bluemix>' -H 'Content-Type: application/json' -d '{"boundTo": "<crn ID service>", "name": "<nom clé API>", "description": "<description clé API>"}' https://iam.ng.bluemix.net/apikeys
```
{: codeblock}

`boundTo` doit désigner le crn de votre ID de service (zone metadata->crn notée depuis la réponse à l'étape 1). Le nom et la description sont à votre guise.

Notez la valeur de entity->apiKey dans la réponse.

Voir [createAPIKey](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createAPIKey) pour plus d'informations sur cette API et les API connexes.

### Etape 4 : Obtenez un jeton d'accès pour la clé d'API de vos ID de service. 

Une fois l'autorisation obtenue, votre service peut émettre des demandes PAP et PDP pour les ressources du service.

Utilisez la valeur de la zone de l'entité **apiKey** de l'étape 3, laquelle indique la valeur de votre clé d'API (apikey_value).

  * Obtenez ensuite le jeton à l'aide de la valeur de la clé d'API (prenez soin d'utiliser des caractères d'échappement) :

    Commande Curl :
```
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<apikey_value>" "https://iam.ng.bluemix.net/oidc/token"
```
{: codeblock}

Utilisez la zone **access_token** (jeton d'accès) dans le résultat, laquelle désigne votre jeton api-key (pour votre ID de service). La valeur **access_token** (jeton d'accès) doit être convertie pour suivre le codage URL lorsqu'elle est utilisée dans la commande curl mentionnée ci-dessus.


### Etape 5 : Enregistrez la liste des actions de service possibles pour le nom de service.

  a. Mappez les actions de service à des rôles définis par le système IAM. Ce mappage sera utilisé plus tard lors de l'enregistrement du service.

  * Vous pouvez examiner la liste des rôles définis par le système IAM via la commande suivante :
  
Commande Curl :
```
curl -X GET --header 'Accept: application/json' --header 'Authorization: <jeton clé API>' 'https://iampap.ng.bluemix.net/acms/v1/roles'
```
{: codeblock}

**Remarque :** Utilisez l'élément *crn version* des rôles définis par le système IAM dans le contenu de l'enregistrement de votre service.

Ci-après figure un exemple de mappage d'actions de service à des rôles.

  <table>
    <tr>
      <th>Noeud final d'API</th>
      <th>Action de service</th>
      <th>Rôles définis par le système IAM</th>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}</td>
      <td>key-protect.keys.create</td>
      <td>Administrateur</td>
    </tr>
    <tr>
      <td>GET /api/keys/{key_id}</td>
      <td>key-protect.keys.read</td>
      <td>Visualiseur, Editeur, Administrateur</td>
    </tr>
    <tr>
      <td>PUT /api/keys/{key_id}</td>
      <td>key-protect.keys.update</td>
      <td>Editeur, Administrateur</td>
    </tr>
    <tr>
      <td>DELETE /api/keys/{key_id}</td>
      <td>key-protect.keys.delete</td>
      <td>Administrateur</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/encode</td>
      <td>key-protect.keys.encode</td>
      <td>Editeur, Administrateur</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/decode</td>
      <td>key-protect.keys.decode</td>
      <td>Editeur, Administrateur</td>
    </tr>
  </table>

  b. Utilisez la commande suivante pour enregistrer votre service dans `PAP` :
```
  curl -X PUT -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'Authorization: <jeton clé API>' -d '{
    "displayName": {
      "default": <nom d'affichage du service>
    },
    "actions": [{
      "id": <service_action>,
      "displayName": {
        "default": <nom d'affichage de l'action du service>
      },
      "roles": [<crn_rôle_défini_par_le_système>]
    }]
  }' 'https://iampap.ng.bluemix.net/acms/v1/services/<nom_service>'
  ```
{: codeblock}
  
Les actions doivent être spécifiées tel que spécifié dans le document
[Format d'action de service](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/index.html#action_format).
  
Par exemple, si vous utilisez le format standard :

  `<nom_service>.<composant>.<instruction>`
  
  Utilisation de l'action `key-protect.keys.decode` de l'exemple précédent 
  * service-name = key-protect
  * component = keys
  * verb = decode
  

### Etape 6 : Vérifiez que le service a été enregistré conformément aux informations de l'étape 5.

```
curl -H "Authorization: <jeton clé API>" "https://iampap.ng.bluemix.net/acms/v1/services/<nom_service>"
```

### Etape 7 (Facultatif) : Supprimez le service que vous avez enregistré à l'étape 5.

```
curl -X DELETE -H "Authorization: <jeton clé API>" "https://iampap.ng.bluemix.net/acms/v1/services/<nom_service>"
```

### Etape 8 : Configurez le service afin d'utiliser le SDK PEP pour vérifier les autorisations dans PDP. Sélectionnez la langue de SDK appropriée.

  * [PEP SDK for Java](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Java)
  * [PEP SDK for Nodejs](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Node)
  * [PEP SDK for Python](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Python)
 

## Terminologie
{: #terminology}

### Terminologie d'identité

* IBMid - Identité fournie et hébergée par IBM pour accéder au cloud IBM, aux applications IBM, aux communautés et au support.
* Id utilisateur - identification qui représente une personne réelle.
* ID de service - Identification qui représente un technicien, un utilisateur, une machine, une application ou des services. Similaire à "ID fonctionnels" ou "ID d'application", lesquels représentent également un technicien, mais utilise le type d'entité "ID utilisateur".
* OAuth 2.0 - Norme ouverte autorisant l'accès à des applications et à des API sans soumission de données d'identification au service cible. OAuth est également utilisé pour héberger des informations d'authentification.
* OpenID Connect - Norme ouverte s'adjoignant à OAuth 2.0 et qui se focalise sur la soumission d'informations sur l'utilisateur authentifié.
* ID client - Les applications qui interagissent avec des noeuds finaux conformes à la norme OAuth 2.0 requièrent une paire ID secrète du client / valeur confidentielle pour l'authentification. Une application doit s'enregistrer auprès d'un service Token Service pour obtenir un ID client.
* Noeud final de jeton - Utilisé par le client pour obtenir un ou plusieurs jetons en présentant des informations sur son identité comme un nom d'utilisateur ou un mot de passe, un jeton d'octroi d'autorisation ou un jeton actualisé.
* Noeud final d'autorisation - Utilisé par le client pour authentifier un utilisateur auprès du service de jeton via l'interface utilisateur.
* Jeton - Chaîne opaque ou transparente permettant à une application d'extraire l'authentification et/ou l'autorisation d'une identité.
* Jeton d'accès - Envoyé aux API en tant qu'informations d'identité. Contient des informations d'identité et n'est valide que pour une période brève.
* Actualisation de jeton - Ce jeton est stocké uniquement sur le client ayant demandé une authentification. Utilisé pour se procurer un nouveau jeton d'accès (c.à.d. pour actualiser le jeton d'accès) s'il est arrivé à expiration. Comme le jeton actualisé a une durée de vie étendue, il ne doit pas quitter le système du client, excepté pour s'actualiser à nouveau.
* Cookie d'identité - Lors de la connexion au service IBM Cloud Token Service, un cookie contenant votre identité est émis à votre navigateur. Vous ne serez pas invité à vous reconnecter tant que ce cookie existe et est valide. Il expire au bout de 24 heures, si vous vous déconnectez du service IBM Cloud Token Service ou si vous fermez votre navigateur.
* Jeton Web JSON - Objet conforme à la norme JSON (RFC 7519) et représentant des jetons d'accès. Le contenu du jeton d'accès est transparent, (c.à.d. qu'il peut être lu sans difficulté). Un jeton JWT est généralement signé pour pouvoir vérifier son origine.
* Clé publique - Peut être utilisée pour valider la signature d'un jeton Web JSON. Si vous utilisez un chiffrement asymétrique, la clé publique peut être utilisée en toute sécurité pour sa consommation par des clients.
* Clé privée - Peut être utilisée pour créer une signature d'un jeton Web JSON. Cette clé doit être gardée secrète, faute de quoi des jetons d'accès valides pourraient être créés par d'autres utilisateurs.
* realmid - Identificateur permettant de distinguer des utilisateurs issus de registres utilisateurs différents. Les valeurs utilisées actuellement sont "IBMid" pour les utilisateurs authentifiés par le système IBMid et "iam" pour les ID de service authentifiés par Token Service.
* identificateur - Identificateur qui ne change jamais et qui identifie de manière unique un utilisateur dans un registre d'utilisateurs (dénoté par le paramètre `realmid`). La combinaison <realmid>-<identificateur> doit toujours déboucher sur un utilisateur identifiable de manière unique. Dans le cas d'IBMid, l'identificateur IBM unique 'IUI' est utilisée.             
* sujet - Nom de l'utilisateur de l'identité. Ressemble souvent à une adresse électronique. Dans le cas d'IBMid, il s'agit de l'IBMid de l'identité.
* réclamations personnalisées - Informations non standard supplémentaires dans un jeton Web JSON.

### Terminologie de gestion des accès

* (PAP) Policy Administration Point - Point qui gère les règles d'autorisation d'accès.
* (PDP) Policy Decision Point - Point qui évalue les demandes par rapport aux règles d'autorisation avant de prononcer des décisions d'accès.
* (PEP) Policy Enforcement Point - Point qui intercepte une demande d'accès d'un utilisateur à une ressource et soumet une demande de décision au PDP pour obtenir la décision d'accès (à savoir, approbation ou rejet de l'accès à la ressource), et agit compte tenu de la décision reçue.
* (PIP) Policy Information Point - Entité système qui sert de source des valeurs d'attribut (c.à.d. une ressource, un sujet et un environnement).
* (PRP) Policy Retrieval Point - Point où les règles d'autorisation XACML sont stockées. Généralement une base de données ou le système de fichiers.
* Sujet - L'élément "qui" dans une paire ressource et sujet (par exemple, un utilisateur ou un groupe). La ressource désigne celle à laquelle le sujet peut accéder.
* rôle - Assortiment d'autorisations pouvant être affectées à un utilisateur, un groupe d'utilisateurs, un système, un service, ou une application pour lui permettre d'effectuer certaines tâches.
* ressource - Objet physique ou logique (par exemple, une organisation, un espace, une base de données ou une table) sur lequel des actions peuvent être effectuées.
* conditions - Fonction qui renvoie la valeur "True", "False" ou “Indeterminate” (Vrai, faux ou indéterminé).
* actions - Tâche définie qu'effectue une application sur un objet ou une ressource suite à un événement.
* stratégie - Ensemble de règles, identificateur de l'algorithme de combinaison de règles et (facultatif) d'un ensemble d'obligations ou de recommandations. Peut être un composant d'un ensemble de stratégies.

## Rôles définis par le système
{: #system_defined_roles}

Les rôles IBM Cloud désignent un assortiment d'actions, lesquelles sont fournies par des services activés pour IAM.

Le regroupement d'actions sous forme de rôles fournit la souplesse requise pour la prise en charge d'actions pour n'importe quel service ou ressource via un jeu minimal de rôles définis par le système. Par exemple, si vous avez besoin d'un `Administrateur` pour les machines virtuelles, le stockage et l'opération en réseau, vous pouvez utiliser le rôle
`Administrateur` pour tous les trois, mais en changeant juste la cible de la règle. `Administrateur` de machines virtuelles, `Administrateur` du stockage
et `Administrateur` réseau.

*Non couvert par IBM Cloud IAM* : Alternative utilisée par d'autres systèmes de gestion des accès pour intégrer des ressources dans le rôle. Cette approche entraîne par inadvertance un nouveau nom de rôle pour chaque
type de ressource introduit dans le système. Par exemple, sous cette approche, vous auriez besoin d'un rôle
`VMAdministrator`, d'un rôle
`StorageAdministrator` et d'un rôle `NetworkAdministrator` pour couvrir
l'administration des ressources de machines virtuelles, de stockage et réseau.


Le tableau suivant présente les rôles définis par le système IAM et des exemples d'actions qui leur sont mappées.

|Nom de rôle IBM Cloud| Description | Exemples d'actions|
|:-----------------|:-----------------|:-----------------|
|Visualiseur|Actions qui ne modifient pas l'état (c.à.d. en lecture seule)| <ul><li>recensement des unités</li><li>lecture d'objet de stockage</li><li>exécution de requête</li><li>exécution de recherche</li></ul>|
|Editeur|Actions pouvant modifier l'état et créer/supprimer des sous-ressources|<ul><li>création d'une machine virtuelle</li><li>suppression d'une machine virtuelle</li><li>rattachement d'un stockage</li><li>réamorçage</li><li>démarrage/arrêt</li><li>attribution d'un nouveau nom</li></ul>|
|Opérateur|Actions requises pour configurer et opérer des ressources|<ul><li>mise à jour de la configuration</li><li>arrêt/démarrage de machine virtuelle</li><li>affichage de journaux</li><li>création de sauvegarde/restauration</li></ul>|
|Administrateur|Toutes les actions, notamment de gestion du contrôle d'accès|<ul><li>invitation d'un utilisateur</li><li>création d'une machine virtuelle</li>mise à jour des stratégies d'accès utilisateur</li><li>recensement des unités</li><li>création d'une machine virtuelle</li><li>suppression d'une machine virtuelle</li><li>rattachement d'un stockage</li><li>réamorçage</li><li>démarrage/arrêt</li><li>attribution d'un nouveau nom</li><li>création de sauvegarde/restauration</li></ul>|
|Administrateur de la facturation|Actions associées à l'administration de la facturation|<ul><li>mise à jour de carte de crédit</li><li>liste des factures</li><li>téléchargement de factures</li></ul>|

La liste actualisée des rôles définis sur le service est disponible sur le micro-service PAP via la commande suivante :

Commande Curl : 

`curl -X GET --header 'Accept: application/json' --header 'Authorization: <jeton clé API>' 'https://iampap.ng.bluemix.net/acms/v1/roles'`
    
    
## Format d'action de service
{: #action_format}

Les actions doivent être définies sous l'un un des deux formats suivants :
  
* Standard :

    `<nom_service>.<composant>.<instruction>`
* Point d'interception de contrôle d'accès : 

    `<METHODE> /<route_API>`
  
### Standard
La plupart des services appellent directement le PDP IAM et peuvent modifier le code source pour prendre en charge le format d'action standard.  
 
 Ce format doit inclure les trois parties et se conformer aux caractères alphanumériques, sans espaces ou caractères spéciaux autres que '-'.

`<nom_service>.<composant>.<instruction>`

Où 
* nom_service - Nom du service tel que défini dans la zone du nom de service CRN.
* composant - ressource ou sous-ressource du service.
* instruction - Instruction qui définit l'action prise en charge pour le composant de nom de service. 
  
Par exemple : `key-protect.keys.decode` 
* service-name = key-protect
* component = keys
* verb = decode

### Point d'interception de contrôle d'accès de l'API REST
{: intercept_point}

Dans certains cas, les demandes à l'API REST sont acheminées via une passerelle qui fait office de point d'interception de contrôle d'accès. Le PDP IAM est appelé directement depuis le point d'interception avant d'appeler le service d'API REST réel. Le service qui traite la demande à l'API REST n'appelle jamais le PDP IAM.

Le point d'interception ne connaît que la route de l'API REST et le noeud final auquel envoyer la demande. Pour plus d'informations, voir [Remarques relatives aux points d'interception du contrôle d'accès](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/intercept_point.html#intercept_point_overview).


 Ce format doit inclure les deux parties et prend en charge les caractères sécurisés pour les URL comme indiqué dans la spécification [RFC 1738](https://www.ietf.org/rfc/rfc1738.txt).
 
 
`<METHODE> /<route_API>`
  
Où
* METHODE - Méthode d'API REST. 
* route_API - URI de l'API REST.

Par exemple : `GET /v1/things/thing123`
* METHOD = GET
* api_url = /v1/things/thing123

<!---
# Setting up access control for your service
{: #setup_access_mgmt}

Onboarding a service to {{site.data.keyword.Bluemix_notm}} is a different set of operations than onboarding a service with Cloud IAM. Technically you can onboard with {{site.data.keyword.Bluemix_notm}} and Cloud IAM independently and in any order. The Cloud IAM team is working with the {{site.data.keyword.Bluemix_notm}} service onboarding team so that the {{site.data.keyword.Bluemix_notm}} service on boarding process will also include Cloud IAM onboarding.

To setup access control for your service you must use the following steps.

#### Step 1: Create a service id by making this http request:
  ```
  POST https://iam.ng.bluemix.net/serviceids
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "name": "<service id name>",
    "description": "<service id description>",
    "boundTo": "<crn>"
  }
  ```
Curl command:
  ```  
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"name": "<service id name>", "description": "<service id description>", "boundTo": "<crn>"}' 'https://iam.ng.bluemix.net/serviceids'
  ```
  
### Service id 
  
The service id name can be the same as the service name that appears in the crns for your service.
  
Your service id must be bound to an account, organization, or space. This binding determines who can manage your service id. For example, the administrator where your service id is bound are able to update or delete. Your {{site.data.keyword.Bluemix_notm}} token needs to have access to the account, organization, and space you are binding the id to. To bind to an account, the `boundTo` crn must look like the following: 

`crn:v1:::<service name>::a/<account id>:::` 
  
For an organization it must look like the following:
`crn:v1:<cname>:<ctype>:<service name>:<region>:o/<organization id>:::` 
  
For a space it must look like the following:
`crn:v1:<cname>:<ctype>:<service name>:<region>:s/<space id>:::`  
  
The `boundTo` value specified has no affect on which resources your service id can access. 
  
IAM access policies control which resources your service id can access. Even though your service id is bound to an IBM organization, IAM policies can be created that allow your service id to access resources outside of that organization.  When on boarding with IAM the first access policy that is created by the IAM team allows the service id to create policies for any resources owned by your service.

See [createServiceid](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createServiceid) for more information on this api and related apis.

###Service crn

The service-name in the `boundTo` crn must match the service name that appears in the crn for your service.
  
See the [CRN spec](https://github.ibm.com/ibmcloud/builders-guide/blob/master/specifications/crn/CRN.md) for help filling in these fields.

From the response, save metadata&ndash>uuid and metadata&ndash>crn, which are your service id and service id crn.


#### Step 2: Contact the AccessControl Squad at [#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 
Your service id will be given the role of Administrator of policies for your service's resources.

Use this format:
```
IAM adopter service info

service id: uuid from step #1
service name: your service name as it will appear in the crns for your service
```

#### Step 3: You must create an api key from your service id. Use the following http request:
```
  POST https://iam.ng.bluemix.net/apikeys
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "boundTo": "<service id crn>",
    "name": "<api key name>",
    "description": "<api key description>"
  }
```
Curl command: 
```
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"boundTo": "<service id crn>", "name": "<api key name>", "description": "<api key description>"}' https://iam.ng.bluemix.net/apikeys
```
`boundTo` needs to be the crn of your service id (field metadata&ndash>crn saved from step 1’s response). The name and description can be anything.

From the response, save entity&ndash>apiKey.

See [createAPIKey](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createAPIKey) for more information on this api and related apis.

#### Step 4: Get an access token for your service id's API key. 

When the permission is established, your service can make PAP and PDP requests for your service's resources.

Use the entity **apiKey** field from step #3, this is your API key value (apikey_value).

  * Then get the token with the API key value (make sure you use escape characters):

    Curl Command: 
    ```
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<apikey_value>" "https://iam.ng.bluemix.net/oidc/token"
    ```

Use the **access_token** field in the result, this is your api key token(for your service id).


#### Step 5: Register the list of possible service actions for the service name.

  a. Map service actions to IAM System Defined Roles. This mapping is used later during the service registration.

  * A list of IAM System Defined Roles can be found by performing the following request:
Curl command:
```
curl -X GET &ndash&ndashheader 'Accept: application/json' &ndash&ndashheader 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'
```

**Note:** Use the _crn version_ of the IAM System Defined Roles in your service registration payload.

The following is an example of mapping service actions to roles.

  <table>
    <tr>
      <th>API Endpoint</th>
      <th>Service Action</th>
      <th>IAM System Defined Roles</th>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}</td>
      <td>key-protect.keys.create</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>GET /api/keys/{key_id}</td>
      <td>key-protect.keys.read</td>
      <td>Viewer, Editor, Administrator</td>
    </tr>
    <tr>
      <td>PUT /api/keys/{key_id}</td>
      <td>key-protect.keys.update</td>
      <td>Editor, Administrator</td>
    </tr>
    <tr>
      <td>DELETE /api/keys/{key_id}</td>
      <td>key-protect.keys.delete</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/encode</td>
      <td>key-protect.keys.encode</td>
      <td>Editor, Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/decode</td>
      <td>key-protect.keys.decode</td>
      <td>Editor, Administrator</td>
    </tr>
  </table>

  b. Use the following command line to register your service with the `PAP`:
```
  curl -X PUT -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'Authorization: <api key token>' -d '{
    "displayName": {
      "default": <service display name>
    },
    "actions": [{
      "id": <service_action>,
      "displayName": {
        "default": <service action display name>
      },
      "roles": [<system_defined_role_crn>]
    }]
  }' 'https://iampap.ng.bluemix.net/acms/v1/services/<service_name>'
  ```
  
Actions must be defined as specified in the 
[Service Action Format](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/index.html#action_format).
  
For example, using the standard format:

  `<service-name>.<component>.<verb>`
  
  Using action `key-protect.keys.decode` from the previous example 
  * service-name = key-protect
  * component = keys
  * verb = decode
  
  [TODO: Also support REST like action format, yet to be approved]: <>

#### Step 6: Configure the service to use the PEP SDK in order to check permissions with the PDP. Pick the corresponding SDK language.

  * [PEP SDK for Java](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Java)
  * [PEP SDK for Nodejs](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Node)
  * [PEP SDK for Python](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Python)


<!---
# Identity and Access Management Adopter Guidelines
{: #iam_guidelines}

Onboarding a service to {{site.data.keyword.Bluemix_notm}} is a different set of operations than onboarding a service with Cloud IAM. Technically you can onboard with {{site.data.keyword.Bluemix_notm}} and Cloud IAM independently and in any order. The Cloud IAM team is working with the {{site.data.keyword.Bluemix_notm}} service onboarding team so that the {{site.data.keyword.Bluemix_notm}} service on boarding process will also include Cloud IAM onboarding. Until that work is complete please use the following onboarding steps.

- Users are identified with their IBMid.
  - Users authenticate with their IBMid and password.
  - Authentication returns a UAA/OAuth token which is used to access services within the IBM Cloud.
  
- Services are identified by their ServiceIDs.
  - Services authenticate with their ServiceID and APIkey.
  - Authentication returns an OAuth token which is used to access other services within the IBM Cloud.
  
- Services grant access to their resources by creating *Access Policies*.
  - *Roles* can be viewed and *Access Policies* can be managed through the 
  *Policy Administration Point (PAP)*.
  - Actions are permitted or denied through the *Policy Enforcement Point (PEP)* and *Policy Decision Point (PDP)*. 
  

## Creating a ServiceID
{: #create_serviceid}

To create a ServiceID you must use one of the following steps:

Make a one-time request for your ServiceID/APIkey.

 * Create a ServiceID with [swagger](https://iam.ng.bluemix.net/docs).
```
POST /serviceids
```
 * Create a ServiceID using `curl`.
```
curl -X POST -H "Authorization: $CF_TOKEN" -H 'Content-Type: application/json' -d '{"name": "IAMdemo", "description": "IAM demo of adopting service", "boundTo": "crn:v1:staging:public:docker-registry:us-south:o/57666a74-e136-4eb0-a085-220345fac266:::"}' 'https://iam.ng.bluemix.net/serviceids’
```
**Note**
The `boundTo` is the {{site.data.keyword.Bluemix_notm}} Org that is owned by you or your admin.

## Creating a ServiceID metadata response
{: #create_serviceid_metadata}

The following is a ServiceID metadata response using `curl`. Your service ID is expressed with a UUID and CRN format.

```
{"metadata":{\
"uuid":"ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07",\
"crn":"crn:v1:staging:public:iam:us-south:o/57666a74-e136-4eb0-a085-220345fac266::\
serviceid:ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07",\
"version":"1-4d9b1b10ce893f750a2d7e0d6ee34fd7"},"entity":{"boundTo":"crn:v1:staging:public:docker-registry:\
us-south:o/57666a74-e136-4eb0-a085-220345fac266:::","name":"IAMdemo","descripti\
on":"IAM demo of adopting service"}}
```

## Creating an APIkey for your ServiceID
{: #create_apikey_serviceid}

Create an APIkey
```
POST /apikeys
```

The following is a `curl` example of creating an APIkey
```
curl -X POST -H 'Authorization: $CF_TOKEN' -H 'Content-Type: application/json' -d '{"boundTo": "crn:v1:staging:public:iam:us-south:o/57666a74-e136-4eb0-a085-220345fac266::serviceid:ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07", "name": "IAMdemo", "description": "IAM deom of adopting service"}' https://iam.ng.bluemix.net/apikeys
```

## Authenticating with an APIkey
{: #auth_apikey}

The following is a `curl` example of authenticating with an APIkey
```
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H \
"Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-ty\
pe%3Aapikey&apikey=DuE2s….bfRKc=" "https://iam.s\tage1.ng.bluemix.net/oidc/token”
{"access_token":"eyJraWQiOiIyMDE2MTAyNC0wMDowMDowMCIsImFsZyI6IlJTMjU2In0.eyJpZG\
VudGlmaWVyIjoiU2VydmljZUlkLTNlYzBkZDAyLTdhMTAtNDBiZi05MmU3LWI5YTMyOTU0N2MwNyIsI\
nN1YiI6IlNlcnZpY2VJZC0zZWMwZGQwMi03YTEwLTQwYmYtOTJlNy1iOWEzMjk1NDdjMDciLCJzdWJf\
dHlwZSI6IlNlcnZpY2VJZCIsImFjY291bnQiOnsiYnNzIjoiMDY0Zjg3NTZlMzZlODk5MDAyYjliM2M\
wNzZiZTM3OGIifSwibWZhIjp7fSwiaWF0IjoxNDc5Mzk3MTYwLCJleHAiOjE0Nzk0MDA3NjAsImlzcy\
I6Imh0dHBzOi8vaWFtLnN0YWdlMS5uZy5ibHVlbWl4Lm5ldC9vaWRjL3Rva2VuIiwiZ3JhbnRfdHlwZ\
SI6InVybjppYm06cGFyYW1zOm9hdXRoOmdyYW50LXR5cGU6YXBpa2V5Iiwic2NvcGUiOiJvcGVuaWQi\
LCJjbGllbnRfaWQiOiJkZWZhdWx0In0.APRVqQmfUwn6K4Kg2sicT_kGpqSGQXr4Vua8Q5p4B0_dfGE\
tbbe10JqHeE4ovud6u8xjclAIcqCcbjIH4RijnUNGReVse49gS6JlXxmiNGA8OVlNGjiL68ygIpYsj-\
crx8kVuTrXAFqx9lhLEBhAzDneldu-gjSz7wrQKqISikcMXPXQkmLDuoT-OGNq8rG4fCiENBiweUrGf\
_Yw9W5NSiWyQGdWmczS70Krc_hx1iXskmt8pz5_0_vPXY6_tG5rY6KPw-bHO1wux91Q7aTZwCmaL0zI\
F2d3cIuFe1XywJ_926MfwWy65MxC3xv7-_rsZMFoprrLtBsuEnshNWUDhg",
"token_type":"Bearer","expires_in":3600,"expiration":1479400760}
```

## Registering your ServiceID with IAM
{: #register_serviceid}

To complete the on boarding process, contact the AccessControl Squad at
[#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 

Your service id will be given the role of Administrator of policies for your 
service's resources.

Call the `PAP` and `GET` the existing policies
```
curl -X GET -H 'Authorization:<APIkeyToken>' \
'https://iampap.ng.bluemix.net/acms/v1/scopes/global/service_ids/\
ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07/policies'

Response:
{"policies":[]}  <-- no policies yet
```

## Creating access policies
{: #creating_policies}

Now that you are fully on boarded, you can begin creating access policies 
for resources owned by your service.
-->

# ID de service et clés d'API Lab

interconnect-service1 :
  * ServiceId-2bc4561c-615f-4ba3-ab50-eba3b70a69d3
  * 7DRDYlbFM8Mpt7cOKS7clQisOItOfFcvItkd4MQsd20M

interconnect-service2 :
  * ServiceId-089f58e9-f0a0-4b47-b3db-a2d9036080aa
  * rOB0ZqGR1pbiWxNMbn_OfFDmuJcULhqnYW_G0hNnJj0w

interconnect-service3:
  * ServiceId-9a57c3ed-2a8d-45ff-8b34-a7feb80e81bd
  * 6qZoPsd_V47hQQHHVFR1Z8PeGwTZKmNxHgGlURH7OIPf

interconnect-service4 :
  * ServiceId-df633c5f-dee3-4e7b-87c3-7a3ed57d6509
  * 3yICAhsR55nlXJLjPA2nLBcAM1SX7LrXpOabjivVeteQ

interconnect-service5 :
  * ServiceId-e3703b76-4f91-4323-9b6d-db3122952a72
  * 1ZD8qf_jqHC7JVOzrrvbuI3Dcr153hkGsr4Ll7EvsXKW

interconnect-service6 :
  * ServiceId-2a31b14e-6cad-4597-82cf-04f2cb16c26d
  * XFROeDFVyBnJfecSjNhZngPDOniX-5qXl9QWZrsuNjYY

interconnect-service7 :
  * ServiceId-56b98026-bb1c-4166-8128-c4841d10373c
  * cBponeC40MEgPy4mW55kb26XbMFAVmF0y2T3T1fYXJuL

interconnect-service8 :
  * ServiceId-7a9cf953-044e-474a-9ffb-e66a1b68f437
  * OEGprDQNk7TLxFNrCbKfvLGxQRrbGS-PvhKSCUYJYn1a

interconnect-service9 :
  * ServiceId-147203b6-0156-41c6-a28c-7306f047eebb
  * 2OiRisDKDXYA0_0BtlA7OyBk-7II9NUa709HgbF-D_kY

interconnect-service10 :
  * ServiceId-87909073-acb8-403c-ab32-91d632e6c5a6
  * 93eWV_Ns2UrjNGENaaau1yOQmGDvTO2FxEivThGIZUOV

interconnect-service11 :
  * ServiceId-0e2ec208-926e-4db7-aab4-c0d3bf44865f
  * gEa6bECSMAVF68cS5AbckIKp47_OX3_q63JNWI6-Q5Y0

interconnect-service12 :
  * ServiceId-c793ae24-5f43-4c55-815a-830b8c79d1ee
  * WRSnr-FJZ_mI2DbG-8MNqPdAZHq3IkVZU-WbWL7l7uNC

interconnect-service13 :
  * ServiceId-b426e816-6975-47df-ac69-01c08560ef3e
  * MkFJJ_zJDg5MiIRUo78dzCC-Mmw3r9DSzZVMvHZ7A63Z

interconnect-service14 :
  * ServiceId-d97a9df4-6dbe-43ab-8b10-a70bb3ff9085
  * N63GX1wfo6UDc5kNrEWYHcPT27bD9V0JLmoB-iKsPfEb

interconnect-service15 :
  * ServiceId-c6090a5b-569d-40cc-84f5-12480a9ede60
  * xLuJdPmW5npQMuHs4hyJOWZMaYY7i_DwZOSjWlZjnjjK

interconnect-service16 :
  * ServiceId-c1d34878-cac3-43a3-bad6-a5b4992d9ed9
  * UZjSMGF8Aw42lzbHtkgDH14FyJxe0s0aN0O4Qk9uBe8T

interconnect-service17 :
  * ServiceId-9ccaba36-6b07-4e9b-8b97-fbe1111f4908
  * CJb3qUI3cQWUiMMSt2RuL3ti9yE-F2-i2-1yIfowOM30

interconnect-service18 :
  * ServiceId-84a01c41-8330-49e3-842f-b45eaa368d3d
  * 8-qw4_k5Sbjd1sxAiKksHubfPIlkjK2C9S0DnK-WpPDo

interconnect-service19 :
  * ServiceId-2ef5d7ea-7ce0-453d-aa70-fbc5f4b781ef
  * Cz4QHZR_qd_WUZsScF-dVcu31J08dPuF_gszMd4oCLJj

interconnect-service20 :
  * ServiceId-9e85525e-fe29-45e1-81b5-0681cd0b7f22
  * -OeamgjtKqnGUmdKFAVOWjKhYJMYP8HstCcPrRKfy4V9

interconnect-service21 :
  * ServiceId-62c49423-3205-446e-a4aa-e24deb9b158e
  * N2XQ6MpKTvRJX_2IuDQoOiMK5AIhICUFj2wMVyg8O6Pn

interconnect-service22 :
  * ServiceId-2de4c08b-f2cc-4e93-bb8b-eebf2222f93e
  * lEOzJvJJV0EgDjQQa8g5kr_D-PawYqIN-QE1QTNpoD5S

interconnect-service23 :
  * ServiceId-49e6dc57-70f2-4a69-aac9-311394454475
  * G7epLqdbohZ8tVs8Jcx4qSjlMzlzrw2piNEnPiP4RZ7A

interconnect-service24 :
  * ServiceId-7a4ac3ec-bd69-4dbf-8439-f8f5a2ffb88a
  * I7d2KnqbyeQG1rk1AcKeVXgNT1iqCwhSAhan9g-pWucx

interconnect-service25 :
  * ServiceId-542a018b-9248-4bb3-bfc1-e0c9d1e70b46
  * WUl0OMnGkLP1BF3bdkqOJeT3niuwD2p1kWd8In05jpho

interconnect-service26 :
  * ServiceId-c94f5b5e-0d43-4843-8153-d402fae7e1b5
  * dBtmioisFz_7gTYBPL1IArA_E9F4HYnYYAKVZJfxIcv3

interconnect-service27 :
  * ServiceId-37986f6b-325c-42c3-8973-c88c7d365c0c
  * SY1kOsSpSPSLOocmBMwuPWO7u-60aglBliO2Qa4tu4dv

interconnect-service28 :
  * ServiceId-08a48402-a02c-4fe6-9260-635188202aad
  * QFaQPoJaYAcVsVlmnVIlkO1haVY_xg8ZZEt-AkmAzAIn

interconnect-service29 :
  * ServiceId-e9414ce2-c8d5-44d6-be68-f6c5176f4482
  * FKiafH2hr8eooB0nS6N-3vDrYkIbltzBZb688U8JxpvD

interconnect-service30 :
  * ServiceId-e5caa06b-4087-4f55-b51c-bbbad4d78d84
  * 2hcjXXt2G7hmyqAhWlqhXHL9OwFlNdr2_3NZ3tVkBMF2

interconnect-service31 :
  * ServiceId-e71b84e8-fe53-4e40-af46-af26f9e59db3
  * 0vwL6DjNl8ATJJ_mvHrEfuzYt9dyeZulA1nKj_q3zUjf

interconnect-service32 :
  * ServiceId-fc200643-5788-4af9-a1a5-847d373331b3
  * gM919kowr90lDhuRNbvc-kt3WOKW0YQLRGYNqLVbwC-B

interconnect-service33 :
  * ServiceId-df0898a2-8b19-49fc-a88b-f4868c6d2b18
  * KjDoJ5z2WGv2hIG9PRJuylkh0SPLnvAYLY7mVRkmCGGf

interconnect-service34 :
  * ServiceId-1eaa9835-fb15-49a6-b19c-74970795a33f
  * wUXkKrKqJmZO8S4io1QoryPlZml9_G6A4L-6WHftl7Ny

interconnect-service35 :
  * ServiceId-14f7e5fc-5be8-49b5-9843-4b338cc0c34e
  * Fi7nwbNHJVU7CXAba-MJR2jiCSG524zQVb5CIFWwAM1D

interconnect-service36 :
  * ServiceId-fdfe7ec7-1ec7-4798-bb1d-1815b0d31b57
  * wEj7KGnheNnadxzLTOjOe1TlSqgOB75pEzEV5tz6xxl9

interconnect-service37 :
  * ServiceId-4488b45e-992f-4479-8cc1-c7160dafb067
  * weXbJ6CkIgcY0K6Aly3yNmjVb6a7cFWhlphaiD27XMdY

interconnect-service38 :
  * ServiceId-5830536e-b38e-47a4-9b2b-d3c996a545dd
  * ElMOFJEGKh6qbq1CLoImqK8gvSP0KQLyxmPlY8bZecbw

interconnect-service39 :
  * ServiceId-a03d5d46-d064-41c3-b330-35dfc149333b
  * qR0PIg9jT-cPWbj8ShWmha42qXP5Qijoin8l0TfxBH8w

interconnect-service40 :
  * ServiceId-8b7e2cdc-b1c6-4707-8554-7c42c7ff1276
  * VZofAdNllinmi7jQMfQlmvbbJcbpAguunzKKeanweF8c

interconnect-service41 :
  * ServiceId-cda9707c-8fee-497d-a514-e593b4e01002
  * Eoj46Od3qp381LaEc5nhYj-CIGZmrJKt4Gc9oRfB1naD

interconnect-service42 :
  * ServiceId-c743b5f8-5ba6-464e-86ed-83e8dd3ee1b5
  * nespdN1a1I_TQ7pwgBD2gCgtjWpHJrUigUk_69GJTCDC

interconnect-service43 :
  * ServiceId-40513e4d-53e6-4dde-8baf-f3a5c82ba234
  * lYCUBuwNSyW9DNOXcBXfof4znnrZihALfdbTRvytni48

interconnect-service44 :
  * ServiceId-afee12ac-c58a-433c-be98-416acbb670e2
  * 2SBqJdVgwwuBBV8k3eDg6_4NVeDBaLynQgImqct4DfFv

interconnect-service45 :
  * ServiceId-65a3733a-eb0a-402b-ae91-5a412dc9725f
  * to5dKzNvpNLearwdg0KeJc-zftazx-xlu0yt1uk1Q0VP

interconnect-service46 :
  * ServiceId-10413fbe-10aa-4bb5-b641-65a9bbeb9d53
  * kKyrLaYCqbhNxH-Axcv7ABcX0aGdPw-MR2nYjkVORVhY

interconnect-service47 :
  * ServiceId-82ead5c9-195a-4780-bbec-b3655a475896
  * -uTIzbpCJSIn45vYZP86YtrKzpgwyQZThibltlL2rRgu

interconnect-service48 :
  * ServiceId-c06741b5-0ec8-4131-8b2b-276a4f72c0a1
  * 6FpfmxrQpdD00X4_m8Jhk-r4Bwg4x47BZRnLfA-qVe67

interconnect-service49 :
  * ServiceId-ee93887b-11d1-49b9-be63-2764a42beb57
  * 46ZqlkPk_n3QjTbweHa3X4HLQc4N-_O0ODYSfDHu_vui

interconnect-service50 :
  * ServiceId-71dd52eb-7bbc-4ff0-aaf3-70816830660e
  * vDhkWd9DzUf7V_5cWaMhmz8IPmyshCJlZcu_tf39EyNm


