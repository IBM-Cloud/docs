---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 預先安裝的 OpenWhisk 套件
{: #openwhisk_ecosystem}

在 {{site.data.keyword.openwhisk}} 中，套件的型錄可讓您輕鬆地使用有用的功能來加強應用程式，以及在生態系統中存取外部服務。啟用 {{site.data.keyword.openwhisk_short}} 功能的外部服務範例包括 Cloudant、Message Hub、Watson、The Weather Company、Slack、GitHub 及其他服務。
{: shortdesc}

在 `/whisk.system` 名稱空間中，型錄可當作套件使用。如需如何使用指令行工具來瀏覽型錄的相關資訊，請參閱[瀏覽套件](./packages.md#browsing-packages)。

## 型錄中的現有套件
{: notoc}

| 套件 | 說明 |
| --- | --- |
| [/whisk.system/alarms](./openwhisk_alarms.html) | 建立定期觸發程式的套件 |
| [/whisk.system/cloudant](./openwhisk_cloudant.html) | 使用 [Cloudant noSQL DB](https://console.ng.bluemix.net/docs/services/Cloudant/index.html) 服務的套件 |
| [/whisk.system/github](./openwhisk_github.html) | 建立 [GitHub](https://developer.github.com/) 的 Webhook 觸發程式的套件 |
| [/whisk.system/messaging](./openwhisk_messagehub.html) | 使用 [Message Hub](https://console.ng.bluemix.net/docs/services/MessageHub/index.html) 服務的套件 |
| [/whisk.system/pushnotifications](./openwhisk_pushnotifications.html) | 使用 [Push Notification](https://console.ng.bluemix.net/docs/services/mobilepush/index.html) 服務的套件 |
| [/whisk.system/slack](./openwhisk_slack.html) | 張貼至 [Slack API](https://api.slack.com/) 的套件 |
| [/whisk.system/watson-translator](./openwhisk_watson_translator.html) | [文字翻譯及語言識別](https://www.ibm.com/watson/developercloud/language-translator.html)的套件 |
| [/whisk.system/watson-speechToText](./openwhisk_watson_speechtotext.html) | 將[語音轉換為文字](https://www.ibm.com/watson/developercloud/speech-to-text.html)的套件 |
| [/whisk.system/watson-textToSpeech](./openwhisk_watson_texttospeech.html) | 將[文字轉換為語音](https://www.ibm.com/watson/developercloud/text-to-speech.html)的套件 |
| [/whisk.system/weather](./openwhisk_weather.html) | 使用 [Weather Company Data](https://console.ng.bluemix.net/docs/services/Weather/index.html) 服務的套件 |
| [/whisk.system/websocket](./openwhisk_websocket.html) | 使用 [Web Socket](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) 伺服器的套件 |
