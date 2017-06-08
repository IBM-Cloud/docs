---

copyright:
  years: 2017
lastupdated: "2017-05-04"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# OpenWhisk REST API の使用
{: #openwhisk_rest_api}

OpenWhisk 環境が有効になった後、OpenWhisk を、REST API 呼び出しを使用して Web アプリまたはモバイル・アプリと共に使用できます。

アクション、アクティベーション、パッケージ、ルール、およびトリガー用の API について詳しくは、[ OpenWhisk API 資料](http://petstore.swagger.io/?url=https://raw.githubusercontent.com/openwhisk/openwhisk/master/core/controller/src/main/resources/apiv1swagger.json)を参照してください。


システム上のすべての機能は、REST API を通じて使用可能です。アクション、トリガー、ルール
、パッケージ、アクティベーション、および名前空間のコレクション・エン
ドポイントとエンティティー・エンドポイントがあります。

以下のコレクション・エンドポイントがあります。
- `https://{APIHOST}/api/v1/namespaces`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/actions`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/triggers`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/rules`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/packages`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/activations`

`{APIHOST}` は、OpenWhisk API ホスト名 (例えば、openwhisk.ng.bluemix.net、172.17.0.1、192.168.99.100、192.168.33.13 など) です。
`{namespace}` には、文字 `_` を使用して、ユーザーの *default namespace* を指定できます。

コレクション・エンドポイントで GET 要求を実行して、コレクションのエンティティーのリストをフェッチします。

エンティティーのタイプごとに以下のエンティティー・エンドポイン
トがあります。
- `https://{APIHOST}/api/v1/namespaces/{namespace}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/actions/[{packageName}/]{actionName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/triggers/{triggerName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/rules/{ruleName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/packages/{packageName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/activations/{activationName}`

名前空間とアクティベーション・エンドポイントのみが GET 要求をサポートします。アクション、トリガー、ルール、およびパッケージのエンドポイントは、GET、PUT、および DELETE 要求をサポートします。アクション、トリガー、およびルールのエンドポイントも POST 要求をサポートします。これは、アクションとトリガーを起動し、ルールを使用可能または使用不可にするために使用されます。 

すべての API は、HTTP 基本認証で保護さ
れています。[wskadmin](../tools/admin/wskadmin) ツールを使用して、新規の名前空間および認証を生成できます。
基本認証の資格情報は `~/.wskprops` ファイルの `AUTH` プロパティーにあり、コロンで区切られています。CLI を使用して `wsk property get --auth` を実行することで、これらの資格情報を取得することもできます。


以下は、[cURL](https://curl.haxx.se) コマンド・ツールを使用して `whisk.system` 名前空間のすべてのパッケージのリストを取得する例を示しています。

```bash
curl -u USERNAME:PASSWORD https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/packages
```
{: pre}

```json
  [
      {
    "name": "slack",
    "binding": false,
    "publish": true,
    "annotations": [
      {
        "key": "description",
        "value": "Package that contains actions to interact with the Slack messaging service"
      }
    ],
    "version": "0.0.1",
    "namespace": "whisk.system"
  }
]
```

この例では、認証は `-u` フラグを使用して渡されましたが、この値を URL の一部として `https://$AUTH@{APIHOST}` のようにして渡すこともできます。

OpenWhisk API は、Web クライアントからの要求/応答呼び出しをサポートします。OpenWhisk は、Cross-Origin Resource Sharing ヘッダーを使用して `OPTIONS` 要求に応答します。現在は、すべてのオリジンが許可され (すなわち、Access-Control-Allow-Origin は「`*`」)、Access-Control-Allow-Headers に許可とコンテンツ・タイプが示されます。

**注意:** OpenWhisk は現在、名前空間当たり 1 つのキーしかサポートしないので、簡単な実験の範囲を超えて CORS を使用することはお勧めできません。アクションをパブリックに公開するには、[Web アクション](webactions.md)または [API ゲートウェイ](apigateway.md)を使用し、CORS を必要とするクライアント・アプリケーションに対して OpenWhisk 許可キーを使用しないでください。

## CLI 冗長モードの使用
{: #openwhisk_rest_api_cli_v}
OpenWhisk CLI は、OpenWhisk REST API へのインターフェースです。
フラグ `-v` を使用して CLI を冗長モードで実行できます。これにより、HTTP 要求と応答に関するすべての情報が出力されます。

現行ユーザーの名前空間値を取得してみましょう。
```
wsk namespace list -v
```
{: pre}
```
REQUEST:
[GET]	https://openwhisk.ng.bluemix.net/api/v1/namespaces
Req Headers
{
  "Authorization": [
    "Basic XXXYYYY"
  ]
}
RESPONSE:Got response with code 200
Resp Headers
{
  "Content-Type": [
    "application/json; charset=UTF-8"
  ]
}
Response body size is 28 bytes
Response body received:
["john@example.com_dev"]
```

ご覧のように、出力された情報は HTTP 要求のプロパティーを提供しており、要求は、基本許可ヘッダー `Basic XXXYYYY` を使用して、URL `https://openwhisk.ng.bluemix.net/api/v1/namespaces` に対して HTTP メソッド `GET` を実行しています。
許可の値は、base64 エンコードの OpenWhisk 許可ストリングです。
応答のコンテンツ・タイプは `application/json` です。

## アクション
{: #openwhisk_rest_api_actions}
アクションを作成または更新するには、アクションのコレクションに対してメソッド `PUT` を指定して HTTP 要求を送信します。例えば、単一ファイル・コンテンツを使用して、`hello` という名前の `nodejs:6` アクションを作成するには、以下を使用します。
```bash
curl -u $AUTH -d '{"namespace":"_","name":"hello","exec":{"kind":"nodejs:6","code":"function main(params) { return {payload:\"Hello \"+params.name}}"}}' -X PUT -H "Content-Type: application/json" https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?overwrite=true 
```
{: pre}

アクションに対してブロッキング起動を実行するには、メソッド `POST` と、入力パラメーター `name` を含む本体を指定して、以下のような HTTP 要求を送信します。
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?blocking=true \
-X POST -H "Content-Type: application/json" \
-d '{"name":"John"}'  
```
{: pre}
以下の応答を受け取ります。
```json
{
  "duration": 2,
  "name": "hello",
  "subject": "john@example.com_dev",
  "activationId": "c7bb1339cb4f40e3a6ccead6c99f804e",
  "publish": false,
  "annotations": [{
    "key": "limits",
    "value": {
      "timeout": 60000,
      "memory": 256,
      "logs": 10
    }
  }, {
    "key": "path",
    "value": "john@example.com_dev/hello"
  }],
  "version": "0.0.1",
  "response": {
    "result": {
  "payload": "Hello John"
    },
    "success": true,
    "status": "success"
  },
  "end": 1493327653769,
  "logs": [],
  "start": 1493327653767,
  "namespace": "john@example.com_dev"
}
```
`response.result` のみを取得する場合は、照会パラメーター `result=true` を指定して、コマンドを再度実行します。
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?blocking=true&result=true" \
-X POST -H "Content-Type: application/json" \
-d '{"name":"John"}' 
```
{: pre}
以下の応答を受け取ります。
```json
{
  "payload": "hello John"
}
```

## アノテーションおよび Web アクション
{: #openwhisk_rest_api_webactions}
アクションを Web アクションとして作成するには、Web アクション用の[アノテーション](annotations.md)である `web-export=true` を追加する必要があります。Web アクションはパブリックにアクセス可能であるため、アノテーション `final=true` を使用して、事前定義パラメーターを保護する (つまり、最終的なものとして扱う) 必要があります。CLI フラグ `--web true` を使用してアクションを作成または更新すると、このコマンドは `web-export=true` と `final=true` の両方のアノテーションを追加します。

アクションに設定するアノテーションの全リストを指定して curl コマンドを実行します。
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"hello","exec":{"kind":"nodejs:6","code":"function main(params) { return {payload:\"Hello \"+params.name}}"},"annotations":[{"key":"web-export","value":true},{"key":"raw-http","value":false},{"key":"final","value":true}]}'
```
{: pre}
これで、OpenWhisk 許可を使用せずに、パブリック URL としてこのアクションを呼び出すことができるようになりました。URL の最後に、例えば `.json` または `.http` などのオプション拡張子を含めて、Web アクション・パブリック URL を使用して呼び出してみます。
```bash
curl https://openwhisk.ng.bluemix.net/api/v1/web/john@example.com_dev/default/hello.json?name=John
```
{: pre}
```json
{
  "payload": "Hello John"
    }
```
この例のソース・コードは、`.http` では機能しないことに注意してください。修正方法については、[Web アクション](webactions.md)の資料を参照してください。
## シーケンス
{: #openwhisk_rest_api_sequences}
アクション・シーケンスを作成するには、シーケンスを構成するアクションの名前を適切な順序で指定し、最初のアクションからの出力が次のアクションへの入力として渡されるようにする必要があります。

$ wsk action create sequenceAction --sequence /whisk.system/utils/split,/whisk.system/utils/sort

アクション `/whisk.system/utils/split` および `/whisk.system/utils/sort` を使用して、シーケンスを作成します。
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/sequenceAction?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"sequenceAction","exec":{"kind":"sequence","components":["/whisk.system/utils/split","/whisk.system/utils/sort"]},"annotations":[{"key":"web-export","value":true},{"key":"raw-http","value":false},{"key":"final","value":true}]}' 
```
{: pre}

アクションの名前を指定する際には、完全修飾名を指定する必要があることに注意してください。

## トリガー
{: #openwhisk_rest_api_triggers}
トリガーを作成する場合、必要最小限の情報は、トリガーの名前です。また、トリガーの起動時にルールを介してアクションに渡されるデフォルト・パラメーターを含めることもできます。

デフォルト・パラメーター `type` の値を `webhook` に設定して、名前が `events` というトリガーを作成します。
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/events?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"events","parameters":[{"key":"type","value":"webhook"}]}' 
```
{: pre}

これで、このトリガーの起動を必要とするイベントが発生するたびに、OpenWhisk 許可キーを使用して、メソッド `POST` を指定して HTTP 要求を行えば済むようになりました。

パラメーター `temperature` を指定したトリガー `events` を起動するには、以下の HTTP 要求を送信します。

```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/events \
-X POST -H "Content-Type: application/json" \
-d '{"temperature":60}' 
```
{: pre}

### フィード・アクションを使用したトリガー
{: #openwhisk_rest_api_triggers_feed}
フィード・アクションを使用して作成できる特殊なトリガーがあります。フィード・アクションとは、トリガーの対象イベントが発生するたびにトリガーの起動を担当するフィード・プロバイダーの構成に役立つアクションです。フィード・プロバイダーについて詳しくは、[feeds.md] 資料を参照してください。

フィード・アクションを活用している利用可能なトリガーには、periodic/alarms、Slack、Github、Cloudant/Couchdb、messageHub/Kafka などがあります。ユーザー独自のフィード・アクションおよびフィード・プロバイダーを作成することもできます。

指定された頻度 (2 時間ごと、すなわち 02:00:00、04:00:00 など) で起動される、名前が `periodic` というトリガーを作成しましょう。

CLI を使用すると、これは 1 つのコマンドで実行されます。
```bash
wsk trigger create periodic --feed /whisk.system/alarms/alarm \
  --param cron "0 */2 * * *" -v
```
{: pre}
ご覧のように、`-v` フラグを使用しているので、2 つの HTTP 要求が送信されます。一方はトリガー `periodic` を作成するための要求であり、もう一方は、2 時間ごとにトリガーを起動するフィード・プロバイダーを構成するためのパラメーターを指定した、フィード・アクション `/whisk.system/alarms/alarm` を呼び出すための要求です。
これと同じ動作を REST API を使用して行うために、まずトリガーを作成しましょう。
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/periodic?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"periodic","annotations":[{"key":"feed","value":"/whisk.system/alarms/alarm"}]}'  
```
{: pre}

アノテーション `feed` がトリガーに保管されているのが分かります。後ほど、トリガーを削除する際に使用するフィード・アクションを判別するために、このアノテーションを使用します。

トリガーが作成されたので、フィード・アクションを呼び出しましょう。
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/actions/alarms/alarm?blocking=true&result=false" \
-X POST -H "Content-Type: application/json" \
-d "{\"authKey\":\"$AUTH\",\"cron\":\"0 */2 * * *\",\"lifecycleEvent\":\"CREATE\",\"triggerName\":\"/_/periodic\"}" 
```
{: pre}

トリガーの削除は、トリガーの作成と似ています。今度は、トリガーを削除し、さらにフィード・プロバイダーを構成するフィード・アクションを使用して、トリガーのハンドラーも削除します。

フィード・プロバイダーからトリガー・ハンドラーを削除するためのフィード・アクションを呼び出します。
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/actions/alarms/alarm?blocking=true&result=false" \
-X POST -H "Content-Type: application/json" \
-d "{\"authKey\":\"$AUTH\",\"lifecycleEvent\":\"DELETE\",\"triggerName\":\"/_/periodic\"}"  
```
{: pre}

HTTP 要求で `DELETE` メソッドを使用して、トリガーを削除します。
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/periodic \
-X DELETE -H "Content-Type: application/json" 
```
{: pre}

## ルール
{: #openwhisk_rest_api_rules}
トリガーをアクションに関連付けるルールを作成するには、`PUT` メソッドを使用し、要求の本体でトリガーとアクションを指定して、HTTP 要求を送信します。
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/rules/t2a?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"t2a","status":"","trigger":"/_/events","action":"/_/hello"}' 
```
{: pre}

ルールは有効または無効にすることができます。また、状況プロパティーを更新することにより、ルールの状況を変更できます。例えば、ルール `t2a` を無効にするには、`POST` メソッドを使用して、要求の本体で `status: "inactive"` を送信します。
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/rules/t2a?overwrite=true \
-X POST -H "Content-Type: application/json" \
-d '{"status":"inactive","trigger":null,"action":null}'  
```
{: pre}

## パッケージ
{: #openwhisk_rest_api_packages}
パッケージ内にアクションを作成するには、最初にパッケージを作成する必要があります。名前が `iot` というパッケージを作成するには、`PUT` メソッドを指定して HTTP 要求を送信します。

```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/packages/iot?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"iot"}' 
```
{: pre}

## アクティベーション
{: #openwhisk_rest_api_activations}
最新の 3 つのアクティベーションのリストを取得するには、`GET` メソッドを指定した HTTP 要求を使用し、照会パラメーター `limit=3` を渡します。
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/activations?limit=3
```
{: pre}

結果およびログを含めたアクティベーションのすべての詳細を取得するには、`GET` メソッドを指定した HTTP 要求を送信し、アクティベーション ID をパス・パラメーターとして渡します。
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/activations/f81dfddd7156401a8a6497f2724fec7b
```
{: pre}
