---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Message Hub パッケージの使用
{: #openwhisk_catalog_message_hub}

このパッケージを使用すると、ハイパフォーマンスのネイティブ Kafka API を使用してコンシューム・メッセージをパブリッシュするために、[Message Hub](https://developer.ibm.com/messaging/message-hub) インスタンスと通信できます。
{: shortdesc}

## IBM MessageHub インスタンスを listen するトリガーの作成
{: #openwhisk_catalog_message_hub_trigger}

Message Hub インスタンスにメッセージがポストされたときに反応するトリガーを作成するためには、`/messaging/messageHubFeed` という名前のフィードを使用する必要があります。このフィード・アクションは、以下のパラメーターをサポートします。

|名前|タイプ |説明|
|---|---|---|
|kafka_brokers_sasl|JSON ストリング配列|このパラメーターは、Message Hub インスタンス内のブローカーを構成する `<host>:<port>` ストリングの配列です。|
|user|ストリング|Message Hub ユーザー名|
|password|ストリング|Message Hub パスワード|
|topic|ストリング|トリガーを listen したいトピック|
|kafka_admin_url|URL ストリング|Message Hub 管理 REST インターフェースの URL|
|isJSONData|ブール (オプション - デフォルトは false)|`true` に設定されると、プロバイダーは、メッセージ値をトリガー・ペイロードとして渡す前に JSON として構文解析しようとします。|
|isBinaryKey|ブール (オプション - デフォルトは false)|`true` に設定されると、プロバイダーは、キー値をトリガー・ペイロードとして渡す前に Base64 としてエンコードします。|
|isBinaryValue|ブール (オプション - デフォルトは false)|`true` に設定されると、プロバイダーは、メッセージ値をトリガー・ペイロードとして渡す前に Base64 としてエンコードします。|

このパラメーター・リストは難しそうに見えるかもしれませんが、package refresh CLI コマンドを使用して自動的に設定できます。

1. OpenWhisk 用に使用している現行の組織およびスペースの下に、Message Hub サービスのインスタンスを作成します。

2. listen したいトピックが既に Message Hub にあることを検証するか、新規トピック (例: `mytopic`) を作成します。

3. 名前空間でパッケージを最新表示します。このリフレッシュにより、作成した Message Hub サービス・インスタンスのパッケージ・バインディングが自動的に作成されます。

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Message_Hub_Credentials-1
  ```

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1 private
  ```

  これで、パッケージ・バインディングには、Message Hub インスタンスと関連付けられた資格情報が含まれるようになります。

4. 残っている作業は、新規メッセージが Message Hub トピックにポストされたら発生するトリガーを作成することだけです。

  ```
  wsk trigger create MyMessageHubTrigger -f /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1/messageHubFeed -p topic mytopic
  ```
  {: pre}

## Bluemix 外部での Message Hub パッケージのセットアップ

Message Hub を Bluemix の外部でセットアップしたい場合は、Message Hub サービスのパッケージ・バインディングを手動で作成する必要があります。Message Hub サービス資格情報と接続情報が必要です。

1. Message Hub サービス用に構成されたパッケージ・バインディングを作成します。

  ```
  wsk package bind /whisk.system/messaging myMessageHub -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p user <your Message Hub user> -p password <your Message Hub password> -p kafka_admin_url https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443
  ```
  {: pre}

2. 次に、新規パッケージを使用して、新規メッセージが Message Hub トピックにポストされたら発生するトリガーを作成できます。

  ```
  wsk trigger create MyMessageHubTrigger -f myMessageHub/messageHubFeed -p topic mytopic -p isJSONData true
  ```
  {: pre}


## メッセージの listen
{: #openwhisk_catalog_message_hub_listen}

トリガー作成後、システムはメッセージング・サービス内で指定されたトピックをモニターするようになります。新規メッセージがポストされると、トリガーが発生します。

そのトリガーのペイロードには、トリガーが最後に発生した以降にポストされたメッセージの配列である `messages` フィールドが含まれます。配列内の各メッセージ・オブジェクトには以下のフィールドが含まれます。
- topic
- partition
- offset
- key
- value

Kafka 用語では、これらのフィールドは自明です。ただし、`key` にはオプション・フィーチャー `isBinaryKey` があり、これを使用すると `key` をバイナリー・データとして送信できます。また、`value` には特別な考慮が必要です。JSON メッセージとバイナリー・メッセージを処理するために、オプション・フィールドとして `isJSONData` と `isBinaryValue` が用意されています。これらのフィールド (`isJSONData` と `isBinaryValue`) は、互いに一緒に使用することはできません。

一例として、トリガーの作成時に `isBinaryKey` が `true` に設定された場合、`key` は、起動されたトリガーのペイロードから返されるときに Base64 ストリングとしてエンコードされます。

例えば、`isBinaryKey` を `true` に設定して、`Some key` という `key` がポストされた場合、トリガー・ペイロードは次のようになります。

```json
 {
   "messages": [
       {
         "partition": 0,
            "key": "U29tZSBrZXk=",
            "offset": 421760,
            "topic": "mytopic",
            "value": "Some value"
        }
    ]
}
```

トリガーが作成されたときに `isJSONData` パラメーターが `false` に設定された (またはまったく設定されなかった) 場合、`value` フィールドは、ポストされたメッセージの未加工値になります。しかし、トリガーが作成されたときに `isJSONData` が `true` に設定された場合は、システムはこの値をできる限り JSON オブジェクトとして構文解析しようとします。構文解析が成功すると、その結果の JSON オブジェクトがトリガー・ペイロード内の `value` になります。

例えば、`isJSONData` を `true` に設定して、`{"title": "Some string", "amount": 5, "isAwesome": true}` のメッセージがポストされた場合、トリガー・ペイロードは次のようになります。

```json
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

```json
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

`isJSONData` と同様に、トリガーの作成時に `isBinaryValue` が `true` に設定された場合、トリガー・ペイロード内の結果の `value` は、Base64 ストリングとしてエンコードされます。

例えば、`isBinaryValue` を `true` に設定して、`Some data` という `value` がポストされた場合、トリガー・ペイロードは次のようになります。

```json
{
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421760,
      "topic": "mytopic",
      "value": "U29tZSBkYXRh"
    }
  ]
}
```

`isBinaryData` を `true` に設定せずに、同じメッセージがポストされた場合、トリガー・ペイロードは以下の例のようになります。

```json
{
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421760,
      "topic": "mytopic",
      "value": "Some data"
    }
  ]
}
```

### メッセージのバッチ処理
トリガー・ペイロードにはメッセージの配列が含まれます。これは、非常に高速でメッセージング・システムにメッセージが生成されている場合には、フィードはポストされたメッセージをひとまとめにして 1 回のトリガー発生にしようとすることを意味します。これによって、メッセージがトリガーにポストされるのが、より高速かつ効率的になります。

トリガーによって起動されるアクションをコーディングするときには、ペイロード内のメッセージの数は技術的には無制限であっても、常に 0 より大きいことに留意してください。以下に、バッチ処理されたメッセージの例を示します (*offset* 値の変化に注意してください)。
 
 ```json
 {
   "messages": [
       {
         "partition": 0,
         "key": null,
         "offset": 100,
         "topic": "mytopic",
         "value": {
             "amount": 5
         }
       },
       {
         "partition": 0,
         "key": null,
         "offset": 101,
         "topic": "mytopic",
         "value": {
             "amount": 1
         }
       },
       {
         "partition": 0,
         "key": null,
         "offset": 102,
         "topic": "mytopic",
         "value": {
             "amount": 999
         }
       }
   ]
 }
 ```

## Message Hub へのメッセージの生成
OpenWhisk アクションを使用して Message Hub へのメッセージを都合よく生成したい場合は、`/messaging/messageHubProduce` アクションを使用できます。このアクションでは、以下のパラメーターを使用します。

|名前|タイプ |説明|
|---|---|---|
|kafka_brokers_sasl|JSON ストリング配列|このパラメーターは、Message Hub インスタンス内のブローカーを構成する `<host>:<port>` ストリングの配列です。|
|user|ストリング|Message Hub ユーザー名|
|password|ストリング|Message Hub パスワード|
|topic|ストリング|トリガーを listen したいトピック|
|value|ストリング|生成したいメッセージの値|
|key|ストリング (オプション)|生成したいメッセージのキー|

最初の 3 つのパラメーターは `wsk package refresh` を使用して自動的にバインドできますが、必要なすべてのパラメーターを指定してアクションを起動する例を以下に示します。

```
wsk action invoke /messaging/messageHubProduce -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p topic mytopic -p user <your Message Hub user> -p password <your Message Hub password> -p value "This is the content of my message"
```
{: pre}

## 例

### OpenWhisk と IBM Message Hub、Node Red、IBM Watson IoT、IBM Object Storage、および IBM Data Science Experience の統合
OpenWhisk と IBM Message Hub、Node Red、IBM Watson IoT、IBM Object Storage、IBM Data Science Experience (Spark) サービスを統合する例は、[ここにあります](https://medium.com/openwhisk/transit-flexible-pipeline-for-iot-data-with-bluemix-and-openwhisk-4824cf20f1e0)。

## リファレンス
- [IBM Message Hub](https://developer.ibm.com/messaging/message-hub/)
- [Apache Kafka](https://kafka.apache.org/)
