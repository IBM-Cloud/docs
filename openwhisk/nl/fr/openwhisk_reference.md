---

 

copyright:

  2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock:.codeblock}
{:screen:.screen}
{:pre: .pre}

# Détails du système {{site.data.keyword.openwhisk_short}}
{: #openwhisk_reference}
*Dernière mise à jour : 14 avril 2016*

Les sections ci-après fournissent davantage de détails sur le système {{site.data.keyword.openwhisk}}.
{: shortdesc}

## Entités {{site.data.keyword.openwhisk_short}}
{: #openwhisk_entities}

### Espaces de nom et packages

Les actions, les déclencheurs et les règles {{site.data.keyword.openwhisk_short}} appartiennent à un espace de nom, et éventuellement, à un
package.

Un package peut contenir des actions et des flux. Il ne peut pas contenir un autre package ; par conséquent, l'imbrication de package n'est pas
autorisée. De plus, les entités ne doivent pas obligatoirement se trouver dans un package.

Dans Bluemix, une paire organisation+espace correspond à un espace de nom {{site.data.keyword.openwhisk_short}}. Par exemple, l'organisation
`BobsOrg` et l'espace `dev` correspondraient à l'espace de nom {{site.data.keyword.openwhisk_short}} `/BobsOrg_dev`.

Vous pouvez créer vos propres espaces de nom si vous y êtes autorisé. L'espace de nom `/whisk.system` est réservé aux entités qui
sont distribuées avec le système {{site.data.keyword.openwhisk_short}}.


### Noms qualifiés complets

Le nom qualifié complet d'une entité est `/nom_espace_nom[/nom_package]/nom_entité`. Notez que `/` est utilisé pour
délimiter les espaces de nom, les packages et les entités. De plus, les espaces de nom doivent être préfixé avec `/`.

Pour des raisons pratiques, l'espace de nom peut être omis s'il s'agit de *l'espace de nom par défaut* de l'utilisateur.

Par exemple, imaginez un utilisateur dont l'espace de nom par défaut est `/monOrg`. Voici des exemples de nom qualifié complet pour
plusieurs entités et leurs alias.

| Nom qualifié complet | Alias | Espace de nom | Package | Nom |
| --- | --- | --- | --- | --- |
| `/whisk.system/cloudant/read` | - | `/whisk.system` | `cloudant` | `read` |
| `/monOrg/video/transcode` | `video/transcode` | `/monOrg` | `video` | `transcode` |
| `/monOrg/filter` | `filter` | `/monOrg` | - | `filter` |

Vous utiliserez ce schéma de dénomination dans l'interface de ligne de commande {{site.data.keyword.openwhisk_short}}, entre autres.

### Noms d'entité

Les noms de toutes les entités, notamment les actions, les déclencheurs, les règles, les packages et les espaces de nom sont une séquence de
caractères au format suivant :

* Le premier caractère doit être un caractère alphanumérique, un chiffre ou un trait de soulignement.
* Les caractères qui suivent doivent être des caractères alphanumériques, des chiffres, des espaces ou l'un des caractères suivants
: `_`, `@`,
`.`, `-`.
* Le dernier caractère ne peut pas être un espace.

Plus précisément, un nom doit correspondre à l'expression régulière suivante (exprimée avec la syntaxe des métacaractères Java) :
`\A([\w]|[\w][\w@ .-]*[\w@.-]+)\z`.


## Sémantique d'action
{: #openwhisk_semantics}

Les sections ci-après présentent les actions {{site.data.keyword.openwhisk_short}} en détail.

### Caractéristique "sans état"

Les implémentations d'action doivent être sans état, ou *idempotent*. Si le système n'applique pas cette propriété, il n'est pas
garanti qu'un état conservé par une action sera disponible pour tous les appels.

De plus, plusieurs instanciations d'une action peuvent exister, chacune possédant son propre état. Un appel d'action peut être envoyé dans n'importe
laquelle de ces instanciations.

### Entrée et sortie d'appel

L'entrée et la sortie d'une action sont un dictionnaire de paires clé-valeur. La clé est une chaîne et la valeur est une valeur JSON valide.

### Ordre des appels d'action
{: #openwhisk_ordering}

Les appels d'une action ne sont pas ordonnés. Si l'utilisateur appelle une action deux fois depuis la ligne de commande ou l'API REST, il est
possible que le deuxième appel soit exécuté avant le premier. Si les actions ont des effets secondaires, ceux-ci peuvent être observés dans n'importe
quel ordre.

De plus, l'exécution des actions de manière atomique n'est pas garantie. Deux actions peuvent s'exécuter simultanément et leurs effets secondaires
peuvent s'imbriquer. Les
effets secondaires liés à la simultanéité dépendent de l'implémentation.

### Sémantique "un au plus"
{: #openwhisk_atmostonce}

Le système prend en charge un appel d'actions au plus.

Lorsqu'une demande d'appel est reçue, le système enregistre la demande et attribue l'activation.

Le système renvoie un ID d'activation (dans le cas d'un appel non bloquant) pour confirmer que l'appel a été reçu. Sachez que même en l'absence de cette réponse (qui peut être due à une connexion réseau rompue), il est possible que l'appel ait été reçu.

Le système tente d'appeler l'action une fois, ce qui génère l'un des quatre résultats suivants :
- *success* : l'appel de l'action a abouti.
- *application error* : l'appel de l'action a abouti, mais l'action a renvoyé une valeur d'erreur car une précondition relative aux
arguments n'a pas été satisfaite par exemple.
- *action developer error* : l'action a été appelée mais s'est terminée anormalement ; par exemple, l'action n'a pas intercepté
d'exception ou il existe une erreur de syntaxe.
- *whisk internal error* : le système n'est pas parvenu à appeler l'action.
Le résultat est enregistré dans la zone
`status` de l'enregistrement d'activation, tel que documenté dans une section ultérieure.

Chaque appel reçu et pour lequel l'utilisateur peut être facturé possède un enregistrement d'activation.


## Enregistrement d'activation
{: #openwhisk_ref_activation}

Chaque appel d'action et chaque exécution de déclencheur génère un enregistrement d'activation.

Un enregistrement d'activation contient les zones suivantes :

- *activationId* : l'ID d'activation.
- *start* et *end* : les horodatages enregistrant le début et la fin de l'activation. Les valeurs sont au
[format de temps UNIX](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap04.html#tag_04_15).
- *namespace* et `name` : espace de nom et nom de l'entité.
- *logs* : tableau de chaînes indiquant les journaux générés par l'action au cours de son activation. Chaque élément de tableau
correspond à une ligne générée dans stdout ou stderr par l'action et inclut l'horodatage et le flux de la sortie journal. La structure est la suivante : ```HORODATAGE FLUX : SORTIE_JOURNAL```.
- *response* : dictionnaire définissant les clés `success`, `status` et `result` :
  - *status* : résultat de l'activation, qui peut être "success",
"application error", "action developer
error", "whisk internal error".
  - *success* : `true` si et seulement si le statut est `"success"`.
- *result* : dictionnaire contenant le résultat de l'activation. Si l'activation a abouti, il s'agit de la valeur renvoyée par l'action. Si
l'activation a échoué, `result` contient la clé `error`, généralement accompagnée d'une explication de l'échec.


## Actions JavaScript
{: #openwhisk_ref_javascript}

### Prototype de fonction

Les actions {{site.data.keyword.openwhisk_short}} JavaScript s'exécutent dans un contexte d'exécution Node.js, actuellement la version 0.12.9.

Les actions écrites en JavaScript doivent se trouver dans un seul fichier. Ce dernier peut contenir plusieurs fonctions mais par convention, une
fonction appelée `main` doit exister ; c'est celle qui est appelée lorsque l'action est appelée. Voici un exemple d'action avec plusieurs
fonctions :

```
function main() {
    return { payload: helper() }
}

function helper() {
    return new Date();
}
```
{: codeblock}

Les paramètres d'entrée de l'action sont transmis sous forme d'objet JSON en tant que paramètre à la fonction
`main`. Le résultat d'une activation réussie est également un objet JSON ; toutefois, il est renvoyé différemment selon que l'action est
synchrone ou asynchrone, comme décrit dans la section suivante.


### Comportement synchrone et asynchrone

Il est fréquent que l'exécution des fonctions JavaScript continue dans une fonction de rappel même après leur retour. En conséquence, l'activation
d'une action JavaScript peut être *synchrone* ou *asynchrone*.

L'activation d'une action JavaScript est **synchrone** si la fonction main se termine dans l'une des conditions suivantes :

- La fonction main se termine sans exécuter d'instruction ```return```.
- La fonction main se termine en exécutant une instruction ```return``` qui renvoie n'importe quelle valeur *sauf* ```whisk.async()``.

Voici deux exemples d'action synchrone.

```
// action synchrone
function main() {
  return {payload: 'Hello, World!'};
}
```
{: codeblock}

```
// action dans laquelle chaque chemin génère une fonction d'activation synchrone main(params) {
  if (params.payload == 0) {
     return;
  } else if (params.payload == 1) {
     return whisk.done();    // indique une fin normale
  } else if (params.payload == 2) {
    return whisk.error();   // indique une fin anormale
}
}
```
{: codeblock}

L'activation d'une action JavaScript est **asynchrone** si la fonction main se termine en appelant ```return
whisk.async();```.  Dans ce cas, le système suppose que l'action est toujours en cours d'exécution jusqu'à ce qu'elle exécute l'une des instructions
suivantes :
- ```return whisk.done();```
- ```return whisk.error();```

Voici un exemple d'action qui s'exécute de façon asynchrone.

```
function main() {
    setTimeout(function() {
        return whisk.done({done: true});
    }, 100);
    return whisk.async();
}
```
{: codeblock}

Une action peut être synchrone pour certaines entrées et asynchrone pour d'autres. Exemple :

```
  function main(params) {
      if (params.payload) {
         setTimeout(function() {
            return whisk.done({done: true});
         }, 100);
         return whisk.async();  // activation asynchrone
      }  else {
         return whisk.done();   // activation synchrone
      }
  }
```
{: codeblock}

- Dans ce cas, la fonction `main` doit renvoyer `whisk.async()`. Lorsque le résultat de l'activation est
disponible, la fonction `whisk.done()` doit être appelée avec le résultat transmis sous forme d'objet JSON. Il s'agit d'une activation
*asynchrone*.

Que l'activation soit synchrone ou asynchrone, l'appel de l'action peut être bloquant ou non bloquant.

### Méthodes de logiciel SDK supplémentaires

La fonction `whisk.invoke()` appelle une autre action. Elle admet comme argument un dictionnaire définissant les paramètres suivants :

- *name* : nom qualifié complet de l'action à appeler.
- *parameters* : objet JSON représentant l'entrée de l'action appelée. S'il est omis, la valeur par défaut est un objet vide.
- *apiKey* : clé d'autorisation avec laquelle appeler l'action. La valeur par défaut est `whisk.getAuthKey()`. 
- *blocking* : indique si l'action doit être appelée en mode bloquant ou non bloquant. La valeur par défaut est
`false` et signifie que l'appel est non bloquant.
- *next* : fonction de rappel facultative à exécuter lorsque l'appel est terminé.

La signature pour `next` est `function(error, activation)`, où :

- `error` est `false` si l'appel a abouti. La valeur est de type true s'il a échoué ; il s'agit
généralement d'une chaîne décrivant l'erreur.
- En cas d'erreur, il se peut que `activation` ne soit pas défini, selon le mode d'échec.
- S'il est défini, le paramètre `activation` est un dictionnaire contenant les zones suivantes :
  - *activationId* : l'ID d'activation :
  - *result* : si l'action a été appelée en mode bloquant, résultat de l'action en tant qu'objet JSON, ou bien `undefined`.

La fonction `whisk.trigger()` exécute un déclencheur. Elle admet comme argument un objet JSON avec les paramètres suivants :

- *name* : nom qualifié complet du déclencheur à appeler.
- *parameters* : objet JSON représentant l'entrée du déclencheur. S'il est omis, la valeur par défaut est un objet vide.
- *apiKey* : clé d'autorisation avec laquelle exécuter le déclencheur. La valeur par défaut est `whisk.getAuthKey()`.
- *next* : rappel facultatif à exécuter lorsque le déclenchement est terminé.

La signature pour `next` est `function(error, activation)`, où :

- `error` est `false` si le déclenchement a abouti. La valeur est de type true s'il a échoué ; il s'agit généralement d'une chaîne décrivant l'erreur.
- En cas d'erreur, il se peut que `activation` ne soit pas défini, selon le mode d'échec.
- S'il est défini, le paramètre `activation` est un dictionnaire comportant une zone `activationId` qui contient l'ID d'activation.

La fonction `whisk.getAuthKey()` renvoie la clé d'autorisation avec laquelle l'action s'exécute. En général, il n'est pas nécessaire de l'appeler directement car elle est utilisée implicitement par les fonctions `whisk.invoke()` et `whisk.trigger()`.

### Environnement d'exécution
{: #openwhisk_ref_runtime_environment}

Les actions JavaScript sont exécutées dans un environnement Node.js version 0.12.9 avec les packages suivants, qui peuvent être utilisés par l'action :

- apn
- async
- body-parser
- btoa
- cloudant
- commander
- consul
- cookie-parser
- cradle
- errorhandler
- express
- express-session
- jade
- log4js
- fusionner/fusion
- moment
- mustache
- nano
- node-uuid
- oauth2-server
- process
- demande
- rimraf
- semver
- serve-favicon
- socket.io
- superagent
- swagger-tools
- tmp
- watson-developer-cloud
- when
- xml2js
- xmlhttprequest
- yauzl


## Actions Docker
{: #openwhisk_ref_docker}

Les actions Docker exécutent un fichier binaire fourni par l'utilisateur dans un conteneur Docker. Le fichier binaire s'exécute dans une image Docker reposant sur Ubuntu 14.04 LTD ; par conséquent, il doit être compatible avec cette distribution.

Le paramètre "payload" de l'entrée d'action est transmis en tant qu'argument de position au programme binaire et la sortie standard de l'exécution du programme est renvoyée dans le paramètre "result".

Le squelette Docker est pratique pour générer des images Docker compatibles avec {{site.data.keyword.openwhisk_short}}. Vous pouvez l'installer avec la commande d'interface de ligne de commande `wsk sdk install docker`.

Le programme binaire principal doit être copié dans le fichier `dockerSkeleton/client/clientApp`. La bibliothèque ou les fichiers associés peuvent se trouver dans le répertoire `dockerSkeleton/client`.

Vous pouvez aussi inclure des étapes de compilation ou des dépendances en modifiant le fichier `dockerSkeleton/Dockerfile`. Par exemple, vous pouvez installer Python si votre action est un script Python.


## Limites du système
{: #openwhisk_syslimits}

{{site.data.keyword.openwhisk_short}} présente quelques limites relatives au système, notamment la quantité de mémoire qu'une action utilise et le nombre d'appels d'action autorisés par heure. Le tableau ci-dessous répertorie les limites par défaut.

| limite | description | configurable | unité | défaut |
| ----- | ----------- | ------------ | -----| ------- |
| timeout | un conteneur ne peut pas s'exécuter plus de N millisecondes | par action |  millisecondes | 60000 |
| memory | un conteneur ne peut pas allouer plus de N Mo de mémoire | par action | Mo | 256 |
| concurrent | il n'est pas possible d'avoir plus de N activations simultanées par espace de nom | par espace de nom | nombre | 100 |
| minuteRate | un utilisateur ne peut pas appeler plus de tant d'actions par minute | par utilisateur | nombre | 120 |
| hourRate | un utilisateur ne peut pas appeler plus de tant d'actions par heure | par utilisateur | nombre | 3600 |

### Délai d'exécution par action (ms) (valeur par défaut : 60 s)
* La limite de délai d'exécution N est comprise dans la plage [100ms..300000ms] et est définie par action en millisecondes.
* Un utilisateur peut changer la limite lorsqu'il crée l'action.
* Un conteneur dont l'exécution dure plus longtemps que N millisecondes est arrêté.

### Mémoire par action (Mo) (valeur par défaut : 256 Mo)
* La limite de mémoire M est comprise dans la plage [128MB..512MB] et est définie par action en Mo.
* Un utilisateur peut changer la limite lorsqu'il crée l'action.
* La quantité de mémoire allouée dans un conteneur ne peut pas être supérieure à la limite.

### Nombre d'appels simultanés par espace de nom (nombre) (valeur par défaut 100)
* Le nombre d'activations qui sont traitées simultanément pour un espace de nom ne peut pas être supérieur à 100.
* La limite par défaut peut être configurée statiquement par whisk dans consul kvstore.
* Un utilisateur ne peut pas changer les limites.


### Appels par minute/heure (nombre) Fixe : 120/3600)
* La limite de débit N est 120/3600 et limite le nombre d'appels d'action dans des fenêtres d'une minute/heure.
* Un utilisateur ne peut pas changer cette limite lorsqu'il crée l'action.
* Un appel d'interface de ligne de commande dépassant cette limite reçoit un code d'erreur correspondant à TOO_MANY_REQUESTS.
