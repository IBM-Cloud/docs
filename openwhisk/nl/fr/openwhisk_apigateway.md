---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-26"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Passerelle d'API
{: #openwhisk_apigateway}

Il est possible de gérer les actions OpenWhisk grâce à la gestion d'API.

La passerelle d'API fait office de proxy pour les [actions Web](webactions.md) et leur fournit des fonctions supplémentaires, telles que le routage de méthode HTTP, les ID/secret client, la limitation de débit, CORS, l'affichage de l'utilisation de l'API et des journaux de réponses et la définition des règles de partage.
Pour plus d'informations sur la fonction de passerelle d'API, voir la documentation de [gestion d'API](/docs/apis/management/manage_openwhisk_apis.html#manage_openwhisk_apis)

## Création d'API à partir d'actions Web OpenWhisk à l'aide de votre navigateur

La passerelle d'API vous permet d'exposer une action OpenWhisk en tant qu'API. Après avoir défini l'API, vous pouvez appliquer les règles de sécurité et de limite de fréquence, afficher l'utilisation de l'API ainsi que les journaux de réponses, et définir les règles de partage.
Dans le tableau de bord OpenWhisk, cliquez sur l'onglet [API](https://console.ng.bluemix.net/openwhisk/apimanagement).


## Création d'API à partir d'actions Web OpenWhisk à l'aide de l'interface de ligne de commande

### Configuration de l'interface de ligne de commande d'OpenWhisk

Configurez l'interface de ligne de commande OpenWhisk avec `wsk property set --apihost openwhisk.ng.bluemix.net`. Pour pouvoir utiliser l'API `wsk api`,  le fichier de configuration d'interface de ligne de commande `~/.wskprops` doit contenir le jeton d'accès Bluemix.
Pour obtenir le jeton d'accès, utilisez la commande d'interface de ligne de commande `wsk bluemix login`. Pour plus d'informations sur la commande, exécutez `wsk bluemix login -h`

**Remarque :** Si les erreurs de commande requièrent l'utilisation d'un code d'accès unique, cela n'est pas pris en charge pour l'instant. Une solution de contournement consiste à vous connecter à l'interface de ligne de commande CloudFoundry à l'aide de `cf login`, puis à copier le jeton d'accès depuis le fichier de configuration du répertoire de base `~/.cf/config.json` dans le fichier `~/.wskprops` avec la propriété `APIGW_ACCESS_TOKEN="value of AccessToken`. Retirez le préfixe `Bearer ` lors de la copie de la chaîne de jeton d'accès. 

**Remarque :** les API que vous avez créées à l'aide de `wsk api-experimental` continueront à fonctionner pendant une durée limitée. Toutefois, vous devriez commencer à les migrer vers les actions Web et à reconfigurer vos API existantes à l'aide de la nouvelle commande d'interface de ligne de commande `wsk api`.

### Création de votre première API à l'aide de l'interface de ligne de commande

1. Créez un fichier JavaScript avec le contenu ci-après. Dans cet exemple, le nom de fichier est 'hello.js'.
  ```javascript
  function main({name:name='Serverless API'}) {
      return {payload: `Hello world ${name}`};
  }
  ```
  {: codeblock}
  
2. Créez une action Web à partir de la fonction JavaScript suivante. Dans cet exemple, l'action s'appelle 'hello'. Prenez soin d'ajouter l'indicateur `--web true`
  
  ```
  wsk action create hello hello.js --web true
  ```
  {: pre}
  ```
  ok: created action hello
  ```
  
3. Créez une API avec le chemin de base `/hello`, le chemin `/world` et la méthode `get` avec le type de réponse `json`
  
  ```
  wsk api create /hello /world get hello --response-type json
  ```
  ```
  ok: created API /hello/world GET for action /_/hello
  https://${APIHOST}:9001/api/21ef035/hello/world
  ```
Une nouvelle URL est générée pour exposer l'action `hello` via une méthode HTTP **GET**.

  
4. Essayez-la en envoyant une demande HTTP vers l'URL.
  
  ```
  $ curl https://${APIHOST}:9001/api/21ef035/hello/world?name=OpenWhisk
  ```
  ```json
    {
  "payload": "Hello world OpenWhisk"
  }
  ```
  L'action Web `hello` a été appelée et a renvoyé un objet JSON incluant le paramètre `name` envoyé un paramètre de requête. Vous pouvez transmettre des paramètres à l'action grâce à de simples paramètres de requête, ou via le corps de demande. Les actions Web vous permettent d'appeler une action de manière publique sans la clé d'API d'autorisation OpenWhisk.
  
### Contrôle complet sur la réponse HTTP
  
  L'indicateur `--response-type` contrôle l'URL cible de l'action Web qui sera envoyée par proxy par la passerelle d'API. L'utilisation de `--response-type json` comme indiqué ci-dessus renvoie le résultat complet de l'action au format JSON et affecte automatiquement `application/json` à l'en-tête Content-Type, ce qui vous permet de commencer facilement.  
  
  Une fois que vous avez commencé, vous souhaitez contrôler entièrement les propriétés de réponses HTTP, telles que `statusCode` et `headers`, et renvoyer différents types de contenu dans `body`. Pour ce faire, utilisez `--response-type http` afin de configurer l'URL cible de l'action Web avec l'extension `http`. 

  Vous pouvez choisir de modifier le code de l'action pour qu'il soit conforme au retour d'actions Web portant l'extension `http` ou inclure l'action dans une séquence et transmettre son résultat à une nouvelle action qui le convertit au format approprié pour une réponse HTTP. Pour en savoir plus sur les types de réponse et les extensions des actions Web, voir la documentation [Actions Web](webactions.md). 

  Modifiez le code pour `hello.js` en renvoyant les propriétés JSON `body`, `statusCode` et `headers`
  ```javascript
  function main({name:name='Serverless API'}) {
      return {
        body: new Buffer(JSON.stringify({payload:`Hello world ${name}`})).toString('base64'), 
        statusCode:200, 
        headers:{ 'Content-Type': 'application/json'}
      };
  }
  ```
  {: codeblock}
  Notez que le corps doit être renvoyé codé en `base64` et non sous forme de chaîne.
  
  Mettez à jour l'action avec le résultat modifié
  ```
  wsk action update hello hello.js --web true
  ```
  {: pre}
  Mettez à jour l'API avec `--response-type http`
  ```
  wsk api create /hello /world get hello --response-type http
  ```
  {: pre}
  Appelez l'API mise à jour
  ```
  curl https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/hello/world
  ```
  {: pre}
  ```json
    {
  "payload": "Hello world Serverless API"
  }
  ```
  Maintenant que vous contrôlez entièrement vos API, vous pouvez contrôler le contenu, tel que le contenu HTML renvoyé, ou définir le code de statut pour des erreurs telles que Introuvable (404), Non autorisé (401) ou Erreur interne (500).
### Exposition de plusieurs actions Web

Supposons que vous souhaitez exposer un ensemble d'actions dans le cadre d'un groupe de lecture qui regroupe vos amis.
Vous disposez d'une série d'actions pour implémenter le back-end du groupe de lecture :

| action | méthode HTTP | description |
| ----------- | ----------- | ------------ |
| getBooks    | GET | extraire les détails d'un livre  |
| postBooks   | POST | ajouter un livre |
| putBooks    | PUT | mettre à jour les détails d'un livre |
| deleteBooks | DELETE | supprimer un livre |

Créez une API pour le groupe de lecture, nommée `Groupe de lecture`, avec `/club` comme chemin de base de l'URL HTTP, et `books` comme ressource.
```
wsk api create -n "Book Club" /club /books get getBooks --response-type http
wsk api create /club /books post postBooks              --response-type http
wsk api create /club /books put putBooks                --response-type http
wsk api create /club /books delete deleteBooks          --response-type http
```

Notez que la première action exposée avec le chemin de base `/club` extrait le libellé d'API nommé `Groupe de lecture`, et toute autre action exposée sous `/club` est associée à `Groupe de lecture`.

Répertoriez toutes les actions que vous venez d'exposer.

```
wsk api list -f
```
```
ok: APIs
Action: getBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: get
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: postBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: post
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: putBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: put
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: deleteBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: delete
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```

Amusez-vous ensuite à ajouter un nouveau livre `JavaScript: The Good Parts` avec une méthode HTTP **POST** :
```
curl -X POST -d '{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}' https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
```
{
  "result": "success"
}
```

Procédez à l'extraction de la liste des livres avec l'action `getBooks` via la méthode HTTP **GET** :
```
curl -X GET https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
```
{
  "result": [{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}]
}
```

### Exportation de la configuration
Exportez l'API nommée `Groupe de lecture` dans un fichier que vous pouvez utiliser comme base pour recréer les API en utilisant un fichier en entrée. 
```
wsk api get "Book Club" > club-swagger.json
```

Testez le fichier swagger en supprimant d'abord toutes les URL exposées sous un chemin de base commun.
Vous pouvez supprimer toutes les URL exposées qui utilisent le chemin de base `/club` ou l'API nommée `"Groupe de lecture"` :
```
wsk api delete /club
```
```
ok: deleted API /club
```
### Modification de la configuration

Vous pouvez éditer la configuration dans le tableau de bord OpenWhisk, cliquer sur l'onglet [API](https://console.ng.bluemix.net/openwhisk/apimanagement) pour configurer la sécurité, la limitation de débit et d'autres fonctions. 

### Importation de la configuration

Restaurez maintenant l'API nommée `Groupe de lecture` à l'aide du fichier `club-swagger.json` :
```
wsk api create --config-file club-swagger.json
```
```
ok: created api /books delete for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books get for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books post for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books put for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```

Vous pouvez vérifier que l'API a été recréée :
```
wsk api list /club
```
```
ok: apis
Action                    Verb         API Name        URL
getBooks                   get         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
postBooks                 post         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
putBooks                   put         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
deleteBooks             delete         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
