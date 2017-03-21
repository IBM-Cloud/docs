---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Exposition de vos actions via la passerelle d'API (expérimental)
{: #openwhisk_apigateway}

Dans {{site.data.keyword.openwhisk}}, vous pouvez appeler vos actions à l'aide de l'[API REST](./openwhisk_reference.html#openwhisk_ref_restapi) en utilisant une demande HTTP uniquement avec une méthode **POST**. Le client HTTP doit alors effectuer la demande avec la clé d'API d'autorisation d'OpenWhisk. Il s'agit d'une clé principale qui, en plus d'autoriser l'appel d'une action, autorise également la suppression et la création d'autres actions.
{: shortdesc}

Cette fonction expérimentale vous permet d'appeler une action avec des méthodes HTTP autres que POST et sans la clé d'API d'autorisation de l'action.

Utilisez l'interface de ligne de commande pour exposer vos actions OpenWhisk via la passerelle d'API OpenWhisk. 

## Configuration de l'interface de ligne de commande d'OpenWhisk
{: #openwhisk_apigateway_cli}
Cette fonction expérimentale fonctionne uniquement avec le nouveau modèle d'authentification OpenWhisk, dans lequel chaque espace de nom est associé à une clé d'authentification unique. Suivez les instructions figurant dans la rubrique [Configuration de l'interface de ligne de commande](https://console.ng.bluemix.net/openwhisk/cli) pour configurer la clé d'authentification de votre espace de nom spécifique.

## Exposition d'une action OpenWhisk
{: #openwhisk_apigateway_hello}

Exposez une action simple déjà préinstallée avec OpenWhisk

```
wsk api-experimental create /hello /echo get /whisk.system/utils/echo
```
{: pre}
```
ok: created api /echo GET for action /whisk.system/utils/echo
https://21ef035.api-gw.mybluemix.net/hello/echo
```
{: screen}
Une nouvelle URL est générée pour exposer l'action `echo` via une méthode HTTP **GET**.

Essayez-la en envoyant une demande HTTP vers l'URL.
```
curl https://21ef035.api-gw.mybluemix.net/hello/echo?marco=polo
```
{: pre}
Cela permet d'appeler l'action `echo`, qui renvoie une chaîne JSON avec les paramètres envoyés.
```
{
  "marco":"polo"
}
```
{: screen}

Vous pouvez transmettre des paramètres à l'action grâce à de simples paramètres de requête, ou via le corps de demande.

### Exposition de plusieurs actions
{: #openwhisk_apigateway_actions}

Supposons que vous souhaitez exposer un ensemble d'actions dans le cadre d'un groupe de lecture qui regroupe vos amis. Vous disposez d'une série d'actions pour implémenter le back-end du groupe de lecture :

| action | méthode http | description |
| ----------- | ----------- | ------------ |
| getBooks    | GET | extraire les détails d'un livre  |
| postBooks   | POST | ajouter un livre |
| putBooks    | PUT | mettre à jour les détails d'un livre |
| deleteBooks | DELETE | supprimer un livre |

Créez une API pour le groupe de lecture, nommée `Groupe de lecture`, avec `/club` comme chemin de base de l'URL HTTP, et `books` comme ressource.
```
wsk api-experimental create -n "Groupe de lecture" /club /books get getBooks
wsk api-experimental create /club /books post postBooks
wsk api-experimental create /club /books put putBooks
wsk api-experimental create /club /books delete deleteBooks
```
{: pre}

Notez que la première action exposée avec le chemin de base `/club` extrait le libellé d'API nommé `Groupe de lecture`, et toute autre action exposée sous `/club` est associée à `Groupe de lecture`.

Répertoriez toutes les actions que vous venez d'exposer.

```
wsk api-experimental list
```
{: pre}
```
ok: apis
Action                   Verb          API Name           URL
getBooks                   get         Groupe de lecture  https://2ef15285-gws.api-gw.mybluemix.net/club/books
postBooks                 post         Groupe de lecture  https://2ef15285-gws.api-gw.mybluemix.net/club/books
putBooks                   put         Groupe de lecture  https://2ef15285-gws.api-gw.mybluemix.net/club/books
deleteBooks             delete         Groupe de lecture  https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

Amusez-vous ensuite à ajouter un nouveau livre `JavaScript: The Good Parts` avec une méthode HTTP **POST** :
```
curl -X POST -d '{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}' https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: pre}
```
{
  "result": "success"
}
```
{: screen}

Procédez à l'extraction de la liste des livres avec l'action `getBooks` via la méthode HTTP **GET** :
```
curl -X GET https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: pre}
```
{
  "result": [{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}]
}
```

### Exportation de la configuration
Exportez l'API nommée `Groupe de lecture` dans un fichier que vous pouvez utiliser comme base pour recréer les API en utilisant un fichier en entrée. 
```
wsk api-experimental get "Book Club" > club-swagger.json
```
{: pre}

Testez le fichier swagger en supprimant d'abord toutes les URL exposées sous un chemin de base commun.
Vous pouvez supprimer toutes les URL exposées qui utilisent le chemin de base `/club` ou l'API nommée `"Groupe de lecture"` :
```
wsk api-experimental delete /club
```
{: pre}
```
ok: deleted API /club
```
{: screen}

Restaurez maintenant l'API nommée `Groupe de lecture` à l'aide du fichier `club-swagger.json` :
```
wsk api-experimental create --config-file club-swagger.json
```
{: pre}
```
ok: created api /books delete for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books get for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books post for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books put for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

Vous pouvez vérifier que l'API a été recréée :
```
wsk api-experimental list /club
```
{: pre}
```
ok: apis
Action                    Verb         API Name           URL
getBooks                   get         Groupe de lecture  https://2ef15285-gws.api-gw.mybluemix.net/club/books
postBooks                 post         Groupe de lecture  https://2ef15285-gws.api-gw.mybluemix.net/club/books
putBooks                   put         Groupe de lecture  https://2ef15285-gws.api-gw.mybluemix.net/club/books
deleteBooks             delete         Groupe de lecture  https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

- **Remarque** : Cette fonction n'est pour l'instant qu'une offre expérimentale qui permet aux utilisateurs de l'essayer et de nous faire part de leurs commentaires. Les commentaires suivants ont déjà été reçus :
  - Aucune possibilité de personnaliser le contrôle d'accès HTTP pour le partage de ressources d'origine croisée (CORS) ; les en-têtes de réponse d'API générés sont actuellement configurés pour autoriser n'importe quelle origine ou instruction HTTP (c'est-à-dire *). Les en-têtes suivants sont toujours renvoyés :
    - Access-Control-Allow-Origin : *
    - Access-Control-Allow-Headers : Authorization, Content-Type
    - Access-Control-Allow-Methods : GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS
  - Seul le type de contenu `application/json` est pris en charge pour la demande et la réponse.
  - Aucun moyen de programmation permettant de contrôler la réponse issue de l'action OpenWhisk.
  - Toutes les actions OpenWhisk sont exposées via l'accès public, aucune possibilité de configurer une clé d'API personnalisée.
  - Les paramètres de chemin ne sont pas pris en charge, seuls le paramètre de requête et le corps de la demande le sont.
  - Si l'API est créée sans nom d'API, le nom est le chemin de base et cela ne peut pas être modifié.
  - Lors de la recréation des API via un fichier en entrée, les API doivent d'abord être supprimées.
  - Lors de l'exportation des API, le contenu inclut la clé d'API OpenWhisk ; ces informations sont sensibles et aucune création de modèle n'est disponible.
