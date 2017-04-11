---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Web アクション
{: #openwhisk_webactions}

Web アクションは、Web ベースのアプリケーションを迅速に作成することを可能にするためにアノテーションを付けた OpenWhisk アクションです。これを使用すると、Web アプリケーションが OpenWhisk 認証鍵を必要とせずに匿名でアクセスできるバックエンド・ロジックをプログラムできます。アクション開発者は、自由に独自の認証および許可 (つまり OAuth フロー) を実装できます。
{: shortdesc}

Web アクションのアクティベーションは、アクションを作成したユーザーと関連付けられます。この処理により、アクションのアクティベーションのコストは呼び出し元ではなく所有者が負うことになります。

以下の JavaScript アクション `hello.js` を見てみましょう。
```javascript
function main({name}) {
  var msg = 'you did not tell me who you are.';
  if (name) {
    msg = `hello ${name}!`
  }
  return {body: `<html><body><h3>${msg}</h3></body></html>`}
}
```
{: codeblock}

以下のように、アノテーション `web-export` を使用して、*Web アクション* `hello` を、名前空間 `guest` のパッケージ `demo` 内に作成できます。 
```
wsk package create demo
```
{: pre}
```
wsk action create /guest/demo/hello hello.js -a web-export true
```
{: pre}

`web-export` アノテーションにより、アクションは新規 REST インターフェースを介して Web アクションとしてアクセス可能になります。構造化された URL は、`https://openwhisk.ng.bluemix.net/api/v1/web/{QUALIFIED ACTION NAME}.{EXT}` です。アクションの完全修飾名は、名前空間、パッケージ名、およびアクション名の 3 つの部分からなります。

*アクションの完全修飾名には、そのアクションのパッケージ名が含まれている必要があり、指定されたパッケージ内にアクションがない場合は「default」になります。*

例えば、`guest/demo/hello` などです。URI の最後の部分は`拡張子`と呼ばれ、通常は `.http` ですが、後述するように他の値も許可されます。API キーなしで Web アクション API パスを `curl` または `wget` で使用できます。ブラウザーに直接入力することも可能です。

[https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.http?name=Jane](https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.http?name=Jane) を、ご使用の Web ブラウザーで開いてみてください。あるいは、次のように `curl` を介してこのアクションを起動してみてください。
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.http?name=Jane
```
{: pre}

以下の Web アクション例は、HTTP リダイレクトを実行します。

```javascript
function main() {
  return { 
    headers: { location: 'http://openwhisk.org' },
    statusCode: 302
  }
}
```
{: codeblock}  

以下は、Cookie を設定する例です。
```javascript
function main() {
  return { 
    headers: { 
      'Set-Cookie': 'UserID=Jane; Max-Age=3600; Version=',
      'Content-Type': 'text/html'
    }, 
    statusCode: 200,
    body: '<html><body><h3>hello</h3></body></html>' }
}
```
{: codeblock}

`image/png` を返す例は、次のようになります。
```javascript
function main() {
    let png = <base 64 encoded string>
    return { headers: { 'Content-Type': 'image/png' },
             statusCode: 200,
             body: png };
}
```
{: codeblock}

`application/json` を返す例は次のようになります。
```javascript
function main(params) {
    return {
        statusCode: 200,
        headers: { 'Content-Type': 'application/json' },
        body: new Buffer(JSON.stringify(params)).toString('base64'),
    };
}
```
{: codeblock}

アクションの[応答サイズ制限](./openwhisk_reference.html)を知っておくことが重要です。事前定義されたシステムしきい値を超える応答は失敗するからです。例えば、ラージ・オブジェクトは OpenWhisk を通してインラインで送信するのではなく、オブジェクト・ストアに置くようにする必要があります。

## アクションを使用した HTTP 要求の処理
{: #openwhisk_webactions_http}

Web アクションでない OpenWhisk アクションは、認証を必要とし、JSON オブジェクトで応答することも必要です。対照的に、Web アクションは認証なしで起動でき、Web アクションを使用して、さまざまなタイプの *headers*、*statusCode*、および *body* コンテンツを使用して応答する HTTP ハンドラーを実装できます。Web アクションはやはり JSON オブジェクトを返さなければなりませんが、OpenWhisk システム (つまり `Controller`) は、Web アクションの結果に最上位 JSON プロパティーとして以下のうち 1 つ以上が含まれている場合は、Web アクションを違う方法で処理します。

- `headers`: キーがヘッダー名であり、値がそれらのヘッダーのストリング値である、JSON オブジェクト (デフォルトはヘッダーなし)。
- `statusCode`: 有効な HTTP 状況コード (デフォルトは 200 OK)。
- `body`: プレーン・テキストまたは Base64 エンコードのストリング (バイナリー・データの場合) のいずれかであるストリング。

コントローラーは、アクションが指定したヘッダーがあれば、要求/応答を終了するときに HTTP クライアントに渡します。同様に、コントローラーは、状況コードがあればそれを付けて応答します。最後に、本体が応答本体として渡されます。アクション結果の `headers` 内に `content-type header` が宣言されている場合を除いて、本体がストリングであるかのように渡されます (そうでない場合はエラーになります)。`content-type` が定義されている場合、コントローラーは応答がバイナリー・データなのかプレーン・テキストなのかを判別し、必要に応じて base64 デコーダーを使用してストリングをデコードします。本体を正しくデコードできない場合、呼び出し元にエラーが返されます。

*注:* JSON オブジェクトまたは配列は、バイナリー・データとして処理され、上の例のように base64 でエンコードされる必要があります。

## HTTP コンテキスト

すべての Web アクションは、起動されると、アクション入力引数へのパラメーターとして、追加の HTTP 要求詳細を受け取ります。それらは以下のとおりです。

- `__ow_method` (タイプ: ストリング): 要求の HTTP メソッド。
- `__ow_headers` (タイプ: ストリング間マップ): 要求ヘッダー。
- `__ow_path` (タイプ: ストリング): マッチングされていない要求のパス (マッチングはアクションの拡張子を取り込んだ後に停止します)。
- `__ow_user` (タイプ: ストリング): OpenWhisk 認証済みサブジェクトを識別する名前空間
- `__ow_body` (タイプ: ストリング): 要求本体エンティティー (コンテンツがバイナリーの場合は base64 エンコード・ストリング、バイナリーではない場合はプレーン・ストリングとして)
- `__ow_query` (タイプ: ストリング): 要求からの照会パラメーター (解析対象外ストリングとして)

上記の `__ow_` パラメーターの指定を要求がオーバーライドすることはできません。それを行うと、要求は 400 Bad Request と等しい状況で失敗します。

`__ow_user` は、Web アクションが[認証を必要とするためにアノテーションを付けている](./openwhisk_annotations.html#openwhisk_annotations_webactions)場合にのみ存在し、Web アクションが独自の許可ポリシーを実装できるようになります。`__ow_query` は、Web アクションが [「未加工」HTTP 要求](#raw-http-handling)を処理することを選択した場合にのみ使用できます。これは、URI から解析された照会パラメーターを含むストリングです (`&` で分離)。`__ow_body` プロパティーは、「未加工」HTTP 要求を処理する場合、または HTTP 要求エンティティーが JSON オブジェクトでも形式データでもない場合に存在します。その他の場合、Web アクションは、アクション引数内の第 1 クラス・プロパティーとして、照会パラメーターおよび本体パラメーターを受け取ります。本体パラメーターが照会パラメーターより優先され、照会パラメーターはアクション・パラメーターおよびパッケージ・パラメーターより優先されます。

## 追加フィーチャー

Web アクション用に次のようなフィーチャーが追加されました。

- `コンテンツ拡張子`: 要求は、その要求にとって望ましいコンテンツ・タイプを、`.json`、`.html`、`.http`、`.svg` または `.text` のいずれかで指定する必要があります。これは、URI 内のアクション名に拡張子を追加することで行われます。これによって、例えば、アクション `/guest/demo/hello` は `/guest/demo/hello.http` として参照されて、HTTP 応答を受け取ります。便宜上、拡張子が検出されない場合は `.http` 拡張子が想定されます。
- `結果からのフィールドの射影`: アクション名の後に続くパスを使用して、応答の 1 つ以上のレベルが射影されます。例えば、`/guest/demo/hello.html/body` です。これによって、ディクショナリー `{body: "..." }` を返すアクションは、`body` プロパティーを射影して、代わりにそのストリング値を直接返すことができます。射影されたパスは、絶対パス・モデル (例: XPath) に従います。
- `入力としての照会パラメーターおよび本体パラメーター`: アクションは、照会パラメーターと、要求本体内のパラメーターを受け取ります。パラメーターをマージする際の優先順位は、パッケージ・パラメーター、アクション・パラメーター、照会パラメーター、本体パラメーターの順序であり、重なり合っている場合は、前の値がオーバーライドされます。例えば、`/guest/demo/hello.http?name=Jane` は、引数 `{name: "Jane"}` をアクションに渡します。
- `形式データ`: 標準 `application/json` に加えて、Web アクションは、入力としてデータ `application/x-www-form-urlencoded data` からエンコードされた URL を受け取ることができます。
- `複数の HTTP 動詞を介したアクティベーション`: Web アクションは、HTTP メソッド (`GET`、`POST`、`PUT`、`PATCH`、および `DELETE`、ならびに `HEAD` および `OPTIONS`) のいずれかを介して起動できます。
- `非 JSON 本体および未加工 HTTP エンティティーの処理`: Web アクションは、JSON オブジェクト以外の HTTP 要求本体を受け入れることができ、不透明値のような値 (バイナリーではない場合はプレーン・テキスト、バイナリーの場合は base64 エンコード・ストリング) を常に受け取ることを選択できます。

以下の例は、Web アクションでこれらのフィーチャーを使用する方法を簡単に示しています。以下のような本体を持つアクション `/guest/demo/hello` を考えてみます。
```javascript
function main(params) {
    return { response: params };
}
```

このアクションが Web アクションとして起動された場合、結果から異なるパスを射影することで、Web アクションの応答を変更できます。
例えば、オブジェクト全体を返して、どの引数をアクションが受け取るかを確認するには、次のようにします。

```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json
```
{: pre}
```json
{
  "response": {
    "__ow_method": "get",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

さらに、照会パラメーターを使用する場合は、次のようになります。
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json?name=Jane
```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "get",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

または、形式データの場合は、次のようになります。
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -d "name":"Jane"
```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "10",      
      "content-type": "application/x-www-form-urlencoded",      
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

または、JSON オブジェクトの場合は、次のようになります。
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -H 'Content-Type: application/json' -d '{"name":"Jane"}'
```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "15",      
      "content-type": "application/json",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

名前 (テキストとして) のみを射影する場合は、次のようになります。
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.text/response/name?name=Jane
```
{: pre}
```
Jane
```

上記の例では、便宜上、照会パラメーター、形式データ、および JSON オブジェクト本体エンティティーはすべてディクショナリーとして扱われ、それぞれの値は、アクション入力プロパティーとして直接アクセス可能です。そうではなく、より直接的に HTTP 要求エンティティーを処理しようとする Web アクションの場合、あるいは Web アクションが JSON オブジェクトではないエンティティーを受け取る場合には、この例は当てはまりません。

上記と同じ例を使って、「text」コンテンツ・タイプを使用する例を以下に示します。
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -H 'Content-Type: text/plain' -d "Jane"
```
{: pre}
```json
{
  "response": {
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "4",      
      "content-type": "text/plain",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": "",
    "__ow_body": "Jane"
  }
}
```


## コンテンツ拡張子
{: #openwhisk_webactions_extensions}

Web アクションを起動する際には、通常、コンテンツ拡張子が必要です。拡張子がない場合は、デフォルトとして `.http` が想定されます。拡張子 `.json` および `.http` は、射影パスを必要としません。拡張子 `.html`、`.svg` および `.text` では必要ですが、簡便にするため、デフォルト・パスが拡張子名に一致すると想定されます。したがって、Web アクションを起動して、`.html` 応答を受け取るには、アクションは、`html` という名前の最上位プロパティーを含む JSON オブジェクトを用いて応答する必要があります (または、応答は明示的に指定されるパスに存在する必要があります)。 言い換えると、`/guest/demo/hello.html` は、`/guest/demo/hello.html/html` のように、`html` プロパティーを明示的に射影することと等価です。
アクションの完全修飾名にはそのアクションのパッケージ名が組み込まれている必要があり、指定されたパッケージ内にアクションがない場合は `default` になります。


## 保護されたパラメーター
{: #openwhisk_webactions_protected}

アクション・パラメーターを保護して、変更不可能として処理することもできます。パラメーターを最終決定するため、および、アクションを Web でアクセス可能にするためには、2 つの [アノテーション](openwhisk_annotations.html) をアクションに付加する必要があります。それは `final` と `web-export` であり、有効にするためにはどちらも `true` に設定する必要があります。前に説明したアクション・デプロイメントをもう一度使用して、これらのアノテーションを次のように追加できます。

```
wsk action create /guest/demo/hello hello.js \
      --parameter name Jane \
      --annotation final true \
      --annotation web-export true
```
{: pre}

これらの変更の結果は、`name` が `Jane` にバインドされ、final アノテーションがあるため照会パラメーターまたは本体パラメーターでオーバーライドされないことです。これは、意図的または偶発的にこの値を変更しようとする照会パラメーターまたは本体パラメーターからアクションを保護します。 

## Web アクションの無効化
{: #openwhisk_webactions_disable}

新規 API (`https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/web/`) を介した Web アクションの起動を無効にするには、アノテーションを削除するか、`false` に設定すればいいだけです。

```
wsk action update /guest/demo/hello hello.js \
      --annotation web-export false
```

## 未加工 HTTP 処理
{: #raw-http-handling}

Web アクションは、アクション入力に使用できる第 1 クラス・プロパティーに JSON オブジェクトをプロモーションせずに、着信 HTTP 本体を直接解釈して処理することを選択できます (例: `args.name` 対 `args.__ow_query` の構文解析)。これは、`raw-http` [アノテーション](openwhisk_annotations.html)を介して行います。前述と同じ例を使用しますが、今度は「未加工」HTTP Web アクションとして使用し、以下のように、照会パラメーターと HTTP 要求本体内の JSON 値の両方として `name` を受け取ります。
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json?name=Jane -X POST -H "Content-Type: application/json" -d '{"name":"Jane"}'
```
{: pre}
```json
{
    "response": {
    "__ow_method": "post",
    "__ow_query": "name=Jane",
    "__ow_body": "eyJuYW1lIjoiSmFuZSJ9",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "15",
      "content-type": "application/json",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"      
    },
    "__ow_path": ""
  }
}
```

この場合、JSON コンテンツはバイナリー値として扱われるので、base64 でエンコードされます。アクションは base64 をデコードし、JSON はこの値を解析して JSON オブジェクトをリカバリーする必要があります。OpenWhisk は、[Spray](https://github.com/spray/spray) フレームワークを使用して、どのコンテンツ・タイプがバイナリーであり、どれがプレーン・テキストであるかを[判別](https://github.com/spray/spray/blob/master/spray-http/src/main/scala/spray/http/MediaType.scala#L282)します。


### 未加工 HTTP 処理の有効化

未加工 HTTP Web アクションは、`true` の値を持つ `raw-http` [アノテーション](openwhisk_annotations.html)を介して有効化します。

```
wsk action create /guest/demo/hello hello.js \
      --annotation web-export true
      --annotation raw-http true
```
{: pre}

**注:** `raw-http` は `web-export` を暗黙指定するので、今後、これらのアノテーションを追加 (および削除) するためのより便利な方法を提供するように CLI を改善する計画です。


### 未加工 HTTP 処理の無効化

未加工 HTTP の無効化は、`raw-http` [アノテーション](openwhisk_annotations.html)の値を `false` に設定することで行います。

```
wsk update create /guest/demo/hello hello.js \
      --annotation web-export true
      --annotation raw-http false
```
{: pre}

**注:**  アクションの作成時または更新時には、1 つのアクションを対象にしたすべてのアノテーションを同時に設定する必要があります。これは、API と CLI にある現在の制限によるものです。このようにしないと、前に付けられたアノテーションはすべて削除されてしまいます。


## エラー処理
{: #openwhisk_webactions_errors}

OpenWhisk アクションで障害が起こるときには、2 つの障害モードがあります。1 つは*アプリケーション・エラー*と呼ばれるものであり、キャッチされた例外に似ています。アクションが返す JSON オブジェクトには、最上位に `error` プロパティーが含まれます。もう 1 つは *開発者エラー*であり、これはアクションで壊滅的な障害が起こって、応答が生成されない場合に発生します (これはキャッチされていない例外に似ています)。Web アクションに対して、コントローラーは以下のようにアプリケーション・エラーを処理します。

- 指定されたパス射影はすべて無視され、コントローラーは代わりに `error` プロパティーを射影します。
- コントローラーはアクションの拡張子で暗黙に示されるコンテンツ処理を `error` プロパティーの値に適用します。

開発者は Web アクションの使用方法としてどのようなものが考えられるのかを検討して、対応するエラー応答を生成しておく必要があります。例えば、`.http` 拡張子と共に使用される Web アクションは HTTP 応答 (例: `{error: { statusCode: 400 }`) を返す必要があります。これを行わないと、拡張子で暗黙に示されるコンテンツ・タイプと、エラー応答内のアクション・コンテンツ・タイプとが一致しないことになります。Web アクションがシーケンスになっている場合は、シーケンスを形成しているコンポーネントが必要に応じて適切なエラーを生成できるように、特別な考慮が必要です。

