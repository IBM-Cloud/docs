---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Web アクション (試験的)
{: #openwhisk_webactions}

Web アクションは、Web ベースのアプリケーションを迅速に作成することを可能にするためにアノテーションを付けた OpenWhisk アクションです。これを使用すると、Web アプリケーションが OpenWhisk 認証鍵を必要とせずに匿名でアクセスできるバックエンド・ロジックをプログラムできます。アクション開発者は、自由に独自の認証および許可 (つまり OAuth フロー) を実装できます。
{: shortdesc}

Web アクションのアクティベーションは、アクションを作成したユーザーと関連付けられます。この処理により、アクションのアクティベーションのコストは呼び出し元ではなく所有者が負うことになります。 

**注:** 現在、このフィーチャーは試験的オファリングであり、ユーザーはこれを早期に試してみて、フィードバックを提供することができます。

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

`web-export` アノテーションにより、アクションは新規 REST インターフェースを介して Web アクションとしてアクセス可能になります。構造化された URL は、`https://{APIHOST}/api/v1/experimental/web/{QUALIFIED ACTION NAME}.{EXT}` です。アクションの完全修飾名は、名前空間、パッケージ名、およびアクション名の 3 つの部分からなります。例えば、`guest/demo/hello` などです。URI の最後の部分は`拡張子`と呼ばれ、通常は `.http` ですが、後述するように他の値も許可されます。API キーなしで Web アクション API パスを `curl` または `wget` で使用できます。ブラウザーに直接入力することも可能です。

[https://${APIHOST}/api/v1/experimental/web/guest/demo/hello.http?name=Jane](https://${APIHOST}/api/v1/experimental/web/guest/demo/hello.http?name=Jane) を、ご使用の Web ブラウザーで開いてみてください。あるいは、次のように `curl` を介してこのアクションを起動してみてください。
```
curl https://openwhisk.{DomainName}/api/v1/experimental/web/guest/demo/hello.http?name=Jane
```
{: pre}
以下の Web アクション例は、HTTP リダイレクトを実行します。
```javascript
function main() {
  return {
    headers: { "location": "http://openwhisk.org" },
    code: 302
  }
}
```
{: codeblock}

以下は、Cookie を設定する例です。
```javascript
function main() {
  return { 
    headers: { 
      "Set-Cookie": "UserID=Jane; Max-Age=3600; Version=",
      "Content-Type": "text/html"  
    }, 
    code: 200, 
    body: "<html><body><h3>hello</h3></body></html" }
}
```
{: codeblock}

`image/png` を返す例は、次のようになります。
```javascript
function main() {
    let png = <base 64 encoded string>
    return { headers: { 'Content-Type': 'image/png' },
             code: 200,
             body: png };
}
```
{: codeblock}

以下の例は、`application/json` を返します。
```javascript
function main(params) { 
    return {
        'code': 200,
        'headers':{'Content-Type':'application/json'},
        'body' : new Buffer(JSON.stringify(params)).toString('base64'),
    };
}
```
{: codeblock}

事前定義されたシステム限度を超える応答は失敗するため、[応答サイズ限度](./openwhisk_reference.html)に注意することは重要です。例えば、ラージ・オブジェクトは OpenWhisk を通してインラインで送信するのではなく、オブジェクト・ストアに置くようにする必要があります。

## アクションを使用した HTTP 要求の処理
{: #openwhisk_webactions_http}

Web アクションでない OpenWhisk アクションは、認証を必要とし、JSON オブジェクトで応答することも必要です。対照的に、Web アクションは認証なしで起動でき、Web アクションを使用して、さまざまなタイプの *ヘッダー*、*状況コード*、および*本体*コンテンツを用いて応答する HTTP ハンドラーを実装できます。Web アクションはやはり JSON オブジェクトを返さなければなりませんが、OpenWhisk システム (つまり `Controller`) は、Web アクションの結果に最上位 JSON プロパティーとして以下のうち 1 つ以上が含まれている場合は、Web アクションを違う方法で処理します。

- `headers`: キーがヘッダー名であり、値がそれらのヘッダーのストリング値である、JSON オブジェクト (デフォルトはヘッダーなし)。
- `code`: 有効な HTTP 状況コード (デフォルトは 200 OK)。
- `body`: プレーン・テキストまたは Base64 エンコードのストリング (バイナリー・データの場合) のいずれかであるストリング。

コントローラーは、アクションが指定したヘッダーがあれば、要求/応答を終了するときに HTTP クライアントに渡します。同様に、コントローラーは、状況コードがあればそれを付けて応答します。最後に、本体が応答本体として渡されます。アクション結果の `headers` 内に `content-type header` が宣言されている場合を除いて、本体がストリングであるかのように渡されます (そうでない場合はエラーになります)。`content-type` が定義されている場合、コントローラーは応答がバイナリー・データなのかプレーン・テキストなのかを判別し、必要に応じて base64 デコーダーを使用してストリングをデコードします。本体を正しくデコードできない場合、呼び出し元にエラーが返されます。

*注:* JSON オブジェクトまたは配列は、バイナリー・データとして処理され、上の例のように base64 でエンコードされる必要があります。

## HTTP コンテキスト

Web アクションは、起動されると、アクションの入力引数への追加パラメーターとして使用可能なすべての HTTP 要求情報を受け取ります。それらは以下のとおりです。

- `__ow_meta_verb`: 要求の HTTP メソッド。
- `__ow_meta_headers`: 要求ヘッダー。
- `__ow_meta_path`: マッチングされていない要求のパス (マッチングはアクションの拡張子を取り込んだ後に停止します)。

上記の `__ow_` パラメーターの指定を要求がオーバーライドすることはできません。それを行うと、要求は 400 Bad Request と等しい状況で失敗します。

## 追加フィーチャー
{: #openwhisk_webactions_extra}

Web アクション用に次のようなフィーチャーが追加されました。

- `コンテンツ拡張子`: 要求は、その要求にとって望ましいコンテンツ・タイプを、`.json`、`.html`、`.text`、または `.http` のいずれかで指定する必要があります。これは、URI 内のアクション名に拡張子を追加することで行われます。これによって、例えば、アクション `/guest/demo/hello` は `/guest/demo/hello.http` として参照されて、HTTP 応答を受け取ります。
- `結果からのフィールドの射影`: アクション名の後に続くパスを使用して、応答の 1 つ以上のレベルが射影されます。例えば、`/guest/demo/hello.html/body` です。これによって、ディクショナリー `{body: "..." }` を返すアクションは、`body` プロパティーを射影して、代わりにそのストリング値を直接返すことができます。射影されたパスは、絶対パス・モデル (例: XPath) に従います。
- `入力としての照会パラメーターおよび本体パラメーター`: アクションは、照会パラメーターと、要求本体内のパラメーターを受け取ります。パラメーターをマージする際の優先順位は、パッケージ・パラメーター、アクション・パラメーター、照会パラメーター、本体パラメーターの順序であり、重なり合っている場合は、前の値がオーバーライドされます。例えば、`/guest/demo/hello.http?name=Jane` は、引数 `{name: "Jane"}` をアクションに渡します。
- `形式データ`: 標準 `application/json` に加えて、Web アクションは、入力としてデータ `application/x-www-form-urlencoded data` からエンコードされた URL を受け取ることができます。
- `複数の HTTP 動詞を介したアクティベーション`: Web アクションは、4 つの HTTP メソッド (`GET`、`POST`、`PUT`、または `DELETE`) のいずれかを介して起動できます。


以下の例は、Web アクションでこれらのフィーチャーを使用する方法を簡単に示しています。以下のような本体を持つアクション `/guest/demo/hello` があるとします。
```javascript
function main(params) {
    return { 'response': params};
}
```
{: codeblock}

照会パラメーター `name` を指定してこのアクションを起動し、JSON 応答を示すために `.json` 拡張子を使用し、フィールド `/response` を射影すると、以下の HTTP 応答が生成されます。
```
curl https://openwhisk.{DomainName}/api/v1/experimental/web/guest/demo/hello.json/response?name=Jane
```
{: pre}
```json
{
    "name": "Jane",
    "__ow_meta_verb": "get",
    "__ow_meta_headers": {
        "accept": "*/*",
        "user-agent": "curl/7.51.0"
    },
    "__ow_meta_path": "/response"
}
```

## コンテンツ拡張子
{: #openwhisk_webactions_extensions}

Web アクションを起動するときには、コンテンツ拡張子が必要です。拡張子 `.json` および `.http` は、射影パスを必要としません。拡張子 `.text` および `.html` では必要ですが、簡便にするため、デフォルト・パスが拡張子名に一致すると想定されます。したがって、Web アクションを起動して、`.html` 応答を受け取るには、アクションは、`html` という名前の最上位プロパティーを含む JSON オブジェクトを用いて応答する必要があります (または、応答は明示的に指定されるパスに存在する必要があります)。 言い換えると、`/guest/demo/hello.html` は、`/guest/demo/hello.html/html` のように、`html` プロパティーを明示的に射影することと等価です。
アクションの完全修飾名にはそのアクションのパッケージ名が組み込まれている必要があり、指定されたパッケージ内にアクションがない場合は `default` になります。


## 保護されたパラメーター
{: #openwhisk_webactions_protected}

アクション・パラメーターを保護して、変更不可能として処理することもできます。パラメーターを最終決定するため、および、アクションを Web でアクセス可能にするためには、2 つの [アノテーション](/openwhisk_annotations.html) をアクションに付加する必要があります。それは `final` と `web-export` であり、有効にするためにはどちらも `true` に設定する必要があります。前に説明したアクション・デプロイメントをもう一度使用して、これらのアノテーションを次のように追加できます。

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

新規 API (`https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/experimental/web/`) を介した Web アクションの起動を無効にするには、アノテーションを削除するか、`false` に設定すればいいだけです。

```
wsk action update /guest/demo/hello hello.js \
      --annotation web-export false
```
{: pre}     

## エラー処理
{: #openwhisk_webactions_errors}

OpenWhisk アクションで障害が起こるときには、2 つの障害モードがあります。1 つは*アプリケーション・エラー*と呼ばれるものであり、キャッチされた例外に似ています。アクションが返す JSON オブジェクトには、最上位に `error` プロパティーが含まれます。もう 1 つは *開発者エラー*であり、これはアクションで壊滅的な障害が起こって、応答が生成されない場合に発生します (これはキャッチされていない例外に似ています)。Web アクションに対して、コントローラーは以下のようにアプリケーション・エラーを処理します。

- 指定されたパス射影はすべて無視され、コントローラーは代わりに `error` プロパティーを射影します。
- コントローラーはアクションの拡張子で暗黙に示されるコンテンツ処理を `error` プロパティーの値に適用します。

開発者は Web アクションの使用方法としてどのようなものが考えられるのかを検討して、対応するエラー応答を生成しておく必要があります。例えば、`.http` 拡張子と共に使用される Web アクションは HTTP 応答 (例: `{error: { code: 400 }`) を返す必要があります。これを行わないと、拡張子で暗黙に示されるコンテンツ・タイプと、エラー応答内のアクション・コンテンツ・タイプとが一致しないことになります。Web アクションがシーケンスになっている場合は、シーケンスを形成しているコンポーネントが必要に応じて適切なエラーを生成できるように、特別な考慮が必要です。
