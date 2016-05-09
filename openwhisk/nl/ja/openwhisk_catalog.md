---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 対応サービスの使用 
{: #openwhisk_ecosystem}
*最終更新日: 2016 年 3 月 28 日*

{{site.data.keyword.openwhisk}} で、パッケージ・カタログは、便利な機能でアプリを強化して、エコシステム内の外部サービスにアクセスするための簡単な方法を提供します。{{site.data.keyword.openwhisk_short}} 対応の外部サービスの例として、Cloudant、The Weather Company、Slack、GitHub などがあります。
{: shortdesc}

カタログは、`/whisk.system` 名前空間でパッケージとして使用可能です。コマンド・ライン・ツールを使用したカタログの参照方法については、[パッケージの参照](./openwhisk_packages.html#openwhisk_packagedisplay)を参照してください。

以降のトピックで、カタログの一部のパッケージについて説明します。

## Cloudant パッケージの使用
{: #openwhisk_catalog_cloudant}
`/whisk.system/cloudant` パッケージを使用すると、Cloudant データベースを処理することができます。これには、以下のアクションおよびフィードが含まれます。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | パッケージ | 
{{site.data.keyword.Bluemix_notm}}ServiceName、host、username、password、dbname、includeDoc、overwrite | 
Cloudant データベースを処理 |
| `/whisk.system/cloudant/read` | アクション | dbname、includeDoc、id | 
データベースから文書を読み取る |
| `/whisk.system/cloudant/write` | アクション | dbname、overwrite、doc | 
データベースに文書を書き込む |
| `/whisk.system/cloudant/changes` | フィード | dbname、includeDoc | 
データベースの変更時にトリガー・イベントを発生させる |

以降のトピックでは、Cloudant データベースのセットアップ、関連付けられたパッケージの構成、および `/whisk.system/cloudant` パッケージのアクションとフィードの使用をウォークスルーします。

### {{site.data.keyword.Bluemix_notm}} での Cloudant データベースのセットアップ

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

{{site.data.keyword.Bluemix_notm}} で {{site.data.keyword.openwhisk_short}} を使用していない場合、
または {{site.data.keyword.Bluemix_notm}} の外部の Cloudant データベースをセットアップしたい場合は、Cloudant アカウントのパッケージ・バインディングを手動で作成する必要があります。
Cloudant のアカウント・ホスト名、ユーザー名、パスワードが必要です。

1. Cloudant アカウント用に構成されるパッケージ・バインディングを作成します。

  ```
  wsk package bind /whisk.system/cloudant myCloudant -p username 'MYUSERNAME' -p password 'MYPASSWORD' -p host 'MYCLOUDANTACCOUNT.cloudant.com'
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

`changes` フィードを使用して、Cloudant データベースが変更されるたびにトリガーを発生させるサービスを構成することができます。

1. 前に作成したパッケージ・バインディングの `changes` フィードを使用してトリガーを作成します。`/myNamespace/myCloudant` を、ご使用のパッケージ名に置き換えてください。

  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb --param includeDocs true
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

**注**: 新規アクティベーションを監視できない場合は、Cloudant データベースからの読み取りと Cloudant データベースへの書き込みに関する後続のセクションを参照してください。以下の読み取りおよび書き込みの検証ステップは、Cloudant 資格情報が正しいことを確認するために役立ちます。

これで、ルールを作成してアクションに関連付け、文書の更新に対応することができるようになります。

生成されたイベントのコンテンツは、トリガーを作成するときの `includeDocs` パラメーターの値によって異なります。true に設定すると、発生する各トリガー・イベントに、変更された Cloudant 文書が含まれます。たとえば、次の変更された文書を考えてみます。 

  ```
  {
    "_id": "6ca436c44074c4c2aa6a40c9a188b348",
    "_rev": "3-bc4960fc13aa368afca8c8427a1c18a8",
    "name": "Heisenberg"
  }
  ```
  {: screen}

この例のコードは、対応する `_id`、`_rev`、および `name` の各パラメーターを使用してトリガー・イベントを生成します。実際には、トリガー・イベントの JSON 表記は文書に一致します。

`includeDocs` が false の場合は、イベントに以下のパラメーターが含まれます。

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

アクションを使用して `testdb` という Cloudant データベースに文書を格納することができます。このデータベースが、ご使用の Cloudant アカウントに必ず存在するようにしてください。

1. 前に作成したパッケージ・バインディングの `write` アクションを使用して、文書を格納します。
`/myNamespace/myCloudant` を、ご使用のパッケージ名に置き換えてください。

  ```
  wsk action invoke /myNamespace/myCoudant/write --blocking --result --param dbname testdb --param doc '{"_id":"heisenberg", "name":"Walter White"}'
  ```
  {: pre}
  ```
  ok: invoked /myNamespace/myCoudant/write with id 62bf696b38464fd1bcaff216a68b8287
  response:
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

アクションを使用して `testdb` という Cloudant データベースから文書を取り出すことができます。このデータベースが、ご使用の Cloudant アカウントに必ず存在するようにしてください。

1. 前に作成したパッケージ・バインディングの `read` アクションを使用して、文書を取り出します。
`/myNamespace/myCloudant` を、ご使用のパッケージ名に置き換えてください。

  ```
  wsk action invoke /myNamespace/myCoudant/read --blocking --result --param dbname testdb --param id heisenberg
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

`/whisk.system/alarms` パッケージを使用して、
指定した頻度でトリガーを発生させることができます。これは、1 時間ごとにシステム・バックアップ・アクションを起動するといった、ジョブやタスクの繰り返しをセットアップする際に便利です。

このパッケージには、以下のフィードが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | パッケージ | - | アラームおよび定期的ユーティリティー |
| `/whisk.system/alarms/alarm` | フィード | cron、trigger_payload、maxTriggers | 
トリガー・イベントを定期的に発生させる |


### トリガー・イベントの定期的な発生

 `/whisk.system/alarms/alarm` フィードは、
Alarm サービスを構成して、指定した頻度でトリガー・イベントを発生させます。パラメーターは次のとおりです。


- `cron`: トリガーを発生させるタイミングを協定世界時 (UTC) で示す、UNIX crontab 構文に基づいたストリング。このストリングは、`X X X X X X ` のようにスペースで区切られた 6 個のフィールドのシーケンスです。cron 構文の使用について詳しくは、https://github.com/ncb000gt/node-cron を参照してください。

- `trigger_payload`: このパラメーターの値は、
トリガーが発生するたびにトリガーのコンテンツになります。

- `maxTriggers`: この限界に達するとトリガーの発生を停止します。デフォルトは 1000 です。

以下は、トリガー・イベントに `name` と `place` の値を指定して、20 秒ごとに 1 回発生するトリガーを作成する例です。

  ```
  wsk trigger create periodic --feed /whisk.system/alarms/alarm --param cron '/20 * * * * *' --param trigger_payload '{"name":"Odin","place":"Asgard"}'
  ```
  {: pre}

生成される各イベントは、`trigger_payload` の値に指定されるプロパティーをパラメーターとして含みます。この場合、各トリガー・イベントは、
パラメーター `name=Odin` と `place=Asgard` を含みます。


## Weather パッケージの使用
{: #openwhisk_catalog_weather}

`/whisk.system/weather` パッケージは、The Weather Company API を呼び出すために便利な方法を提供します。

このパッケージには、以下のアクションが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/weather` | パッケージ | apiKey | The Weather Company からのサービス |
| `/whisk.system/weather/forecast` | アクション | apiKey、latitude、longitude | 
Weather.com の 10 日間の予報 |

必須ではありませんが、`apiKey` 値を使用してパッケージ・バインディングを作成することをお勧めします。この方法を使用すると、パッケージ内のアクションを起動するたびにキーを指定する必要はありません。

### 場所を指定した天気予報の取得

`/whisk.system/weather/forecast` アクションは、
The Weather Company から API を呼び出して、場所を指定した 10 日間の天気予報を返します。パラメーターは次のとおりです。


- `apiKey`: 10 日間の予測 API を起動する権限を与えられた The Weather Company の API キー。

- `latitude`: 場所の経度の座標。
- `longitude`: 場所の緯度の座標。

以下は、パッケージ・バインディングを作成してから 10 日間の予測を取得する例です。

1. API キーを使用してパッケージ・バインディングを作成します。

  ```
  wsk package bind /whisk.system/weather myWeather --param apiKey 'MY_WEATHER_API'
  ```
  {: pre}

2. パッケージ・バインディングの `forecast` アクションを起動して、天気予報を取得します。

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


## Watson パッケージの使用
{: #openwhisk_catalog_watson}

`/whisk.system/watson` パッケージは、各種の Watson API を呼び出すために便利な方法を提供します。

このパッケージには、以下のアクションが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/watson` | パッケージ | username、password | Watson 分析 API のアクション |
| `/whisk.system/watson/translate` | アクション | translateFrom、translateTo、translateParam、username、password | テキストの変換 |
| `/whisk.system/watson/languageId` | アクション | payload、username、password | 言語の識別 |

必須ではありませんが、`username` と `password` の値を使用して、パッケージ・バインディングを作成することをお勧めします。この方法を使用すると、パッケージ内のアクションを起動するたびにこれらの資格情報を指定する必要はありません。

### テキストの変換

`/whisk.system/watson/translate` アクションは、テキストをある言語から別の言語に変換します。パラメーターは次のとおりです。


- `username`: Watson API ユーザー名。
- `password`: Watson API パスワード。
- `translateParam`: 変換する入力パラメーター。例えば、
`translateParam=payload` の場合は、アクションに渡される `payload` パラメーターの値が変換されます。
- `translateFrom`: ソース言語の 2 桁のコード。
- `translateTo`: ターゲット言語の 2 桁のコード。

以下は、パッケージ・バインディングを作成してテキストを変換する例です。

1. Watson の資格情報を使用してパッケージ・バインディングを作成します。

  ```
  wsk package bind /whisk.system/watson myWatson --param username 'MY_WATSON_USERNAME' --param password 'MY_WATSON_PASSWORD'
  ```
  {: pre}

2. パッケージ・バインディングの `translate` アクションを起動して、テキストを英語からフランス語に変換します。

  ```
  wsk action invoke myWatson/translate --blocking --result --param payload 'Blue skies ahead' --param translateParam 'payload' --param translateFrom 'en' --param translateTo 'fr'
  ```
  {: pre}

  ```
  {
      "payload": "Ciel bleu a venir"
  }
  ```
  {: screen}


### テキストの言語の識別

`/whisk.system/watson/languageId` アクションは、テキストの言語を識別します。パラメーターは次のとおりです。


- `username`: Watson API ユーザー名。
- `password`: Watson API パスワード。
- `payload`: 識別するテキスト。

以下は、パッケージ・バインディングを作成してテキストの言語を識別する例です。

1. Watson の資格情報を使用してパッケージ・バインディングを作成します。

  ```
  wsk package bind /whisk.system/watson myWatson -p username 'MY_WATSON_USERNAME' -p password 'MY_WATSON_PASSWORD'
  ```
  {: pre}

2. パッケージ・バインディングの `languageId` アクションを起動して、言語を識別します。

  ```
  wsk action invoke myWatson/languageId --blocking --result --param payload 'Ciel bleu a venir'
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


## Slack パッケージの使用
{: #openwhisk_catalog_slack}

`/whisk.system/slack` パッケージは、
[Slack API](https://api.slack.com/) を使用する便利な方法を提供します。

このパッケージには、以下のアクションが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/slack` | パッケージ | url、channel、username | Slack API と対話 |
| `/whisk.system/slack/post` | アクション | text、url、channel、username | 
Slack チャネルへメッセージをポスト |

必須ではありませんが、`username`、
`url`、および「channel」の各値を使用してパッケージ・バインディングを作成することをお勧めします。バインディングを使用すると、パッケージでアクションを起動するたびに値を指定する必要はありません。

### Slack チャネルへのメッセージのポスト

`/whisk.system/slack/post` アクションは、指定された Slack チャネルにメッセージをポストします。パラメーターは次のとおりです。


- `url`: Slack の Webhook URL。
- `channel`: メッセージのポスト先の Slack チャネル。
- `username`: メッセージをポストするユーザーの名前。
- `text`: ポストするメッセージ。

以下は、Slack を構成し、パッケージ・バインディングを作成して、
メッセージをチャネルにポストする例です。

1. チームに Slack の [Incoming Webhook](https://api.slack.com/incoming-webhooks) を構成します。

  Slack の構成後、`https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`
のような Webhook URL を取得する必要があります。これは次のステップで必要になります。

2. Slack の資格情報、ポスト先のチャネル、およびポストするユーザー名を指定して、パッケージ・バインディングを作成します。

  ```
  wsk package bind /whisk.system/slack mySlack --param url 'https://hooks.slack.com/services/...' --param username 'Bob' --param channel '#MySlackChannel'
  ```
  {: pre}

3. パッケージ・バインディングの `post` アクションを起動し、ご使用の Slack チャネルにメッセージをポストします。

  ```
  wsk action invoke mySlack/post --blocking --result --param text 'Hello from OpenWhisk!'
  ```
  {: pre}


## GitHub パッケージの使用
{: #openwhisk_catalog_github}

`/whisk.system/github` パッケージは、
[GitHub API](https://developer.github.com/) を使用するための便利な方法を提供します。

このパッケージには、以下のフィードが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/github` | パッケージ | username、
repository、accessToken | GitHub API と対話 |
| `/whisk.system/github/webhook` | フィード | events、username、repository、accessToken | 
GitHub アクティビティーでトリガー・イベントを発生させる |

必須ではありませんが、`username`、
`repository`、および `accessToken` の各値を使用してパッケージ・ バインディングを作成することをお勧めします。バインディングを使用すると、パッケージのフィードを使用するたびに値を指定する必要はありません。

### GitHub アクティビティーによるトリガー・イベントの発生

`/whisk.system/github/webhook` フィードは、指定された GitHub リポジトリーにアクティビティーがある場合にトリガーを発生させるサービスを構成します。パラメーターは次のとおりです。


- `username`: GitHub リポジトリーのユーザー名。
- `repository`: GitHub リポジトリー。
- `accessToken`: ご使用の GitHub パーソナル・アクセス・トークン。[トークンの作成](https://github.com/settings/tokens)時に、必ず repo:status スコープと public_repo スコープを選択してください。また、リポジトリーに既に定義された Webhook がないようにしてください。
- `events`: 対象の [GitHub
アクティビティー・タイプ](https://developer.github.com/v3/activity/events/types/)。

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

