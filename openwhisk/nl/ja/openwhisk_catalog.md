---

 

copyright:

  years: 2016
lastupdated: "2016-09-09"
 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 対応の {{site.data.keyword.Bluemix_notm}} サービスの使用
{: #openwhisk_ecosystem}

{{site.data.keyword.openwhisk}} で、パッケージ・カタログは、便利な機能でアプリを強化して、エコシステム内の外部サービスにアクセスするための簡単な方法を提供します。{{site.data.keyword.openwhisk_short}} 対応の外部サービスの例として、Cloudant、The Weather Company、Slack、GitHub などがあります。
{: shortdesc}

カタログは、`/whisk.system` 名前空間でパッケージとして使用可能です。コマンド・ライン・ツールを使用したカタログの参照方法については、[パッケージの参照](./openwhisk_packages.html#openwhisk_packagedisplay)を参照してください。

以降のトピックで、カタログの一部のパッケージについて説明します。

## Cloudant パッケージの使用
{: #openwhisk_catalog_cloudant}
`/whisk.system/cloudant` パッケージを使用すると、Cloudant データベースを処理することができます。これには、以下のアクションおよびフィードが含まれます。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | パッケージ | {{site.data.keyword.Bluemix_notm}}ServiceName、host、username、password、dbname、includeDoc、overwrite | Cloudant データベースを処理 |
| `/whisk.system/cloudant/read` | アクション | dbname、includeDoc、id | データベースから文書を読み取る |
| `/whisk.system/cloudant/write` | アクション | dbname、overwrite、doc | データベースに文書を書き込む |
| `/whisk.system/cloudant/changes` | フィード | dbname、includeDoc、maxTriggers | データベースの変更時にトリガー・イベントを発生させる |

以降のトピックでは、Cloudant データベースのセットアップ、関連付けられたパッケージの構成、および `/whisk.system/cloudant` パッケージのアクションとフィードの使用をウォークスルーします。

### {{site.data.keyword.Bluemix_notm}} での Cloudant データベースのセットアップ
{: #openwhisk_catalog_cloudant_in}

{{site.data.keyword.Bluemix}} から {{site.data.keyword.openwhisk_short}} を使用している場合、
{{site.data.keyword.openwhisk_short}} は {{site.data.keyword.Bluemix_notm}} Cloudant サービス・インスタンスのパッケージ・バインディングを自動的に作成します。{{site.data.keyword.Bluemix_notm}} から {{site.data.keyword.openwhisk_short}} および Cloudant を使用していない場合は、次のステップにスキップします。

1. {{site.data.keyword.Bluemix_notm}}[ ダッシュボード](http://console.ng.{{site.data.keyword.Bluemix_notm}}.net)で Cloudant サービス・インスタンスを作成します。

  サービス・インスタンスの名前、およびユーザーが所属している {{site.data.keyword.Bluemix_notm}} の組織とスペースの名前を忘れないようにしてください。

2. ご使用の {{site.data.keyword.openwhisk_short}} CLI が、前のステップで使用した {{site.data.keyword.Bluemix_notm}} 組織とスペースに対応する名前空間に存在するようにします。

  ```
  wsk property set --namespace my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space
  ```
  {: pre}

  あるいは、`wsk property set --namespace` を使用して、アクセス可能な名前空間のリストから名前空間を設定することができます。

3. 名前空間でパッケージを最新表示します。最新表示により、ユーザーが作成した Cloudant サービス・インスタンスのパッケージ・バインディングが自動的に作成されます。

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

  {{site.data.keyword.Bluemix_notm}} Cloudant サービス・インスタンスに対応するパッケージ・バインディングの完全修飾名が表示されます。

4. 前に作成されたパッケージ・バインディングが Cloudant {{site.data.keyword.Bluemix_notm}} サービス・インスタンスのホストと資格情報で構成されているかどうかを確認します。

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

### {{site.data.keyword.Bluemix_notm}} 外部の Cloudant データベースのセットアップ
{: #openwhisk_catalog_cloudant_outside}

{{site.data.keyword.Bluemix_notm}} で {{site.data.keyword.openwhisk_short}} を使用していない場合、
または {{site.data.keyword.Bluemix_notm}} の外部の Cloudant データベースをセットアップしたい場合は、Cloudant アカウントのパッケージ・バインディングを手動で作成する必要があります。
Cloudant のアカウント・ホスト名、ユーザー名、パスワードが必要です。

1. Cloudant アカウント用に構成されるパッケージ・バインディングを作成します。

  ```
  wsk package bind /whisk.system/cloudant myCloudant -p username MYUSERNAME -p password MYPASSWORD -p host MYCLOUDANTACCOUNT.cloudant.com
  ```
  {: pre}

2. パッケージ・バインディングが存在することを確認します。

  ```
wsk package list
  ```
  {: pre}
  ```
packages
  /myNamespace/myCloudant private binding
  ```
  {: screen}


### Cloudant データベースに対する変更の listen
{: #openwhisk_catalog_cloudant_listen}

`changes` フィードを使用して、Cloudant データベースが変更されるたびにトリガーを発生させるサービスを構成することができます。パラメーターは次のとおりです。


- `dbname`: Cloudant データベースの名前。
- `includeDoc`: true に設定すると、発生する各トリガー・イベントに、変更された Cloudant 文書が含まれます。 
- `maxTriggers`: この限界に達するとトリガーの発生を停止します。デフォルトは 1000 です。最大 10,000 に設定できます。10,000 を超える値に設定しようとすると、要求は拒否されます。

1. 前に作成したパッケージ・バインディングの `changes` フィードを使用してトリガーを作成します。`/myNamespace/myCloudant` を、ご使用のパッケージ名に置き換えてください。

  ```
wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb --param includeDoc true
  ```
  {: pre}
  ```
ok: created trigger feed myCloudantTrigger
  ```
  {: screen}

2. アクティベーションをポーリングします。

  ```
wsk activation poll
  ```
  {: pre}

3. Cloudant ダッシュボードで、既存の文書を変更するか、新しい文書を作成します。

4. 文書を変更するたびに、`myCloudantTrigger` トリガーの新規アクティベーションを監視します。

**注**: 新規アクティベーションを監視できない場合は、Cloudant データベースからの読み取りと Cloudant データベースへの書き込みに関する後続のセクションを参照してください。以下の読み取りおよび書き込みのステップを試してみると、Cloudant 資格情報が正しいことを確認するのに役立ちます。

これで、ルールを作成してアクションに関連付け、文書の更新に対応することができるようになります。

生成されたイベントのコンテンツは、トリガーを作成するときの `includeDoc` パラメーターの値によって異なります。パラメーターを true に設定すると、発生する各トリガー・イベントに、変更された Cloudant 文書が含まれます。たとえば、次の変更された文書を考えてみます。 

  ```
  {
    "_id": "6ca436c44074c4c2aa6a40c9a188b348",
    "_rev": "3-bc4960fc13aa368afca8c8427a1c18a8",
    "name": "Heisenberg"
  }
  ```
  {: screen}

この例のコードは、対応する `_id`、`_rev`、および `name` の各パラメーターを使用してトリガー・イベントを生成します。実際には、トリガー・イベントの JSON 表記は文書に一致します。

`includeDoc` が false の場合は、イベントに以下のパラメーターが含まれます。

- `id`: 文書 ID。
- `seq`: Cloudant によって生成されるシーケンス ID。
- `changes`: オブジェクトの配列。それぞれに文書の改訂 ID が含まれる `rev` フィールドがあります。

トリガー・イベントの JSON 表記は、以下のようになります。

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


### Cloudant データベースへの書き込み
{: #openwhisk_catalog_cloudant_write}

アクションを使用して `testdb` という Cloudant データベースに文書を格納することができます。このデータベースが、ご使用の Cloudant アカウントに必ず存在するようにしてください。

1. 前に作成したパッケージ・バインディングの `write` アクションを使用して、文書を格納します。
`/myNamespace/myCloudant` を、ご使用のパッケージ名に置き換えてください。

  ```
  wsk action invoke /myNamespace/myCloudant/write --blocking --result --param dbname testdb --param doc "{\"_id\":\"heisenberg\",\"name\":\"Walter White\"}"
  ```
  {: pre}
  ```
  ok: invoked /myNamespace/myCloudant/write with id 62bf696b38464fd1bcaff216a68b8287
  {
    "id": "heisenberg",
    "ok": true,
    "rev": "1-9a94fb93abc88d8863781a248f63c8c3"
  }
  ```
  {: screen}

2. Cloudant ダッシュボードで参照して、文書が存在していることを確認します。

  `testdb` データベースのダッシュボード URL は、
`https://MYCLOUDANTACCOUNT.cloudant.com/dashboard.html#database/testdb/_all_docs?limit=100` のようになります。


### Cloudant データベースからの読み取り
{: #openwhisk_catalog_cloudant_read}

アクションを使用して `testdb` という Cloudant データベースから文書を取り出すことができます。このデータベースが、ご使用の Cloudant アカウントに必ず存在するようにしてください。

1. 前に作成したパッケージ・バインディングの `read` アクションを使用して、文書を取り出します。
`/myNamespace/myCloudant` を、ご使用のパッケージ名に置き換えてください。

  ```
  wsk action invoke /myNamespace/myCloudant/read --blocking --result --param dbname testdb --param id heisenberg
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


## Alarm パッケージの使用
{: #openwhisk_catalog_alarm}

`/whisk.system/alarms` パッケージを使用して、指定した頻度でトリガーを発生させることができます。これは、1 時間ごとにシステム・バックアップ・アクションを起動するといった、ジョブやタスクの繰り返しをセットアップする際に便利です。

このパッケージには、以下のフィードが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | パッケージ | - | アラームおよび定期的ユーティリティー |
| `/whisk.system/alarms/alarm` | フィード | cron、trigger_payload、maxTriggers | トリガー・イベントを定期的に発生させる |


### トリガー・イベントの定期的な発生
{: #openwhisk_catalog_alarm_fire}

 `/whisk.system/alarms/alarm` フィードは、
Alarm サービスを構成して、指定した頻度でトリガー・イベントを発生させます。パラメーターは次のとおりです。


- `cron`: トリガーを発生させるタイミングを協定世界時 (UTC) で示す、UNIX crontab 構文に基づいたストリング。このストリングは、`X X X X X X ` のようにスペースで区切られた 6 個のフィールドのシーケンスです。cron 構文の使用について詳しくは、https://github.com/ncb000gt/node-cron を参照してください。ストリングで示される頻度のいくつかの例を以下に示しま す。

  - `* * * * * *`: 毎秒。
  - `0 * * * * *`: 毎分の先頭。
  - `* 0 * * * *`: 毎時の先頭。
  - `0 0 9 8 * *`: 毎月 8 日目の午前 9:00:00 (UTC)

- `trigger_payload`: このパラメーターの値は、
トリガーが発生するたびにトリガーのコンテンツになります。

- `maxTriggers`: この限界に達するとトリガーの発生を停止します。デフォルトは 1000 です。最大 10,000 に設定できます。10,000 を超える値に設定しようとすると、要求は拒否されます。

以下は、トリガー・イベントに `name` と `place` の値を指定して、20 秒ごとに 1 回発生するトリガーを作成する例です。

  ```
  wsk trigger create periodic --feed /whisk.system/alarms/alarm --param cron "*/20 * * * * *" --param trigger_payload "{\"name\":\"Odin\",\"place\":\"Asgard\"}"
  ```
  {: pre}

生成される各イベントは、`trigger_payload` の値に指定されるプロパティーをパラメーターとして含みます。この場合、各トリガー・イベントは、
パラメーター `name=Odin` と `place=Asgard` を含みます。


## Weather パッケージの使用
{: #openwhisk_catalog_weather}

`/whisk.system/weather` パッケージは、Weather Company Data for IBM Bluemix API を呼び出すのに便利な方法を提供します。

このパッケージには、以下のアクションが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/weather` | パッケージ | username、password | Weather Company Data for IBM Bluemix API からのサービス  |
| `/whisk.system/weather/forecast` | アクション | latitude、longitude、timePeriod | 指定された時間枠の予測|

`username` と `password` の値を使用して、パッケージ・バインディングを作成することをお勧めします。この方法を使用すると、パッケージ内のアクションを起動するたびに資格情報を指定する必要はありません。

### 場所を指定した天気予報の取得
{: #openwhisk_catalog_weather_forecast}

`/whisk.system/weather/forecast` アクション
は、The Weather Company から API を呼び出して、場所を指定した天気予報を返します。パラメーターは次のとおりです。


- `username`: 予測 API を起動する権限を与えられた Weather Company Data for IBM Bluemix のユーザー名。
- `password`: 予測 API を起動する権限を与えられた Weather Company Data for IBM Bluemix のパスワード。
- `latitude`: 場所の経度の座標。
- `longitude`: 場所の緯度の座標。
- `timeperiod`: 予測の時間枠。有効なオプションは、デフォルトの「10 日間」(毎日の予測を 10 日間返す)、「48 時間」(毎時の予測を 2 日間返す)、「現在」(現在の天気状況を返す)、「時系列」(現在の日時から、現在の観測と過去 24 時間までの観測の両方を返す) です。


以下は、パッケージ・バインディングを作成してから 10 日間の予測を取得する例です。

1. API キーを使用してパッケージ・バインディングを作成します。

  ```
  wsk package bind /whisk.system/weather myWeather --param username MY_USERNAME --param password MY_PASSWORD
  ```
  {: pre}

2. パッケージ・バインディングの `forecast` アクションを起動して、天気予報を取得します。

  ```
  wsk action invoke myWeather/forecast --blocking --result --param latitude 43.7 --param longitude -79.4
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


## Watson パッケージの使用
{: #openwhisk_catalog_watson}

`/whisk.system/watson` パッケージは、各種の Watson API を呼び出すために便利な方法を提供します。

このパッケージには、以下のアクションが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/watson` | パッケージ | username、password | Watson 分析 API のアクション |
| `/whisk.system/watson/translate` | アクション | translateFrom、translateTo、translateParam、username、password | テキストの変換 |
| `/whisk.system/watson/languageId` | アクション | payload、username、password | 言語の識別 |
| `/whisk.system/watson/speechToText` | アクション | payload、content_type、encoding、username、password、continuous、inactivity_timeout、interim_results、keywords、keywords_threshold、max_alternatives、model、timestamps、watson-token、word_alternatives_threshold、word_confidence、X-Watson-Learning-Opt-Out | 音声のテキストへの変換 |
| `/whisk.system/watson/textToSpeech` | アクション | payload、voice、accept、encoding、username、password | テキストの音声への変換 |

`username` と `password` の値を使用して、パッケージ・バインディングを作成することをお勧めします。この方法を使用すると、パッケージ内のアクションを起動するたびにこれらの資格情報を指定する必要はありません。

### テキストの変換
{: #openwhisk_catalog_watson_translate}

`/whisk.system/watson/translate` アクションは、テキストをある言語から別の言語に変換します。パラメーターは次のとおりです。


- `username`: Watson API ユーザー名。
- `password`: Watson API パスワード。
- `translateParam`: 変換するテキストを示す入力パラメーター。例えば、`translateParam=payload` の場合は、アクションに渡される `payload` パラメーターの値が変換されます。
- `translateFrom`: ソース言語の 2 桁のコード。
- `translateTo`: ターゲット言語の 2 桁のコード。

以下は、パッケージ・バインディングを作成してテキストを変換する例です。

1. Watson の資格情報を使用してパッケージ・バインディングを作成します。

  ```
  wsk package bind /whisk.system/watson myWatson --param username MY_WATSON_USERNAME --param password MY_WATSON_PASSWORD
  ```
  {: pre}

2. パッケージ・バインディングの `translate` アクションを起動して、テキストを英語からフランス語に変換します。

  ```
  wsk action invoke myWatson/translate --blocking --result --param payload "Blue skies ahead" --param translateParam payload --param translateFrom en --param translateTo fr
  ```
  {: pre}

  ```
  {
      "payload": "Ciel bleu a venir"
  }
  ```
  {: screen}


### テキストの言語の識別
{: #openwhisk_catalog_watson_identifylang}

`/whisk.system/watson/languageId` アクションは、テキストの言語を識別します。パラメーターは次のとおりです。


- `username`: Watson API ユーザー名。
- `password`: Watson API パスワード。
- `payload`: 識別するテキスト。

以下は、パッケージ・バインディングを作成してテキストの言語を識別する例です。

1. Watson の資格情報を使用してパッケージ・バインディングを作成します。

  ```
  wsk package bind /whisk.system/watson myWatson -p username MY_WATSON_USERNAME -p password MY_WATSON_PASSWORD
  ```
  {: pre}

2. パッケージ・バインディングの `languageId` アクションを起動して、言語を識別します。

  ```
  wsk action invoke myWatson/languageId --blocking --result --param payload "Ciel bleu a venir"
  ```
  {: pre}
  ```
  {
    "payload": "Ciel bleu a venir",
    "language": "fr",
    "confidence": 0.710906
  }
  ```
  {: screen}


### テキストをスピーチに変換
{: #openwhisk_catalog_watson_texttospeech}

`/whisk.system/watson/textToSpeech` アクショ
ンはテキストを音声スピーチに変換します。パラメーターは次のとおりです。


- `username`: Watson API ユーザー名。
- `password`: Watson API パスワード。
- `payload`: スピーチに変換するテキスト。
- `voice`: スピーカーの音声。
- `accept`: スピーチ・ファイルの形式。
- `encoding`: スピーチ・バイナリー・データの
エンコード。

以下は、パッケージ・バインディングを作成してテキストをスピーチに変換する例です。

1. Watson の資格情報を使用してパッケージ・バインディングを作成します。

  ```
  wsk package bind /whisk.system/watson myWatson -p username MY_WATSON_USERNAME -p password MY_WATSON_PASSWORD
  ```
  {: pre}

2. パッケージ・バインディングで
`textToSpeech` アクションを起動して、テキストを変換
します。

  ```
  wsk action invoke myWatson/textToSpeech --blocking --result --param payload Hey. --param voice en-US_MichaelVoice --param accept audio/wav --param encoding base64
  ```
  {: pre}
  ```
  {
        "payload": "<base64 encoding of a .wav file>"
  }
  ```
  {: screen}


### スピーチのテキストへの変換
{: #openwhisk_catalog_watson_speechtotext}

`/whisk.system/watson/speechToText` アクショ
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
 
以下は、パッケージ・バインディングを作成してスピーチをテキストに変換する例です。

1. Watson の資格情報を使用してパッケージ・バインディングを作成します。

  ```
  wsk package bind /whisk.system/watson myWatson -p username MY_WATSON_USERNAME -p password MY_WATSON_PASSWORD
  ```
  {: pre}

2. パッケージ・バインディングで
`speechToText` アクションを起動して、エンコードされ
た音声を変換します。

  ```
  wsk action invoke myWatson/speechToText --blocking --result --param payload <base64 encoding of a .wav file> --param content_type audio/wav --param encoding base64
  ```
  {: pre}
  ```
  {
        "data": "Hello Watson"
  }
  ```
  {: screen}
  
 
## Slack パッケージの使用
{: #openwhisk_catalog_slack}

`/whisk.system/slack` パッケージは、
[Slack API](https://api.slack.com/) を使用する便利な方法を提供します。

このパッケージには、以下のアクションが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/slack` | パッケージ | url、channel、username | Slack API と対話 |
| `/whisk.system/slack/post` | アクション | text、url、channel、username | Slack チャネルへメッセージをポスト |

`username`、`url`、および `channel` の各値を使用してパッケージ・バインディングを作成することをお勧めします。バインディングを使用すると、パッケージでアクションを起動するたびに値を指定する必要はありません。

### Slack チャネルへのメッセージのポスト
{: #openwhisk_catalog_slack_post}

`/whisk.system/slack/post` アクションは、指定された Slack チャネルにメッセージをポストします。パラメーターは次のとおりです。


- `url`: Slack の Webhook URL。
- `channel`: メッセージのポスト先の Slack チャネル。
- `username`: メッセージをポストするユーザーの名前。
- `text`: ポストするメッセージ。
- `token`: (オプション) Slack [アクセス・トークン](https://api.slack.com/tokens)。Slack アクセス・トークンの使用について詳しくは、[以下](./openwhisk_catalog.html#openwhisk_catalog_slack_token)を参照してください。

以下は、Slack を構成し、パッケージ・バインディングを作成して、
メッセージをチャネルにポストする例です。

1. チームに Slack の [Incoming Webhook](https://api.slack.com/incoming-webhooks) を構成します。

  Slack の構成後、`https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc` のような Web フック URL を取得します。これは次のステップで必要になります。

2. Slack の資格情報、ポスト先のチャネル、およびポストするユーザー名を指定して、パッケージ・バインディングを作成します。

  ```
  wsk package bind /whisk.system/slack mySlack --param url "https://hooks.slack.com/services/..." --param username Bob --param channel "#MySlackChannel"
  ```
  {: pre}

3. パッケージ・バインディングの `post` アクションを起動し、ご使用の Slack チャネルにメッセージをポストします。

  ```
  wsk action invoke mySlack/post --blocking --result --param text "Hello from OpenWhisk!"
  ```
  {: pre}

### Slack トークン・ベースの API の使用
{: #openwhisk_catalog_slack_token}

オプションで、webhook API ではなく、Slack のトークン・ベース API を使用することを選択できます。そうするよう選択した場合、Slack [アクセス・トークン](https://api.slack.com/tokens)を含んでいる `token` パラメーターを渡します。次に、任意の [Slack API メソッド](https://api.slack.com/methods)を `url` パラメーターとして使用します。例えば、メッセージをポストするために、`url` パラメーター値 [slack.postMessage](https://api.slack.com/methods/chat.postMessage) を使用します。

## GitHub パッケージの使用
{: #openwhisk_catalog_github}

`/whisk.system/github` パッケージは、
[GitHub API](https://developer.github.com/) を使用するための便利な方法を提供します。

このパッケージには、以下のフィードが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/github` | パッケージ | username、repository、accessToken | GitHub API と対話 |
| `/whisk.system/github/webhook` | フィード | events、username、repository、accessToken | GitHub アクティビティーでトリガー・イベントを発生させる |

`username`、`repository`、および `accessToken` の各値を使用してパッケージ・バインディングを作成することをお勧めします。バインディングを使用すると、パッケージのフィードを使用するたびに値を指定する必要はありません。

### GitHub アクティビティーによるトリガー・イベントの発生
{: #openwhisk_catalog_github_fire}

`/whisk.system/github/webhook` フィードは、指定された GitHub リポジトリーにアクティビティーがある場合にトリガーを発生させるサービスを構成します。パラメーターは次のとおりです。


- `username`: GitHub リポジトリーのユーザー名。
- `repository`: GitHub リポジトリー。
- `accessToken`: ご使用の GitHub パーソナル・アクセス・トークン。[トークンの作成](https://github.com/settings/tokens)時に、必ず repo:status スコープと public_repo スコープを選択してください。また、リポジトリーに既に定義された Web フックがないようにしてください。
- `events`: 対象の [GitHub イベント・タイプ](https://developer.github.com/v3/activity/events/types/)。

以下は、GitHub リポジトリーに新規コミットがあるたびに発生するトリガーを作成する例です。

1. GitHub [ パーソナル・アクセス・トークンを作成します。](https://github.com/settings/tokens).

  アクセス・トークンは次のステップで使用します。

2. GitHub リポジトリー用に構成されるパッケージ・バインディングを、アクセス・トークンを使用して作成します。

  ```
wsk package bind /whisk.system/github myGit --param username myGitUser --param repository myGitRepo --param accessToken aaaaa1111a1a1a1a1a111111aaaaaa1111aa1a1a
  ```
  {: pre}

3. `myGit/webhook` フィードを使用して、GitHub `push` イベント・タイプのトリガーを作成します。

  ```
wsk trigger create myGitTrigger --feed myGit/webhook --param events push
  ```
  {: pre}

`git push` を使用して GitHub リポジトリーへのコミットが行われると、Web フックによってトリガーが発生します。トリガーに突き合わせるルールが存在する場合は、関連付けられたアクションが呼び出されます。
アクションは、GitHub Web フック・ペイロードを入力パラメーターとして受け取ります。各 GitHub Web フック・イベントは、類似した JSON スキーマを持っていますが、それぞれのイベント・タイプによって判別される固有のペイロード・オブジェクトです。
ペイロード・コンテンツについては、[GitHub events and payload](https://developer.github.com/v3/activity/events/types/) API の資料を参照してください。


## Push パッケージの使用
{: #openwhisk_catalog_pushnotifications}

`/whisk.system/pushnotifications` パッケージを使用すると、プッシュ・サービスを処理することができます。 

このパッケージには、以下のアクションおよびフィードが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/pushnotifications` | パッケージ | appId、appSecret  | プッシュ・サービスの処理 |
| `/whisk.system/pushnotifications/sendMessage` | アクション | text、url、deviceIds、platforms、tagNames、apnsBadge、apnsCategory、apnsActionKeyTitle、apnsSound、apnsPayload、apnsType、gcmCollapseKey、gcmDelayWhileIdle、gcmPayload、gcmPriority、gcmSound、gcmTimeToLive | 1 つ以上の指定されたデバイスにプッシュ通知を送信 |
| `/whisk.system/pushnotifications/webhook` | フィード | events | プッシュ・サービスでデバイスのアクティビティー (デバイスの登録、登録解除、サブスクリプション、アンサブスクリプション) に基づきトリガー・イベントを発生させる |
`appId` と `appSecret` の値を使用して、パッケージ・バインディングを作成することをお勧めします。この方法を使用すると、パッケージ内のアクションを起動するたびにこれらの資格情報を指定する必要はありません。

### Push パッケージ・バインディングの作成
{: #openwhisk_catalog_pushnotifications_create}

Push Notifications パッケージ・バインディングを作成する際に、以下のパラメーターを指定してください。

-  `appId`: Bluemix アプリ GUID。
-  `appSecret`: Bluemix プッシュ通知サービス appSecret。

以下は、パッケージ・バインディングを作成する方法の例です。

1. [Bluemix ダッシュボード](http://console.ng.bluemix.net)で Bluemix アプリケーションを作成します。

2. Push Notification Service を初期化して、サービスを Bluemix アプリケーションにバインドします。

3. [Push Notification アプリケーション](https://console.ng.bluemix.net/docs/services/mobilepush/index.html)を構成します。

  作成した Bluemix アプリケーションの`「App GUID」`と`「App Secret」`を必ず覚えておいてください。


4. `/whisk.system/pushnotifications` を使用してパッケージ・バインディングを作成します。

  ```
  wsk package bind /whisk.system/pushnotifications myPush -p appId myAppID -p appSecret myAppSecret
  ```
  {: pre}

5. パッケージ・バインディングが存在することを確認します。

  ```
wsk package list
  ```
  {: pre}

  ```
  packages
  /myNamespace/myPush private binding
  ```
  {: screen}

### プッシュ通知の送信
{: #openwhisk_catalog_pushnotifications_send}

`/whisk.system/pushnotifications/sendMessage` アクションは、プッシュ通知を登録デバイスに送信します。パラメーターは次のとおりです。

- `text`: ユーザーに表示する通知メッセージ。例えば、`-p text "Hi ,OpenWhisk send a notification"` などです。
- `url`: アラートと一緒に送信できるオプションの URL。例えば、`-p url "https:\\www.w3.ibm.com"` などです。
- `deviceIds` 指定デバイスのリスト。例: `-p deviceIds "[\"deviceID1\"]"`
- `platforms` 通知を指定プラットフォームのデバイスに送信します。「A」は Apple (iOS) デバイス、「G」は Google (Android) デバイスです。例: `-p platforms "[\"A\"]"`
- `tagNames` 該当するタグのいずれかを購読しているデバイスに通知を送信します。例: `-p tagNames "[\"tag1\"]" `
- `gcmPayload`: 通知メッセージの一部として送信されるカスタム JSON ペイロード。例: `-p gcmPayload "{\"hi\":\"hello\"}"`
- `gcmSound`: 通知がデバイスに到着したときに再生が試行される (デバイス上の) 音声ファイル。
- `gcmCollapseKey`: このパラメーターは、メッセージのグループを識別します。
- `gcmDelayWhileIdle`: このパラメーターが true に設定されている場合、デバイスがアクティブになるまでメッセージが送信されないことを示します。
- `gcmPriority`: メッセージの優先順位を設定します。
- `gcmTimeToLive`: このパラメーターは、デバイスがオフラインの場合に GCM ストレージ内にメッセージを保持する時間 (秒) を指定します。
- `apnsBadge`: アプリケーション・アイコンのバッジとして表示する番号。
- `apnsCategory`: 対話式プッシュ通知に使用されるカテゴリー ID。
- `apnsIosActionKey`: アクション・キーのタイトル。
- `apnsPayload`: 通知メッセージの一部として送信されるカスタム JSON ペイロード。
- `apnsType`: ['DEFAULT', 'MIXED', 'SILENT']。
- `apnsSound`: アプリケーション・バンドル内の音声ファイルの名前。このファイルの音がアラートとして再生されます。

pushnotification パッケージからプッシュ通知を送信する例を以下に示します。

1. 前に作成したパッケージ・バインディング内の `sendMessage` アクションを使用して、プッシュ通知を送信します。`/myNamespace/myPush` を、ご使用のパッケージ名に置き換えてください。

  ```
  wsk action invoke /myNamespace/myPush/sendMessage --blocking --result  -p url https://example.com -p text "this is my message"  -p sound soundFileName -p deviceIds "[\"T1\",\"T2\"]"
  ```
  {: pre}

  ```
  {
  "result": {
  "pushResponse": "{"messageId":"11111H","message":{"message":{"alert":"this is my message","url":"http.google.com"},"settings":{"apns":{"sound":"default"},"gcm":{"sound":"default"},"target":{"deviceIds":["T1","T2"]}}}"
  },
  "status": "success",
  "success": true
  }
  ```
  {: screen}

### Push アクティビティーにおけるトリガー・イベントの発生
{: #openwhisk_catalog_pushnotifications_fire}

`/whisk.system/pushnotifications/webhook` は、指定されたアプリケーションでデバイス・アクティビティー (デバイスの登録 / 登録解除、またはサブスクリプション / アンサブスクリプションなど) があったときにトリガーを発生するように Push サービスを構成します。

パラメーターは次のとおりです。


- `appId:` Bluemix アプリ GUID。
- `appSecret:` Bluemix プッシュ通知サービス appSecret。
- `events:` サポートされるイベントは、`onDeviceRegister`、 `onDeviceUnregister`、`onDeviceUpdate`、`onSubscribe`、`onUnsubscribe`です。すべてのイベントの通知を受け取るようにするには、ワイルドカード文字 `*` を使用します。

以下は、Push Notifications サービス・アプリケーションに新規デバイスが登録されるたびに発生するトリガーを作成する例です。

1. ご使用の appId と appSecret を使用して、Push Notifications サービス用に構成されたパッケージ・バインディングを作成します。

  ```
  wsk package bind /whisk.system/pushnotifications myNewDeviceFeed --param appID myapp --param appSecret myAppSecret --param events onDeviceRegister
  ```
  {: pre}

2. `myPush/webhook` フィードを使用して、Push Notifications サービス `onDeviceRegister` イベント・タイプのトリガーを作成します。

  ```
  wsk trigger create myPushTrigger --feed myPush/webhook --param events onDeviceRegister
  ```
  {: pre}
