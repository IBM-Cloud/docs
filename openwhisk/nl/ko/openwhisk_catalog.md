---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 사전 설치된 OpenWhisk 패키지
{: #openwhisk_ecosystem}

{{site.data.keyword.openwhisk}}에서 패키지 카탈로그는 유용한 기능으로 앱을 강화하고 에코시스템 내에서 외부 서비스에 액세스할 수 있는 쉬운 방법을 제공합니다. {{site.data.keyword.openwhisk_short}} 사용이 가능한 외부 서비스의 예는 Cloudant, Message Hub, Watson, The Weather Company, Slack, GitHub 등입니다.
{: shortdesc}

카탈로그는 `/whisk.system` 네임스페이스에서 패키지로 사용 가능합니다. 명령행 도구를 사용하여 카탈로그를 찾는 방법에 대한 정보는 [패키지 찾아보기](./packages.md#browsing-packages)를 참조하십시오.

## 카탈로그의 기존 패키지
{: notoc}

| 패키지 | 설명 |
| --- | --- |
| [/whisk.system/alarms](./openwhisk_alarms.html) | 주기적 트리거를 작성하기 위한 패키지 |
| [/whisk.system/cloudant](./openwhisk_cloudant.html) | [Cloudant noSQL DB](https://console.ng.bluemix.net/docs/services/Cloudant/index.html) 서비스 작업을 위한 패키지 |
| [/whisk.system/github](./openwhisk_github.html) | [GitHub](https://developer.github.com/)에 대한 webhook 트리거 작성을 위한 패키지 |
| [/whisk.system/messaging](./openwhisk_messagehub.html) | [Message Hub](https://console.ng.bluemix.net/docs/services/MessageHub/index.html) 서비스 작업을 위한 패키지 |
| [/whisk.system/pushnotifications](./openwhisk_pushnotifications.html) | [Push Notification](https://console.ng.bluemix.net/docs/services/mobilepush/index.html) 서비스 작업을 위한 패키지 |
| [/whisk.system/slack](./openwhisk_slack.html) | [Slack APIs](https://api.slack.com/)에 게시하기 위한 패키지 |
| [/whisk.system/watson-translator](./openwhisk_watson_translator.html) | [텍스트 번역 및 언어 식별](https://www.ibm.com/watson/developercloud/language-translator.html)을 위한 패키지 |
| [/whisk.system/watson-speechToText](./openwhisk_watson_speechtotext.html) | [음성을 텍스트로](https://www.ibm.com/watson/developercloud/speech-to-text.html) 변환하기 위한 패키지 |
| [/whisk.system/watson-textToSpeech](./openwhisk_watson_texttospeech.html) | [텍스트를 음성으로 ](https://www.ibm.com/watson/developercloud/text-to-speech.html) 변환하기 위한 패키지 |
| [/whisk.system/weather](./openwhisk_weather.html) | [Weather Company Data](https://console.ng.bluemix.net/docs/services/Weather/index.html) 서비스 작업을 위한 패키지 |
| [/whisk.system/websocket](./openwhisk_websocket.html) | [Web Socket](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) 서버 작업을 위한 패키지 |
