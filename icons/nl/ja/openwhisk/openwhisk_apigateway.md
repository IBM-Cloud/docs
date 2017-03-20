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

# API ゲートウェイを介したアクションの公開 (試験的)
{: #openwhisk_apigateway}

{{site.data.keyword.openwhisk}} では、[REST API](./openwhisk_reference.html#openwhisk_ref_restapi) を使用したアクションの起動は、**POST** メソッドを介した HTTP 要求のみを使用して行うことができます。
これには、アクションの起動を許可するのに加えて多くのアクションの削除および作成も許可するマスター・キーである OpenWhisk 許可 API キーを使用して、HTTP クライアントが要求を行うことが必要です。
{: shortdesc}

この試験的フィーチャーによって、アクションの許可 API キーなしで、POST 以外の HTTP メソッドを使用してアクションを起動できるようになります。

CLI を使用して、OpenWhisk API ゲートウェイを介して OpenWhisk アクションを公開します。 

## OpenWhisk CLI 構成
{: #openwhisk_apigateway_cli}
この試験的フィーチャーは、名前空間ごとに固有の認証鍵が関連付けられるようになった新しい OpenWhisk 認証モデルと一緒に使用される場合のみ機能します。
特定の名前空間の認証鍵の設定方法については、[CLI の構成](https://console.ng.bluemix.net/openwhisk/cli)に説明されている手順を参照してください。

## OpenWhisk アクションの公開
{: #openwhisk_apigateway_hello}

OpenWhisk と共に既に事前インストールされている単純なアクションを公開してみましょう。

```
wsk api-experimental create /hello /echo get /whisk.system/utils/echo
```
{: pre}
```
ok: created api /echo GET for action /whisk.system/utils/echo
https://21ef035.api-gw.mybluemix.net/hello/echo
```
{: screen}
**GET** HTTP メソッドを介して `echo` アクションを公開する新規 URL が生成されます。

その URL に HTTP 要求を送信してみましょう。
```
curl https://21ef035.api-gw.mybluemix.net/hello/echo?marco=polo
```
{: pre}
これによって `echo` アクションが起動され、送信されたパラメーターを含んでいる JSON ストリングが返されます。
```
{
  "marco":"polo"
}
```
{: screen}

このアクションには単純な照会パラメーターまたは要求本体を介してパラメーターを渡すことができます。

### 複数アクションの公開
{: #openwhisk_apigateway_actions}

友人たちの読書クラブ用にアクションのセットを公開したいと想定します。
この読書クラブのバックエンドを実装するために、以下の一連のアクションがあります。

| アクション | HTTP メソッド | 説明 |
| ----------- | ----------- | ------------ |
| getBooks    | GET | 本の詳細を取得する  |
| postBooks   | POST | 本を追加する |
| putBooks    | PUT | 本の詳細を更新する |
| deleteBooks | DELETE | 本を削除する |

読書クラブの API を作成しましょう。名前を `Book Club` とし、HTTP URL 基本パスとして `/club` を、リソースとして `books` を使用します。
```
wsk api-experimental create -n "Book Club" /club /books get getBooks
wsk api-experimental create /club /books post postBooks
wsk api-experimental create /club /books put putBooks
wsk api-experimental create /club /books delete deleteBooks
```
{: pre}

基本パス `/club` で公開された最初のアクションには `Book Club` という名前の API ラベルが付いていて、`/club` の下に公開される他のどのアクションも `Book Club` と関連付けられることに注意してください。

公開したばかりのすべてのアクションをリストしましょう。

```
wsk api-experimental list
```
{: pre}
```
ok: apis
Action                   Verb          API Name        URL
getBooks                   get         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
postBooks                 post         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
putBooks                   put         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
deleteBooks             delete         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

次に、新しい本「`JavaScript: The Good Parts`」を HTTP **POST** を使用して追加してみましょう。
```
curl -X POST -d '{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}' https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: pre}
```
{
  "result": "success"
}
```
{: screen}

HTTP **GET** を介してアクション `getBooks` を使用して本のリストを取得しましょう。
```
curl -X GET https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: pre}
```
{
  "result": [{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}]
}
```

### 構成のエクスポート
`Book Club` という名前の API をファイルにエクスポートしましょう。そのファイルは、入力としてファイルを使用して API を再作成するためのベースとして使用できます。 
```
wsk api-experimental get "Book Club" > club-swagger.json
```
{: pre}

この swagger ファイルをテストしましょう。そのため、まず、共通の基本パスの下に公開されたすべての URL を削除します。
公開されたすべての URL の削除は、基本パス `/club` を使用して行うか、または API 名前ラベル `"Book Club"` を使用して行うことができます。
```
wsk api-experimental delete /club
```
{: pre}
```
ok: deleted API /club
```
{: screen}

次に、`club-swagger.json` ファイルを使用して、`Book Club` という名前の API をリストアしましょう。
```
wsk api-experimental create --config-file club-swagger.json
```
{: pre}
```
ok: created api /books delete for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books get for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books post for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books put for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

API が再作成されたことを確認できます。
```
wsk api-experimental list /club
```
{: pre}
```
ok: apis
Action                    Verb         API Name        URL
getBooks                   get         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
postBooks                 post         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
putBooks                   put         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
deleteBooks             delete         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

- **注:** 現在、このフィーチャーは試験的オファリングであり、ユーザーはこれを早期に試してみて、フィードバックを提供することができます。以下のフィードバックが既に受け付けられました。
  - CORS (Cross-Origin Resource Sharing) 用の HTTP アクセス制御をカスタマイズする機能がありません。現在のところ、生成される API 応答ヘッダーは任意の HTTP 動詞またはオリジン (つまり、*) を許容するように構成されます。常に以下のヘッダーが返されます。
    - Access-Control-Allow-Origin: *
    - Access-Control-Allow-Headers: Authorization, Content-Type
    - Access-Control-Allow-Methods: GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS
  - 要求と応答に対してサポートされているコンテンツ・タイプは `application/json` のみです。
  - OpenWhisk アクションからの応答をプログラマチックに制御する方法がありません。
  - すべての OpenWhisk アクションはパブリック・アクセスを介して公開され、カスタム API キーを構成する機能がありません。
  - パス・パラメーターはサポートされず、照会パラメーターおよび要求本体のみがサポートされます。
  - API 名なしで API が作成された場合、名前は基本パスになり、変更できません。
  - 入力ファイルを介して API を再作成するとき、まず API を削除する必要があります。
  - API をエクスポートするとき、これには OpenWhisk API キーが含まれますが、この情報は機密性が高く、テンプレート手法は使用可能ではありません。
