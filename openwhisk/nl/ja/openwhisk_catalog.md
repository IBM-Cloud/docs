---

 

copyright:

  years: 2016, 2017
lastupdated: "2017-01-04"
 

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
| `/whisk.system/cloudant` | パッケージ | {{site.data.keyword.Bluemix_notm}}ServiceName、host、username、password、dbname、overwrite | Cloudant データベースを処理 |
| `/whisk.system/cloudant/read` | アクション | dbname、includeDoc、id | データベースから文書を読み取る |
| `/whisk.system/cloudant/write` | アクション | dbname、overwrite、doc | データベースに文書を書き込む |
| `/whisk.system/cloudant/changes` | フィード | dbname、maxTriggers | データベースの変更時にトリガー・イベントを発生させる |

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
- `maxTriggers`: この限界に達するとトリガーの発生を停止します。デフォルトは無限です。

1. 前に作成したパッケージ・バインディングの `changes` フィードを使用してトリガーを作成します。`/myNamespace/myCloudant` を、ご使用のパッケージ名に置き換えてください。

  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
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

生成されるイベントの内容には、以下のパラメーターがあります。

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

### Cloudant データベースからの文書の処理を行うためのアクション・シーケンスおよび変更トリガーの使用

ルールでアクション・シーケンスを使用して、Cloudant 変更イベントに関連する文書をフェッチして処理することができます。

以下は、文書を処理するアクションのサンプル・コードです。
```
function main(doc){
  return { "isWalter:" : doc.name === "Walter White"};
}
```
{: codeblock}

Cloudant からの文書を処理するアクションを作成します。
```
wsk action create myAction myAction.js
```
{: pre}

データベースから文書を読み取るには、Cloudant パッケージから `read` アクションを使用できます。
`read` アクションを `myAction` と組み合わせてアクション・シーケンスを作成することもできます。
```
wsk action create sequenceAction --sequence /myNamespace/myCloudant/read,myAction
```
{: pre}

新規 Cloudant トリガー・イベントでアクションを活動化するルール内で、アクション `sequenceAction` を使用できます。
```
wsk rule create myRule myCloudantTrigger sequenceAction
```
{: pre}

**注:** Cloudant `changes` トリガーは、以前はパラメーター `includeDoc` を使用していましたが、これはもうサポートされなくなりました。
  `includeDoc` を使用して以前に作成されたトリガーは作成し直す必要があります。トリガーを作成し直すには、以下のステップを実行してください。
  ```
  wsk trigger delete myCloudantTrigger
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
  ```
  {: pre}

  上の例を使用して、変更された文書を読み取って既存のアクションを呼び出すアクション・シーケンスを作成できます。
  もう有効ではない可能性のあるすべてのルールを忘れずに使用不可にし、アクション・シーケンス・パターンを使用して新しく作成するようにしてください。

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


- `cron`: トリガーを発生させるタイミングを協定世界時 (UTC) で示す、UNIX crontab 構文に基づいたストリング。このストリングは、`X X X X X` のようにスペースで区切られた 5 個のフィールドのシーケンスです。cron 構文の使用について詳しくは、http://crontab.org を参照してください。ストリングで示される頻度のいくつかの例を以下に示しま す。

  - `* * * * *`: 毎分の先頭。
  - `0 * * * *`: 毎時の先頭。
  - `0 */2 * * *`: 2 時間ごと (つまり、02:00:00、04:00:00、...)
  - `0 9 8 * *`: 毎月 8 日目の午前 9:00:00 (UTC)

- `trigger_payload`: このパラメーターの値は、
トリガーが発生するたびにトリガーのコンテンツになります。

- `maxTriggers`: この限界に達するとトリガーの発生を停止します。デフォルトは 1,000,000 です。無限 (-1) に設定できます。

以下は、トリガー・イベントに `name` と `place` の値を指定して、2 分ごとに 1 回発生するトリガーを作成する例です。

  ```
  wsk trigger create periodic --feed /whisk.system/alarms/alarm --param cron "*/2 * * * *" --param trigger_payload "{\"name\":\"Odin\",\"place\":\"Asgard\"}"
  ```
  {: pre}

生成される各イベントは、`trigger_payload` の値に指定されるプロパティーをパラメーターとして含みます。この場合、各トリガー・イベントは、
パラメーター `name=Odin` と `place=Asgard` を含みます。

**注**: パラメーター `cron` も、6 個のフィールドのカスタム構文をサポートします。ここで、最初のフィールドは秒を表します。
このカスタム cron 構文の使用について詳しくは、https://github.com/ncb000gt/node-cron を参照してください。
以下は、6 個のフィールドの表記を使用した例です。
  - `*/30 * * * * *`: 30 秒ごと。

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

Watson パッケージは、各種の Watson API を呼び出すために便利な方法を提供します。

以下の Watson パッケージが提供されています。

| パッケージ | 説明 |
| --- | --- |
| `/whisk.system/watson-translator`   | テキスト翻訳および言語識別のパッケージ |
| `/whisk.system/watson-textToSpeech` | テキストをスピーチに変換するパッケージ |
| `/whisk.system/watson-speechToText` | スピーチをテキストに変換するパッケージ |

**注** パッケージ `/whisk.system/watson` は現在、非推奨です。上記の新しいパッケージにマイグレーションしてください。新しいアクションでは、同じインターフェースが提供されています。

### Watson Translator パッケージの使用

`/whisk.system/watson-translator` パッケージを利用して、変換するための Watson API を簡単に呼び出すことができます。

このパッケージには、以下のアクションが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/watson-translator` | パッケージ | username、password | テキスト翻訳および言語識別のパッケージ  |
| `/whisk.system/watson-translator/translator` | アクション | payload、translateFrom、translateTo、translateParam、username、password | テキストの変換 |
| `/whisk.system/watson-translator/languageId` | アクション | payload、username、password | 言語の識別 |

**注:** パッケージ `/whisk.system/watson` は、アクション `/whisk.system/watson/translate` および `/whisk.system/watson/languageId` を含め、非推奨です。

#### Bluemix での Watson Translator パッケージのセットアップ

Bluemix から OpenWhisk を使用している場合、Bluemix Watson サービス・インスタンスのパッケージ・バインディングは OpenWhisk が自動的に作成します。

1. Bluemix [ダッシュボード](http://console.ng.Bluemix.net)で Watson Translator のサービス・インスタンスを作成します。

  サービス・インスタンスの名前、およびユーザーが所属している Bluemix の組織とスペースの名前を忘れないようにしてください。

2. ご使用の OpenWhisk CLI が、前のステップで使用した Bluemix 組織とスペースに対応する名前空間に存在するようにします。

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  あるいは、`wsk property set --namespace` を使用して、アクセス可能な名前空間のリストから名前空間を設定することができます。

3. 名前空間でパッケージを最新表示します。最新表示により、ユーザーが作成した Watson サービス・インスタンスのパッケージ・バインディングが自動的に作成されます。

  ```
wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_Translator_Credentials-1
  ```
  {: screen}

  ```
wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_Translator_Credentials-1 private
  ```
  {: screen}


#### Bluemix 外部での Watson Translator パッケージのセットアップ

Bluemix で OpenWhisk を使用していない場合、または Bluemix の外部で Watson Translator をセットアップしたい場合は、Watson Translator サービスのパッケージ・バインディングを手動で作成する必要があります。Watson Translator サービスのユーザー名とパスワードが必要になります。

- Watson Translator サービス用に構成されるパッケージ・バインディングを作成します。

  ```
  wsk package bind /whisk.system/watson-translator myWatsonTranslator -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### テキストの変換
{: #openwhisk_catalog_watson_translate}

`/whisk.system/watson-translator/translator` アクションは、テキストをある言語から別の言語に変換します。パラメーターは次のとおりです。


- `username`: Watson API ユーザー名。
- `password`: Watson API パスワード。
- `payload`: 変換するテキスト。
- `translateParam`: 変換するテキストを示す入力パラメーター。例えば、`translateParam=payload` の場合は、アクションに渡される `payload` パラメーターの値が変換されます。
- `translateFrom`: ソース言語の 2 桁のコード。
- `translateTo`: ターゲット言語の 2 桁のコード。

- パッケージ・バインディングの `translator` アクションを起動して、テキストを英語からフランス語に変換します。

  ```
  wsk action invoke myWatsonTranslator/translator --blocking --result --param payload 'Blue skies ahead' --param translateFrom 'en' --param translateTo 'fr'
  ```
  {: pre}

  ```
  {
      "payload": "Ciel bleu a venir"
  }
  ```
  {: screen}


#### テキストの言語の識別
{: #openwhisk_catalog_watson_identifylang}

`/whisk.system/watson-translator/languageId` アクションは、テキストの言語を識別します。パラメーターは次のとおりです。


- `username`: Watson API ユーザー名。
- `password`: Watson API パスワード。
- `payload`: 識別するテキスト。

- パッケージ・バインディングの `languageId` アクションを起動して、言語を識別します。

  ```
  wsk action invoke myWatsonTranslator/languageId --blocking --result --param payload 'Ciel bleu a venir'
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


### Watson Text to Speech パッケージの使用
{: #openwhisk_catalog_watson_texttospeech}

`/whisk.system/watson-textToSpeech` パッケージを利用して、テキストをスピーチに変換するための Watson API を簡単に呼び出すことができます。

このパッケージには、以下のアクションが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/watson-textToSpeech` | パッケージ | username、password | テキストをスピーチに変換するパッケージ |
| `/whisk.system/watson-textToSpeech/textToSpeech` | アクション | payload、voice、accept、encoding、username、password | テキストの音声への変換 |

**注:** パッケージ `/whisk.system/watson` は、アクション `/whisk.system/watson/textToSpeech` を含め、非推奨です。

#### Bluemix での Watson Text to Speech パッケージのセットアップ

Bluemix から OpenWhisk を使用している場合、Bluemix Watson サービス・インスタンスのパッケージ・バインディングは OpenWhisk が自動的に作成します。

1. Bluemix [ダッシュボード](http://console.ng.Bluemix.net)で Watson Text to Speech のサービス・インスタンスを作成します。

  サービス・インスタンスの名前、およびユーザーが所属している Bluemix の組織とスペースの名前を忘れないようにしてください。

2. ご使用の OpenWhisk CLI が、前のステップで使用した Bluemix 組織とスペースに対応する名前空間に存在するようにします。

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  あるいは、`wsk property set --namespace` を使用して、アクセス可能な名前空間のリストから名前空間を設定することができます。

3. 名前空間でパッケージを最新表示します。最新表示により、ユーザーが作成した Watson サービス・インスタンスのパッケージ・バインディングが自動的に作成されます。

  ```
wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_TextToSpeech_Credentials-1
  ```
  {: screen}

  ```
wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_TextToSpeec_Credentials-1 private
  ```
  {: screen}


#### Bluemix 外部での Watson Text to Speech パッケージのセットアップ

Bluemix で OpenWhisk を使用していない場合、または Bluemix の外部で Watson Text to Speech をセットアップしたい場合は、Watson Text to Speech サービスのパッケージ・バインディングを手動で作成する必要があります。Watson Text to Speech サービスのユーザー名とパスワードが必要になります。

- Watson Speech to Text サービス用に構成されるパッケージ・バインディングを作成します。

  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonTextToSpeech -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### テキストをスピーチに変換
{: #openwhisk_catalog_watson_speechtotext}

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
  ```
  {
        "payload": "<base64 encoding of a .wav file>"
  }
  ```
  {: screen}


### Watson Speech to Text パッケージの使用
{: #openwhisk_catalog_watson_speechtotext}

`/whisk.system/watson-speechToText` パッケージを利用して、スピーチをテキストに変換するための Watson API を簡単に呼び出すことができます。

このパッケージには、以下のアクションが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/watson-speechToText` | パッケージ | username、password | スピーチをテキストに変換するパッケージ |
| `/whisk.system/watson-speechToText/speechToText` | アクション | payload、content_type、encoding、username、password、continuous、inactivity_timeout、interim_results、keywords、keywords_threshold、max_alternatives、model、timestamps、watson-token、word_alternatives_threshold、word_confidence、X-Watson-Learning-Opt-Out | 音声のテキストへの変換 |

**注:** パッケージ `/whisk.system/watson` は、アクション `/whisk.system/watson/speechToText` を含め、非推奨です。

#### Bluemix での Watson Speech to Text パッケージのセットアップ

Bluemix から OpenWhisk を使用している場合、Bluemix Watson サービス・インスタンスのパッケージ・バインディングは OpenWhisk が自動的に作成します。

1. Bluemix [ダッシュボード](http://console.ng.Bluemix.net)で Watson Speech to Text のサービス・インスタンスを作成します。

  サービス・インスタンスの名前、およびユーザーが所属している Bluemix の組織とスペースの名前を忘れないようにしてください。

2. ご使用の OpenWhisk CLI が、前のステップで使用した Bluemix 組織とスペースに対応する名前空間に存在するようにします。

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  あるいは、`wsk property set --namespace` を使用して、アクセス可能な名前空間のリストから名前空間を設定することができます。

3. 名前空間でパッケージを最新表示します。最新表示により、ユーザーが作成した Watson サービス・インスタンスのパッケージ・バインディングが自動的に作成されます。

  ```
wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_SpeechToText_Credentials-1
  ```
  {: screen}

  ```
wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_SpeechToText_Credentials-1 private
  ```
  {: screen}


#### Bluemix 外部での Watson Speech to Text パッケージのセットアップ

Bluemix で OpenWhisk を使用していない場合、または Bluemix の外部で Watson Speech to Text をセットアップしたい場合は、Watson Speech to Text サービスのパッケージ・バインディングを手動で作成する必要があります。Watson Speech to Text サービスのユーザー名とパスワードが必要になります。

- Watson Speech to Text サービス用に構成されるパッケージ・バインディングを作成します。

  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonSpeechToText -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### スピーチのテキストへの変換

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
  ```
  {
        "data": "Hello Watson"
  }
  ```
  {: screen}
 
 
## Message Hub パッケージの使用
{: #openwhisk_catalog_message_hub}

このパッケージを使用すると、Bluemix 上の [Message Hub](https://developer.ibm.com/messaging/message-hub/) サービス・インスタンスにメッセージがポストされたときに反応するトリガーを作成できます。

### Message Hub インスタンスを listen するトリガーの作成
{: #openwhisk_catalog_message_hub_trigger}
Message Hub インスタンスにメッセージがポストされたときに反応するトリガーを作成するためには、`messaging/messageHubFeed` という名前のフィードを使用する必要があります。このフィードは、以下のパラメーターをサポートします。

|名前|タイプ |説明|
|---|---|---|
|kafka_brokers_sasl|JSON ストリング配列|このパラメーターは、Message Hub インスタンス内のブローカーを構成する `<host>:<port>` ストリングの配列です。|
|user|ストリング|Message Hub ユーザー名|
|password|ストリング|Message Hub パスワード|
|topic|ストリング|トリガーを listen したいトピック|
|kafka_admin_url|URL ストリング|Message Hub 管理 REST インターフェースの URL|
|api_key|ストリング|Message Hub API キー|
|isJSONData|ブール (オプション - デフォルトは false)|`true` に設定されると、フィードは、メッセージ・コンテンツをトリガー・ペイロードとして渡す前に JSON として構文解析しようとします。|

このパラメーター・リストは難しそうに見えるかもしれませんが、package refresh CLI コマンドを使用して自動的に設定できます。

1. OpenWhisk 用に使用している現行の組織およびスペースの下に、Message Hub サービスのインスタンスを作成します。

2. listen したいトピックが既に Message Hub にあることを検証するか、メッセージを確認するために listen の対象とする新規トピック (例: `mytopic`) を作成します。

2. 名前空間でパッケージを最新表示します。このリフレッシュにより、作成した Message Hub サービス・インスタンスのパッケージ・バインディングが自動的に作成されます。

  ```
wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Message_Hub_Credentials-1
  ```
  {: screen}

  ```
wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1 private
  ```
  {: screen}

  これで、パッケージ・バインディングには、Message Hub インスタンスと関連付けられた資格情報が含まれるようになります。

3. 残っている作業は、新規メッセージが Message Hub にポストされたら発生するトリガーを作成することだけです。

  ```
  wsk trigger create MyMessageHubTrigger -f /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1/messageHubFeed -p topic mytopic
  ```
  {: pre}

### Bluemix 外部での Message Hub パッケージのセットアップ

Bluemix 内で OpenWhisk を使用していない場合、または、Message Hub を Bluemix の外部でセットアップしたい場合は、Message Hub サービスのパッケージ・バインディングを手動で作成する必要があります。Message Hub サービス資格情報と接続情報が必要です。

- Message Hub サービス用に構成されたパッケージ・バインディングを作成します。

  ```
  wsk trigger create MyMessageHubTrigger -f /whisk.system/messaging/messageHubFeed -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p topic mytopic -p user <your Message Hub user> -p password <your Message Hub password> -p kafka_admin_url https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443 -p api_key <your API key>
  ```
  {: pre}

### Message Hub インスタンスへのメッセージの listen
{: #openwhisk_catalog_message_hub_listen}
トリガー作成後、システムはメッセージング・サービス内で指定されたトピックをモニターするようになります。新規メッセージがポストされると、トリガーが発生します。

そのトリガーのペイロードには、トリガーが最後に発生した以降にポストされたメッセージの配列である `messages` フィールドが含まれます。配列内の各メッセージ・オブジェクトには以下のフィールドが含まれます。
- topic
- partition
- offset
- key
- value

Kafka 用語では、これらのフィールドは自明です。ただし、`value` には特別な考慮が必要です。トリガーが作成されたときに `isJSONData` パラメーターが `false` に設定された (またはまったく設定されなかった) 場合、`value` フィールドは、ポストされたメッセージの未加工値になります。しかし、トリガーが作成されたときに `isJSONData` が `true` に設定された場合は、システムはこの値をできる限り JSON オブジェクトとして構文解析しようとします。構文解析が成功すると、その結果の JSON オブジェクトがトリガー・ペイロード内の `value` になります。

例えば、`isJSONData` を `true` に設定して、`{"title": "Some string", "amount": 5, "isAwesome": true}` のメッセージがポストされた場合、トリガー・ペイロードは次のようになります。

```
{
  "messages": [
      {
        "partition": 0,
        "key": null,
        "offset": 421760,
        "topic": "mytopic",
        "value": {
            "amount": 5,
            "isAwesome": true,
            "title": "Some string"
        }
      }
  ]
}
```

しかし、`isJSONData` を `false` に設定して、同じメッセージ内容がポストされた場合は、トリガー・ペイロードは次のようになります。

```
{
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421761,
      "topic": "mytopic",
      "value": "{\"title\": \"Some string\", \"amount\": 5, \"isAwesome\": true}"
    }
  ]
}
```

### メッセージのバッチ処理
トリガー・ペイロードにはメッセージの配列が含まれます。これは、非常に高速でメッセージング・システムにメッセージが生成されている場合には、フィードはポストされたメッセージをひとまとめにして 1 回のトリガー発生にしようとすることを意味します。これによって、メッセージがトリガーにポストされるのが、より高速かつ効率的になります。

トリガーによって起動されるアクションをコーディングするときには、ペイロード内のメッセージの数は技術的には無制限だが、常に 0 より大きいことに留意してください。


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
