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

# 事前インストール済み OpenWhisk パッケージ
{: #openwhisk_ecosystem}

{{site.data.keyword.openwhisk}} で、パッケージ・カタログは、便利な機能でアプリを強化して、エコシステム内の外部サービスにアクセスするための簡単な方法を提供します。{{site.data.keyword.openwhisk_short}} 対応の外部サービスの例として、Cloudant、Message Hub、Watson、The Weather Company、Slack、GitHub などがあります。
{: shortdesc}

カタログは、`/whisk.system` 名前空間でパッケージとして使用可能です。コマンド・ライン・ツールを使用したカタログの参照方法については、[パッケージの参照](./packages.md#browsing-packages)を参照してください。

## カタログにある既存パッケージ
{: notoc}

| パッケージ | 説明 |
| --- | --- |
| [/whisk.system/alarms](./openwhisk_alarms.html) | 定期的トリガーを作成するためのパッケージ |
| [/whisk.system/cloudant](./openwhisk_cloudant.html) | [Cloudant noSQL DB](https://console.ng.bluemix.net/docs/services/Cloudant/index.html) サービスを使用した処理を行うためのパッケージ |
| [/whisk.system/github](./openwhisk_github.html) | [GitHub](https://developer.github.com/) の Web フック・トリガーを作成するためのパッケージ |
| [/whisk.system/messaging](./openwhisk_messagehub.html) | [Message Hub](https://console.ng.bluemix.net/docs/services/MessageHub/index.html) サービスを使用した処理を行うためのパッケージ |
| [/whisk.system/pushnotifications](./openwhisk_pushnotifications.html) | [Push Notification](https://console.ng.bluemix.net/docs/services/mobilepush/index.html) サービスを使用した処理を行うためのパッケージ |
| [/whisk.system/slack](./openwhisk_slack.html) | [Slack API](https://api.slack.com/) を POST するためのパッケージ |
| [/whisk.system/watson-translator](./openwhisk_watson_translator.html) | [テキスト翻訳および言語識別](https://www.ibm.com/watson/developercloud/language-translator.html)のパッケージ |
| [/whisk.system/watson-speechToText](./openwhisk_watson_speechtotext.html) | [スピーチをテキスト](https://www.ibm.com/watson/developercloud/speech-to-text.html)に変換するパッケージ |
| [/whisk.system/watson-textToSpeech](./openwhisk_watson_texttospeech.html) | [テキストをスピーチ](https://www.ibm.com/watson/developercloud/text-to-speech.html)に変換するパッケージ |
| [/whisk.system/weather](./openwhisk_weather.html) | [Weather Company Data](https://console.ng.bluemix.net/docs/services/Weather/index.html) サービスを使用した処理を行うためのパッケージ |
| [/whisk.system/websocket](./openwhisk_websocket.html) | [Web Socket](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) サーバーを使用した処理を行うためのパッケージ |
