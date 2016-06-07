---

 

copyright:

  2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Utilisation de services compatibles avec {{site.data.keyword.openwhisk_short}} 
{: #openwhisk_ecosystem}
*Dernière mise à jour : 28 mars 2016*

Dans {{site.data.keyword.openwhisk}}, un catalogue de packages permet d'améliorer facilement votre application en ajoutant des fonctions
utiles, ainsi que d'accéder à des services externes dans l'écosystème. Cloudant, The Weather Company,
Slack et GitHub sont des exemples de service externe compatibles avec {{site.data.keyword.openwhisk_short}}.
{: shortdesc}

Le catalogue est disponible sous forme de packages dans l'espace de nom `/whisk.system`. Voir
[Parcours des packages](./openwhisk_packages.html#openwhisk_packagedisplay) pour des informations sur le parcours du catalogue à l'aide de
l'outil de ligne de commande.

Les rubriques qui suivent présentent certains packages du catalogue.

## Utilisation du package Cloudant
{: #openwhisk_catalog_cloudant}
Le package `/whisk.system/cloudant` permet d'utiliser une base de données Cloudant. Il inclut les actions et les flux ci-après.

| Entité | Type | Paramètres | Description |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | package | {{site.data.keyword.Bluemix_notm}}ServiceName, host, username, password, dbname, includeDoc, overwrite | Utiliser
une base de données Cloudant |
| `/whisk.system/cloudant/read` | action | dbname, includeDoc, id | Lire un document à partir d'une base de données |
| `/whisk.system/cloudant/write` | action | dbname, overwrite, doc | Ecrire un document dans une base de données |
| `/whisk.system/cloudant/changes` | flux | dbname, includeDoc | Exécuter des événements déclencheurs en cas de modification dans une
base de données |

Les rubriques ci-après expliquent comment configurer une base de données Cloudant, comment configurer un package associé, et comment utiliser les
actions et les flux du package `/whisk.system/cloudant`.

### Configuration d'une base de données Cloudant dans {{site.data.keyword.Bluemix_notm}}

Si vous utilisez {{site.data.keyword.openwhisk_short}} depuis {{site.data.keyword.Bluemix}},
{{site.data.keyword.openwhisk_short}} crée automatiquement des liaisons de package pour vos instances de service
{{site.data.keyword.Bluemix_notm}} Cloudant. Si vous n'utilisez pas {{site.data.keyword.openwhisk_short}} et Cloudant depuis
{{site.data.keyword.Bluemix_notm}}, ignorez l'étape suivante.

1. Créez une instance de service Cloudant dans votre [tableau de
bord](http://console.ng.{{site.data.keyword.Bluemix_notm}}.net) {{site.data.keyword.Bluemix_notm}}.

  Mémorisez le nom de l'instance de service ainsi que l'organisation et l'espace {{site.data.keyword.Bluemix_notm}} dans lesquels vous vous
trouvez.

2. Assurez-vous que votre interface de ligne de commande {{site.data.keyword.openwhisk_short}} se trouve dans l'espace de nom qui correspond
à l'organisation et à l'espace {{site.data.keyword.Bluemix_notm}} que vous avez utilisés à l'étape précédente.

  ```
  wsk property set --namespace monOrg{{site.data.keyword.Bluemix_notm}}_monEspace{{site.data.keyword.Bluemix_notm}}
  ```
  {: pre}

  Vous pouvez aussi utiliser `wsk property set --namespace` pour définir un espace de nom à partir d'une liste des espaces de nom
auxquels vous pouvez accéder.

3. Actualisez les packages dans votre espace de nom. L'actualisation crée automatiquement une liaison de package pour l'instance de service Cloudant
que vous avez créée.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  {{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages

/monOrg{{site.data.keyword.Bluemix_notm}}_monEspace{{site.data.keyword.Bluemix_notm}}/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1
private binding
  ```
  {: screen}

  Le nom qualifié complet de la liaison de package qui correspond à votre instance de service {{site.data.keyword.Bluemix_notm}} Cloudant
doit apparaître.

4. Vérifiez que la liaison de package créée précédemment est configurée avec l'hôte et les données d'identification de votre instance de service
{{site.data.keyword.Bluemix_notm}} Cloudant.

  ```
  wsk package get
/monOrg{{site.data.keyword.Bluemix_notm}}_monEspace{{site.data.keyword.Bluemix_notm}}/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1
  ```
  {: pre}
  ```
  ok: got package
/monOrg{{site.data.keyword.Bluemix_notm}}_monEspace{{site.data.keyword.Bluemix_notm}}/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1,
projecting parameters
  [
      ...
      {
          "key": "username",
          "value": "cdb18832-2bbb-4df2-b7b1-{{site.data.keyword.Bluemix_notm}}"
      },
      {
          "key": "host",
          "value": "cdb18832-2bbb-4df2-b7b1-{{site.data.keyword.Bluemix_notm}}.cloudant.com"
      },
      {
          "key": "password",
          "value": "c9088667484a9ac827daf8884972737"
      }
      ...
  ]
  ```
  {: screen}

### Configuration d'une base de données Cloudant hors de {{site.data.keyword.Bluemix_notm}}

Si vous n'utilisez pas {{site.data.keyword.openwhisk_short}} dans {{site.data.keyword.Bluemix_notm}} ou si vous voulez configurer
votre base de données Cloudant hors de {{site.data.keyword.Bluemix_notm}}, vous devez créer une liaison de package manuellement pour votre compte
Cloudant. Vous avez besoin du nom d'hôte, du nom d'utilisateur et du mot de passe du compte Cloudant.

1. Créez une liaison de package configurée pour votre compte Cloudant.

  ```
  wsk package bind /whisk.system/cloudant monCloudant -p username 'MON_NOM_UTILISATEUR' -p password 'MON_MOT_DE_PASSE' -p host
'MON_COMPTE_CLOUDANT.cloudant.com'
  ```
  {: pre}

2. Vérifiez que la liaison de package existe.

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /monEspaceNom/monCloudant private binding
  ```
  {: screen}


### Ecoute des modifications apportées dans une base de données Cloudant

Vous pouvez utiliser le flux `changes` pour configurer un service afin d'exécuter un déclencheur à chaque fois qu'une modification
est apportée dans votre base de données Cloudant.

1. Créez un déclencheur avec le flux `changes` dans la liaison de package que vous avez créée précédemment. Veillez à remplacer `/monEspaceNom/monCloudant` par votre nom de package.

  ```
  wsk trigger create monDéclencheurCloudant --feed /monEspaceNom/monCloudant/changes --param dbname testdb --param includeDocs true
  ```
  {: pre}
  ```
  ok: created trigger feed monDéclencheurCloudant
  ```
  {: screen}

2. Recherchez les activations.

  ```
  wsk activation poll
  ```
  {: pre}

3. Dans votre tableau de bord Cloudant, modifiez un document existant ou créez-en un.

4. Observez les nouvelles activations pour le déclencheur `monDéclencheurCloudant` pour chaque modification de document.

**Remarque** : si vous ne parvenez pas à observer de nouvelles activations, reportez-vous aux sections suivantes relatives à la
lecture et à l'écriture dans une base de données Cloudant. Testez les étapes de lecture et d'écriture ci-après pour vérifier que vos données
d'identification Cloudant sont correctes.

A présent, vous pouvez créer des règles et les associer à des actions afin de réagir aux mises à jour de document.

Le contenu des événements générés dépend de la valeur du paramètre `includeDocs` lors de la création du déclencheur. Si la valeur
est true, chaque événement déclencheur qui est exécuté inclut le document Cloudant modifié. Par exemple, imaginez le document modifié suivant :

  ```
  {
    "_id": "6ca436c44074c4c2aa6a40c9a188b348",
    "_rev": "3-bc4960fc13aa368afca8c8427a1c18a8",
    "name": "Heisenberg"
  }
  ```
  {: screen}

Le code dans cet exemple génère un événement déclencheur avec les paramètres `_id`, `_rev` et
`name` correspondants. En fait, la représentation JSON de l'événement déclencheur est identique au document.

Sinon, si `includeDocs` a pour valeur false, les événements incluent les paramètres suivants :

- `id` : l'ID de document.
- `seq` : l'identificateur de séquence généré par Cloudant.
- `changes` : un tableau d'objets possédant chacun une zone `rev` qui contient l'ID de révision du document.

La représentation JSON de l'événement déclencheur est la suivante :

  ```
  {
      "id": "6ca436c44074c4c2aa6a40c9a188b348",
      "seq": "2-g1AAAAL9aJyV-GJCaEuqx4-BktQkYp_dmIfC",
      "changes": [
          {
              "rev": "2-da3f80848a480379486fb4a2ad98fa16"
          }
      ]
  }
  ```


### Ecriture dans une base de données Cloudant

Vous pouvez utiliser une action pour stocker un document dans une base de données Cloudant appelée `testdb`. Assurez-vous que cette
base de données existe sur votre compte Cloudant.

1. Stockez un document en utilisant l'action `write` dans la liaison de package que vous avez créée précédemment. Veillez à
remplacer `/monEspaceNom/monCloudant` par le nom de votre package.

  ```
  wsk action invoke /monEspaceNom/monCloudant/write --blocking --result --param dbname testdb --param doc '{"_id":"heisenberg", "name":"Walter White"}'
  ```
  {: pre}
  ```
  ok: invoked /monEspaceNom/monCloudant/write with id 62bf696b38464fd1bcaff216a68b8287
  response:
  {
    "id": "heisenberg",
    "ok": true,
    "rev": "1-9a94fb93abc88d8863781a248f63c8c3"
  }
  ```
  {: screen}

2. Vérifiez que le document existe en le recherchant dans votre tableau de bord Cloudant.

  L'adresse URL du tableau de bord pour la base de données `testdb` est similaire à la suivante :
`https://MON_COMPTE_CLOUDANT.cloudant.com/dashboard.html#database/testdb/_all_docs?limit=100`.


### Lecture depuis une base de données Cloudant

Vous pouvez utiliser une action pour extraire un document depuis une base de données Cloudant appelée `testdb`. Assurez-vous que
cette base de données existe sur votre compte Cloudant.

1. Procédez à l'extraction d'un document en utilisant l'action `read` dans la liaison de package que vous avez créée précédemment. Veillez à remplacer `/monEspaceNom/monCloudant` par le nom de votre package.

  ```
  wsk action invoke /monEspaceNom/monCloudant/read --blocking --result --param dbname testdb --param id heisenberg
  ```
  {: pre}
  ```
  {
    "_id": "heisenberg",
    "_rev": "1-9a94fb93abc88d8863781a248f63c8c3"
    "name": "Walter White"
  }
  ```
  {: screen}


## Utilisation du package Alarm
{: #openwhisk_catalog_alarm}

Vous pouvez utiliser le package `/whisk.system/alarms` pour exécuter un déclencheur à une fréquence spécifiée. Il peut être
utile pour configurer des tâches ou des travaux récurrents, comme l'appel d'une action de sauvegarde du système toutes les heures.

Le package inclut le flux ci-dessous.

| Entité | Type | Paramètres | Description |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | package | - | Alarmes et utilitaire périodique |
| `/whisk.system/alarms/alarm` | flux | cron, trigger_payload, maxTriggers | Exécuter un événement déclencheur régulièrement |


### Exécution régulière d'un événement déclencheur

Le flux `/whisk.system/alarms/alarm` configure le service Alarm pour exécuter un événement déclencheur à une fréquence
spécifiée. Les paramètres sont les suivants :

- `cron` : chaîne basée sur la syntaxe crontab Unix, qui indique quand déclencher la tâche périodique (en temps universel coordonné). Il s'agit d'une
séquence de six zones séparées par un espace : `X X X X X X `. Pour plus d'informations sur l'utilisation de la syntaxe cron, voir :
https://github.com/ncb000gt/node-cron.

- `trigger_payload` : la valeur de ce paramètre devient le contenu du déclencheur à chaque fois que le déclencheur est exécuté.

- `maxTriggers` : l'exécution de déclencheurs s'arrête lorsque cette limite est atteinte. La valeur par défaut est 1000.

Voici un exemple de création de déclencheur qui sera exécuté toutes les 20 secondes avec les valeurs `name` et
`place` dans l'événement déclencheur.

  ```
  wsk trigger create periodic --feed /whisk.system/alarms/alarm --param cron '/20 * * * * *' --param trigger_payload '{"name":"Odin","place":"Asgard"}'
  ```
  {: pre}

Chaque événement généré inclut sous forme de paramètres les propriétés spécifiées dans la valeur `trigger_payload`. Dans ce cas,
chaque événement déclencheur possède les paramètres `name=Odin` et `place=Asgard`.


## Utilisation du package Weather
{: #openwhisk_catalog_weather}

Le package `/whisk.system/weather` permet d'appeler l'API The Weather Company.

Le package inclut l'action ci-dessous.

| Entité | Type | Paramètres | Description |
| --- | --- | --- | --- |
| `/whisk.system/weather` | package | apiKey | Services de The Weather Company |
| `/whisk.system/weather/forecast` | action | apiKey, latitude, longitude | Prévisions à 10 jours de Weather.com |

Bien que ce ne soit pas obligatoire, il est recommandé de créer une liaison de package avec la valeur `apiKey`. Ainsi, il n'est pas
nécessaire de spécifier la clé à chaque fois que vous appelez les actions du package.

### Obtention d'une prévision météorologique pour un lieu

L'action `/whisk.system/weather/forecast` renvoie une prévision météorologique à 10 jours pour un lieu en appelant l'API de The Weather
Company. Les paramètres sont les suivants :

- `apiKey` : clé d'API pour The Weather Company autorisée à appeler l'API de prévision à 10 jours.
- `latitude` : coordonnée de latitude du lieu.
- `longitude` : coordonnée de longitude du lieu.

Voici un exemple de création d'une liaison de package, puis d'obtention d'une prévision à 10 jours.

1. Créez une liaison de package avec votre clé d'API.

  ```
  wsk package bind /whisk.system/weather myWeather --param apiKey 'MON_API_METEO'
  ```
  {: pre}

2. Appelez l'action `forecast` dans votre liaison de package pour obtenir la prévision météorologique.

  ```
  wsk action invoke myWeather/forecast --blocking --result --param latitude '43.7' --param longitude '-79.4'
  ```
  {: pre}

  ```
  {
      "forecasts": [
          {
              "dow": "Wednesday",
              "max_temp": -1,
              "min_temp": -16,
              "narrative": "Chance of a few snow showers. Highs -2 to 0C and lows -17 to -15C.",
              ...
          },
          {
              "class": "fod_long_range_daily",
              "dow": "Thursday",
              "max_temp": -4,
              "min_temp": -8,
              "narrative": "Mostly sunny. Highs -5 to -3C and lows -9 to -7C.",
              ...
          },
          ...
      ],
  }
  ```
  {: screen}


## Utilisation du package Watson
{: #openwhisk_catalog_watson}

Le package `/whisk.system/watson` permet d'appeler diverses API Watson.

Le package inclut les actions ci-dessous.

| Entité | Type | Paramètres | Description |
| --- | --- | --- | --- |
| `/whisk.system/watson` | package | username, password | Actions pour les API d'analyse Watson |
| `/whisk.system/watson/translate` | action | translateFrom, translateTo, translateParam, username, password | Traduire le texte |
| `/whisk.system/watson/languageId` | action | payload, username, password | Identifier la langue |

Bien que ce ne soit pas obligatoire, il est recommandé de créer un package de liaison avec les valeurs `username` et
`password`. Ainsi, il n'est pas nécessaire de spécifier ces données d'identification à chaque fois que vous appelez les actions du package.

### Traduction de texte

L'action `/whisk.system/watson/translate` traduit un texte d'une langue vers une autre. Les paramètres sont les suivants :

- `username` : nom d'utilisateur de l'API Watson.
- `password` : mot de passe de l'API Watson.
- `translateParam` : paramètre d'entrée à traduire. Par exemple, si `translateParam=payload`, la valeur du
paramètre `payload` qui est transmise à l'action est traduite.
- `translateFrom` : code à deux chiffres de la langue source.
- `translateTo` : code à deux chiffres de la langue cible.

Voici un exemple de création d'une liaison de package et de traduction de texte.

1. Créez une liaison de package avec vos données d'identification Watson.

  ```
  wsk package bind /whisk.system/watson myWatson --param username 'MON_NOM_UTILISATEUR_WATSON' --param password 'MON_MOT_DE_PASSE_WATSON'
  ```
  {: pre}

2. Appelez l'action `translate` dans votre liaison de package pour traduire du texte anglais en français.

  ```
  wsk action invoke myWatson/translate --blocking --result --param payload 'Blue skies ahead' --param translateParam 'payload' --param translateFrom 'en' --param translateTo 'fr'
  ```
  {: pre}

  ```
  {
      "payload": "Ciel bleu à venir"
  }
  ```
  {: screen}


### Identification de la langue d'un texte

L'action `/whisk.system/watson/languageId` identifie la langue d'un texte. Les paramètres sont les suivants :

- `username` : nom d'utilisateur de l'API Watson.
- `password` : mot de passe de l'API Watson.
- `payload` : texte à identifier.

Voici un exemple de création de liaison de package et d'identification de la langue d'un texte.

1. Créez une liaison de package avec vos données d'identification Watson.

  ```
  wsk package bind /whisk.system/watson myWatson -p username 'MON_NOM_UTILISATEUR_WATSON' -p password 'MON_MOT_DE_PASSE_WATSON'
  ```
  {: pre}

2. Appelez l'action `languageId` dans votre liaison de package pour identifier la langue.

  ```
  wsk action invoke myWatson/languageId --blocking --result --param payload 'Ciel bleu à venir'
  ```
  {: pre}
  ```
  {
    "payload": "Ciel bleu à venir",
    "language": "fr",
    "confidence": 0.710906
  }
  ```
  {: screen}


## Utilisation du package Slack
{: #openwhisk_catalog_slack}

Le package `/whisk.system/slack` permet d'utiliser les [API Slack](https://api.slack.com/).

Le package inclut les actions suivantes :

| Entité | Type | Paramètres | Description |
| --- | --- | --- | --- |
| `/whisk.system/slack` | package | url, channel, username | Interagir avec l'API Slack |
| `/whisk.system/slack/post` | action | text, url, channel, username | Publier un message dans un canal Slack |

Bien que ce ne soit pas obligatoire, il est recommandé de créer une liaison de package avec les valeurs `username`,
`url` et 'channel'. Grâce à la liaison, il n'est pas nécessaire de spécifier les valeurs à chaque fois que vous appelez l'action dans le
package.

### Publication d'un message dans un canal Slack

L'action `/whisk.system/slack/post` publie un message dans un canal Slack spécifié. Les paramètres sont les suivants :

- `url` : URL du webhook Slack.
- `channel` : canal Slack dans lequel publier le message.
- `username` : nom sous lequel publier le message.
- `text` : message à publier.

L'exemple ci-dessous explique comment configurer Slack, créer une liaison de package et publier un message dans un canal.

1. Configurez un [webhook entrant](https://api.slack.com/incoming-webhooks) Slack pour votre équipe.

  Une fois Slack configuré, vous devez obtenir une adresse URL de webhook similaire à `https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`. Vous
en aurez besoin à l'étape suivante.

2. Créez une liaison de package avec vos données d'identification Slack, le canal dans lequel publier le message, et le nom d'utilisateur sous
lequel publier le message.

  ```
  wsk package bind /whisk.system/slack mySlack --param url 'https://hooks.slack.com/services/...' --param username 'Bob' --param channel '#MySlackChannel'
  ```
  {: pre}

3. Appelez l'action `post` dans votre liaison de package pour publier un message dans votre canal Slack.

  ```
  wsk action invoke mySlack/post --blocking --result --param text 'Bonjour d'OpenWhisk!'
  ```
  {: pre}


## Utilisation du package GitHub
{: #openwhisk_catalog_github}

Le package `/whisk.system/github` permet d'utiliser les [API GitHub](https://developer.github.com/).

Le package inclut le flux suivant :

| Entité | Type | Paramètres | Description |
| --- | --- | --- | --- |
| `/whisk.system/github` | package | username, repository, accessToken | Interagir avec l'API GitHub |
| `/whisk.system/github/webhook` | flux | events, username, repository, accessToken | Exécuter des événements déclencheurs en cas
d'activité GitHub |

Bien que ce ne soit pas obligatoire, il est recommandé de créer une liaison de package avec les valeurs `username`,
`repository` et `accessToken`.  Grâce à la liaison, il n'est pas nécessaire de spécifier les valeurs à chaque fois que
vous utilisez le flux dans le package.

### Exécution d'un événement déclencheur avec une activité GitHub

Le flux `/whisk.system/github/webhook` configure un service pour qu'il exécute un déclencheur lorsqu'il existe une activité dans un
référentiel GitHub spécifié. Les paramètres sont les suivants :

- `username` : nom d'utilisateur du référentiel GitHub.
- `repository` : référentiel GitHub.
- `accessToken` : votre jeton d'accès personnel GitHub. Lorsque vous [créez votre
jeton](https://github.com/settings/tokens), veillez à sélectionner les portées repo:status et public_repo. De plus, vérifiez qu'aucun webhook n'est défini pour votre référentiel.
- `events` : [type d'activité GitHub](https://developer.github.com/v3/activity/events/types/) qui vous intéresse.

Voici un exemple de création de déclencheur qui sera exécuté à chaque fois qu'une nouvelle validation est effectuée dans un référentiel GitHub.

1. Générez un [jeton d'accès personnel](https://github.com/settings/tokens) GitHub.

  Le jeton d'accès va être utilisé à l'étape suivante.


2. Créez une liaison de package configurée pour votre référentiel GitHub et avec votre jeton d'accès.

  ```
  wsk package bind /whisk.system/github monGit --param username monUtilisateurGit --param repository monRéférentielGit --param accessToken
aaaaa1111a1a1a1a1a111111aaaaaa1111aa1a1a
  ```
  {: pre}

3. Créez un déclencheur pour le type d'événement `push` GitHub avec votre flux `monGit/webhook`.

  ```
  wsk trigger create monDéclencheurGit --feed monGit/webhook --param events push
  ```
  {: pre}

