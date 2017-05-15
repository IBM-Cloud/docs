---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Packages OpenWhisk préinstallés
{: #openwhisk_ecosystem}

Dans {{site.data.keyword.openwhisk}}, un catalogue de packages permet d'améliorer facilement votre application en ajoutant des fonctions utiles. Il permet également d'accéder à des services externes dans l'écosystème. Cloudant, Message Hub, Watson, The Weather Company, Slack, Github, etc. sont des exemples de service externe compatibles avec {{site.data.keyword.openwhisk_short}}.
{: shortdesc}

Le catalogue est disponible sous forme de packages dans l'espace de nom `/whisk.system`. Voir [Parcours des packages](./packages.md#browsing-packages) pour des informations sur le parcours du catalogue à l'aide de l'outil de ligne de commande.

## Packages existants dans le catalogue
{: notoc}

| Package | Description |
| --- | --- |
| [/whisk.system/alarms](./openwhisk_alarms.html) | Package permettant de créer des déclencheurs périodiques |
| [/whisk.system/cloudant](./openwhisk_cloudant.html) | Package permettant d'utiliser un service [Cloudant noSQL DB](https://console.ng.bluemix.net/docs/services/Cloudant/index.html) |
| [/whisk.system/github](./openwhisk_github.html) | Package permettant de créer des déclencheurs webhook pour [GitHub](https://developer.github.com/) |
| [/whisk.system/messaging](./openwhisk_messagehub.html) | Package permettant d'utiliser le service [Message Hub](https://console.ng.bluemix.net/docs/services/MessageHub/index.html) |
| [/whisk.system/pushnotifications](./openwhisk_pushnotifications.html) | Package permettant d'utiliser le service [Push Notification](https://console.ng.bluemix.net/docs/services/mobilepush/index.html) |
| [/whisk.system/slack](./openwhisk_slack.html) | Package permettant d'effectuer des publications sur les [API Slack](https://api.slack.com/) |
| [/whisk.system/watson-translator](./openwhisk_watson_translator.html) | Package pour [la traduction d'un texte et l'identification d'une langue](https://www.ibm.com/watson/developercloud/language-translator.html) |
| [/whisk.system/watson-speechToText](./openwhisk_watson_speechtotext.html) | Package permettant de convertir [la parole en texte](https://www.ibm.com/watson/developercloud/speech-to-text.html) |
| [/whisk.system/watson-textToSpeech](./openwhisk_watson_texttospeech.html) | Package permettant de convertir [le texte en parole](https://www.ibm.com/watson/developercloud/text-to-speech.html) |
| [/whisk.system/weather](./openwhisk_weather.html) | Package permettant d'utiliser le service [Weather Company Data](https://console.ng.bluemix.net/docs/services/Weather/index.html) |
| [/whisk.system/websocket](./openwhisk_websocket.html) | Package permettant d'utiliser le serveur [Web Socket](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) |
