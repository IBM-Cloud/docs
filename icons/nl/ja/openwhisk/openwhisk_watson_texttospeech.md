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

# Watson Text to Speech パッケージの使用
{: #openwhisk_catalog_watson_texttospeech}

`/whisk.system/watson-textToSpeech` パッケージを利用して、テキストをスピーチに変換するための Watson API を簡単に呼び出すことができます。

このパッケージには、以下のアクションが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/watson-textToSpeech` | パッケージ | username、password | テキストをスピーチに変換するパッケージ |
| `/whisk.system/watson-textToSpeech/textToSpeech` | アクション | payload、voice、accept、encoding、username、password | テキストの音声への変換 |

**注:** パッケージ `/whisk.system/watson` は、アクション `/whisk.system/watson/textToSpeech` を含め、非推奨です。

## Bluemix での Watson Text to Speech パッケージのセットアップ

Bluemix から OpenWhisk を使用している場合、Bluemix Watson サービス・インスタンスのパッケージ・バインディングは OpenWhisk が自動的に作成します。

1. Bluemix [ダッシュボード](http://console.ng.Bluemix.net)で Watson Text to Speech のサービス・インスタンスを作成します。
  
  サービス・インスタンスの名前、およびユーザーが所属している Bluemix の組織とスペースの名前を忘れないようにしてください。
  
2. 名前空間でパッケージを最新表示します。最新表示により、ユーザーが作成した Watson サービス・インスタンスのパッケージ・バインディングが自動的に作成されます。
  
  ```
wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_TextToSpeech_Credentials-1
  ```
  ```
wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_TextToSpeec_Credentials-1 private
  ```
  
  
## Bluemix 外部での Watson Text to Speech パッケージのセットアップ

Bluemix で OpenWhisk を使用していない場合、または Bluemix の外部で Watson Text to Speech をセットアップしたい場合は、Watson Text to Speech サービスのパッケージ・バインディングを手動で作成する必要があります。Watson Text to Speech サービスのユーザー名とパスワードが必要になります。

- Watson Speech to Text サービス用に構成されるパッケージ・バインディングを作成します。
  
  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonTextToSpeech -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}
  

## テキストをスピーチに変換

`/whisk.system/watson-speechToText/textToSpeech` アクショ
ンはテキストを音声スピーチに変換します。パラメーターは次のとおりです。


- `username`: Watson API ユーザー名。
- `password`: Watson API パスワード。
- `payload`: スピーチに変換するテキスト。
- `voice`: スピーカーの音声。
- `accept`: スピーチ・ファイルの形式。
- `encoding`: スピーチ・バイナリー・データの
エンコード。


- パッケージ・バインディングで
`textToSpeech` アクションを起動して、テキストを変換
します。
  
  ```
  wsk action invoke myWatsonTextToSpeech/textToSpeech --blocking --result --param payload 'Hey.' --param voice 'en-US_MichaelVoice' --param accept 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```json
  {
          "payload": "<base64 encoding of a .wav file>"
  }
  ```
  
