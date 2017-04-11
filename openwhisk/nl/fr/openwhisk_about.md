---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# A propos d'{{site.data.keyword.openwhisk_short}}

{{site.data.keyword.openwhisk}} est une plateforme de traitement gérée par des événements également appelée traitement sans serveur ou Function as a Service (FaaS) qui exécute un code en réponse à des événements ou des appels directs. La figure ci-dessous présente l'architecture générale d'{{site.data.keyword.openwhisk}}.
{: shortdesc}

![Architecture {{site.data.keyword.openwhisk_short}}](./images/OpenWhisk.png)

Par exemple, les événements peuvent être des modifications apportées aux enregistrements d'une base de données, des relevés de capteur IoT dépassant une certaine température, de nouvelles validations de code dans un référentiel GitHub ou des demandes HTTP simples provenant d'applications Web ou mobiles. Les événements provenant de sources d'événements externes et internes sont canalisés via un déclencheur, et des règles permettent de réagir à ces événements par le biais d'actions.

Les actions peuvent être de petits fragments de code JavaScript ou Swift ou un code binaire personnalisé imbriqué dans un conteneur Docker. Les actions dans {{site.data.keyword.openwhisk_short}} sont instantanément déployées et exécutées à chaque fois qu'un déclencheur est exécuté. Plus le nombre de déclencheurs exécutés est élevé, plus le nombre d'actions appelées est élevé. Si aucun déclencheur n'est exécuté, aucun code d'action n'est exécuté et par conséquent, aucun frais n'est engendré.

En plus d'associer des actions à des déclencheurs, il est possible d'appeler une action directement à l'aide de l'API {{site.data.keyword.openwhisk_short}}, de l'interface de ligne de commande ou du logiciel SDK pour iOS. Des actions peuvent également être assemblées sans qu'il ne soit nécessaire d'écrire un code. Chaque action de la chaîne est appelée séquentiellement ; la sortie d'une action est transmise en tant qu'entrée à l'action suivante dans la séquence.

Avec les machines virtuelles ou les conteneurs à exécution longue classiques, il est courant de déployer plusieurs machines virtuelles ou conteneurs pour assurer la résilience en cas d'indisponibilité d'une instance unique. Toutefois, {{site.data.keyword.openwhisk_short}} propose un modèle alternatif sans coût supplémentaire lié à la résilience. L'exécution des actions à la demande assure une évolutivité inhérente et une utilisation optimale car le nombre d'actions en cours d'exécution correspond toujours à la fréquence de déclenchement. De plus, le développeur se consacre désormais uniquement au code et ne se préoccupe pas de la surveillance, de la mise à jour et de la sécurisation de l'infrastructure de serveur, de stockage, de réseau et de système d'exploitation sous-jacente.

Des intégrations à des services et à des fournisseurs d'événements supplémentaires peuvent être ajoutées à l'aide de packages. Un package est un regroupement de flux et d'actions. Un flux est un élément de code qui configure une source d'événements externe en vue de l'exécution d'événements déclencheurs. Par exemple, un déclencheur créé avec un flux de modifications Cloudant configure un service de sorte qu'il exécute le déclencheur à chaque fois qu'un document est modifié ou ajouté dans une base de données Cloudant. Les actions dans les packages représentent une logique réutilisable qu'un fournisseur de services peut mettre à disposition pour que les développeurs puissent utiliser le service en tant que source d'événements, mais aussi appeler les API de ce service.

Un catalogue de packages existant permet d'améliorer les applications avec des fonctions utiles et d'accéder à des services externes dans l'écosystème rapidement. Cloudant, The Weather Company, Slack et GitHub sont des exemples de service externe compatibles avec {{site.data.keyword.openwhisk_short}}.


## Fonctionnement d'{{site.data.keyword.openwhisk_short}}
{: #openwhisk_how}

En tant que projet open source, OpenWhisk repose sur les épaules de géants, tels que Nginx, Kafka, Consul, Docker, CouchDB. Tous ces composants sont regroupés pour constituer un "service de programmation basé sur des événements sans serveur". Pour passer en revue tous ces composants, suivons un appel d'une action via le système lorsqu'il se produit. Un appel dans OpenWhisk est la principale action exécutée par un moteur sans serveur : exécuter le code que l'utilisateur a injecté dans le système et renvoyer les résultats de cette exécution.

### Création de l'action

Pour donner un peu de contexte à notre explication, créons commençons par créer une action dans le système. Nous utiliserons cette action pour expliquer les concepts ultérieurement lors du suivi dans le système. Pour les commandes suivantes, nous partons du principe que l'[interface de ligne de commande d'OpenWhisk est correctement configurée](https://github.com/openwhisk/openwhisk/tree/master/docs#setting-up-the-openwhisk-cli).

Nous allons d'abord créer un fichier *action.js* contenant le code suivant qui imprimera "Hello World" dans la sortie standard et renverra un objet JSON incluant "world" sous la clé "hello".
```javascript
function main() {
    console.log('Hello World');
    return { hello: 'world' };
}
```
{: codeblock}

Nous créons cette action comme suit :
```
wsk action create myAction action.js
```
{: pre}

L'action est créée. A présent, nous voulons appeler cette action :
```
wsk action invoke myAction
```
{: pre}

## Flux de traitement interne
Que se passe-t-il dans les coulisses d'OpenWhisk ?

![Flux OpenWhisk de traitement](images/OpenWhisk_flow_of_processing.png)

### Entrée dans le système : nginx

L'API utilisateur d'OpenWhisk est entièrement basée sur HTTP et repose sur une conception RESTful. Par conséquent, la commande envoyée via l'interface de ligne de commande wsk correspond essentiellement à une demande HTTP émise sur le système OpenWhisk. La commande spécifique ci-dessus pourrait se traduire par :
```
POST /api/v1/namespaces/$userNamespace/actions/myAction
Host: $openwhiskEndpoint
```
{: screen}

Notez la variable *$userNamespace* ici. Un utilisateur a accès à au moins un espace. Pour plus de simplicité, nous allons supposer que l'utilisateur possède l'espace-noms dans lequel *myAction* est placé.

Le premier point d'entrée dans le système s'effectue via **nginx**, "un serveur proxy inverse et HTTP". Il est principalement utilisé pour la terminaison SSL et l'acheminement d'appels HTTP appropriés vers le composant suivant.

### Entrée dans le système : Contrôleur

N'ayant pas fait grand-chose sur notre demande HTTP, nginx la transmet au **contrôleur**, composant suivant dans notre visite guidée d'OpenWhisk. Il s'agit d'une implémentation Scala de l'API REST réelle (basée sur **Akka** et **Spray**) et qui par conséquent sert d'interface pour toutes les tâches qu'un utilisateur peut réaliser, y compris les demandes [CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete) pour vos entités dans OpenWhisk et l'appel d'actions (opération que nous sommes en train d'effectuer).

Le contrôleur commence par clarifier ce que l'utilisateur essaie de faire. Pour cela, il se base sur la méthode HTTP utilisée dans la demande HTTP. Selon la traduction ci-dessus, l'utilisateur émet une demande POST vers une action existante, que le contrôleur traduit en un **appel d'une action**.

Etant donné le rôle central du contrôleur (d'où son nom), il sera utilisé dans toutes les étapes suivantes :

### Authentification et autorisation : CouchDB

Le contrôleur vérifie qui vous êtes (*Authentification*) et si vous êtes autorisé à faire ce que vous essayez de faire avec cette entité (*Autorisation*). Les données d'identification incluses dans la demande sont vérifiées par rapport à la base de données nommée **subjects** dans une instance **CouchDB**.

En l'occurrence, le contrôleur vérifie que l'utilisateur existe dans la base de données d'OpenWhisk et qu'il est autorisé à appeler l'action myAction ; pour rappel, nous avons pris pour hypothèse que cette action se trouve dans un espace-noms dont le contrôleur est propriétaire. Ce dernier accorde effectivement à l'utilisateur les droits nécessaires pour appeler l'action, opération qu'il souhaite effectuer.

Tout est validé et l'étape de traitement suivante peut commencer.

### Obtention de l'action : CouchDB

Maintenant que le contrôleur est certain que l'utilisateur est authentifié et autorisé à appeler son action, il charge cette action (en l'occurrence, *myAction*) à partir de la base de données **whisks** dans CouchDB.

L'enregistrement de l'action contient principalement le code à exécuter (illustré ci-dessus) et les paramètres par défaut que vous souhaitez transmettre à votre action, fusionnés avec les paramètres que vous avez inclus dans la demande d'appel proprement dite. Il contient également les restrictions de ressource imposées lors de son exécution, telles que la mémoire dans laquelle il peut être consommé.

Dans ce cas particulier, notre action n'utilise aucun paramètre (la définition de paramètre de la fonction est une liste vide), par conséquent, nous partons du principe que nous n'avons défini aucun paramètre par défaut et que nous n'avons envoyé aucun paramètre spécifique à l'action, ce qui rend ce cas le plus simple possible.

### Qui peut appeler l'action : Consul

Le contrôleur (ou plus spécifiquement sa partie d'équilibrage de charge) dispose de tout ce dont il a besoin pour lancer l'exécution de votre code. Toutefois, il a besoin de savoir qui est disponible pour effectuer cette opération. **Consul**, système de reconnaissance de service, est utilisé pour vérifier quels sont les programmes d'exécution disponibles dans le système en surveillant leur état de santé en permanence. On appelle ces programmes d'exécution des **auteurs d'appel**.

Le contrôleur, qui sait désormais quels sont les auteurs d'appel disponibles, choisit l'un d'entre eux pour appeler l'action demandée.

Imaginons que le 3 auteurs d'appel (auteurs d'appel 0 à 2) sont disponibles sur le système et que le contrôleur choisit l'*auteur d'appel 2* pour appeler l'action concernée.

### Kafka

A partir de maintenant, deux problèmes peuvent se produire avec la demande d'appel que vous avez envoyée :

1. Le système tombe en panne, ce qui provoque la perte de votre appel.
2. La charge du système est telle que l'appel doit attendre la fin d'autres appels.

La solution à ces deux problèmes est **Kafka**, un "système de messagerie de publication et d'abonnement distribué à débit élevé". Le contrôleur et l'auteur de l'appel communiquent uniquement via des messages mis en mémoire tampon et conservés par Kafka. Cela augmente la charge de mise en mémoire tampon, entraînant un risque d'erreur *OutOfMemoryException* aussi bien au niveau du contrôleur que de l'auteur de l'appel, tout en garantissant également que les messages ne seront pas perdus si le système tombe en panne.

Pour que l'action soit appelée, le contrôleur publie un message sur Kafka, qui contient l'action à appeler et les paramètres à transmettre à cette action (en l'occurrence, aucun paramètre n'est à transmettre). Ce message est envoyé à l'auteur de l'appel, choisi précédemment par le contrôleur dans la liste fournie par Consul.

Une fois que Kafka a confirmé la bonne réception du message, un **ActivationId** est envoyé en réponse à la demande HTTP émise vers l'utilisateur. Ce dernier se servira de cette information ultérieurement pour accéder aux résultats de cet appel. Notez qu'il s'agit d'un modèle d'appel asynchrone dans lequel la demande HTTP est terminée une fois que le système a accepté la demande d'appel d'une action. Un modèle synchrone (appelé appel de blocage) est disponible, mais il n'est pas abordé dans cet article.

### Appel du code : auteur de l'appel

L'**auteur de l'appel** est le centre nerveux d'OpenWhisk. Sa tâche consiste à appeler une action. Il est également implémenté dans Scala. Mais plus encore, pour exécuter des actions de manière et en toute sécurité, il utilise **Docker**.

Docker est utilisé pour configurer un nouvel environnement auto-encapsulé (appelé *conteneur*) pour chaque action que nous appelons de manière rapide, isolée et contrôlée. En résumé, pour chaque appel d'action, un conteneur Docker est généré, le code d'action est injecté, puis exécuté à l'aide des paramètres qui lui ont été transmis, le résultat est obtenu, le conteneur est détruit. En outre, l'optimisation des performances est renforcée afin de réduire le temps système et offrir des temps de réponse les plus bas possibles. 

Dans le cas qui nous intéresse, comme l'action concernée est basée sur *Node.js*, l'auteur de l'appel démarrera un conteneur Node.js, injectera le code à partir de *myAction*, l'exécutera sans paramètre, procédera à l'extraction du résultat, sauvegardera les journaux et détruira à nouveau le conteneur Node.js.

### Stockage des résultats : CouchDB

Le résultat étant obtenu par l'auteur de l'appel, il est stocké dans la base de données **whisks** en tant qu'activation sous l'élément ActivationId mentionné précédemment. La base de données **whisks** se situe dans **CouchDB**.

Dans le cas qui nous intéresse, l'auteur de l'appel reçoit l'objet JSON résultant de l'action, récupère le journal écrit par Docker, place tous ces éléments dans l'enregistrement d'activation et stocke ce dernier dans la base de données. Cet enregistrement est semblable à ce qui suit :

```json
    {
   "activationId": "31809ddca6f64cfc9de2937ebd44fbb9",
   "response": {
       "statusCode": 0,
       "result": {
           "hello": "world"
       }
   },
   "end": 1474459415621,
   "logs": [
       "2016-09-21T12:03:35.619234386Z stdout: Hello World"
   ],
   "start": 1474459415595,
}
```
{: codeblock}

Notez que l'enregistrement contient à la fois le résultat renvoyé et les journaux qui ont été écrits. Il contient également l'heure de début et de fin de l'appel de l'action. Un enregistrement d'activation contient davantage de zones ; la version représentée ici est épurée dans un souci de simplicité.

A présent vous pouvez réutiliser l'API REST (en reprenant à partir de l'étape 1) pour obtenir votre activation, puis le résultat de votre action. Pour cela, utilisez :

```bash
wsk activation get 31809ddca6f64cfc9de2937ebd44fbb9
```
{: pre} 

### Récapitulatif

Nous avons étudié de quelle façon une simple action **wsk action invoke myAction** transite par différentes étapes du système {{site.data.keyword.openwhisk_short}}. Le système proprement dit n'est constitué que deux composants personnalisés, le **contrôleur** et l'**auteur de l'appel**. Tout le reste est déjà là, développé par toutes ces personnes de la communauté open source.

Vous trouverez des informations supplémentaires sur {{site.data.keyword.openwhisk_short}} dans les rubriques suivantes :

* [Noms d'entité](./openwhisk_reference.html#openwhisk_entities)
* [Sémantique d'action](./openwhisk_reference.html#openwhisk_semantics)
* [Limites](./openwhisk_reference.md#openwhisk_syslimits)
* [API REST](./openwhisk_reference.md#openwhisk_ref_restapi)
