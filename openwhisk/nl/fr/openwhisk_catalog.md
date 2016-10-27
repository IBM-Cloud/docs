---

 

copyright:

  2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Utilisation des services {{site.data.keyword.Bluemix_notm}} qui sont activés pour {{site.data.keyword.openwhisk_short}}
{: #openwhisk_ecosystem}
Dernière mise à jour : 9 septembre 2016
{: .last-updated}

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
| `/whisk.system/cloudant/changes` | flux | dbname, includeDoc, maxTriggers | Exécuter des événements déclencheurs en cas de modification dans une
base de données |

Les rubriques ci-après expliquent comment configurer une base de données Cloudant, comment configurer un package associé, et comment utiliser les
actions et les flux du package `/whisk.system/cloudant`.

### Configuration d'une base de données Cloudant dans {{site.data.keyword.Bluemix_notm}}
{: #openwhisk_catalog_cloudant_in}

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
  wsk property set --namespace my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space
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
  /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1 private binding
  ```
  {: screen}

  Le nom qualifié complet de la liaison de package qui correspond à votre instance de service {{site.data.keyword.Bluemix_notm}} Cloudant apparaît.

4. Vérifiez que la liaison de package qui a été créée précédemment est configurée avec l'hôte et les données d'identification de votre instance de service
{{site.data.keyword.Bluemix_notm}} Cloudant.

  ```
  wsk package get /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1
  ```
  {: pre}
  ```
  ok: got package /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1, projecting parameters
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
{: #openwhisk_catalog_cloudant_outside}

Si vous n'utilisez pas {{site.data.keyword.openwhisk_short}} dans {{site.data.keyword.Bluemix_notm}} ou si vous voulez configurer
votre base de données Cloudant hors de {{site.data.keyword.Bluemix_notm}}, vous devez créer une liaison de package manuellement pour votre compte
Cloudant. Vous avez besoin du nom d'hôte, du nom d'utilisateur et du mot de passe du compte Cloudant.

1. Créez une liaison de package qui est configurée pour votre compte Cloudant.

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
{: #openwhisk_catalog_cloudant_listen}

Vous pouvez utiliser le flux `changes` pour configurer un service afin d'exécuter un déclencheur à chaque fois qu'une modification
est apportée dans votre base de données Cloudant. Les paramètres sont les suivants :

- `dbname` : Nom de la base de données Cloudant.
- `includeDoc` : Si la valeur est true, chaque événement déclencheur qui est exécuté inclut le document Cloudant modifié. 
- `maxTriggers` : L'exécution de déclencheurs s'arrête lorsque cette limite est atteinte. La valeur par défaut est 1000. La valeur maximale que vous pouvez définir est 10 000. Si vous tentez de définir une valeur supérieure à 10 000, la demande est rejetée.

1. Créez un déclencheur avec le flux `changes` dans la liaison de package que vous avez créée précédemment. Prenez
soin de remplacer `/monEspaceNom/monCloudant` par votre nom de package.

  ```
  wsk trigger create monDéclencheurCloudant --feed /monEspaceNom/monCloudant/changes --param dbname bdtest --param includeDoc true
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
lecture et à l'écriture dans une base de données Cloudant. Les tests de lecture et d'écriture ci-après vous aideront à vérifier que vos données d'identification
Cloudant sont correctes.

A présent, vous pouvez créer des règles et les associer à des actions afin de réagir aux mises à jour de document.

Le contenu des événements générés dépend de la valeur du paramètre `includeDoc` lors de la création du déclencheur. Si la valeur
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

Sinon, si `includeDoc` a pour valeur false, les événements incluent les paramètres suivants :

- `id` : ID de document.
- `seq` : identificateur de séquence généré par Cloudant.
- `changes` : tableau d'objets possédant chacun une zone `rev` qui contient l'ID de révision du document.

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
{: #openwhisk_catalog_cloudant_write}

Vous pouvez utiliser une action pour stocker un document dans une base de données Cloudant appelée `bdtest`. Assurez-vous que
cette base de données existe sur votre compte Cloudant.

1. Stockez un document en utilisant l'action `write` dans la liaison de package que vous avez créée précédemment. Prenez
soin de remplacer `/monEspaceNom/monCloudant` par votre nom de package.

  ```
  wsk action invoke /monEspaceNom/monCloudant/write --blocking --result --param dbname bdtest --param doc '{"_id":"heisenberg", "name":"Walter White"}'
  ```
  {: pre}
  ```
  ok: invoked /monEspaceNom/monCloudant/write with id 62bf696b38464fd1bcaff216a68b8287
  {
    "id": "heisenberg",
    "ok": true,
    "rev": "1-9a94fb93abc88d8863781a248f63c8c3"
  }
  ```
  {: screen}

2. Vérifiez que le document existe en le recherchant dans votre tableau de bord Cloudant.

  L'adresse URL du tableau de bord pour la base de données `bdtest` est similaire à la suivante :
`https://MON_COMPTE_CLOUDANT.cloudant.com/dashboard.html#database/bdtest/_all_docs?limit=100`.


### Lecture depuis une base de données Cloudant
{: #openwhisk_catalog_cloudant_read}

Vous pouvez utiliser une action pour extraire un document depuis une base de données Cloudant appelée `bdtest`. Assurez-vous que
cette base de données existe sur votre compte Cloudant.

1. Procédez à l'extraction d'un document en utilisant l'action `read` dans la liaison de package que vous avez créée précédemment. Prenez
soin de remplacer `/monEspaceNom/monCloudant` par votre nom de package.

  ```
  wsk action invoke /monEspaceNom/monCloudant/read --blocking --result --param dbname bdtest --param id heisenberg
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

Le package `/whisk.system/alarms` peut être utilisé pour exécuter un déclencheur à une fréquence spécifiée. Il peut être
utile pour configurer des tâches ou des travaux récurrents, comme l'appel d'une action de sauvegarde du système toutes les heures.

Le package inclut le flux ci-dessous.

| Entité | Type | Paramètres | Description |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | package | - | Alarmes et utilitaire périodique |
| `/whisk.system/alarms/alarm` | flux | cron, trigger_payload, maxTriggers | Exécuter un événement déclencheur régulièrement |


### Exécution régulière d'un événement déclencheur
{: #openwhisk_catalog_alarm_fire}

Le flux `/whisk.system/alarms/alarm` configure le service Alarm pour exécuter un événement déclencheur à une fréquence
spécifiée. Les paramètres sont les suivants :

- `cron` : chaîne basée sur la syntaxe crontab UNIX, qui indique quand déclencher la tâche périodique (en temps universel coordonné). Il s'agit d'une
séquence de six zones séparées par un espace : `X X X X X X `. Pour plus d'informations sur l'utilisation de la syntaxe cron, voir : https://github.com/ncb000gt/node-cron. Voici quelques exemples de la fréquence indiquée par la chaîne :

  - `* * * * * *` : chaque seconde.
  - `0 * * * * *` : au début de chaque minute.
  - `* 0 * * * *` : au début de chaque heure.
  - `0 0 9 8 * *` à 9:00:00 du matin (UTC) le huitième jour de chaque mois.

- `trigger_payload` : la valeur de ce paramètre devient le contenu du déclencheur à chaque fois que le déclencheur est exécuté.

- `maxTriggers` : l'exécution de déclencheurs s'arrête lorsque cette limite est atteinte. La valeur par défaut est 1000. La valeur maximale que vous pouvez définir est 10 000. Si vous tentez de définir une valeur supérieure à 10 000, la demande est rejetée.

Voici un exemple de création de déclencheur qui sera exécuté toutes les 20 secondes avec les valeurs `name` et
`place` dans l'événement déclencheur :

  ```
  wsk trigger create periodic --feed /whisk.system/alarms/alarm --param cron '*/20 * * * * *' --param trigger_payload '{"name":"Odin","place":"Asgard"}'
  ```
  {: pre}

Chaque événement généré inclut sous forme de paramètres les propriétés spécifiées dans la valeur `trigger_payload`. Dans ce cas,
chaque événement déclencheur possède les paramètres `name=Odin` et `place=Asgard`.


## Utilisation du package Weather
{: #openwhisk_catalog_weather}

Le package `/whisk.system/weather` offre une méthode pratique pour appeler The Weather Company Data for IBM Bluemix API.

Le package inclut l'action ci-dessous.

| Entité | Type | Paramètres | Description |
| --- | --- | --- | --- |
| `/whisk.system/weather` | package | username, password | Services de Weather Company Data for IBM Bluemix API  |
| `/whisk.system/weather/forecast` | action | latitude, longitude, timePeriod | prévision pour la période spécifiée|

Il est recommandé de créer une liaison de package avec les valeurs `username` et `password`. Ainsi, il n'est pas nécessaire de spécifier les données d'identification à chaque fois que vous appelez les actions du package.

### Obtention d'une prévision météorologique pour un lieu
{: #openwhisk_catalog_weather_forecast}

L'action `/whisk.system/weather/forecast` renvoie une prévision météorologique pour un emplacement en appelant une API de
The Weather Company. Les paramètres sont les suivants :

- `username` : nom d'utilisateur pour The Weather Company Data for IBM Bluemix qui est autorisé à appeler l'API de prévision.
- `password` : mot de passe pour The Weather Company Data for IBM Bluemix qui est autorisé à appeler l'API de prévision. 
- `latitude` : coordonnée de latitude du lieu.
- `longitude` : coordonnée de longitude du lieu.
- `timeperiod` : période sur laquelle porte la prévision. Les options valides sont '10day' - (valeur par défaut) Renvoie une
prévision quotidienne sur 10 jours, '48hour' - Renvoie une prévision horaire sur 2 jours, 'current' - Renvoie les conditions météorologiques actuelles,
'timeseries' - Renvoie les observations actuelles et jusqu'à 24 heures d'observations antérieures à partir de la date et et de l'heure en cours. 


Voici un exemple de création d'une liaison de package, puis d'obtention d'une prévision à 10 jours :

1. Créez une liaison de package avec votre clé d'API.

  ```
  wsk package bind /whisk.system/weather myWeather --param username 'MON_NOM_UTILISATEUR' --param password 'MON_MOT_DE_PASSE'
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
| `/whisk.system/watson/speechToText` | action | payload, content_type, encoding, username, password, continuous, inactivity_timeout,
interim_results, keywords, keywords_threshold, max_alternatives, model, timestamps, watson-token, word_alternatives_threshold, word_confidence,
X-Watson-Learning-Opt-Out | Convertir le contenu audio en texte |
| `/whisk.system/watson/textToSpeech` | action | payload, voice, accept, encoding, username, password | Convertir le texte en contenu audio |

Il est recommandé de créer une liaison de package avec les valeurs `username` et `password`. Ainsi, il n'est pas nécessaire de spécifier ces données d'identification à chaque fois que vous appelez les actions du package.

### Traduction de texte
{: #openwhisk_catalog_watson_translate}

L'action `/whisk.system/watson/translate` traduit un texte d'une langue vers une autre. Les paramètres sont les suivants :

- `username` : nom d'utilisateur de l'API Watson.
- `password` : mot de passe de l'API Watson.
- `translateParam`: paramètre d'entrée indiquant le texte à traduire. Par exemple, si `translateParam=payload`, la valeur du paramètre `payload` qui est transmise à l'action est traduite.
- `translateFrom` : code à deux chiffres de la langue source.
- `translateTo` : code à deux chiffres de la langue cible.

Voici un exemple de création d'une liaison de package et de traduction de texte.

1. Créez une liaison de package avec vos données d'identification Watson.

  ```
  wsk package bind /whisk.system/watson monWatson --param username 'MON_NOM_UTILISATEUR_WATSON' --param password 'MON_MOT_DE_PASSE_WATSON'
  ```
  {: pre}

2. Appelez l'action `translate` dans votre liaison de package pour traduire du texte anglais en français.

  ```
  wsk action invoke monWatson/translate --blocking --result --param payload 'Ciel bleu à venir' --param translateParam 'payload' --param translateFrom 'en' --param translateTo 'fr'
  ```
  {: pre}

  ```
  {
      "payload": "Ciel bleu à venir"
  }
  ```
  {: screen}


### Identification de la langue d'un texte
{: #openwhisk_catalog_watson_identifylang}

L'action `/whisk.system/watson/languageId` identifie la langue d'un texte. Les paramètres sont les suivants :

- `username` : nom d'utilisateur de l'API Watson.
- `password` : mot de passe de l'API Watson.
- `payload` : texte à identifier.

Voici un exemple de création de liaison de package et d'identification de la langue d'un texte :

1. Créez une liaison de package avec vos données d'identification Watson.

  ```
  wsk package bind /whisk.system/watson monWatson -p username 'MON_NOM_UTILISATEUR_WATSON' -p password 'MON_MOT_DE_PASSE_WATSON'
  ```
  {: pre}

2. Appelez l'action `languageId` dans votre liaison de package pour identifier la langue.

  ```
  wsk action invoke monWatson/languageId --blocking --result --param payload 'Ciel bleu à venir'
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


### Conversion de texte en paroles
{: #openwhisk_catalog_watson_texttospeech}

L'action `/whisk.system/watson/textToSpeech` convertit du texte en contenu audio. Les paramètres sont les suivants :

- `username` : nom d'utilisateur de l'API Watson.
- `password` : mot de passe de l'API Watson.
- `payload` : texte à convertir en paroles.
- `voice` : voix du conférencier.
- `accept` : format du fichier vocal.
- `encoding` : codage du fichier binaire vocal.

Voici un exemple de création de liaison de package et de conversion d'un texte en paroles .

1. Créez une liaison de package avec vos données d'identification Watson.

  ```
  wsk package bind /whisk.system/watson monWatson -p username 'MON_NOM_UTILISATEUR_WATSON' -p password 'MON_MOT_DE_PASSE_WATSON'
  ```
  {: pre}

2. Appelez l'action `textToSpeech` dans votre liaison de package pour convertir le texte.

  ```
  wsk action invoke monWatson/textToSpeech --blocking --result --param payload 'Hey.' --param voice 'en-US_MichaelVoice' --param accept 'audio/wav' --param encoding
'base64'
  ```
  {: pre}
  ```
  {
    "payload": "<Codage en base 64 d'un fichier .wav>"
  }
  ```
  {: screen}


### Conversion de paroles en texte
{: #openwhisk_catalog_watson_speechtotext}

L'action `/whisk.system/watson/speechToText` convertit un contenu audio en texte. Les paramètres sont les suivants :

- `username` : nom d'utilisateur de l'API Watson.
- `password` : mot de passe de l'API Watson.
- `payload` : données binaires des paroles à convertir en texte.
- `content_type` : type MIME du contenu audio.
- `encoding` : codage du fichier binaire vocal.
- `continuous` : indique si plusieurs résultats finaux représentant des phrases consécutives séparées par de longues pauses doivent être renvoyés.
- `inactivity_timeout` : nombre de secondes après lequel, si seul un silence est détecté dans le contenu audio soumis,
la connexion est fermée.
- `interim_results` : indique si le service doit renvoyer des résultats intermédiaires.
- `keywords` : liste de mots clés à rechercher dans le contenu audio.
- `keywords_threshold` : niveau de fiabilité plancher pour l'identification d'un mot clé.
- `max_alternatives` : nombre maximal de transcriptions alternatives à renvoyer.
- `model` : identificateur du modèle à utiliser pour la demande de reconnaissance.
- `timestamps`: indique si l'horodatage doit être renvoyé pour chaque mot.
- `watson-token` : fournit un jeton d'authentification pour le service au lieu des données d'identification au service.
- `word_alternatives_threshold` : niveau de fiabilité plancher pour l'identification d'une hypothèse
comme alternative possible d'un mot.
- `word_confidence` : indique si un niveau de fiabilité sur la plage 0 à 1 doit être renvoyé pour chaque mot.
- `X-Watson-Learning-Opt-Out` : indique si la collecte de données doit être ignorée pour l'appel.
 
Voici un exemple de création de liaison de package et de conversion de paroles en texte :

1. Créez une liaison de package avec vos données d'identification Watson.

  ```
  wsk package bind /whisk.system/watson monWatson -p username 'MON_NOM_UTILISATEUR_WATSON' -p password 'MON_MOT_DE_PASSE_WATSON'
  ```
  {: pre}

2. Appelez l'action `speechToText` dans votre liaison de package pour convertir le contenu audio codé.

  ```
  wsk action invoke monWatson/speechToText --blocking --result --param payload <codage base64 d'un fichier .wav> --param
content_type 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```
  {
    "data": "Hello Watson"
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

Il est recommandé de créer une liaison de package avec les valeurs `username`, `url` et `channel`. Grâce à la liaison, il n'est pas nécessaire de spécifier les valeurs à chaque fois que vous appelez l'action dans le
package.

### Publication d'un message dans un canal Slack
{: #openwhisk_catalog_slack_post}

L'action `/whisk.system/slack/post` publie un message dans un canal Slack spécifié. Les paramètres sont les suivants :

- `url` : URL du webhook Slack.
- `channel` : canal Slack dans lequel publier le message.
- `username` : nom sous lequel publier le message.
- `text` : message à publier.
- `token` : (facultatif) [Jeton d'accès](https://api.slack.com/tokens) Slack. Voir
[ci-après](./openwhisk_catalog.html#openwhisk_catalog_slack_token) pour plus de détails sur l'utilisation de jetons d'accès Slack.


L'exemple ci-dessous explique comment configurer Slack, créer une liaison de package et publier un message dans un canal.

1. Configurez un [webhook entrant](https://api.slack.com/incoming-webhooks) Slack pour votre équipe.

  Une fois Slack configuré, vous obtenez une adresse URL de webhook similaire à `https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`. Vous
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

### Utilisation de l'API reposant sur le jeton Slack 
{: #openwhisk_catalog_slack_token}

Si vous préférez, vous pouvez choisir d'utiliser l'API reposant sur le jeton Slack plutôt que l'API de webhook. Dans ce cas, transmettez un paramètre `token` contenant votre [jeton d'accès](https://api.slack.com/tokens) Slack. Vous
pourrez ensuite utiliser l'une des [méthodes d'API Slack](https://api.slack.com/methods) comme paramètre `url`. Par
exemple, pour envoyer un message, utilisez [slack.postMessage](https://api.slack.com/methods/chat.postMessage) comme valeur de
paramètre `url`. 

## Utilisation du package GitHub
{: #openwhisk_catalog_github}

Le package `/whisk.system/github` permet d'utiliser les [API GitHub](https://developer.github.com/).

Le package inclut le flux suivant :

| Entité | Type | Paramètres | Description |
| --- | --- | --- | --- |
| `/whisk.system/github` | package | username, repository, accessToken | Interagir avec l'API GitHub |
| `/whisk.system/github/webhook` | flux | events, username, repository, accessToken | Exécuter des événements déclencheurs en cas
d'activité GitHub |

Il est recommandé de créer une liaison de package avec les valeurs `username`, `repository` et `accessToken`.  Grâce à la liaison, il n'est pas nécessaire de spécifier les valeurs à chaque fois que
vous utilisez le flux dans le package.

### Exécution d'un événement déclencheur avec une activité GitHub
{: #openwhisk_catalog_github_fire}

Le flux `/whisk.system/github/webhook` configure un service pour qu'il exécute un déclencheur lorsqu'il existe une activité dans un
référentiel GitHub spécifié. Les paramètres sont les suivants :

- `username` : nom d'utilisateur du référentiel GitHub.
- `repository` : référentiel GitHub.
- `accessToken` : votre jeton d'accès personnel GitHub. Lorsque vous [créez votre
jeton](https://github.com/settings/tokens), veillez à sélectionner les portées repo:status et public_repo. De plus, vérifiez qu'aucun webhook n'est défini pour votre référentiel.
- `events` : [type d'événement GitHub](https://developer.github.com/v3/activity/events/types/) qui vous intéresse.

Voici un exemple de création de déclencheur qui sera exécuté à chaque fois qu'une nouvelle validation est effectuée dans un référentiel GitHub.

1. Générez un [jeton d'accès personnel](https://github.com/settings/tokens) GitHub.

  Le jeton d'accès va être utilisé à l'étape suivante.

2. Créez une liaison de package configurée pour votre référentiel GitHub et avec votre jeton d'accès.

  ```
  wsk package bind /whisk.system/github monGit --param username monUtilisateurGit --param repository monRéférentielGit --param accessToken
aaaaa1111a1a1a1a1a111111aaaaaa1111aa1a1a
  ```
  {: pre}

3. Créez un déclencheur pour le type d'événement `push` GitHub à l'aide de votre flux `myGit/webhook`.

  ```
  wsk trigger create monDéclencheurGit --feed monGit/webhook --param events push
  ```
  {: pre}

Une validation au référentiel GitHub via une commande `git push` provoque l'exécution du déclencheur par le webhook. Si une règle correspond au déclencheur, l'action associée sera appelée.
L'action reçoit le contenu de webhook GitHub comme paramètre d'entrée. Chaque événement de webhook GitHub comporte un schéma JSON similaire, mais un objet de contenu unique qui est déterminé par son type d'événement.
Pour plus d'informations sur le contenu, voir la documentation de l'API des [événements et de contenu GitHub](https://developer.github.com/v3/activity/events/types/).


## Utilisation du package Push
{: #openwhisk_catalog_pushnotifications}

Le package `/whisk.system/pushnotifications` vous permet d'utiliser un service push. 

Le package inclut l'action et le flux suivants :

| Entité | Type | Paramètres | Description |
| --- | --- | --- | --- |
| `/whisk.system/pushnotifications` | package | appId, appSecret  | utilisation du service push |
| `/whisk.system/pushnotifications/sendMessage` | action | text, url, deviceIds, platforms, tagNames, apnsBadge, apnsCategory, apnsActionKeyTitle, apnsSound, apnsPayload, apnsType, gcmCollapseKey, gcmDelayWhileIdle, gcmPayload, gcmPriority, gcmSound, gcmTimeToLive | Envoi de notification push à un ou plusieurs périphérique(s) spécifié(s) |
| `/whisk.system/pushnotifications/webhook` | flux | events | Exécution d'événements déclencheur sur des activités de périphérique
(enregistrement, annulation d'enregistrement, abonnement ou annulation d'abonnement de périphérique) sur le service Push |
Il est recommandé de créer une liaison de package avec les valeurs `appId` et `appSecret`. Ainsi, il n'est pas nécessaire de spécifier ces données d'identification à chaque fois que vous appelez les actions du package.

### Création d'une liaison de package Push
{: #openwhisk_catalog_pushnotifications_create}

Lors de la création d'une liaison de package Notifications push, vous devez spécifier les paramètres suivants :

-  `appId` : Identificateur global unique d'application Bluemix.
-  `appSecret` : Valeur confidentielle d'application du service de notification push Bluemix.

Voici un exemple de création d'une liaison de package.

1. Créez une application Bluemix dans le [tableau de bord Bluemix](http://console.ng.bluemix.net).

2. Initialisez le service de notification push et liez celui-ci à l'application Bluemix.

3. Configurez l'[application de notification push](https://console.ng.bluemix.net/docs/services/mobilepush/index.html).

  Prenez soin de mémoriser l'`identificateur global unique d'application` et la `valeur confidentielle d'application` de l'application Bluemix que vous avez créée.


4. Créez une liaison de package avec `/whisk.system/pushnotifications`.

  ```
  wsk package bind /whisk.system/pushnotifications monPush -p appId "monIDApp" -p appSecret "maValeurConfApp"
  ```
  {: pre}

5. Vérifiez que la liaison de package existe.

  ```
  wsk package list
  ```
  {: pre}

  ```
  packages
  /nomEspaceNom/monPush private binding
  ```
  {: screen}

### Envoi de notifications push
{: #openwhisk_catalog_pushnotifications_send}

L'action `/whisk.system/pushnotifications/sendMessage` envoie des notifications push à des périphériques enregistrés. Les paramètres sont les suivants :
- `text` : message de notification à présenter à l'utilisateur. Par exemple : `-p text "Bonjour, OpenWhisk a envoyé une
notification"`.
- `url` : URL facultative qui peut être envoyée en même temps que l'alerte. Par exemple : `-p url "https:\\www.w3.ibm.com"`.
- `gcmPayload` : contenu JSON personnalisé qui sera envoyé dans le cadre du message de notification. Par exemple : `-p gcmPayload "{"hi":"hello"}"`
- `gcmSound` : fichier son (sur le périphérique) qui est utilisé lorsque la notification arrive sur le périphérique.
- `gcmCollapseKey` : ce paramètre identifie un groupe de messages
- `gcmDelayWhileIdle` : lorsque ce paramètre a pour valeur true, il indique que le message ne doit pas être envoyé tant que le périphérique n'est pas actif.
- `gcmPriority` : définit la priorité du message.
- `gcmTimeToLive` : ce paramètre spécifie le nombre de secondes pendant lesquelles le message doit être conservé dans le stockage GCM si le périphérique est hors ligne.
- `apnsBadge` : numéro à afficher en tant que badge de l'icône d'application.
- `apnsCategory` : identificateur de catégorie à utiliser pour les notifications push interactives.
- `apnsIosActionKey` : titre de la clé d'action.
- `apnsPayload` : contenu JSON personnalisé qui sera envoyé dans le cadre du message de notification.
- `apnsType` : ['DEFAULT', 'MIXED', 'SILENT'].
- `apnsSound` : nom du fichier son dans l'ensemble d'applications. Le son de ce fichier est utilisé pour une alerte.

Voici un exemple d'envoi d'une notification push depuis le package de notification push.

1. Envoyez une notification push à l'aide de l'action `sendMessage` dans la liaison de package que vous avez créée précédemment. Prenez soin de remplacer `/nomEspaceNom/monPush` par votre nom de package.

  ```
  wsk action invoke /nomEspaceNom/monPush/sendMessage --blocking --result  -p url https://exemple.com -p text "ceci est mon message"  -p sound
nomFichierSon -p deviceIds '["T1","T2"]'
  ```
  {: pre}

  ```
  {
  "result": {
  "pushResponse": "{"messageId":"11111H","message":{"message":{"alert":"ceci est mon message","url":"http.google.com"},"settings":{"apns":{"sound":"default"},"gcm":{"sound":"default"},"target":{"deviceIds":["T1","T2"]}}}"
  },
      "status": "success",
      "success": true
  }
  ```
  {: screen}

### Exécution d'un événement déclencheur sur une activité Push
{: #openwhisk_catalog_pushnotifications_fire}

`/whisk.system/pushnotifications/webhook` configure le service Push pour qu'il exécute un déclencheur lorsqu'il existe une activité de périphérique, telle qu'un enregistrement ou une annulation d'enregistrement ou un abonnement ou une annulation d'abonnement de périphérique dans une application spécifiée.

Les paramètres sont les suivants :

- `appId :` identificateur global unique d'application Bluemix.
- `appSecret :` valeur confidentielle d'application du service de notification push Bluemix.
- `events :` les événements pris en charge sont `onDeviceRegister`, `onDeviceUnregister`, `onDeviceUpdate`, `onSubscribe`, `onUnsubscribe`. Pour être avertis de tous les événements, utilisez le caractère générique `*`.

Voici un exemple de création d'un déclencheur qui sera exécuté chaque fois qu'un nouveau périphérique est enregistré avec l'application Push Notifications :

1. Créez une liaison de package configurée pour votre service Push Notifications avec vos paramètres appId et appSecret.

  ```
  wsk package bind /whisk.system/pushnotifications monNouveauFluxPériphérique --param appID monapp --param appSecret mavaleurconfapp --param
events onDeviceRegister
  ```
  {: pre}

2. Créez un déclencheur pour le type d'événement `onDeviceRegister` du service Push Notifications en utilisant votre flux `monPush/webhook`.

  ```
  wsk trigger create monDéclencheurPush --feed myPush/webhook --param events onDeviceRegister
  ```
  {: pre}
