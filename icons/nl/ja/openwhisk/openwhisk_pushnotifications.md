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

# Push Notifications パッケージの使用
{: #openwhisk_catalog_pushnotifications}

`/whisk.system/pushnotifications` パッケージを使用すると、プッシュ・サービスを処理することができます。

このパッケージには、以下のアクションおよびフィードが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/pushnotifications` | パッケージ | appId、appSecret  | プッシュ・サービスの処理 |
| `/whisk.system/pushnotifications/sendMessage` | アクション | text、url、deviceIds、platforms、tagNames、gcmPayload、gcmSound、gcmCollapseKey、gcmDelayWhileIdle、gcmPriority、gcmTimeToLive、gcmSync、gcmVisibility、gcmStyleType、gcmStyleTitle、gcmStyleUrl、gcmStyleText、gcmStyleLines、apnsBadge、apnsCategory、apnsIosActionKey、apnsPayload、apnsType、apnsSound、fireFoxTitle、fireFoxIconUrl、fireFoxTimeToLive、fireFoxPayload、chromeTitle、chromeIconUrl、chromeTimeToLive、chromePayload、chromeAppExtTitle、chromeAppExtCollapseKey、chromeAppExtDelayWhileIdle、chromeAppExtIconUrl、chromeAppExtTimeToLive、chromeAppExtPayload | 1 つ以上の指定されたデバイスにプッシュ通知を送信 |
| `/whisk.system/pushnotifications/webhook` | フィード | events | プッシュ・サービスでデバイスのアクティビティー (デバイスの登録、登録解除、サブスクリプション、アンサブスクリプション) に基づきトリガー・イベントを発生させる |
`appId` と `appSecret` の値を使用して、パッケージ・バインディングを作成することをお勧めします。この方法を使用すると、パッケージ内のアクションを起動するたびにこれらの資格情報を指定する必要はありません。

## Push パッケージ・バインディングの作成
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
  

## プッシュ通知の送信
{: #openwhisk_catalog_pushnotifications_send}

`/whisk.system/pushnotifications/sendMessage` アクションは、プッシュ通知を登録デバイスに送信します。パラメーターは次のとおりです。

- `text`: ユーザーに表示する通知メッセージ。例えば、`-p text "Hi ,OpenWhisk send a notification"` などです。
- `url`: アラートと一緒に送信できるオプションの URL。例えば、`-p url "https:\\www.w3.ibm.com"` などです。
- `deviceIds` 指定デバイスのリスト。例えば、`-p deviceIds ["deviceID1"]` などです。
- `platforms` 通知を指定プラットフォームのデバイスに送信します。「A」は Apple (iOS) デバイス、「G」は Google (Android) デバイスです。例えば、`-p platforms ["A"]` などです。
- `tagNames` 該当するタグのいずれかを購読しているデバイスに通知を送信します。例: `-p tagNames "[\"tag1\"]" `
- `gcmPayload`: 通知メッセージの一部として送信されるカスタム JSON ペイロード。例: `-p gcmPayload "{\"hi\":\"hello\"}"`
- `gcmSound`: 通知がデバイスに到着したときに再生が試行される (デバイス上の) 音声ファイル。
- `gcmCollapseKey`: このパラメーターは、メッセージのグループを識別します。
- `gcmDelayWhileIdle`: このパラメーターが true に設定されている場合、デバイスがアクティブになるまでメッセージが送信されないことを示します。
- `gcmPriority`: メッセージの優先順位を設定します。
- `gcmTimeToLive`: このパラメーターは、デバイスがオフラインの場合に GCM ストレージ内にメッセージを保持する時間 (秒) を指定します。
- `gcmSync`: デバイス・グループ・メッセージングは、グループ内のすべてのアプリ・インスタンスが最新メッセージング状態を反映することを可能にします。
- `gcmVisibility`: private/public - 通知がいつ、どのように、ロックされた保護画面に表示されるのかに影響する、この通知の可視性。
- `gcmStyleType`: 拡張可能な通知のタイプを指定します。指定できる値は、`bigtext_notification`、`picture_notification`、`inbox_notification` です。
- `gcmStyleTitle`: 通知のタイトルを指定します。タイトルは通知が拡張されるときに表示されます。拡張可能な 3 つの通知のすべてにタイトルが指定される必要があります。
- `gcmStyleUrl`: 通知のピクチャーの取得元である URL。picture_notification にはこれを指定する必要があります。
- `gcmStyleText`: bigtext_notification の拡張時に表示される必要があるビッグ・テキスト。bigtext_notification にはこれを指定する必要があります。
- `gcmStyleLines`: inbox_notification の場合にボックス内スタイルで表示されるストリングの配列。inbox_notification にはこれを指定する必要があります。
- `apnsBadge`: アプリケーション・アイコンのバッジとして表示する番号。
- `apnsCategory`: 対話式プッシュ通知に使用されるカテゴリー ID。
- `apnsIosActionKey`: アクション・キーのタイトル。
- `apnsPayload`: 通知メッセージの一部として送信されるカスタム JSON ペイロード。
- `apnsType`: ['DEFAULT', 'MIXED', 'SILENT']。
- `apnsSound`: アプリケーション・バンドル内の音声ファイルの名前。このファイルの音がアラートとして再生されます。
- `fireFoxTitle`: Web プッシュ通知に対して設定されるタイトルを指定します。
- `fireFoxIconUrl`: Web プッシュ通知に対して設定されるアイコンの URL。
- `fireFoxTimeToLive`: このパラメーターは、デバイスがオフラインの場合に GCM ストレージ内にメッセージを保持する時間 (秒) を指定します。
- `fireFoxPayload`: 通知メッセージの一部として送信されるカスタム JSON ペイロード。
- `chromeTitle`: Web プッシュ通知に対して設定されるタイトルを指定します。
- `chromeIconUrl`: Web プッシュ通知に対して設定されるアイコンの URL。
- `chromeTimeToLive`: このパラメーターは、デバイスがオフラインの場合に GCM ストレージ内にメッセージを保持する時間 (秒) を指定します。
- `chromePayload`: 通知メッセージの一部として送信されるカスタム JSON ペイロード。
- `chromeAppExtTitle`: Web プッシュ通知に対して設定されるタイトルを指定します。
- `chromeAppExtCollapseKey`: このパラメーターは、メッセージのグループを識別します。
- `chromeAppExtDelayWhileIdle`: このパラメーターが true に設定されている場合、デバイスがアクティブになるまでメッセージが送信されてはならないことを示します。
- `chromeAppExtIconUrl`: Web プッシュ通知に対して設定されるアイコンの URL。
- `chromeAppExtTimeToLive`: このパラメーターは、デバイスがオフラインの場合に GCM ストレージ内にメッセージを保持する時間 (秒) を指定します。
- `chromeAppExtPayload`: 通知メッセージの一部として送信されるカスタム JSON ペイロード。

*pushnotification* パッケージからプッシュ通知を送信する例を以下に示します。

- 前に作成したパッケージ・バインディング内の `sendMessage` アクションを使用して、プッシュ通知を送信します。`/myNamespace/myPush` を、ご使用のパッケージ名に置き換えてください。
  
  ```
  wsk action invoke /myNamespace/myPush/sendMessage --blocking --result  -p url https://example.com -p text "this is my message"  -p sound soundFileName -p deviceIds "[\"T1\",\"T2\"]"
  ```
  {: pre}
  ```json
  {
      "result": {
  "pushResponse": 
      {
        "messageId":"11111H",
        "message":{
          "alert":"this is my message",
          "url":""
        },
        "settings":{
          "apns":{
            "sound":"default"
          },
          "gcm":{
            "sound":"default"
            },
          "target":{
            "deviceIds":["T1","T2"]
          }
        }
      }
    },
  "status": "success",
  "success": true
  }
  ```
  

## Push Notifications サービス・アクティビティーにおけるトリガー・イベントの発生
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
  
3. 新規デバイスが登録されるたびにメッセージを送信するルールを作成できます。前のアクションとトリガーを使用して新規ルールを作成します。
  
  ```
  wsk rule create --enable myRule myPushTrigger sendMessage
  ```
  {: pre}
  
  `wsk activation poll` で結果をチェックします。

  Bluemix アプリケーションでデバイスを登録すると、openWhisk [dashboard] (https://console.{Domain}/openwhisk/dashboard) で、`rule`、`trigger`、および `action` が実行されることを確認できます。

  アクションはプッシュ通知を送信します。
  
