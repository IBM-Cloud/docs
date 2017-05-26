---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-26"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# API ゲートウェイ
{: #openwhisk_apigateway}

OpenWhisk アクションを API Management によって管理することでメリットがあります。

API ゲートウェイは、[Web アクション](webactions.md)へのプロキシーとして機能し、アクションに、HTTP メソッド・ルーティング、クライアント ID/秘密、速度制限、CORS など、追加の機能を提供し、API の使用量および応答ログを表示し、API 共有ポリシーを定義します。API ゲートウェイ機能について詳しくは、[API 管理資料](/docs/apis/management/manage_openwhisk_apis.html#manage_openwhisk_apis)を参照してください。

## ブラウザーを使用した OpenWhisk Web アクションからの API の作成

API ゲートウェイを使用して、OpenWhisk アクションを API として公開できます。API を定義した後に、セキュリティー・ポリシーおよびレート制限ポリシーを適用したり、API 使用量および応答ログを表示したり、API 共有ポリシーを定義したりすることができます。OpenWhisk ダッシュボードで、[「API」タブ](https://console.ng.bluemix.net/openwhisk/apimanagement)をクリックします。


## CLI を使用した OpenWhisk Web アクションからの API の作成

### OpenWhisk CLI 構成

API ホスト `wsk property set --apihost openwhisk.ng.bluemix.net` を使用して、OpenWhisk CLI を構成します。`wsk api` を使用できるようにするには、CLI 構成ファイル `~/.wskprops` に Bluemix アクセス・トークンを含める必要があります。
アクセス・トークンを取得するには、CLI コマンド `wsk bluemix login` を使用します。このコマンドについて詳しくは、`wsk bluemix login -h` を実行してください。

**注:** シングル・サインオン (sso) が必要なコマンド・エラーが発生したとしても、現在、これはサポートされていません。次善策として、CloudFoundry CLI で `cf login` を使用してログインし、HOME ディレクトリー構成ファイル `~/.cf/config.json` からアクセス・トークンを `~/.wskprops` ファイルに、プロパティー `APIGW_ACCESS_TOKEN="value of AccessToken` としてコピーしてください。アクセス・トークン・ストリングをコピーする際、接頭部 `Bearer ` を削除してください。

**注:** `wsk api-experimental` を使用して作成された API は短期間は機能し続けますが、ご使用の API を Web アクションにマイグレーションし、新規 CLI コマンド `wsk api` を使用して既存の API を再構成することをお勧めします。

### CLI を使用した、最初の API の作成

1. 以下の内容を持つ JavaScript ファイルを作成します。この例では、ファイル名は 'hello.js' です。
  ```javascript
  function main({name:name='Serverless API'}) {
      return {payload: `Hello world ${name}`};
  }
  ```
  {: codeblock}
  
2. 以下の JavaScript 関数から Web アクションを作成します。この例では、アクションは「hello」という名前です。必ずフラグ `--web true` を追加してください。
  
  ```
  wsk action create hello hello.js --web true
  ```
  {: pre}
  ```
  ok: created action hello
  ```
  
3. 基本パス `/hello`、パス `/world`、メソッド `get`、および応答タイプ `json`を使用して、API を作成します。
  
  ```
  wsk api create /hello /world get hello --response-type json
  ```
  ```
  ok: created API /hello/world GET for action /_/hello
  https://${APIHOST}:9001/api/21ef035/hello/world
  ```
**GET** HTTP メソッドを介して `hello` アクションを公開する新規 URL が生成されます。
  
4. その URL に HTTP 要求を送信してみましょう。
  
  ```
  $ curl https://${APIHOST}:9001/api/21ef035/hello/world?name=OpenWhisk
  ```
  ```json
  {
      "payload": "Hello world OpenWhisk"
  }
  ```
Web アクション `hello` が呼び出され、照会パラメーターを介して送信されたパラメーター `name` を含む JSON オブジェクトが戻りました。このアクションには単純な照会パラメーターまたは要求本体を介してパラメーターを渡すことができます。Web アクションにより、OpenWhisk 許可 API キーを使用せず、パブリックな方法でアクションを呼び出すことができます。
  
### HTTP 応答の完全な制御
  
  `--response-type` フラグは、API ゲートウェイによってプロキシーされるように Web アクションのターゲット URL を制御します。上記のように `--response-type json` を使用すると、アクションの完全な結果が JSON フォーマットで戻り、Content-Type ヘッダーが `application/json` に自動的に設定されるため、簡単に開始できます。 
  
  開始後に `statusCode`、`headers` などの HTTP 応答プロパティーを完全に制御し、`body` 内に異なるコンテンツ・タイプが返るようにしたいと考える場合があります。これを行うには、`--response-type http` を使用します。これは、`http` 拡張機能付きの Web アクションのターゲット URL を構成します。

  アクションのコードを、`http` 拡張機能付きの Web アクションの戻りに従うように変更することを選択することも、適切に HTTP 応答用にフォーマットされるように結果を変換する新規アクションに結果を渡す順序でアクションを含めることを選択することもできます。応答タイプおよび Web アクションの拡張については、[Web アクション](webactions.md)資料を参照してください。

  JSON プロパティー `body`、`statusCode`、および `headers` を返す `hello.js` のコードに変更します。
  ```javascript
  function main({name:name='Serverless API'}) {
      return {
        body: new Buffer(JSON.stringify({payload:`Hello world ${name}`})).toString('base64'), 
        statusCode:200, 
        headers:{ 'Content-Type': 'application/json'}
      };
  }
  ```
  {: codeblock}
本体はストリングではなく `base64` でエンコードされて戻る必要がある点に注意してください。
  
  変更された結果でアクションを更新
  ```
  wsk action update hello hello.js --web true
  ```
  {: pre}
`--response-type http` で API を更新
  ```
  wsk api create /hello /world get hello --response-type http
  ```
  {: pre}
更新された API を呼び出してみましょう。
  ```
  curl https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/hello/world
  ```
  {: pre}
  ```json
  {
      "payload": "Hello world Serverless API"
  }
  ```
  API を完全に制御している状態であるため、HTML を返すなど、コンテンツを制御したり、「見つかりません (404)」、「認証が必要 (401)」、「内部エラー (500)」などの状況コードを設定できます。
### 複数 Web アクションの公開

友人たちの読書クラブ用にアクションのセットを公開したいと想定します。
この読書クラブのバックエンドを実装するために、以下の一連のアクションがあります。

| アクション | HTTP メソッド (HTTP method) | 説明 |
| ----------- | ----------- | ------------ |
| getBooks    | GET | 本の詳細を取得する  |
| postBooks   | POST | 本を追加する |
| putBooks    | PUT | 本の詳細を更新する |
| deleteBooks | DELETE | 本を削除する |

読書クラブの API を作成しましょう。名前を `Book Club` とし、HTTP URL 基本パスとして `/club` を、リソースとして `books` を使用します。
```
wsk api create -n "Book Club" /club /books get getBooks --response-type http
wsk api create /club /books post postBooks              --response-type http
wsk api create /club /books put putBooks                --response-type http
wsk api create /club /books delete deleteBooks          --response-type http
```

基本パス `/club` で公開された最初のアクションには `Book Club` という名前の API ラベルが付いていて、`/club` の下に公開される他のどのアクションも `Book Club` と関連付けられることに注意してください。

公開したばかりのすべてのアクションをリストしましょう。

```
wsk api list -f
```
```
ok: APIs
Action: getBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: get
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: postBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: post
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: putBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: put
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: deleteBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: delete
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```

次に、新しい本「`JavaScript: The Good Parts`」を HTTP **POST** を使用して追加してみましょう。
```
curl -X POST -d '{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}' https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
```
{
  "result": "success"
}
```

HTTP **GET** を介してアクション `getBooks` を使用して本のリストを取得しましょう。
```
curl -X GET https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
```
{
  "result": [{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}]
}
```

### 構成のエクスポート
`Book Club` という名前の API をファイルにエクスポートしましょう。そのファイルは、入力としてファイルを使用して API を再作成するためのベースとして使用できます。 
```
wsk api get "Book Club" > club-swagger.json
```

この swagger ファイルをテストしましょう。そのため、まず、共通の基本パスの下に公開されたすべての URL を削除します。
公開されたすべての URL の削除は、基本パス `/club` を使用して行うか、または API 名前ラベル `"Book Club"` を使用して行うことができます。
```
wsk api delete /club
```
```
ok: deleted API /club
```
### 構成の変更

OpenWhisk ダッシュボードで構成を編集し、[「API」タブ](https://console.ng.bluemix.net/openwhisk/apimanagement)をクリックして、セキュリティー、速度制限、およびその他の機能をセットアップできます。

### 構成のインポート

次に、`club-swagger.json` ファイルを使用して、`Book Club` という名前の API をリストアしましょう。
```
wsk api create --config-file club-swagger.json
```
```
ok: created api /books delete for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books get for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books post for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books put for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```

API が再作成されたことを確認できます。
```
wsk api list /club
```
```
ok: apis
Action                    Verb         API Name        URL
getBooks                   get         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
postBooks                 post         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
putBooks                   put         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
deleteBooks             delete         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
