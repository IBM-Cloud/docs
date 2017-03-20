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

# Watson Speech to Text パッケージの使用
{: #openwhisk_catalog_watson_texttospeech}

`/whisk.system/watson-speechToText` パッケージを利用して、スピーチをテキストに変換するための Watson API を簡単に呼び出すことができます。

このパッケージには、以下のアクションが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/watson-speechToText` | パッケージ | username、password | スピーチをテキストに変換するパッケージ |
| `/whisk.system/watson-speechToText/speechToText` | アクション | payload、content_type、encoding、username、password、continuous、inactivity_timeout、interim_results、keywords、keywords_threshold、max_alternatives、model、timestamps、watson-token、word_alternatives_threshold、word_confidence、X-Watson-Learning-Opt-Out | 音声のテキストへの変換 |

**注:** パッケージ `/whisk.system/watson` は、アクション `/whisk.system/watson/speechToText` を含め、非推奨です。

## Bluemix での Watson Speech to Text パッケージのセットアップ

Bluemix から OpenWhisk を使用している場合、Bluemix Watson サービス・インスタンスのパッケージ・バインディングは OpenWhisk が自動的に作成します。

1. Bluemix [ダッシュボード](http://console.ng.Bluemix.net)で Watson Speech to Text のサービス・インスタンスを作成します。
  
  サービス・インスタンスの名前、およびユーザーが所属している Bluemix の組織とスペースの名前を忘れないようにしてください。
  
2. 名前空間でパッケージを最新表示します。最新表示により、ユーザーが作成した Watson サービス・インスタンスのパッケージ・バインディングが自動的に作成されます。
  
  ```
wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_SpeechToText_Credentials-1
  ```
  ```
wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_SpeechToText_Credentials-1 private
  ```
  

## Bluemix 外部での Watson Speech to Text パッケージのセットアップ

Bluemix で OpenWhisk を使用していない場合、または Bluemix の外部で Watson Speech to Text をセットアップしたい場合は、Watson Speech to Text サービスのパッケージ・バインディングを手動で作成する必要があります。Watson Speech to Text サービスのユーザー名とパスワードが必要になります。

- Watson Speech to Text サービス用に構成されるパッケージ・バインディングを作成します。
  
  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonSpeechToText -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}
  

## スピーチのテキストへの変換

`/whisk.system/watson-speechToText/speechToText` アクショ
ンは 音声スピーチをテキストに変換します。パラメーターは次のとおりです。


- `username`: Watson API ユーザー名。
- `password`: Watson API パスワード。
- `payload`: テキストに変換するエンコード・ス
ピーチ・バイナリー・データ。
- `content_type`: 音声の MIME タイプ。
- `encoding`: スピーチ・バイナリー・データの
エンコード。
- `continuous`: 長い休止で区切られた連続する句を示す複数の最終結果が返されるかどうかを示します。
- `inactivity_timeout`: 送信された音声に音声が検出されない場合に、この時間 (秒数) が経過すると、接続がクローズされます。
- `interim_results`: サービスが暫定の結果を返すかどうかを示します。
- `keywords`: 音声で特定するキーワードのリスト。
- `keywords_threshold`: キーワードを特定するための下限である信頼値。
- `max_alternatives`: 返される代替トランスクリプトの最大数。
- `model`: 認識要求のために使用されるモデルの識別子。
- `timestamps`: 単語ごとにタイム・アライメントが返されるかどうかを示します。
- `watson-token`: サービス資格情報を指定する代わりとして、サービスに認証トークンを指定します。
- `word_alternatives_threshold`: 可能な単語の代替として仮説を識別するための下限である信頼値。
- `word_confidence`: 単語ごとに信頼度の指標を 0 から 1 の範囲で返すかどうかを示します。
- `X-Watson-Learning-Opt-Out`: 呼び出しのデータ収集をオプトアウトするかどうかを示します。
 

- パッケージ・バインディングで
`speechToText` アクションを起動して、エンコードされ
た音声を変換します。
  
  ```
  wsk action invoke myWatsonSpeechToText/speechToText --blocking --result --param payload <base64 encoding of a .wav file> --param content_type 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```json
  {
          "data": "Hello Watson"
  }
  ```
  
