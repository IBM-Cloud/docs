---

copyright:
  years: 2017
lastupdated: "2017-05-04"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilisation des API REST OpenWhisk 
{: #openwhisk_rest_api}

Une fois votre environnement OpenWhisk activé, vous pouvez utiliser OpenWhisk avec vos applications Web ou mobiles à l'aide d'appels d'API REST. 

Pour plus de détails sur les API pour les actions, les activations, les packages, les règles et les déclencheurs, voir la [documentation de l'API OpenWhisk](http://petstore.swagger.io/?url=https://raw.githubusercontent.com/openwhisk/openwhisk/master/core/controller/src/main/resources/apiv1swagger.json).


Toutes les fonctions du système sont disponibles via une API REST. Des noeuds finaux de collection et d'entité sont présents pour les actions, les déclencheurs, les packages, les activations, et les espaces de nom.

Les noeuds finaux de collection sont les suivants :
- `https://{HOTEAPI}/api/v1/namespaces`
- `https://{HOTEAPI}/api/v1/namespaces/{espaceNom}/actions`
- `https://{HOTEAPI}/api/v1/namespaces/{espaceNom}/triggers`
- `https://{HOTEAPI}/api/v1/namespaces/{espaceNom}/rules`
- `https://{HOTEAPI}/api/v1/namespaces/{espaceNom}/packages`
- `https://{HOTEAPI}/api/v1/namespaces/{espaceNom}/activations`

`{HOTEAPI}` est le nom d'hôte de l'API OpenWhisk (par exemple openwhisk.ng.bluemix.net, 172.17.0.1, 192.168.99.100, 192.168.33.13, etc.).
Pour `{espaceNom}/`, vous pouvez utiliser le caractère `_` afin de spécifier l'*espace de nom par défaut*
de l'utilisateur.


Vous pouvez lancer une requête GET sur les noeuds finaux de collection pour extraire une liste d'entités dans la collection.

Des noeuds finaux d'entité sont présents pour chaque type d'entité :
- `https://{HOTEAPI}/api/v1/namespaces/{espaceNom}/`
- `https://{HOTEAPI}/api/v1/namespaces/{espaceNom}/actions/[{nomPackage}/]{nomAction}`
- `https://{HOTEAPI}/api/v1/namespaces/{espaceNom}/triggers/{nomDéclencheur}`
- `https://{HOTEAPI}/api/v1/namespaces/{espaceNom}/rules/{nomRègle}`
- `https://{HOTEAPI}/api/v1/namespaces/{espaceNom}/packages/{nomPackage}`
- `https://{HOTEAPI}/api/v1/namespaces/{espaceNom}/activations/{nomActivation}`

Les noeuds finaux d'espace de nom et d'activation ne prennent en charge que les requêtes GET. Les noeuds finaux d'actions, de déclencheurs, de règles et
de packages prennent en charge les requêtes GET, PUT et DELETE. Les noeuds finaux d'actions, de déclencheurs et de règles prennent également en charge les
requêtes POST, lesquelles sont utilisées pour appeler des actions et des déclencheurs et pour activer ou désactiver des règles. 

Toutes les API sont protégées via une authentification HTTP de base.
Vous pouvez utiliser l'outil [wskadmin](../tools/admin/wskadmin) pour générer un nouvel espace de nom et une nouvelle authentification.
Les données d'identification pour l'authentification de base figurent dans la propriété
`AUTH` de votre fichier `~/.wskprops` et sont délimitées par un signe deux-points.
Vous pouvez également extraire ces données d'identification via l'interface de ligne de commande en exécutant `wsk property get --auth`.


Voici un exemple qui utilise l'outil de commande [cURL](https://curl.haxx.se) pour extraire la liste de tous les packages dans l'espace de nom `whisk.system` :

```bash
curl -u NOMUTILISATEUR:MOTDEPASSE https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/packages
```
{: pre}

```json
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
    "version": "0.0.1",
    "namespace": "whisk.system"
  }
]
```

Dans cet exemple, l'authentification est transmise avec l'indicateur `-u` ; vous pouvez également transmettre cette valeur dans l'adresse URL sous la forme `https://$AUTH@{HOTEAPI}`. 

L'API OpenWhisk prend en charge les appels demande-réponse de clients Web. OpenWhisk répond aux demandes `OPTIONS` avec des en-têtes CORS (Cross-Origin Resource Sharing). Actuellement, toutes les origines sont autorisées (la valeur de Access-Control-Allow-Origin est "`*`") et les en-têtes Access-Control-Allow-Header fournissent l'autorisation et le type de contenu.

**Attention :** étant donné qu'OpenWhisk ne prend en charge qu'une seule clé par espace de nom, il n'est pas recommandé d'utiliser CORS (Cross-Origin Response Sharing) au-delà de simples expérimentations. Utilisez les [actions Web](webactions.md) ou la [passerelle d'API](apigateway.md) pour exposer vos actions au public et ne pas utiliser la clé d'autorisation OpenWhisk pour les applications client requérant CORS. 

## Utilisation du mode prolixe de l'interface de ligne de commande 
{: #openwhisk_rest_api_cli_v}
L'interface de ligne de commande OpenWhisk assure l'interface avec l'API REST d'OpenWhisk.
Vous pouvez l'exécuter en mode prolixe avec l'indicateur `-v` pour afficher toutes les informations sur la demande HTTP et la réponse. 

Essayons d'obtenir la valeur d'espace de nom pour l'utilisateur en cours. 
```
wsk namespace list -v
```
{: pre}
```
REQUEST:
[GET]	https://openwhisk.ng.bluemix.net/api/v1/namespaces
Req Headers
{
  "Authorization": [
    "Basic XXXYYYY"
  ]
}
RESPONSE:Got response with code 200
Resp Headers
{
  "Content-Type": [
    "application/json; charset=UTF-8"
  ]
}
Response body size is 28 bytes
Response body received:
["john@example.com_dev"]
```

Comme vous pouvez le constater, les informations affichées indiquent les propriétés de la demande HTTP ; la méthode HTTP `GET` est exécutée sur l'adresse URL `https://openwhisk.ng.bluemix.net/api/v1/namespaces` avec un en-tête d'autorisation de base `Basic XXXYYYY`.
Notez que la valeur d'autorisation est votre chaîne d'autorisation OpenWhisk codée en base64.
Le type de contenu de la réponse est `application/json`.

## Actions
{: #openwhisk_rest_api_actions}
Pour créer ou mettre à jour une action, envoyez une demande HTTP avec la méthode `PUT` à la collection d'actions. Par exemple, pour créer une action `nodejs:6` avec le nom `hello` en utilisant un contenu de fichier unique, entrez la commande suivante : 
```bash
curl -u $AUTH -d '{"namespace":"_","name":"hello","exec":{"kind":"nodejs:6","code":"function main(params) { return {payload:\"Hello \"+params.name}}"}}' -X PUT -H "Content-Type: application/json" https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?overwrite=true 
```
{: pre}

Pour procéder à un appel bloquant sur une action, envoyez une demande HTTP avec la méthode `POST` et un corps contenant le paramètre d'entrée `name` en entrant la commande suivante : 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?blocking=true \
-X POST -H "Content-Type: application/json" \
-d '{"name":"John"}'  
```
{: pre}
Vous obtenez la réponse suivante :
```json
    {
  "duration": 2,
  "name": "hello",
  "subject": "john@example.com_dev",
  "activationId": "c7bb1339cb4f40e3a6ccead6c99f804e",
  "publish": false,
  "annotations": [{
    "key": "limits",
    "value": {
      "timeout": 60000,
      "memory": 256,
      "logs": 10
    }
  }, {
    "key": "path",
    "value": "john@example.com_dev/hello"
  }],
  "version": "0.0.1",
  "response": {
    "result": {
      "payload": "Hello John"
    },
    "success": true,
    "status": "success"
  },
  "end": 1493327653769,
  "logs": [],
  "start": 1493327653767,
  "namespace": "john@example.com_dev"
}
```
Si vous voulez obtenir la partie `response.result` seulement, réexécutez la commande avec le paramètre de requête `result=true` :
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?blocking=true&result=true" \
-X POST -H "Content-Type: application/json" \
-d '{"name":"John"}' 
```
{: pre}
Vous obtenez la réponse suivante :
```json
    {
  "payload": "hello John"
}
```

## Annotations et actions Web 
{: #openwhisk_rest_api_webactions}
Pour créer une action en tant qu'action Web, vous devez ajouter une [annotation](annotations.md) de `web-export=true` pour les actions Web. Etant donné que les actions Web sont accessibles publiquement, il est conseillé de protéger les paramètres prédéfinis (c'est-à-dire de les traiter en tant que paramètres finaux) à l'aide de l'annotation `final=true`. Si vous créez ou mettez à jour une action à l'aide de l'indicateur d'interface de ligne de commande `--web true`, cette commande ajoute les annotations `web-export=true` et `final=true`.

Exécutez la commande curl en fournissant la liste complète des annotations à définir pour l'action :
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"hello","exec":{"kind":"nodejs:6","code":"function main(params) { return {payload:\"Hello \"+params.name}}"},"annotations":[{"key":"web-export","value":true},{"key":"raw-http","value":false},{"key":"final","value":true}]}'
```
{: pre}
A présent, vous pouvez appeler cette action sous forme d'adresse URL publique sans autorisation OpenWhisk. Essayez de l'appeler avec l'adresse URL publique de l'action Web en incluant une extension facultative telle que `.json` ou `.http`, par exemple à la fin de l'adresse URL.
```bash
curl https://openwhisk.ng.bluemix.net/api/v1/web/john@example.com_dev/default/hello.json?name=John
```
{: pre}
```json
    {
  "payload": "Hello John"
}
```
Notez que cet exemple de code source ne fonctionne pas avec `.http`. Voir la documentation relative aux [actions Web](webactions.md) pour savoir comment le modifier.

## Séquences
{: #openwhisk_rest_api_sequences}
Si vous créez une séquence d'actions, fournissez les noms des actions devant composer la séquence dans l'ordre souhaité, de sorte que le résultat de la première action soit transmis en tant qu'entrée à l'action suivante. 

$ wsk action create sequenceAction --sequence /whisk.system/utils/split,/whisk.system/utils/sort

Créez une séquence avec les actions `/whisk.system/utils/split` et `/whisk.system/utils/sort`.
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/sequenceAction?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"sequenceAction","exec":{"kind":"sequence","components":["/whisk.system/utils/split","/whisk.system/utils/sort"]},"annotations":[{"key":"web-export","value":true},{"key":"raw-http","value":false},{"key":"final","value":true}]}' 
```
{: pre}

Sachez que vous devez spécifier des noms d'action qualifiés complets. 

## Déclencheurs
{: #openwhisk_rest_api_triggers}
Pour créer un déclencheur, vous devez au minimum indiquer son nom. Vous pouvez aussi inclure des paramètres par défaut qui seront transmis à l'action via une règle lorsque le déclencheur sera exécuté. 

Créez un déclencheur dont le nom est `events` avec le paramètre par défaut `type` associé à la valeur `webhook`. 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/events?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"events","parameters":[{"key":"type","value":"webhook"}]}' 
```
{: pre}

Désormais, à chaque fois qu'un événement devra exécuter ce déclencheur, il suffira d'émettre une demande HTTP avec la méthode `POST` en utilisant la clé d'autorisation OpenWhisk. 

Pour exécuter le déclencheur `events` avec un paramètre `temperature`, envoyez la demande HTTP suivante :

```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/events \
-X POST -H "Content-Type: application/json" \
-d '{"temperature":60}' 
```
{: pre}

### Déclencheurs avec actions de flux 
{: #openwhisk_rest_api_triggers_feed}
Il existe des déclencheurs spéciaux que vous pouvez créer avec une action de flux. L'action de flux est une action qui contribue à la configuration d'un fournisseur de flux en charge de l'exécution du déclencheur à chaque fois qu'un événement correspond au déclencheur. Lisez la documentation [feeds.md] pour en savoir plus sur ces fournisseurs de flux. 

Certains des déclencheurs disponibles qui optimisent une action de flux sont des déclencheurs périodiques/alarmes, Slack, Github, Cloudant/Couchdb et messageHub/Kafka. Vous pouvez aussi créer votre propre action de flux et votre propre fournisseur de flux. 

Créons un déclencheur dont le nom est `periodic` et qui sera déclenché à la fréquence spécifiée, toutes les 2 heures (c'est-à-dire 02:00:00, 04:00:00, ...).

Dans l'interface de ligne de commande, il suffit d'entrer la commande suivante : 
```bash
wsk trigger create periodic --feed /whisk.system/alarms/alarm \
  --param cron "0 */2 * * *" -v
```
{: pre}
Comme vous le constaterez, étant donné que nous utilisons l'indicateur `-v`, deux demandes HTTP sont envoyées, l'une pour créer un déclencheur appelé `periodic` et l'autre pour appeler l'action de flux `/whisk.system/alarms/alarm` avec les paramètres permettant de configurer le fournisseur de flux de sorte qu'il exécute le déclencheur toutes les 2 heures.

Pour effectuer les mêmes opérations avec l'API REST, créez d'abord le déclencheur : 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/periodic?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"periodic","annotations":[{"key":"feed","value":"/whisk.system/alarms/alarm"}]}'  
```
{: pre}

Comme vous pouvez le constater, l'annotation `feed` est stockée dans le déclencheur. Ultérieurement, nous utiliserons cette annotation pour identifier l'action de flux à utiliser lors de la suppression du déclencheur. 

Maintenant que le déclencheur a été créé, appelons l'action de flux : 
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/actions/alarms/alarm?blocking=true&result=false" \
-X POST -H "Content-Type: application/json" \
-d "{\"authKey\":\"$AUTH\",\"cron\":\"0 */2 * * *\",\"lifecycleEvent\":\"CREATE\",\"nomDéclencheur\":\"/_/periodic\"}" 
```
{: pre}

La suppression du déclencheur est similaire à la création du déclencheur, mais cette fois, vous supprimez le déclencheur et utilisez également l'action de flux pour configurer le fournisseur de flux de sorte qu'il supprime le gestionnaire pour le déclencheur. 

Appelez l'action de flux afin de supprimer le gestionnaire de déclencheur du fournisseur de flux : 
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/actions/alarms/alarm?blocking=true&result=false" \
-X POST -H "Content-Type: application/json" \
-d "{\"authKey\":\"$AUTH\",\"lifecycleEvent\":\"DELETE\",\"nomDéclencheur\":\"/_/periodic\"}"  
```
{: pre}

A présent, supprimez le déclencheur avec une demande HTTP à l'aide de la méthode `DELETE` : 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/periodic \
-X DELETE -H "Content-Type: application/json" 
```
{: pre}

## Règles 
{: #openwhisk_rest_api_rules}
Pour créer une règle qui associe un déclencheur à une action, envoyez une demande HTTP avec la méthode `PUT` en fournissant le déclencheur et l'action dans le corps de la demande. 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/rules/t2a?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"t2a","status":"","trigger":"/_/events","action":"/_/hello"}' 
```
{: pre}

Les règles peuvent être activées ou désactivées. De plus, vous pouvez changer le statut d'une règle en mettant à jour sa propriété de statut. Par exemple, pour désactiver la règle `t2a`, envoyez `status: "inactive"` dans le corps de la demande avec la méthode `POST`.
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/rules/t2a?overwrite=true \
-X POST -H "Content-Type: application/json" \
-d '{"status":"inactive","trigger":null,"action":null}'  
```
{: pre}

## Packages
{: #openwhisk_rest_api_packages}
Pour créer une action dans un package, vous devez d'abord créer un package. Pour créer un package dont le nom est `iot`, envoyez une demande HTTP avec la méthode `PUT`. 

```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/packages/iot?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"iot"}' 
```
{: pre}

## Activations
{: #openwhisk_rest_api_activations}
Pour obtenir la liste des trois dernières activations, envoyez une demande HTTP avec la méthode `GET` en transmettant le paramètre de requête `limit=3`. 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/activations?limit=3
```
{: pre}

Pour obtenir tous les détails d'une activation incluant les résultats et les journaux, envoyez une demande HTTP avec la méthode `GET` en transmettant l'identificateur de l'activation comme paramètre de chemin. 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/activations/f81dfddd7156401a8a6497f2724fec7b
```
{: pre}
