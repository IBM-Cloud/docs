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

# Cloudant パッケージの使用
{: #openwhisk_catalog_cloudant}
`/whisk.system/cloudant` パッケージを使用すると、Cloudant データベースを処理することができます。これには、以下のアクションおよびフィードが含まれます。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | パッケージ | dbname、host、username、password | Cloudant データベースを処理 |
| `/whisk.system/cloudant/read` | アクション | dbname、id | データベースから文書を読み取る |
| `/whisk.system/cloudant/write` | アクション | dbname、overwrite、doc | データベースに文書を書き込む |
| `/whisk.system/cloudant/changes` | フィード | dbname、maxTriggers | データベースの変更時にトリガー・イベントを発生させる |

以降のトピックでは、Cloudant データベースのセットアップ、関連付けられたパッケージの構成、および `/whisk.system/cloudant` パッケージのアクションとフィードの使用をウォークスルーします。

## Bluemix での Cloudant データベースのセットアップ
{: #openwhisk_catalog_cloudant_in}

Bluemix から OpenWhisk を使用している場合、Bluemix Cloudant サービス・インスタンスのパッケージ・バインディングは OpenWhisk が自動的に作成します。Bluemix から OpenWhisk および Cloudant を使用していない場合は、次のステップにスキップします。

1. Bluemix [ ダッシュボード](http://console.ng.Bluemix.net)で Cloudant サービス・インスタンスを作成します。

  サービス・インスタンスの名前、およびユーザーが所属している Bluemix の組織とスペースの名前を忘れないようにしてください。

2. ご使用の OpenWhisk CLI が、前のステップで使用した Bluemix 組織とスペースに対応する名前空間に存在するようにします。

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
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
  Bluemix_testCloudant_Credentials-1
  ```

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_testCloudant_Credentials-1 private binding
  ```

  Bluemix Cloudant サービス・インスタンスに対応するパッケージ・バインディングの完全修飾名が表示されます。

4. 前に作成されたパッケージ・バインディングが Cloudant Bluemix サービス・インスタンスのホストと資格情報で構成されているかどうかを確認します。

  ```
  wsk package get /myBluemixOrg_myBluemixSpace/Bluemix_testCloudant_Credentials-1 parameters
  ```
  {: pre}
  ```
  ok: got package /myBluemixOrg_myBluemixSpace/Bluemix_testCloudant_Credentials-1, displaying field parameters
  ```
  ```json
  [
      {
          "key": "username",
          "value": "cdb18832-2bbb-4df2-b7b1-Bluemix"
      },
      {
          "key": "host",
          "value": "cdb18832-2bbb-4df2-b7b1-Bluemix.cloudant.com"
      },
      {
          "key": "password",
          "value": "c9088667484a9ac827daf8884972737"
      }
      ]
  ```

## Bluemix 外部の Cloudant データベースのセットアップ
{: #openwhisk_catalog_cloudant_outside}

Bluemix で OpenWhisk を使用していない場合、または Bluemix の外部の Cloudant データベースをセットアップしたい場合は、Cloudant アカウントのパッケージ・バインディングを手動で作成する必要があります。Cloudant のアカウント・ホスト名、ユーザー名、パスワードが必要です。

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


## Cloudant データベースに対する変更の listen
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
  
  ```json
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
  
## Cloudant データベースへの書き込み
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
  ```
  ```json
  {
    "id": "heisenberg",
    "ok": true,
    "rev": "1-9a94fb93abc88d8863781a248f63c8c3"
  }
  ```

2. Cloudant ダッシュボードで参照して、文書が存在していることを確認します。

  `testdb` データベースのダッシュボード URL は、
`https://MYCLOUDANTACCOUNT.cloudant.com/dashboard.html#database/testdb/_all_docs?limit=100` のようになります。


## Cloudant データベースからの読み取り
{: #openwhisk_catalog_cloudant_read}

アクションを使用して `testdb` という Cloudant データベースから文書を取り出すことができます。このデータベースが、ご使用の Cloudant アカウントに必ず存在するようにしてください。

- 前に作成したパッケージ・バインディングの `read` アクションを使用して、文書を取り出します。
`/myNamespace/myCloudant` を、ご使用のパッケージ名に置き換えてください。

  ```
  wsk action invoke /myNamespace/myCloudant/read --blocking --result --param dbname testdb --param id heisenberg
  ```
  {: pre}
  ```json
  {
    "_id": "heisenberg",
    "_rev": "1-9a94fb93abc88d8863781a248f63c8c3",
    "name": "Walter White"
  }
  ```

## Cloudant データベースからの文書の処理を行うためのアクション・シーケンスおよび変更トリガーの使用
{: #openwhisk_catalog_cloudant_read_change notoc}
ルールでアクション・シーケンスを使用して、Cloudant 変更イベントに関連する文書をフェッチして処理することができます。

以下は、文書を処理するアクションのサンプル・コードです。
```javascript
function main(doc){
  return { "isWalter:" : doc.name === "Walter White"};
}
```

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
  ```
  {: pre}
  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
  ```
  {: pre}

  上の例を使用して、変更された文書を読み取って既存のアクションを呼び出すアクション・シーケンスを作成できます。
  もう有効ではない可能性のあるすべてのルールを忘れずに使用不可にし、アクション・シーケンス・パターンを使用して新しく作成するようにしてください。

