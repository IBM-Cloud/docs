---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Exemples Insights for Twitter
{: #examples}

Pour vous initier au service {{site.data.keyword.twittershort}}, utilisez les exemples fournis afin d'apprendre à utiliser le service de façon optimale.
{: shortdesc}

## Démonstration Insights for Twitter
{: #insights_twitter_demo}

Une application exemple est à votre disposition pour vous permettre d'effectuer des recherches dans des flux de données Twitter qui utilisent le service {{site.data.keyword.twittershort}}. L'application est accessible à partir de [https://cdetestapp.mybluemix.net/](https://cdetestapp.mybluemix.net/){: new.window}. Elle s'ouvre dans votre navigateur et affiche une zone de rechercher, avec les boutons **Twitter Search** et **Twitter Count**. 

![Image de l'interface utilisateur avec la zone de recherche.](images/sample1_UI.jpg "Image de l'interface utilisateur avec la zone de recherche.")

Depuis l'application exemple, vous pouvez rechercher des tweets en utilisant les paramètres et les opérateurs pris en charge qui sont décrits dans [Langage d'interrogation](twitter_rest_apis.html#querylanguage){: new.window}. Ainsi, si vous entrez "IBM Twitter" (avec un espace indiquant une opération booléenne AND) puis cliquez sur **Twitter Search**, les tweets contenant les deux termes sont renvoyés.

![Image d'un terme de requête et des résultats de recherche retournés.](images/sample1_tweet_search.jpg "Image d'un terme de requête et des résultats de recherche retournés")

Si "IBM Twitter" est spécifié dans la zone de recherche et que vous cliquez sur **Twitter Count**, le nombre de tweets contenant les deux termes est retourné.

![Image d'un terme de requête et du résultat retourné.](images/sample1_tweet_count.jpg "Image d'un terme de requête et du résultat retourné.")

## Création d'un suivi basé sur des règles
{: #creating_rule_track}

Les utilisateurs du plan payant peuvent créer des suivis basés sur des règles pour filtrer les Tweets collectés dans le flux de données PowerTrack. Les exemples des sections suivantes montrent comment éditer et supprimer des suivis ou exécuter un appel d'API de recherche ou de comptage sur le flux PowerTrack. Pour créer un suivi basé sur des règles, créez une demande **POST** avec l'opération /api/v1/tracks operation, spécifiez le type de suivi (**Rule**), indiquez une propriété EndDate et incluez au moins une règle. Le fragment de code suivant est une demande exemple qui inclut deux règles :

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks
HTTP/1.1 Content-Type: application/json
{
    "endDate": "2015-10-03T10:23:00Z",
    "name": "My First Rule Track",
    "type": "Rule",
    "rules": [
        {"value": "Canada"},
        {"value": "sport hockey"}
    ]
}
```

Les valeurs `username` et `password` sont des valeurs uniques à votre application et instance de service. Ces informations figurent dans les variables d'environnement **VCAP_SERVICES**. Pour plus d'informations, voir [Initiation à {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}.

Le corps de la réponse est similaire au fragment de code suivant :

```
HTTP/1.1 201 Created
Content-Type: application/json;charset=utf-8
Location: https://cdeservice.mybluemix.net:443/api/v1/tracks/66ff1961-51fe-4475-8bcd-c02f071d6fd1
{
    "id": "66ff1961-51fe-4475-8bcd-c02f071d6fd1",
    "type": "Rule",
    "state": "Active",
    "createdDate": "2015-08-06T20:38:28.940Z",
    "endDate": "2015-10-03T10:23:00Z",
    "name": "My First Rule Track",
    "rules": [
        {
          "id": "06497963-4fe3-47e8-90cd-aaef25f31314"
          "value": "Canada"
        },
        {
          "id": "d021165d-85e2-456a-af16-b9c026d76208",
          "value": "sport hockey"
        }
    ]
}
```

La réponse contient l'ID unique qui est associé au suivi qui vient d'être créé. En outre, chaque règle reçoit un ID unique. La propriété endDate indique le moment où le suivi s'arrête de collecter les messages ; il doit être conforme au format UTC format (`YYYY-MM-DD` ou `YYYY-MM-DDTHH:MM:SSZ`). La propriété type doit être spécifiée en tant que **Rule** ou **Aggregated**. L'exemple illustrant la création d'un suivi basé sur des règles, le type **Rule** a été défini.

Si la propriété state n'est pas spécifiée dans la demande, le suivi est créé avec l'état **Active**, par défaut. La propriété name  est facultative et n'est pas nécessairement unique. Pour faciliter la gestion des filtres, il est recommandé de choisir un nom unique et descriptif.

Pour des informations détaillées sur la syntaxe des règles, voir {{site.data.keyword.twittershort}} - [Langage d'interrogation](twitter_rest_apis.html#querylanguage){: new.window}.

## Création d'un suivi agrégé
{: #creating_aggregated_track}

Les utilisateurs du plan payant peuvent créer des suivis complexes associant plusieurs suivis existants. Les suivis agrégés (complexes) peuvent inclure à la fois des suivis basés sur des règles et d'autres suivis agrégés. La recherche de tweets dans un suivi agrégé renvoie les résultats des suivis qui le composent. Pour créer un suivi agrégé, émettez une demande **POST** avec l'opération  /api/v1/tracks, spécifiez le type de suivi (**Aggregated**) et incluez plusieurs ID de suivi. Le fragment de code suivant est une demande exemple qui inclut deux suivis :

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks
HTTP/1.1 Content-Type: application/json
{
    "name": "My Aggregated Track",
    "type": "Aggregated",
    "trackIds": [
       {"id": "a22206cd-b72b-4b7d-a5a3-e2d08ce02a88"},
       {"id": "180356df-9a78-491e-b070-f3ffbe00bdf2"}
     ]
}
```
Les valeurs `username` et `password` sont des valeurs uniques à votre application et instance de service. Ces informations figurent dans les variables d'environnement **VCAP_SERVICES**. Pour plus d'informations, voir [Initiation à {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}.

Le corps de la réponse est similaire au fragment de code suivant :

```
HTTP/1.1 201 Created
Content-Type: application/json;charset=utf-8
Location: https://cdeservice.mybluemix.net:443/api/v1/tracks/66ff1961-51fe-4475-8bcd-c02f071d6fd1
{
  "id": "9808fb82-7ea8-4b8e-9cd5-ad653a6dabe6",
  "type": "Aggregated",
  "createdDate": "2015-08-07T17:05:51.214Z",
  "name": "My Aggregated Track",
  "trackIds": [
    {
      "id": "a22206cd-b72b-4b7d-a5a3-e2d08ce02a88"
    },
    {
      "id": "180356df-9a78-491e-b070-f3ffbe00bdf2"
    }
  ]
}
```

La réponse inclut l'ID unique qui est associé au suivi agrégé. A la différence des suivis basés sur des règles, les suivis agrégés n'incluent pas de propriétés endDate ou state, car ces propriétés sont gérées au sein des suivis individuels à base de règles.

## Edition des suivis
{: #editing_tracks}

Vous pouvez éditer les suivis basés sur des règles et complexes pour affiner le filtrage des données du flux PowerTrack. Quand des règles sont ajoutées (ou modifiées) dans des suivis existants, les messages qui ont été extraits en fonction des règles précédentes sont conservés dans le suivi. Pour être sûr que les résultats de recherche retournent les données correspondant au dernier ensemble de règles, supprimez le suivi et créez-en un nouveau avec l'ensemble de règles souhaité.

L'exemple de la rubrique [Création d'un suivi basé sur des règles](#creating_rule_track){: new.window} inclut deux règles avec l'ID de suivi `66ff1961-51fe-4475-8bcd-c02f071d6fd1`. Pour ajouter une nouvelle règle intitulée "Champions", utilisez l'opération POST /api/v1/tracks/{track Id} et ajoutez la nouvelle règle.

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/66ff1961-51fe-4475-8bcd-c02f071d6fd1
HTTP/1.1 Content-Type: application/json
{
    "endDate": "2015-10-03T10:23:00Z",
    "name": "My First Rule Track",
    "type": "Rule",
    "rules": [
        {"value": "Canada"},
        {"value": "sport hockey"},
        {"value": "Champions"}
    ]
}
```
De la même façon, vous pouvez retirer des règles d'un suivi existant en émettant une opération GET /api/v1/tracks/{track Id} et en retirant les règles inutiles.

L'exemple de la rubrique [Création d'un suivi agrégé](#creating_aggregated_track) inclut deux suivis. Un autre suivi, avec l'ID `c4562594-1eeb-4a95-8fac-255428d74bce`, pourrait être ajouté au suivi agrégé existant en émettant l'opération suivante :

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/9808fb82-7ea8-4b8e-9cd5-ad653a6dabe6
HTTP/1.1 Content-Type: application/json
{
  "trackIds": [
    {"id": "a22206cd-b72b-4b7d-a5a3-e2d08ce02a88"},
    {"id": "180356df-9a78-491e-b070-f3ffbe00bdf2"},
    {"id": "c4562594-1eeb-4a95-8fac-255428d74bce"}
  ]
}
```

## Suppression des suivis
{: #deleting_tracks}

Vous pouvez supprimer les suivis qui ne sont plus nécessaires en émettant une opération /api/v1/tracks/{trackId}. Cette opération peut s'appliquer aussi bien aux suivis basés sur des règles qu'aux suivis complexes. Les suivis intégrés à des suivis complexes doivent d'abord en être retirés pour pouvoir être supprimés. L'exemple suivant montre comment supprimer un suivi avec l'ID `a22206cd-b72b-4b7d-a5a3-e2d08ce02a88`:

```
DELETE https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/a22206cd-b72b-4b7d-a5a3-e2d08ce02a88
HTTP/1.1
```

Sinon, il est aussi possible d'arrêter la collecte des tweets dans un suivi particulier en changeant son état à Inactive. Au lieu de supprimer le suivi, l'exemple suivant le désactive :

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/a22206cd-b72b-4b7d-a5a3-e2d08ce02a88
HTTP/1.1
{
    "state": "Inactive"
}
```

## Recherche de tweets
{: #searching_tweets}

Vous pouvez utiliser une opération GET dans votre application afin d'extraire des tweets de l'un ou l'autre des flux de données. Ainsi, une recherche de tweets Decahose est implémentée comme suit : `/api/v1/messages/search?q=QUERY&size=NUMBER&from=NUMBER`. Pour les utilisateurs du plan payant, la recherche de tweets dans le flux PowerTrack est implémentée de la façon suivante : `/api/v1/tracks/{trackId}/messages/search?q=QUERY&size=NUMBER&from=NUMBER`.

Le paramètre "size" spécifie le nombre de messages à renvoyer dans une réponse à une requête, tandis que le paramètre "from" indique le message initial  à renvoyer dans l'ensemble de résultat complet. La référence {trackId} est l'identificateur unique d'un suivi spécifique.
En utilisant cURL, vous pouvez rechercher dans le flux Decahose des tweets contenant "IBM", en entrant :

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/messages/search?q=IBM
```

La requête correspondante pour le flux PowerTrack serait : 

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/{trackId}/messages/search?q=IBM
```

Les valeurs `username` et `password` sont des valeurs uniques à votre application et instance de service. Ces informations figurent dans les variables d'environnement **VCAP_SERVICES**. Pour plus d'informations, voir [Initiation à {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}.

Le service renvoie des réponses au format JSON. Le tableau ci-dessous répertorie les codes de réponse possibles.

| **Code de statut HTTP** 	| **Motif**                                                           	|
|------------------	|------------------------------------------------------------------	|
| 200              	| OK                                                               	|
| 400              	| Propriétés de contenu de demande manquantes ou non valides.                   	|
| 401              	| Echec de l'authentification. Un nom d'utilisateur et un mot de passe valides sont requis. 	|
| 403              	| Interdit, limite atteinte.                                        	|
| 500              	| Une erreur interne est survenue.                                  	|

** Tableau 1. Messages de réponse

Le corps de la réponse peut apparaître comme suit :

```
{
    "search": {
        "results": 16283624
    },
    "tweets": [{
        "message": {
            ...
            "body": "this is a nice tweet",
            "actor": {
                "followersCount”: 456,
                "displayName": "IBM Tweeter"
                ...
            },
            "cde": {
                "sentiment": {"polarity": "POSITIVE"...
                },
                "author": {"gender": "male"...
                },
                ...
            }
        }
    }]
}
```

L'expression de requête codée sous forme d'URL suivante extrait les tweets sur un film, en fonction d'une fenêtre de temps et d'un nombre
d'occurrences donnés. Cet exemple peut être utilisé pour déterminer l'intérêt ou les réactions suscités par une bande-annonce.

```
/api/v1/messages/search?q=%28posted:2015-02-01T00:00:00Z%20AND%20%23americansniper%29&size=5 
```

En décodant l'URL, la syntaxe de requête et l'opération deviennent "(posted:2015-02-01T00:00:00Z AND #americansniper) &size=5".

## Comptage du nombre de tweets
{: #counting_tweets}

Vous pouvez appliquer une opération GET dans votre application pour extraire le nombre de tweets correspondant à une requête spécifiée. Les requêtes sur Decahose sont émises sous la forme : `/api/v1/messages/count?q=QUERY` tandis que les appels au flux PowerTrack utilisent le format suivant : 

```
/api/v1/tracks/{trackId}/messages/count?q=QUERY
```

En utilisant cURL, vous pouvez trouver, dans Decahose, le nombre de tweets contenant "IBM", en entrant :

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/messages/count?q=IBM
```

La même requête peut être créée pour la source de données PowerTrack : 

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/{trackId}/messages/count?q=IBM
```

Les valeurs `username` et `password` sont des valeurs uniques à votre application et instance de service. Ces informations figurent dans les variables d'environnement **VCAP_SERVICES**. Pour plus d'informations, voir [Initiation à {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}.

Le service renvoie des réponses au format JSON. Le tableau ci-dessous répertorie les messages de réponse possibles.

| **Code de statut HTTP** 	| **Motif**                                                           	|
|------------------	|------------------------------------------------------------------	|
| 200              	| OK                                                               	|
| 400              	| Propriétés de contenu de demande manquantes ou non valides.                   	|
| 401              	| Echec de l'authentification. Un nom d'utilisateur et un mot de passe valides sont requis. 	|
| 403              	| Interdit, limite atteinte.                                        	|
| 500              	| Une erreur interne est survenue.                                  	|

**Tableau 2. Messages de réponse**

Le corps de la réponse peut apparaître comme suit :
```
{
  "related": {
      "search": {
          "href": "https://server.bluemix.net/api/v1/messages/search?q=ibm" 
      }
  },
  "search": {
      "results": 21695
  }
}
```

L'expression de requête suivante extrait le nombre de tweets positifs qui contiennent à la fois "IBM" et "Bluemix". Dans ce cas, les tweets de Decahose sont renvoyés dans la réponse.

`.../api/v1/messages/count?q="IBM Bluemix sentiment:positive`

L'expression de requête codée sous forme d'URL suivante extrait le nombre de tweets qui contiennent "IBM" sur une période spécifiée. Cet exemple de requête vous permet d'évaluer la popularité d'un sujet et déterminer sa tendance. Les tweets du flux PowerTrack sont renvoyés dans cet exemple.

`.../api/v1/tracks/{trackId}/messages/count?q=%28posted:2015-02-01T00:00:00Z,2015-02-15T00:00:00Z AND %23IBM%29`

En décodant l'URL, la syntaxe de requête et l'opération deviennent "(posted:2015-02-01T00:00:00Z,2015-02-15T00:00:00Z AND #IBM)".
