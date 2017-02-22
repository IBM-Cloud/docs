---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock:.codeblock}
{:screen:.screen}
{:pre: .pre}

# Détails du système {{site.data.keyword.openwhisk_short}}
{: #openwhisk_reference}


Les sections ci-après fournissent davantage de détails sur le système {{site.data.keyword.openwhisk}}.
{: shortdesc}

## Entités {{site.data.keyword.openwhisk_short}}
{: #openwhisk_entities}

### Espaces de nom et packages
{: #openwhisk_entities_namespaces}

Les actions, les déclencheurs et les règles {{site.data.keyword.openwhisk_short}} appartiennent à un espace de nom, et éventuellement, à un
package.

Un package peut contenir des actions et des flux. Il ne peut pas contenir un autre package ; par conséquent, l'imbrication de package n'est pas
autorisée. De plus, les entités ne doivent pas obligatoirement se trouver dans un package.

Dans Bluemix, une paire organisation+espace correspond à un espace de nom {{site.data.keyword.openwhisk_short}}. Par exemple, l'organisation
`BobsOrg` et l'espace `dev` correspondraient à l'espace de nom {{site.data.keyword.openwhisk_short}} `/BobsOrg_dev`.

Vous pouvez créer vos propres espaces de nom si vous y êtes autorisé. L'espace de nom `/whisk.system` est réservé aux entités qui
sont distribuées avec le système {{site.data.keyword.openwhisk_short}}.


### Noms qualifiés complets
{: #openwhisk_entities_fullyqual}

Le nom qualifié complet d'une entité est `/nom_espace_nom[/nom_package]/nom_entité`. Notez que `/` est utilisé pour
délimiter les espaces de nom, les packages et les entités. De plus, les espaces de noms doivent être précédés du préfixe `/`.

Pour des raisons pratiques, l'espace de noms peut être omis s'il s'agit de l'*espace de noms par défaut* de l'utilisateur.

Par exemple, imaginez un utilisateur dont l'espace de nom par défaut est `/monOrg`. Voici des exemples de nom qualifié complet pour
plusieurs entités et leurs alias :

| Nom qualifié complet | Alias | Espace de nom | Package | Nom |
| --- | --- | --- | --- | --- |
| `/whisk.system/cloudant/read` |  | `/whisk.system` | `cloudant` | `read` |
| `/monOrg/video/transcode` | `video/transcode` | `/monOrg` | `video` | `transcode` |
| `/monOrg/filter` | `filter` | `/monOrg` |  | `filter` |

Vous utiliserez ce schéma de dénomination dans l'interface de ligne de commande {{site.data.keyword.openwhisk_short}}, entre autres.

### Noms d'entité
{: #openwhisk_entities_names}

Les noms de toutes les entités, notamment les actions, les déclencheurs, les règles, les packages et les espaces de noms sont une séquence de
caractères au format suivant :

* Le premier caractère doit être un caractère alphanumérique ou un trait de soulignement.
* Les caractères qui suivent doivent être des caractères
alphanumériques, des espaces ou l'un des caractères suivants :
`_`, `@`, `.`,
`-`.
* Le dernier caractère ne peut pas être un espace.

Plus précisément, un nom doit correspondre à l'expression régulière suivante (exprimée avec la syntaxe des métacaractères Java) :
`\A([\w]|[\w][\w@ .-]*[\w@.-]+)\z`.


## Sémantique d'action
{: #openwhisk_semantics}

Les sections ci-après présentent les actions {{site.data.keyword.openwhisk_short}} en détail.

### Caractéristique "sans état"
{: #openwhisk_semantics_stateless}

Les implémentations d'action doivent être sans état, ou *idempotent*. Si le système n'applique pas cette propriété, il n'est pas
garanti qu'un état conservé par une action sera disponible pour tous les appels.

De plus, plusieurs instanciations d'une action peuvent exister, chacune possédant son propre état. Un appel d'action peut être envoyé dans n'importe
laquelle de ces instanciations.

### Entrée et sortie d'appel
{: #openwhisk_semantics_invocationio}

L'entrée et la sortie d'une action sont un dictionnaire de paires clé-valeur. La clé est une chaîne et la valeur est une valeur JSON valide.

### Ordre des appels d'action
{: #openwhisk_ordering}

Les appels d'une action ne sont pas ordonnés. Si l'utilisateur appelle une action deux fois depuis la ligne de commande ou l'API REST, il est
possible que le deuxième appel soit exécuté avant le premier. Si les actions ont des effets secondaires, ceux-ci peuvent être observés dans n'importe
quel ordre.

De plus, l'exécution des actions de manière atomique n'est pas garantie. Deux actions peuvent s'exécuter simultanément et leurs effets secondaires
peuvent s'imbriquer. OpenWhisk ne garantit aucun un modèle de cohérence spécifique quant aux effets secondaires. Les
effets secondaires liés à la simultanéité dépendent de l'implémentation.

### Garanties de l'exécution des actions
{: #openwhisk_atmostonce}

Lorsqu'une demande d'appel est reçue, le système enregistre la demande et attribue l'activation.

Le système renvoie un ID d'activation (dans le cas d'un appel non bloquant) pour confirmer que l'appel a été reçu.
Sachez que si une défaillance du réseau, ou toute autre panne, survient avant que vous ne receviez de réponse HTTP, il est tout de même possible
qu'{{site.data.keyword.openwhisk_short}} ait reçu et traité la demande.

Le système tente d'appeler l'action une fois, ce qui génère l'un des quatre résultats suivants :
- *success* : l'appel de l'action a abouti.
- *application error* : l'appel de l'action a abouti, mais l'action a renvoyé une valeur d'erreur car une précondition relative aux
arguments n'a pas été satisfaite par exemple.
- *action developer error* : l'action a été appelée mais s'est terminée anormalement ; par exemple, l'action n'a pas détecté d'exception ou il existe une erreur de syntaxe.
- *whisk internal error* : le système n'est pas parvenu à appeler l'action.
Le résultat est enregistré dans la zone
`status` de l'enregistrement d'activation, tel que documenté dans une section ultérieure.

Chaque appel reçu et pour lequel l'utilisateur peut être facturé possède un enregistrement d'activation.

Notez que dans le cas d'une erreur de type *action developer error*, il se peut que l'action ait été exécutée partiellement et
qu'elle ait
généré des effets secondaires externes visibles.   Il revient à l'utilisateur de vérifier que de tels effets secondaires ont été générés et d'émettre une
logique de relance s'il le souhaite.   Sachez également que certaines erreurs de type *whisk internal error* indiquent que l'exécution d'une
action a commencé mais que le système est tombé en panne avant la fin de l'action enregistrée.

## Enregistrement d'activation
{: #openwhisk_ref_activation}

Chaque appel d'action et chaque exécution de déclencheur génère un enregistrement d'activation.

Un enregistrement d'activation contient les zones suivantes :

- *activationId* : l'ID d'activation.
- *start* et *end* : les horodatages enregistrant le début et la fin de l'activation. Les valeurs sont au
[format de temps UNIX](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap04.html#tag_04_15).
- *namespace* et `name` : espace de nom et nom de l'entité.
- *logs* : tableau de chaînes indiquant les journaux qui sont générés par l'action au cours de son activation. Chaque élément de tableau
correspond à une ligne générée dans `stdout` ou `stderr` par l'action et inclut l'horodatage et le flux de la sortie journal. La
structure est la suivante : `HORODATAGE FLUX : JOURNAL_SORTIE`.
- *response* : dictionnaire qui définit les clés `success`, `status` et `result` :
  - *status* : résultat de l'activation, qui peut être "success",
"application error", "action developer
error", "whisk internal error".
  - *success* : `true` si et seulement si le statut est `"success"`.
- *result* : dictionnaire contenant le résultat de l'activation. Si l'activation a abouti, il s'agit de la valeur qui est renvoyée par l'action. Si
l'activation a échoué, `result` contient la clé `error`, généralement accompagnée d'une explication de l'échec.


## Actions JavaScript
{: #openwhisk_ref_javascript}

### Prototype de fonction
{: #openwhisk_ref_javascript_fnproto}

Les actions {{site.data.keyword.openwhisk_short}} JavaScript
s'exécutent dans un contexte d'exécution Node.js.

Les actions écrites en JavaScript doivent se trouver dans un seul fichier. Ce dernier peut contenir plusieurs fonctions mais par convention, une
fonction appelée `main` doit exister ; c'est celle qui est appelée lorsque l'action est appelée. Voici un exemple d'action avec plusieurs
fonctions :

```
function main() {
    return { payload: helper() }
} function helper() {
    return new Date();
}
```
{: codeblock}

Les paramètres d'entrée de l'action sont transmis sous forme d'objet JSON en tant que paramètre à la fonction
`main`. Le résultat d'une activation réussie est également un objet JSON ; toutefois, il est renvoyé différemment selon que l'action est
synchrone ou asynchrone, comme décrit dans la section suivante.


### Comportement synchrone et asynchrone
{: #openwhisk_ref_javascript_synchasynch}

Il est fréquent que l'exécution des fonctions JavaScript continue dans une fonction de rappel même après leur retour. En conséquence, l'activation
d'une action JavaScript peut être *synchrone* ou *asynchrone*.

L'activation d'une action JavaScript est **synchrone** si la fonction main se termine dans l'une des conditions suivantes :

- La fonction main se termine sans exécuter d'instruction `return`.
- La fonction main se termine en exécutant une instruction `return` qui renvoie n'importe quelle valeur *sauf* une
promesse (objet Promise).

Voici un exemple d'action qui s'exécute de façon synchrone :

```
// action dans laquelle chaque chemin génère une fonction d'activation synchrone main(params) {
  if (params.payload == 0) {
     return;
  } else if (params.payload == 1) {
     return {payload: 'Hello, World!'};
  } else if (params.payload == 2) {
    return {error: 'payload must be 0 or 1'};
  }
}
```
{: codeblock}

L'activation d'une action JavaScript est **asynchrone** si la fonction main se termine en renvoyant une promesse (objet Promise).  Dans ce cas, le système suppose que l'action est toujours en cours d'exécution jusqu'à ce que la promesse (objet Promise) soit satisfaite ou rejetée.
Commencez par instancier une nouvelle promesse (objet Promise) que vous transmettez à une fonction de rappel. La fonction de rappel admet deux arguments, resolve et reject, qui sont tous les deux des fonctions. Tout le code asynchrone est inséré dans ce rappel.


Voici un exemple illustrant la manière de satisfaire une promesse (objet Promise) en appelant la fonction resolve.

```
function main(args) {
     return new Promise(function(resolve, reject) {
       setTimeout(function() {
         resolve({ done: true });
       }, 100);
    })
 }
```
{: codeblock}

Voici un exemple illustrant la manière de rejeter une promesse (objet Promise) en appelant la fonction reject.

```
function main(args) {
     return new Promise(function(resolve, reject) {
       setTimeout(function() {
         reject({ done: true });
       }, 100);
    })
 }
```
{: codeblock}

Une action peut être synchrone pour certaines entrées et asynchrone pour d'autres. En voici un exemple :

```
  function main(params) {
      if (params.payload) {
         // activation asynchrone
         return new Promise(function(resolve, reject) {
                setTimeout(function() {
                  resolve({ done: true });
       }, 100);
    })
      } else {
         // activation synchrone
         return {done: true};
      }
  }
```
{: codeblock}

Remarque : que l'activation soit synchrone ou asynchrone, l'appel de l'action peut être bloquant ou non bloquant.

### Objet global whisk JavaScript déprécié

L'objet global `whisk` est actuellement déprécié ;
vous devez migrer vos actions nodejs pour qu'elles utilisent d'autres
méthodes.
Pour les fonctions `whisk.invoke()` et
`whisk.trigger()`, vous pouvez utiliser la bibliothèque client [openwhisk](https://www.npmjs.com/package/openwhisk).
Pour `whisk.getAuthKey()`, vous pouvez extraire la valeur de
la clé d'API à partir de la variable d'environnement `__OW_API_KEY`.
Pour `whisk.error()`, vous pouvez renvoyer une promesse rejetée (Promise.reject).

### Environnements d'exécution JavaScript
{: #openwhisk_ref_javascript_environments}

Les actions JavaScript sont exécutées par défaut dans un environnement
Node.js version 6.9.1.  L'environnement 6.9.1 est également utilisé pour une
action si l'option `--kind` est explicitement spécifiée avec
la valeur 'nodejs:6' lors de la création/mise à jour de l'action.
Les packages suivants sont disponibles pour être utilisés dans l'environnement
Node.js 6.9.1 :

- apn v2.1.2
- async v2.1.4
- btoa v1.1.2
- cheerio v0.22.0
- cloudant v1.6.2
- commander v2.9.0
- consul v0.27.0
- cookie-parser v1.4.3
- cradle v0.7.1
- errorhandler v1.5.0
- glob v7.1.1
- gm v1.23.0
- lodash v4.17.2
- log4js v0.6.38
- iconv-lite v0.4.15
- marked v0.3.6
- merge v1.2.0
- moment v2.17.0
- mongodb v2.2.11
- mustache v2.3.0
- nano v6.2.0
- node-uuid v1.4.7
- nodemailer v2.6.4
- oauth2-server v2.4.1
- openwhisk v3.0.0
- pkgcloud v1.4.0
- process v0.11.9
- pug v2.0.0-beta6
- redis v2.6.3
- request v2.79.0
- request-promise v4.1.1
- rimraf v2.5.4
- semver v5.3.0
- sendgrid v4.7.1
- serve-favicon v2.3.2
- socket.io v1.6.0
- socket.io-client v1.6.0
- superagent v3.0.0
- swagger-tools v0.10.1
- tmp v0.0.31
- twilio v2.11.1
- underscore v1.8.3
- uuid v3.0.0
- validator v6.1.0
- watson-developer-cloud v2.9.0
- when v3.7.7
- winston v2.3.0
- ws v1.1.1
- xml2js v0.4.17
- xmlhttprequest v1.8.0
- yauzl v2.7.0

L'environnement Node.js version 0.12.17 est utilisé pour une action si
l'option `--kind` est explicitement spécifiée avec la valeur
'nodejs' lors de la création/mise à jour de l'action.
Les packages suivants sont disponibles pour être utilisés dans l'environnement
Node.js 0.12.17 :

**Remarque** : Node.js version 0.12.x est obsolète,
migrez toutes vos actions Node.js de telle sorte qu'elles utilisent Node.js version
6.x.

- apn v1.7.4
- async v1.5.2
- btoa v1.1.2
- cheerio v0.20.0
- cloudant v1.4.1
- commander v2.7.0
- consul v0.18.1
- cookie-parser v1.3.4
- cradle v0.6.7
- errorhandler v1.3.5
- gm v1.20.0
- jade v1.9.2
- log4js v0.6.38
- merge v1.2.0
- moment v2.8.1
- mustache v2.1.3
- nano v5.10.0
- node-uuid v1.4.2
- oauth2-server v2.4.0
- openwhisk v3.0.0
- process v0.11.0
- request v2.79.0
- rimraf v2.5.1
- semver v4.3.6
- serve-favicon v2.2.0
- socket.io v1.3.5
- socket.io-client v1.3.5
- superagent v1.3.0
- swagger-tools v0.8.7
- tmp v0.0.28
- watson-developer-cloud v1.4.1
- when v3.7.3
- ws v1.1.0
- xml2js v0.4.15
- xmlhttprequest v1.7.0
- yauzl v2.3.1

## Actions Python

Les actions Python sont exécutées par défaut avec Python 2.7.12.
En plus de la bibliothèque Python standard, les packages suivants peuvent également être utilisés par les actions Python :

- attrs v16.1.0
- beautifulsoup4 v4.5.1
- cffi v1.7.0
- click v6.6
- cryptography v1.5
- cssselect v0.9.2
- enum34 v1.1.6
- flask v0.11.1
- gevent v1.1.2
- greenlet v0.4.10
- httplib2 v0.9.2
- idna v2.1
- ipaddress v1.0.16
- itsdangerous v0.24
- jinja2 v2.8
- lxml v3.6.4
- markupsafe v0.23
- parsel v1.0.3
- pyasn1 v0.1.9
- pyasn1-modules v0.0.8
- pycparser v2.14
- pydispatcher v2.0.5
- pyopenssl v16.1.0
- python-dateutil v2.5.3
- queuelib v1.4.2
- requests v2.11.1
- scrapy v1.1.2
- service-identity v16.0.0
- simplejson v3.8.2
- six v1.10.0
- twisted v16.4.0
- w3lib v1.15.0
- werkzeug v0.11.10
- zope.interface v4.3.1

## Actions Docker
{: #openwhisk_ref_docker}

Les actions Docker exécutent un fichier binaire fourni par l'utilisateur dans un conteneur Docker. Le fichier binaire s'exécute dans une image Docker
reposant sur [python:2.7.12-alpine](https://hub.docker.com/r/library/python) ; par conséquent, il doit être compatible avec cette
distribution.

Le squelette Docker est pratique pour générer des images Docker compatibles avec OpenWhisk. Vous pouvez l'installer avec la commande d'interface de ligne de commande `wsk sdk install docker`.

Le programme binaire principal doit se trouver dans `/action/exec` à l'intérieur du conteneur. Le fichier exécutable reçoit les
arguments d'entrée via `stdin` et doit renvoyer un résultat via `stdout`.

Vous pouvez inclure des étapes de compilation ou des dépendances en modifiant le document `Dockerfile` inclus dans
`dockerSkeleton`.

## API REST
{: #openwhisk_ref_restapi}

Toutes les fonctions du système sont disponibles via une API REST. Des noeuds finaux de collection et d'entité sont présents pour les
actions, les déclencheurs, les packages, les activations, et les espaces de nom.

Les noeuds finaux de collection sont les suivants :

- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">NomDomaine</span>`/api/v1/namespaces`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">NomDomaine</span>`/api/v1/namespaces/{espace_nom}/actions`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">NomDomaine</span>`/api/v1/namespaces/{espace_nom}/triggers`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">NomDomaine</span>`/api/v1/namespaces/{espace_nom}/rules`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">NomDomaine</span>`/api/v1/namespaces/{espace_nom}/packages`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">NomDomaine</span>`/api/v1/namespaces/{espace_nom}/activations`

`openwhisk.`<span class="keyword" data-hd-keyref="DomainName">NomDomaine</span>` est le nom d'hôte de l'API OpenWhisk (par exemple
openwhisk.ng.bluemix.net, 172.17.0.1, etc.).

Pour `{espace_nom}`, le caractère `_` peut être utilisé afin de spécifier l'*espace de nom par défaut* (adresse électronique) pour l'utilisateur

Vous pouvez lancer une requête GET sur les noeuds finaux de collection pour extraire une liste d'entités dans la collection.

Des noeuds finaux d'entité sont présents pour chaque type d'entité :

- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">NomDomaine</span>`/api/v1/namespaces/{espace_nom}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">NomDomaine</span>`/api/v1/namespaces/{espace_nom}/actions/[{nom_package}/]{nom_action}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">NomDomaine</span>`/api/v1/namespaces/{espace_nom}/triggers/{nom_déclencheur}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">NomDomaine</span>`/api/v1/namespaces/{espace_nom}/rules/{nom_règle}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">NomDomaine</span>`/api/v1/namespaces/{espace_nom}/packages/{nom_package}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">NomDomaine</span>`/api/v1/namespaces/{espace_nom}/activations/{nom_activation}`


Les noeuds finaux d'espace de nom et d'activation ne prennent en charge que les requêtes GET. Les noeuds finaux d'actions, de déclencheurs, de règles et
de packages prennent en charge les requêtes GET, PUT et DELETE. Les noeuds finaux d'actions, de déclencheurs et de règles prennent également en charge les
requêtes POST, lesquelles sont utilisées pour appeler des actions et des déclencheurs et pour activer ou désactiver des règles. Reportez-vous au document
[API
reference](https://new-console.{DomainName}/apidocs/98) pour plus d'informations.

Toutes les API sont protégées via une authentification HTTP Basic. Les données d'identification pour l'authentification de base résident dans la propriété
`AUTH` de votre fichier `~/.wskprops`, et sont délimitées par un signe deux-points. Vous pouvez également extraire ces données
d'identification lors des [étapes de configuration de l'interface de ligne de commande](./index.html#openwhisk_start_configure_cli).

Voici un exemple qui utilise la commande cURL pour extraire la liste de tous les packages dans l'espace de nom `whisk.system` :

```
curl -u NOM_UTILISATEUR:MOT_DE_PASSE https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/packages
```
{: pre}
```
[
  {
    "name": "slack",
    "binding": false,
    "publish": true,
    "annotations": [
      {
        "key": "description",
        "value": "Package contenant des actions pour interaction avec le service de messagerie Slack"
      }
    ],
    "version": "0.0.9",
    "namespace": "whisk.system"
  },
  ...
]
```
{: screen}

L'API OpenWhisk prend en charge les appels demande-réponse de clients Web. OpenWhisk répond aux demandes `OPTIONS` avec des en-têtes CORS (Cross-Origin Resource Sharing). Actuellement, toutes les origines sont autorisées (la valeur de Access-Control-Allow-Origin est "`*`") et les en-têtes Access-Control-Allow-Header fournissent l'autorisation et le type de contenu.

**Attention :** Comme OpenWhisk ne prend en charge qu'une seule clé par compte, il n'est pas recommandé d'utiliser CORS (Cross-Origin Response Sharing) au-delà de simples expérimentations. Votre clé doit être imbriquée dans le code côté client afin d'être visible par le public. A utiliser
avec précaution.

## Limites du système
{: #openwhisk_syslimits}

### Actions
{{site.data.keyword.openwhisk_short}} présente quelques limites
relatives au système, notamment la quantité de mémoire qu'une action
peut utiliser et le nombre d'appels d'action autorisés par minute. 

Le tableau ci-dessous répertorie les limites par défaut pour les actions.

| limite | description | configurable | unité | défaut |
| ----- | ----------- | ------------ | -----| ------- |
| timeout | un conteneur ne peut pas s'exécuter plus de N millisecondes | par action |  millisecondes | 60000 |
| memory | un conteneur ne peut pas allouer plus de N Mo de mémoire | par action | Mo | 256 |
| logs | un conteneur ne peut pas écrire plus de N Mo de données dans la sortie standard | par action | Mo | 10 |
| concurrent | N activation maximum sont autorisées par espace de nom en cours d'exécution ou en file d'attente pour l'exécution | par espace de nom | nombre | 1000 |
| minuteRate | un utilisateur ne peut pas appeler plus de tant d'actions par minute | par utilisateur | nombre | 5000 |
| codeSize | taille maximale du code d'action | non configurable, limite par action | Mo | 48 |
| parameters | taille maximale des paramètres pouvant être associés | non configurable, limite par action/package/déclencheur | Mo | 1 |

### Délai d'exécution par action (ms) (valeur par défaut : 60 s)
{: #openwhisk_syslimits_timeout}
* La limite de délai d'exécution N est comprise dans la plage [100ms..300000ms] et est définie par action en millisecondes.
* Un utilisateur peut changer la limite lorsqu'il crée l'action.
* Un conteneur dont l'exécution dure plus longtemps que N millisecondes est arrêté.

### Mémoire par action (Mo) (valeur par défaut : 256 Mo)
{: #openwhisk_syslimits_memory}
* La limite de mémoire M est comprise dans la plage [128MB..512MB] et est définie par action en Mo.
* Un utilisateur peut changer la limite lorsqu'il crée l'action.
* La quantité de mémoire allouée dans un conteneur ne peut pas être supérieure à la limite.

### Par journal des actions (Mo) (valeur par défaut : 10 Mo)
{: #openwhisk_syslimits_logs}
* La limite de journal N est comprise dans la plage [0 Mo - 10 Mo] et est définie par action.
* Un utilisateur peut changer la limite lorsqu'il crée ou met à jour l'action.
* Les journaux qui dépassent la limite définie sont tronqués et un avertissement est ajouté comme dernière sortie de l'activation pour indiquer que celle-ci a dépassé la limite de journal définie.

### Par artefact d'action (Mo) (fixe : 48 Mo)
{: #openwhisk_syslimits_artifact}
* La taille de code maximale pour l'action est 48 Mo.
* Pour une action JavaScript, il est recommandé d'utiliser un outil permettant de concaténer tout le code source, y compris les dépendances dans un fichier regroupé unique.

### Par taille de contenu d'activation (Mo) (fixe : 1 Mo)
{: #openwhisk_syslimits_activationsize}
* La taille maximale du contenu POST, plus tout paramètre transmis pour un appel d'action ou l'exécution d'un déclencheur est d'1 Mo.

### Nombre d'appels simultanés par espace de nom (valeur par défaut : 1000)
{: #openwhisk_syslimits_concur}
* Le nombre d'activations qui sont exécutées ou mises en file d'attente pour l'exécution pour un espace de nom ne peut pas être supérieur à 1000.
* La limite par défaut peut être configurée statiquement par whisk dans consul kvstore.
* Un utilisateur ne peut pas changer les limites.

### Appels par minute (valeur fixe : 5000)
{: #openwhisk_syslimits_invocations}
* La limite de débit N est 5000 et limite le nombre d'appels d'action dans des fenêtres d'une minute.
* Un utilisateur ne peut pas changer cette limite lorsqu'il crée l'action.
* Un appel d'interface de ligne de commande ou API dépassant cette limite reçoit un code d'erreur correspondant au code de statut HTTP `429:
TOO MANY REQUESTS`.

### Taille des paramètres (fixe : 1 Mo)
{: #openwhisk_syslimits_parameters}
* La taille limite pour les paramètres lors de la création ou de la mise à jour d'une action, d'un package ou d'un déclencheur est 1 Mo.
* Cette limite ne peut pas être modifiée par l'utilisateur.
* Une entité comportant des paramètres dont la taille est trop élevée sera rejetée lorsqu'elle fera l'objet d'une tentative de création ou de mise à jour.

### Valeur ulimit pour le nombre de fichiers ouverts par action Docker (fixe : 64:64)
{: #openwhisk_syslimits_openulimit}
* Le nombre maximal de fichiers ouverts est 64 (pour les limites absolues et les limites souples).
* La commande docker run utilise l'argument `--ulimit nofile=64:64`.
* Pour plus d'informations sur l'utilisation de ulimit pour les fichiers ouverts, voir la documentation [docker run](https://docs.docker.com/engine/reference/commandline/run).

### Valeur ulimit pour le nombre de processus par action Docker (fixe : 512:512)
{: #openwhisk_syslimits_proculimit}
* Le nombre maximal de processus disponibles pour un utilisateur est 512 (pour les limites absolues et les limites souples).
* La commande docker run utilise l'argument `--ulimit nproc=512:512`.
* Pour plus d'informations sur l'utilisation de ulimit pour le nombre maximal de processus, voir la documentation [docker run](https://docs.docker.com/engine/reference/commandline/run).

### Déclencheurs

Les déclencheurs sont soumis à un débit de déclenchements par minute, comme indiqué dans le tableau ci-dessous.

| limite | description | configurable | unité | défaut |
| ----- | ----------- | ------------ | -----| ------- |
| minuteRate | un utilisateur ne peut pas déclencher plus que ce nombre de déclencheurs par minute | par utilisateur | nombre | 5000 |

### Déclencheurs par minute (valeur fixe : 5000)
{: #openwhisk_syslimits_triggerratelimit}
* La limite de débit N est 5000 et limite le nombre de déclencheurs dans des fenêtres d'une minute.
* Un utilisateur ne peut pas changer cette limite lorsqu'il crée le déclencheur.
* Un appel d'interface de ligne de commande ou API dépassant cette limite reçoit un code d'erreur correspondant au code de statut HTTP `429:
TOO MANY REQUESTS`.
