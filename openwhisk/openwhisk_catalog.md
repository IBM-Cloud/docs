---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Pre-installed OpenWhisk Packages
{: #openwhisk_ecosystem}

In {{site.data.keyword.openwhisk}}, a catalog of packages gives you an easy way to enhance your app with useful capabilities, and to access external services in the ecosystem. Examples of external services that are {{site.data.keyword.openwhisk_short}}-enabled include Cloudant, Message Hub, Watson, The Weather Company, Slack, GitHub and others.
{: shortdesc}

The catalog is available as packages in the `/whisk.system` namespace. See [Browsing packages](./packages.md#browsing-packages) for information about how to browse the catalog by using the command line tool.

## Existing packages in catalog
{: notoc}

| Package | Description |
| --- | --- |
| [/whisk.system/alarms](./openwhisk_alarms.html) | Package to create periodic triggers |
| [/whisk.system/cloudant](./openwhisk_cloudant.html) | Package to work with [Cloudant noSQL DB](https://console.ng.bluemix.net/docs/services/Cloudant/index.html) service |
| [/whisk.system/github](./openwhisk_github.html) | Package to create webhook triggers for [GitHub](https://developer.github.com/) |
| [/whisk.system/messaging](./openwhisk_messagehub.html) | Package to work with [Message Hub](https://console.ng.bluemix.net/docs/services/MessageHub/index.html) service |
| [/whisk.system/pushnotifications](./openwhisk_pushnotifications.html) | Package to work with [Push Notification](https://console.ng.bluemix.net/docs/services/mobilepush/index.html) service |
| [/whisk.system/slack](./openwhisk_slack.html) | Package to post to the [Slack APIs](https://api.slack.com/) |
| [/whisk.system/watson-translator](./openwhisk_watson_translator.html) | Package for [text translation and language identification](https://www.ibm.com/watson/developercloud/language-translator.html) |
| [/whisk.system/watson-speechToText](./openwhisk_watson_speechtotext.html) | Package to convert [speech into text](https://www.ibm.com/watson/developercloud/speech-to-text.html) |
| [/whisk.system/watson-textToSpeech](./openwhisk_watson_texttospeech.html) | Package to convert [text into speech](https://www.ibm.com/watson/developercloud/text-to-speech.html) |
| [/whisk.system/weather](./openwhisk_weather.html) | Package to work with [Weather Company Data](https://console.ng.bluemix.net/docs/services/Weather/index.html) service |
| [/whisk.system/websocket](./openwhisk_websocket.html) | Package to work with a [Web Socket](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) server |
