---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Actions Web (expérimentales)
{: #openwhisk_webactions}

Les actions Web sont des actions OpenWhisk annotées pour vous permettre de générer rapidement des applications basées sur le Web. Cela vous permet de programmer une logique de back end à laquelle votre application Web peut accéder de manière anonyme sans avoir besoin de fournir une clé d'authentification OpenWhisk. Il revient au développeur d'action d'implémenter son propre mécanisme d'authentification et ses propres autorisations (c'est-à-dire son flux de protocole d'autorisation OAuth).
{: shortdesc}

Des activations d'action Web seront associées à l'utilisateur qui a créé l'action. Cela défère le coût d'une activation d'action de l'appelant au propriétaire de l'action.  

**Remarque** : Cette fonction n'est pour l'instant qu'une offre expérimentale qui permet aux utilisateurs de l'essayer et de nous faire part de leurs commentaires.

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

L'annotation `web-export` permet à l'action d'être accessible en tant qu'action Web via une nouvelle interface REST. L'URL est structurée comme suit : `https://{APIHOST}/api/v1/experimental/web/{QUALIFIED ACTION NAME}.{EXT}`. Le nom qualifié complet d'une action se compose de trois parties : l'espace-noms, le nom du package et le nom de l'action. Par exemple, `guest/demo/hello`. La dernière partie de l'URI appelée l'`extension` est généralement `.http` même si d'autres valeurs sont également autorisées, comme décrit ultérieurement. Le chemin de l'API d'action Web peut être utilisé avec `curl` ou `wget` sans clé d'API. Il peut même être entré directement dans votre navigateur. 

Tentez d'ouvrir [https://${APIHOST}/api/v1/experimental/web/guest/demo/hello.http?name=Jane](https://${APIHOST}/api/v1/experimental/web/guest/demo/hello.http?name=Jane) dans votre navigateur Web. Ou essayez d'appeler l'action via `curl` :
```
curl https://openwhisk.{DomainName}/api/v1/experimental/web/guest/demo/hello.http?name=Jane
```
{: pre}
Voici un exemple d'action Web qui effectue une redirection HTTP :
```javascript
function main() {
  return { 
    headers: { "location": "http://openwhisk.org" }, 
    code: 302 
  }
}
```
{: codeblock}

Voici un exemple d'action Web qui définit un cookie :
```javascript
function main() {
  return {
    headers: { 
      "Set-Cookie": "UserID=Jane; Max-Age=3600; Version=",
      "Content-Type": "text/html"  
    }, 
    code: 200, 
    body: "<html><body><h3>hello</h3></body></html" }
}
```
{: codeblock}

Voici un exemple d'action Web qui renvoie un élément `image/png` :
```javascript
function main() {
    let png = <base 64 encoded string>
    return { headers: { 'Content-Type': 'image/png' },
             code: 200,
             body: png };
}
```
{: codeblock}

Voici un exemple d'action Web qui renvoie un élément `application/json` :
```javascript
function main(params) {
    return {
        'code': 200,
        'headers':{'Content-Type':'application/json'},
        'body' : new Buffer(JSON.stringify(params)).toString('base64'),
    };
}
```
{: codeblock}

Il est essentiel de connaître la [taille limite de la réponse](./openwhisk_reference.html) des actions car une réponse dont la taille est supérieure à celle prédéfinie par le système échouera. Les objets volumineux ne doivent pas être envoyés en ligne via OpenWhisk, mais différés vers un conteneur d'objets, par exemple.

## Traitement des demandes HTTP à l'aide d'actions
{: #openwhisk_webactions_http}

Une action OpenWhisk qui n'est pas une action Web requiert les deux authentifications et doit répondre avec un objet JSON. En revanche, des actions Web peuvent être appelées sans authentification et peuvent être utilisées pour implémenter des gestionnaires HTTP qui répondent avec un contenu *headers*, *status code* et *body* de différents types. L'action Web doit toujours renvoyer un objet JSON, mais le système OpenWhisk (nommé le `contrôleur`) traitera une action Web différemment si son résultat inclut un ou plusieurs des éléments suivants comme propriétés JSON de niveau supérieur :

- `headers` : objet JSON dans lequel les clés sont des noms d'en-tête et les valeurs sont des valeurs de chaîne pour ces en-têtes (par défaut, il n'y a aucune valeur d'en-tête). 
- `code` : code d'état HTTP valide (la valeur par défaut est 200 OK).
- `body` : chaîne qui est un texte en clair ou une chaîne codée en base64 (pour les données binaires).

Le contrôleur transmettra les en-têtes spécifiés par une action, le cas échéant, au client HTTP lors de la finalisation de la demande-réponse. De même, le contrôleur répondra avec le code d'état donné, lorsque celui-ci existe. Enfin, le corps sera transmis en tant que corps de la réponse. Sauf si un en-tête `content-type` est déclaré dans la zone `headers` du résultat d'action, le corps est transmis en l'état s'il s'agit d'une chaîne (sinon, une erreur est générée). Lorsque l'élément `content-type` est défini, le contrôleur détermine si la réponse contient des données binaires ou un texte en clair et décode la chaîne à l'aide d'un décodeur de base64 si besoin. Si le corps ne peut pas être correctement décodé, une erreur est renvoyée à l'appelant. 

*Remarque* : un objet ou tableau JSON est traité en tant que données binaires et doit être codé en base64, comme illustré dans l'exemple ci-dessus. 

## Contexte HTTP

Lorsqu'elle est appelée, une action Web reçoit toutes les informations de demande HTTP disponibles en tant que paramètres supplémentaires pour l'argument d'entrée d'action. En voici la liste :

- `__ow_meta_verb` : méthode HTTP de la demande. 
- `__ow_meta_headers` : en-têtes de demande. 
- `__ow_meta_path` : chemin sans correspondance de la demande (la correspondance cesse une fois l'extension d'action consommée). 

Il se peut que la demande ne remplace pas les paramètres `__ow_` nommés ci-dessus ; dans ce cas, la demande échoue avec l'état 400 Bad Request.

## Fonctions supplémentaires
{: #openwhisk_webactions_extra}

Les actions Web offrent des fonctions supplémentaires, parmi lesquelles :

- Des `extensions de contenu` : la demande doit préciser le type de contenu souhaité, par exemple, `.json`, `.html`, `.text` ou `.http`. Pour ce faire, une extension est ajoutée au nom d'action dans l'URI, ainsi, une action `/guest/demo/hello` est référencée comme `/guest/demo/hello.http` par exemple pour recevoir une réponse HTTP en retour. 
- La `projection de zones à partir du résultat` : le chemin qui suit le nom d'action est utilisé pour projeter un ou plusieurs niveaux de la réponse. Par exemple, `/guest/demo/hello.html/body`. Cela permet à une action qui renvoie un dictionnaire `{body: "..." }` de projeter la propriété `body` et de renvoyer directement sa valeur de chaîne à la place. Le chemin projeté suit un modèle de chemin d'accès absolu (comme dans XPath).
- Des `paramètres de requête et de corps en tant qu'entrées` : l'action reçoit des paramètres de requête, mais également des paramètres dans le corps de la demande. l'ordre de priorité pour la fusion des paramètres est le suivant : paramètres de package, paramètres d'action, paramètres de requête, paramètres de corps, chacun d'eux remplaçant les valeurs précédentes en cas de chevauchement. Par exemple, `/guest/demo/hello.http?name=Jane` transmet l'argument `{name: "Jane"}` à l'action.
- Des `données de formulaire` : outre l'élément `application/json` standard, les actions Web peuvent recevoir une URL codée à partir de `application/x-www-form-urlencoded data` comme entrée. 
- Une `activation via plusieurs verbes HTTP` : une action Web peut être appelée via l'une des quatre méthodes HTTP suivantes : `GET`, `POST`, `PUT` ou `DELETE`.


L'exemple ci-dessous montre de façon sommaire comment utiliser ces fonctions dans une action Web. Imaginons une action `/guest/demo/hello` avec le corps suivant :
```javascript
function main(params) { 
    return { 'response': params};
}
```
{: codeblock}

L'appel de l'action avec un paramètre de requête `name` en utilisant l'extension `.json` pour indiquer une réponse JSON et en projetant la zone `/response` générera la réponse HTTP suivante :
```
curl https://openwhisk.{DomainName}/api/v1/experimental/web/guest/demo/hello.json/response?name=Jane
```
{: pre}
```json
    {
    "name": "Jane",
    "__ow_meta_verb": "get",
    "__ow_meta_headers": {
        "accept": "*/*",
        "user-agent": "curl/7.51.0"
    },
    "__ow_meta_path": "/response"
}
```

## Extensions de contenu
{: #openwhisk_webactions_extensions}

Une extension de contenu est requise lors de l'appel d'une action Web. Les extensions `.json` et `.http` ne requièrent pas de chemin de projection. En revanche, les extensions `.text` et `.html` nécessitent un chemin de projection. Toutefois, pour des raisons de commodité, on considère que le chemin par défaut correspond au nom d'extension. Par conséquent, pour appeler une action Web et recevoir une réponse `.html`, l'action doit répondre avec un objet JSON qui contient une propriété de niveau supérieur nommée `html` (ou bien la réponse doit figurer dans le chemin défini explicitement). En d'autres termes, `/guest/demo/hello.html` revient à projeter la propriété `html` de manière explicite, comme dans `/guest/demo/hello.html/html`. Le nom qualifié complet de l'action doit inclure son nom de package, qui est `default` si l'action ne figure pas dans un package nommé. 


## Paramètres protégés
{: #openwhisk_webactions_protected}

les paramètres d'action peuvent également être protégés et traités comme non modifiables. Pour finaliser les paramètres et pour rendre une action Web accessible, vous devez associer deux [annotations](/openwhisk_annotations.html) à l'action : `final` et `web-export`, l'une ou l'autre devant avoir la valeur `true` pour prendre effet. En reprenant le déploiement d'action précédent, nous ajoutons les annotations comme suit :

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

Pour empêcher qu'une action Web puisse être appelée via la nouvelle API (`https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/experimental/web/`), il suffit de retirer l'annotation ou de lui affecter la valeur `false`.

```
wsk action update /guest/demo/hello hello.js \
      --annotation web-export false
```
{: pre}     

## Traitement des erreurs
{: #openwhisk_webactions_errors}

Lorsqu'une action OpenWhisk échoue, deux modes de panne sont possibles. Le permier, nommé *erreur d'application*, est semblable à une exception interceptée : l'action renvoie un objet JSON contenant une propriété `error` de niveau supérieur. Le second, nommé *erreur de développeur*, est activé lorsque l'action échoue de manière désastreuse et ne génère pas de réponse (semblable à une exception non interceptée). Pour les actions Web, le contrôleur traite les erreurs d'application comme suit :

- Toute projection de chemin spécifiée est ignorée et le contrôleur projette la propriété `error` à la place. 
- Le contrôleur applique le traitement de contenu induit par l'extension d'action à la valeur de la propriété `error`. 

Les développeurs doivent savoir comment les actions Web peuvent être utilisées et ils doivent générer des réponses d'erreur en conséquence. Par exemple, une action Web utilisée avec l'extension `.http` doit renvoyer une réponse HTTP, par exemple : `{error: { code: 400 }`. Si tel n'est pas le cas, une non-concordance est générée entre le type de contenu induit par l'extension et le type de contenu d'action dans la réponse d'erreur. Une attention particulière doit être accordée aux actions Web qui sont des séquences, de sorte que les composants qui constituent une séquence puissent générer les erreurs appropriées lorsque cela est nécessaire. 
