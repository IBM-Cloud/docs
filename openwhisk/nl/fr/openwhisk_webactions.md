---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Actions Web
{: #openwhisk_webactions}

Les actions Web sont des actions OpenWhisk annotées pour vous permettre de générer rapidement des applications basées sur le Web. Cela vous permet de programmer une logique de back end à laquelle votre application Web peut accéder de manière anonyme sans avoir besoin de fournir une clé d'authentification OpenWhisk. Il revient au développeur d'action d'implémenter son propre mécanisme d'authentification et ses propres autorisations (c'est-à-dire son flux de protocole d'autorisation OAuth).
{: shortdesc}

Des activations d'action Web seront associées à l'utilisateur qui a créé l'action. Cela défère le coût d'une activation d'action de l'appelant au propriétaire de l'action.

Imaginons l'action JavaScript `hello.js` suivante :
```javascript
function main({name}) {
  var msg = 'you did not tell me who you are.';
  if (name) {
    msg = `hello ${name}!`
  }
  return {body: `<html><body><h3>${msg}</h3></body></html>`}
}
```
{: codeblock}

Vous pouvez créer une *action Web* `hello` dans le package `demo` pour l'espace-noms `guest` à l'aide de l'annotation `web-export` :
```
wsk package create demo
```
{: pre}
```
wsk action create /guest/demo/hello hello.js -a web-export true
```
{: pre}

L'annotation `web-export` permet à l'action d'être accessible en tant qu'action Web via une nouvelle interface REST. L'URL est structurée comme suit : `https://openwhisk.ng.bluemix.net/api/v1/web/{QUALIFIED ACTION NAME}.{EXT}`. Le nom qualifié complet d'une action se compose de trois parties : l'espace-noms, le nom du package et le nom de l'action.

*Le nom qualifié complet de l'action doit inclure son nom de package, qui est 'default' si l'action ne figure pas dans un package nommé.*

Par exemple, `guest/demo/hello`. La dernière partie de l'URI appelée l'`extension` est généralement `.http` même si d'autres valeurs sont également autorisées, comme décrit ultérieurement. Le chemin de l'API d'action Web peut être utilisé avec `curl` ou `wget` sans clé d'API. Il peut même être entré directement dans votre navigateur.

Tentez d'ouvrir [https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.http?name=Jane](https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.http?name=Jane) dans votre navigateur Web. Ou essayez d'appeler l'action via `curl` :
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.http?name=Jane
```
{: pre}

Voici un exemple d'action Web qui effectue une redirection HTTP :
```javascript
function main() {
  return { 
    headers: { location: 'http://openwhisk.org' },
    statusCode: 302
  }
}
```
{: codeblock}  

Voici un exemple d'action Web qui définit un cookie :
```javascript
function main() {
  return { 
    headers: { 
      'Set-Cookie': 'UserID=Jane; Max-Age=3600; Version=',
      'Content-Type': 'text/html'
    }, 
    statusCode: 200,
    body: '<html><body><h3>hello</h3></body></html>' }
}
```
{: codeblock}

Voici un exemple d'action Web qui renvoie un élément `image/png` :
```javascript
function main() {
    let png = <base 64 encoded string>
    return { headers: { 'Content-Type': 'image/png' },
             statusCode: 200,
             body: png };
}
```
{: codeblock}

Or returns `application/json`:
```javascript
function main(params) { 
    return {
        statusCode: 200,
        headers: { 'Content-Type': 'application/json' },
        body: new Buffer(JSON.stringify(params)).toString('base64'),
    };
}
```
{: codeblock}

It is important to be aware of the [taille limite de la réponse](./openwhisk_reference.html) des actions car une réponse dont la taille est supérieure à celle prédéfinie par le système échouera. Les objets volumineux ne doivent pas être envoyés en ligne via OpenWhisk, mais différés vers un conteneur d'objets, par exemple.

## Traitement des demandes HTTP à l'aide d'actions
{: #openwhisk_webactions_http}

Une action OpenWhisk qui n'est pas une action Web requiert les deux authentifications et doit répondre avec un objet JSON. En revanche, des actions Web peuvent être appelées sans authentification et peuvent être utilisées pour implémenter des gestionnaires HTTP qui répondent avec un contenu *headers*, *statusCode* et *body* de différents types. L'action Web doit toujours renvoyer un objet JSON, mais le système OpenWhisk (nommé le `contrôleur`) traitera une action Web différemment si son résultat inclut un ou plusieurs des éléments suivants comme propriétés JSON de niveau supérieur :

- `headers` : objet JSON dans lequel les clés sont des noms d'en-tête et les valeurs sont des valeurs de chaîne pour ces en-têtes (par défaut, il n'y a aucune valeur d'en-tête).
- `statusCode`: code d'état HTTP valide (la valeur par défaut est 200 OK). 
- `body` : chaîne qui est un texte en clair ou une chaîne codée en base64 (pour les données binaires).

Le contrôleur transmettra les en-têtes spécifiés par une action, le cas échéant, au client HTTP lors de la finalisation de la demande-réponse. De même, le contrôleur répondra avec le code d'état donné, lorsque celui-ci existe. Enfin, le corps sera transmis en tant que corps de la réponse. Sauf si un en-tête `content-type` est déclaré dans la zone `headers` du résultat d'action, le corps est transmis en l'état s'il s'agit d'une chaîne (sinon, une erreur est générée). Lorsque l'élément `content-type` est défini, le contrôleur détermine si la réponse contient des données binaires ou un texte en clair et décode la chaîne à l'aide d'un décodeur de base64 si besoin. Si le corps ne peut pas être correctement décodé, une erreur est renvoyée à l'appelant.

*Remarque* : un objet ou tableau JSON est traité en tant que données binaires et doit être codé en base64, comme illustré dans l'exemple ci-dessus.

## Contexte HTTP

Lorsqu'elles sont appelées, toutes les actions Web reçoivent des informations de demande HTTP supplémentaires en tant que paramètres pour l'argument d'entrée d'action. En voici la liste :

- `__ow_method` (type : chaîne) : méthode HTTP de la demande 
- `__ow_headers` (type : mappe chaîne à chaîne) : en-têtes de demande 
- `__ow_path` (type : chaîne) : chemin sans correspondance de la demande (la correspondance cesse une fois l'extension d'action consommée) 
- `__ow_user` (type : chaîne) : espace-noms qui identifie l'objet authentifié par OpenWhisk
- `__ow_body` (type : chaîne) : entité de corps de demande sous la forme d'une chaîne codée en base64 lorsque le contenu est binaire, sinon, sous la forme d'une chaîne en clair
- `__ow_query` (type : chaîne) : paramètres de requête de la demande en tant que chaîne non analysée

Il se peut qu'une demande ne remplace pas les paramètres `__ow_` nommés ci-dessus ; dans ce cas, la demande échoue avec l'état 400 Bad Request.

Le paramètre `__ow_user` n'est présent que lorsque l'action Web est [annotée pour indiquer que l'authentification est requise](./openwhisk_annotations.html#openwhisk_annotations_webactions) et permet à une action Web d'implémenter sa propre règle d'autorisation. Le paramètre `__ow_query` n'est disponible que lorsqu'une action Web choisit de traiter la [demande HTTP "raw"](#raw-http-handling). Il s'agit d'une chaîne contenant les paramètres de requête analysés à partir de l'URI (séparés par `&`). La propriété `__ow_body` est présente soit lorsque des demandes HTTP "raw" sont traitées, soit lorsque l'entité de demande HTTP n'est pas un objet JSON ni des données de formulaire. Sinon, les actions Web reçoivent les paramètres de requête et de corps comme propriétés de première classe dans les arguments d'action, les paramètres de corps étant prioritaires sur les paramètres de requête, lesquels étant prioritaires sur les paramètres d'action et de package. 

## Fonctions supplémentaires

Les actions Web offrent des fonctions supplémentaires, parmi lesquelles :

- Des `extensions de contenu` : la demande doit préciser le type de contenu souhaité, par exemple, `.json`, `.html`, `.http`, `.svg` ou `.text`. Pour ce faire, une extension est ajoutée au nom d'action dans l'URI, ainsi, une action `/guest/demo/hello` est référencée comme `/guest/demo/hello.http` par exemple pour recevoir une réponse HTTP en retour. Par souci de commodité, l'extension `.http` est utilisée par défaut lorsqu'aucune extension n'est détectée. 
- La `projection de zones à partir du résultat` : le chemin qui suit le nom d'action est utilisé pour projeter un ou plusieurs niveaux de la réponse. Par exemple, `/guest/demo/hello.html/body`. Cela permet à une action qui renvoie un dictionnaire `{body: "..." }` de projeter la propriété `body` et de renvoyer directement sa valeur de chaîne à la place. Le chemin projeté suit un modèle de chemin d'accès absolu (comme dans XPath).
- Des `paramètres de requête et de corps en tant qu'entrées` : l'action reçoit des paramètres de requête, mais également des paramètres dans le corps de la demande. l'ordre de priorité pour la fusion des paramètres est le suivant : paramètres de package, paramètres d'action, paramètres de requête, paramètres de corps, chacun d'eux remplaçant les valeurs précédentes en cas de chevauchement. Par exemple, `/guest/demo/hello.http?name=Jane` transmet l'argument `{name: "Jane"}` à l'action.
- Des `données de formulaire` : outre l'élément `application/json` standard, les actions Web peuvent recevoir une URL codée à partir de `application/x-www-form-urlencoded data` comme entrée.
- Une `activation via plusieurs verbes HTTP` : une action Web peut être appelée via l'une des méthodes HTTP suivantes : `GET`, `POST`, `PUT`, `PATCH`, `DELETE`, `HEAD` et `OPTIONS`.
- Un `traitement de corps autre que JSON et d'entité HTTP raw` : une action Web peut accepter un corps de demande HTTP autre qu'un objet JSON et peut choisir de toujours recevoir de telles valeurs comme valeurs opaques (texte en clair avec des données non binaires, sinon, chaîne codée en base64). 

L'exemple ci-dessous montre de façon sommaire comment utiliser ces fonctions dans une action Web. Imaginons une action `/guest/demo/hello` avec le corps suivant : 
```javascript
function main(params) { 
    return { response: params };
}
```

Lorsque cette action est appelée en tant qu'action Web, vous pouvez modifier la réponse de l'action Web en projetant différents chemins à partir du résultat.
Par exemple, pour renvoyer la totalité de l'objet et voir les arguments que l'action reçoit :

```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json
```
{: pre}
```json
    {
  "response": {
    "__ow_method": "get",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

et avec un paramètre de requête :
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json?name=Jane
```
{: pre}
```json
    {
  "response": {
    "name": "Jane",
    "__ow_method": "get",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

ou des données de formulaire :
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -d "name":"Jane"
```
{: pre}
```json
    {
  "response": {
    "name": "Jane",
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "10",      
      "content-type": "application/x-www-form-urlencoded",      
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

ou un objet JSON :
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -H 'Content-Type: application/json' -d '{"name":"Jane"}'
```
{: pre}
```json
    {
  "response": {
    "name": "Jane",
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "15",      
      "content-type": "application/json",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

et pour projeter uniquement le nom (en tant que texte) :
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.text/response/name?name=Jane
```
{: pre}
```
Jane
```

Comme vous pouvez le constater avec l'exemple précédent, par souci de commodité, les paramètres de requête, les données de formulaire et les entités de corps d'objet JSON sont tous traités en tant que dictionnaires car leurs valeurs sont directement accessibles en tant que propriétés d'entrée d'action. Ce n'est pas le cas des actions Web qui choisissent de traiter les entités de demande HTTP plus directement ou lorsque l'action Web reçoit une entité qui n'est pas un objet JSON. 

Voici un exemple d'utilisation d'un type de contenu "text" avec le même exemple que celui illustré précédemment :
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -H 'Content-Type: text/plain' -d "Jane"
```
{: pre}
```json
    {
  "response": {
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "4",      
      "content-type": "text/plain",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": "",
    "__ow_body": "Jane"
  }
}
```


## Extensions de contenu
{: #openwhisk_webactions_extensions}

Une extension de contenu est généralement requise lors de l'appel d'une action Web ; en l'absence d'extension, `.http` est utilisé par défaut. Les extensions `.json` et `.http` ne requièrent pas de chemin de projection. En revanche, les extensions `.html`, `.svg` et `.text` nécessitent un chemin de projection. Toutefois, pour des raisons de commodité, on considère que le chemin par défaut correspond au nom d'extension. Par conséquent, pour appeler une action Web et recevoir une réponse `.html`, l'action doit répondre avec un objet JSON qui contient une propriété de niveau supérieur nommée `html` (ou bien la réponse doit figurer dans le chemin défini explicitement). En d'autres termes, `/guest/demo/hello.html` revient à projeter la propriété `html` de manière explicite, comme dans `/guest/demo/hello.html/html`. Le nom qualifié complet de l'action doit inclure son nom de package, qui est `default` si l'action ne figure pas dans un package nommé.


## Paramètres protégés
{: #openwhisk_webactions_protected}

les paramètres d'action peuvent également être protégés et traités comme non modifiables. Pour finaliser les paramètres et pour rendre une action Web accessible, vous devez associer deux [annotations](openwhisk_annotations.html) à l'action : `final` et `web-export`, l'une ou l'autre devant avoir la valeur `true` pour prendre effet. En reprenant le déploiement d'action précédent, nous ajoutons les annotations comme suit :

```
wsk action create /guest/demo/hello hello.js \
      --parameter name Jane \
      --annotation final true \
      --annotation web-export true
```
{: pre}

Ces modifications ont pour conséquence de lier `name` à `Jane`, ce qui ne peut pas être remplacé par des paramètres de requête ou de corps en raison de l'annotation finale. Cela permet de sécuriser l'action sur les paramètres de requête ou de corps qui tentent de modifier cette valeur de manière intentionnelle ou fortuite. 

## Désactivation d'actions Web
{: #openwhisk_webactions_disable}

Pour empêcher qu'une action Web puisse être appelée via la nouvelle API (`https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/web/`), il suffit de retirer l'annotation ou de lui affecter la valeur `false`.

```
wsk action update /guest/demo/hello hello.js \
      --annotation web-export false
```

## Traitement de demande HTTP "raw"
{: #raw-http-handling}

Une action Web peut choisir d'interpréter et de traiter directement un corps HTTP entrant sans la promotion d'un objet JSON vers les propriétés de première classe disponibles pour l'entrée d'action (par exemple, `args.name` et `args.__ow_query` d'analyse). Cela s'effectue via des [annotations](openwhisk_annotations.html) `raw-http`. Utilisation du même exemple que celui illustré précédemment, mais avec une action Web HTTP "raw" qui reçoit `name` comme paramètre de requête et comme valeur JSON dans le corps de demande HTTP :
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json?name=Jane -X POST -H "Content-Type: application/json" -d '{"name":"Jane"}'
```
{: pre}
```json
    {
  "response": {
    "__ow_method": "post",
    "__ow_query": "name=Jane",
    "__ow_body": "eyJuYW1lIjoiSmFuZSJ9",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "15",
      "content-type": "application/json",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"      
    },
    "__ow_path": ""
  }
}
```

Notez que dans ce cas, le contenu JSON est codé en base64 car il est traité en tant que valeur binaire. L'action doit décoder en base64 et effectuer une analyse JSON de cette valeur pour récupérer l'objet JSON. OpenWhisk utilise l'infrastructure [Spray](https://github.com/spray/spray) pour [déterminer](https://github.com/spray/spray/blob/master/spray-http/src/main/scala/spray/http/MediaType.scala#L282) les types de contenu binaires et les types de contenu de texte en clair. 


### Activation du traitement de demande HTTP "raw"

Les actions Web HTTP "raw" sont activées via les [annotations](openwhisk_annotations.html) `raw-http` auxquelles la valeur `true` est affectée.

```
wsk action create /guest/demo/hello hello.js \
      --annotation web-export true
      --annotation raw-http true
```
{: pre}

**Remarque :** Etant donné que `raw-http` implique `web-export`, nous prévoyons d'améliorer l'interface de ligne de commande afin de fournir un moyen plus pratique d'ajouter (et de retirer) ces annotations dans le futur. 


### Désactivation du traitement de demande HTTP "raw"

Pour désactiver le traitement de demande HTTP "raw", affectez aux [annotations](openwhisk_annotations.html) `raw-http` la valeur `false`.

```
wsk update create /guest/demo/hello hello.js \
      --annotation web-export true
      --annotation raw-http false
```
{: pre}

**Remarque :** toutes les annotations doivent être définies en même temps pour une action, que ce soit lors de la création ou de la mise à jour de celle-ci. Cela est dû à une limitation actuelle de l'API et de l'interface de ligne de commande. Si vous ne procédez pas ainsi, toute annotation précédemment associée sera retirée. 


## Traitement des erreurs
{: #openwhisk_webactions_errors}

Lorsqu'une action OpenWhisk échoue, deux modes de panne sont possibles. Le permier, nommé *erreur d'application*, est semblable à une exception interceptée : l'action renvoie un objet JSON contenant une propriété `error` de niveau supérieur. Le second, nommé *erreur de développeur*, est activé lorsque l'action échoue de manière désastreuse et ne génère pas de réponse (semblable à une exception non interceptée). Pour les actions Web, le contrôleur traite les erreurs d'application comme suit :

- Toute projection de chemin spécifiée est ignorée et le contrôleur projette la propriété `error` à la place.
- Le contrôleur applique le traitement de contenu induit par l'extension d'action à la valeur de la propriété `error`.

Les développeurs doivent savoir comment les actions Web peuvent être utilisées et ils doivent générer des réponses d'erreur en conséquence. Par exemple, une action Web utilisée avec l'extension `.http` doit renvoyer une réponse HTTP, par exemple : `{error: { statusCode: 400 }`. Si tel n'est pas le cas, une non-concordance est générée entre le type de contenu induit par l'extension et le type de contenu d'action dans la réponse d'erreur. Une attention particulière doit être accordée aux actions Web qui sont des séquences, de sorte que les composants qui constituent une séquence puissent générer les erreurs appropriées lorsque cela est nécessaire.

