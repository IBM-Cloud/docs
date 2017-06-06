---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-24"

---

{:shortdesc: .shortdesc}
{:codeblock:.codeblock}
{:screen:.screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} システムの詳細
{: #openwhisk_reference}


以下のセクションでは、{{site.data.keyword.openwhisk}} システムについて詳しく説明します。
{: shortdesc}

## {{site.data.keyword.openwhisk_short}} のエンティティー
{: #openwhisk_entities}

### 名前空間とパッケージ
{: #openwhisk_entities_namespaces}

{{site.data.keyword.openwhisk_short}} のアクション、トリガー、およびルールは、名前空間と、オプションでパッケージに属します。

パッケージは、アクションとフィードを含むことができます。パッケージに別のパッケージを含めることはできないため、パッケージのネスティングはできません。また、エンティティーをパッケージに含める必要はありません。

Bluemix では、組織とスペースのペアが {{site.data.keyword.openwhisk_short}} 名前空間に相当します。
例えば、組織 `BobsOrg` とスペース `dev` は {{site.data.keyword.openwhisk_short}} 名前空間
`/BobsOrg_dev` に相当します。

ユーザー固有の名前空間の作成も、該当する権限があれば可能です。
名前空間 `/whisk.system` は、{{site.data.keyword.openwhisk_short}} システムで配布されるエンティティー用に予約済みです。


### 完全修飾名
{: #openwhisk_entities_fullyqual}

エンティティーの完全修飾名は、`/namespaceName[/packageName]/entityName` です。
名前空間、パッケージ、エンティティーの区切りに `/` が使用されることに注意してください。
また、名前空間の前には必ず `/` を付けてください。

便宜上、ユーザーの*デフォルト名前空間* である名前空間は、省略できます。

例えば、ユーザーのデフォルト名前空間が `/myOrg` であるとします。
以下に、いくつかのエンティティーの完全修飾名と別名の例を示します。

| 完全修飾名 | 別名 | 名前空間 | パッケージ | 名前 |
| --- | --- | --- | --- | --- |
| `/whisk.system/cloudant/read` |  | `/whisk.system` | `cloudant` | `read` |
| `/myOrg/video/transcode` | `video/transcode` | `/myOrg` | `video` | `transcode` |
| `/myOrg/filter` | `filter` | `/myOrg` |  | `filter` |

中でも特に {{site.data.keyword.openwhisk_short}} CLI を使用する場合、この命名体系を使用します。

### エンティティー名
{: #openwhisk_entities_names}

アクション、トリガー、ルール、パッケージ、名前空間を含むすべてのエンティティーの名前は、以下のフォーマットに従った文字列になります。

* 先頭文字は、英数字または下線でなければなりません。
* 後続の文字には、英数字、スペース、または `_`、`@`、`.`、`-` のどれでも含めることができます。
* 最後の文字をスペースにすることはできません。

より正確に言うと、名前は次の (Java メタキャラクター構文で表した) 正規表現に一致する必要があります。`\A([\w]|[\w][\w@ .-]*[\w@.-]+)\z`


## アクションのセマンティクス
{: #openwhisk_semantics}

以下のセクションでは、{{site.data.keyword.openwhisk_short}} アクションについて詳しく説明します。

### ステートレス
{: #openwhisk_semantics_stateless}

アクションの実装はステートレス、つまり*べき等* である必要があります。この特性はシステムによって強制されませんが、アクションで維持された状態が、呼び出しをまたがって使用可能である保証はありません。

さらに、アクションの複数のインスタンス化が存在して、それぞれのインスタンス化が固有の状態であることもあります。アクションの呼び出しは、これらの中で任意のインスタンス化にディスパッチされる可能性があります。

### 呼び出しの入力および出力
{: #openwhisk_semantics_invocationio}

アクションに対する入力および出力は、キーと値のペアのディクショナリーです。キーはストリングで、値は有効な JSON 値です。

### アクションの呼び出し順序
{: #openwhisk_ordering}

アクションの呼び出しは順序付けられません。ユーザーがコマンド・ラインまたは REST API からアクションを 2 回呼び出した場合に、2 番目の呼び出しが最初の呼び出しより前に実行される可能性があります。アクションに副次作用がある場合、それらが検出される順序は一定ではありません。

さらに、アクションがアトミックに実行される保証はありません。2 つのアクションが並行して実行され、その副次作用がインターリーブする可能性があります。
OpenWhisk は、副次作用として特定の並行一貫性モデルを保証しません。
並行性の副次作用は実装に依存します。

### アクション実行の保証
{: #openwhisk_atmostonce}

呼び出し要求が受信されると、システムは要求を記録し、アクティベーションをディスパッチします。

システムは (非ブロッキング呼び出しの場合) アクティベーション ID を返し、呼び出しが受信されたことを確認します。HTTP 応答を受け取る前にネットワーク障害またはその他の障害が介在する場合に {{site.data.keyword.openwhisk_short}} が要求を受け取って処理した可能性があることに注意してください。

システムはアクションの呼び出しを 1 回試行します。これにより、以下の 4 つのいずれかの結果になります。
- *success (成功)* : アクションの呼び出しが正常に完了しました。
- *application error (アプリケーション・エラー)* : アクションの呼び出しは成功しましたが、引数の前提条件が満たされなかったなどの理由で、アクションが意図的にエラー値を返しました。
- *action developer error (アクション開発者エラー)* : アクションが呼び出されましたが、異常終了しました。例えば、アクションが例外を検出しなかったり、または、構文エラーがあったりしました。
- *whisk internal error (whisk 内部エラー)* : システムがアクションを呼び出せませんでした。
結果は、以下のセクションに示されているように、アクティベーション・レコードの `status` フィールドに記録されます。

正常に受信され、ユーザーに課金されるすべての呼び出しには、最終的にアクティベーション・レコードがあります。

*action developer error* (アクション開発者エラー) の場合、アクションが部分的に実行されて外部で可視の副作用を生成した可能性があることに注意してください。そういった副作用が実際に起こったかどうかをチェックし、必要であれば再試行ロジックを実行するのは、ユーザーの責任です。また、ある種の *whisk internal errors* (whisk 内部エラー) は、アクションが実行を開始したが、アクションが完了を登録する前にシステムで障害が起こったことを示すことに注意してください。

## アクティベーション・レコード
{: #openwhisk_ref_activation}

各アクションの呼び出しおよびトリガーの発生により、アクティベーション・レコードが生成されます。

アクティベーション・レコードには、以下のフィールドが含まれています。

- *activationId* : アクティベーション ID。
- *start* および *end* : アクティベーションの開始と終了を記録するタイム・スタンプ。値は、[UNIX の時刻形式](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap04.html#tag_04_15)です。
- *namespace* および `name`: エンティティーの名前空間および名前。
- *logs* : アクティベーション中にアクションによって生成されたログを含むストリング配列。各配列エレメントは、アクションによって `stdout` または `stderr` に出力された行に対応し、ログ出力の時刻とストリームを含みます。構造は `TIMESTAMP STREAM: LOG_OUTPUT` です。
- *response* : `success`、`status`、および `result` のキーを定義したディクショナリー。
  - *status* : アクティベーションの結果。「success (成功)」、「application error (アプリケーション・エラー)」、「action developer error (アクション開発者エラー)」、「whisk internal error (whisk 内部エラー)」のいずれかの値が可能です。
  - *success* : 状況が`「success」`の場合に限り、`true` になります。
- *result* : アクティベーションの結果を含むディクショナリー。アクティベーションが成功した場合、アクションによって返された値がこれに入ります。アクティベーションが成功しなかった場合、`result` に `error` キーが含まれます。これには通常、失敗の説明が伴います。


## JavaScript アクション
{: #openwhisk_ref_javascript}

### 関数プロトタイプ
{: #openwhisk_ref_javascript_fnproto}

{{site.data.keyword.openwhisk_short}} JavaScript アクションは、Node.js ランタイムで実行されます。

JavaScript で記述されたアクションは、単一ファイルに限定されなければなりません。ファイルは複数の関数を含むことができますが、規則により `main` という関数が存在しなければならず、これが、アクションを起動したときに呼び出されます。例えば、以下は、複数の関数を含むアクションの例です。

```
function main() {
    return { payload: helper() }
}

function helper() {
    return new Date();
}
```
{: codeblock}

アクションの入力パラメーターは、`main` 関数へのパラメーターで JSON オブジェクトとして渡されます。成功したアクティベーションの結果も JSON オブジェクトですが、これは、以下のセクションに示すように、アクションが同期か非同期かによって、戻り方が異なります。


### 同期と非同期の動作
{: #openwhisk_ref_javascript_synchasynch}

JavaScript 関数が、戻った後でもコールバック関数で実行を続行することはよくあります。これに対応するため、JavaScript アクションのアクティベーションは、*同期* にすることも*非同期* にすることもできます。

JavaScript アクションのアクティベーションは、main 関数が以下のいずれかの条件で終了する場合に**同期**となります。

- main 関数が `return` ステートメントを実行せずに終了する。
- main 関数が `return` ステートメントを実行して終了し、Promise *以外* の値を返す。

以下は、同期アクションの例です。

```
// an action in which each path results in a synchronous activation
function main(params) {
  if (params.payload == 0) {
     return;
  } else if (params.payload == 1) {
     return {payload: 'Hello, World!'};
  } else if (params.payload == 2) {
    return {error: 'payload must be 0 or 1'};
  }
}
```
{: codeblock}

JavaScript アクションのアクティベーションは、main 関数が Promise を返して終了する場合に**非同期**となります。この場合、Promise が完了するか、拒否されるまで、システムはアクションがまだ実行中であると見なします。
まず、新規の Promise オブジェクトをインスタンス化して、それをコールバック関数に渡します。コールバックは、resolve と reject という 2 つの引数を使用します。これらはどちらも関数です。すべての非同期コードが、そのコールバックに入っていきます。


以下は、resolve 関数を呼び出して Promise を完了する方法の例です。

```
function main(args) {
     return new Promise(function(resolve, reject) {
       setTimeout(function() {
         resolve({ done: true });
       }, 100);
    })
 }
```
{: codeblock}

以下は、reject 関数を呼び出して Promise を拒否する方法の例です。

```
function main(args) {
     return new Promise(function(resolve, reject) {
       setTimeout(function() {
         reject({ done: true });
       }, 100);
    })
 }
```
{: codeblock}

アクションは、ある入力では同期で、別の入力では非同期であることもあります。以下に例を示します。

```
  function main(params) {
      if (params.payload) {
         // asynchronous activation
         return new Promise(function(resolve, reject) {
                setTimeout(function() {
                  resolve({ done: true });
                }, 100);
             })
      }  else {
         // synchronous activation
         return {done: true};
      }
  }
```
{: codeblock}

アクティベーションが同期か非同期かに関係なく、アクションの呼び出しにはブロッキングまたは非ブロッキングが可能です。

### JavaScript グローバル whisk オブジェクトの削除

グローバル・オブジェクト `whisk` が削除されました。nodejs アクションをマイグレーションして代替メソッドを使用するようにしてください。
関数 `whisk.invoke()` および `whisk.trigger()` には、既にインストール済みのクライアント・ライブラリーの [openwhisk](https://www.npmjs.com/package/openwhisk) を使用してください。
`whisk.getAuthKey()` では、環境変数 `__OW_API_KEY` から API キー値を取得できます。
`whisk.error()` では、拒否された Promise (つまり Promise.reject) を返すことができます。

### JavaScript ランタイム環境
{: #openwhisk_ref_javascript_environments}

JavaScript アクションは、デフォルトで Node.js バージョン 6.9.1 環境で実行されます。アクションの作成/更新時に `--kind` フラグが値「nodejs:6」で明示的に指定された場合にも、6.9.1 環境がアクションに使用されます。
Node.js 6.9.1 環境では、以下のパッケージを使用できます。

- apn v2.1.2
- async v2.1.4
- btoa v1.1.2
- cheerio v0.22.0
- cloudant v1.6.2
- commander v2.9.0
- consul v0.27.0
- cookie-parser v1.4.3
- cradle v0.7.1
- errorhandler v1.5.0
- glob v7.1.1
- gm v1.23.0
- lodash v4.17.2
- log4js v0.6.38
- iconv-lite v0.4.15
- marked v0.3.6
- merge v1.2.0
- moment v2.17.0
- mongodb v2.2.11
- mustache v2.3.0
- nano v6.2.0
- node-uuid v1.4.7
- nodemailer v2.6.4
- oauth2-server v2.4.1
- openwhisk v3.3.2
- pkgcloud v1.4.0
- process v0.11.9
- pug v2.0.0-beta6
- redis v2.6.3
- request v2.79.0
- request-promise v4.1.1
- rimraf v2.5.4
- semver v5.3.0
- sendgrid v4.7.1
- serve-favicon v2.3.2
- socket.io v1.6.0
- socket.io-client v1.6.0
- superagent v3.0.0
- swagger-tools v0.10.1
- tmp v0.0.31
- twilio v2.11.1
- underscore v1.8.3
- uuid v3.0.0
- validator v6.1.0
- watson-developer-cloud v2.29.0
- when v3.7.7
- winston v2.3.0
- ws v1.1.1
- xml2js v0.4.17
- xmlhttprequest v1.8.0
- yauzl v2.7.0


## Python ランタイム環境
{: #openwhisk_ref_python_environments}

OpenWhisk は、異なる 2 つのランタイム・バージョンを使用した Python アクションの実行をサポートします。

### Python 3 アクション

Python 3 アクションは、Python 3.6.1 を使用して実行されます。このランタイムを使用するには、アクションの作成または更新時に `wsk` CLI パラメーター `--kind python:3` を指定します。
Python 3.6 の標準ライブラリーに加えて、以下のパッケージも Python アクションによって使用可能です。

- aiohttp v1.3.3
- appdirs v1.4.3
- asn1crypto v0.21.1
- async-timeout v1.2.0
- attrs v16.3.0
- beautifulsoup4 v4.5.1
- cffi v1.9.1
- chardet v2.3.0
- click v6.7
- cryptography v1.8.1
- cssselect v1.0.1
- Flask v0.12
- gevent v1.2.1
- greenlet v0.4.12
- httplib2 v0.9.2
- idna v2.5
- itsdangerous v0.24
- Jinja2 v2.9.5
- kafka-python v1.3.1
- lxml v3.6.4
- MarkupSafe v1.0
- multidict v2.1.4
- packaging v16.8
- parsel v1.1.0
- pyasn1 v0.2.3
- pyasn1-modules v0.0.8
- pycparser v2.17
- PyDispatcher v2.0.5
- pyOpenSSL v16.2.0
- pyparsing v2.2.0
- python-dateutil v2.5.3
- queuelib v1.4.2
- requests v2.11.1
- Scrapy v1.1.2
- service-identity v16.0.0
- simplejson v3.8.2
- six v1.10.0
- Twisted v16.4.0
- w3lib v1.17.0
- Werkzeug v0.12
- yarl v0.9.8
- zope.interface v4.3.3

### Python 2 アクション

Python 2 アクションは、Python 2.7.12 を使用して実行されます。アクションの作成または更新時に `--kind` フラグを指定していない限り、これが Python アクションのデフォルト・ランタイムです。このランタイムを明示的に選択するには、`--kind python:2` を使用します。Python 2.7 の標準ライブラリーに加えて、以下のパッケージも Python 2 アクションによって使用可能です。

- appdirs v1.4.3
- asn1crypto v0.21.1
- attrs v16.3.0
- beautifulsoup4 v4.5.1
- cffi v1.9.1
- click v6.7
- cryptography v1.8.1
- cssselect v1.0.1
- enum34 v1.1.6
- Flask v0.11.1
- gevent v1.1.2
- greenlet v0.4.12
- httplib2 v0.9.2
- idna v2.5
- ipaddress v1.0.18
- itsdangerous v0.24
- Jinja2 v2.9.5
- kafka-python v1.3.1
- lxml v3.6.4
- MarkupSafe v1.0
- packaging v16.8
- parsel v1.1.0
- pyasn1 v0.2.3
- pyasn1-modules v0.0.8
- pycparser v2.17
- PyDispatcher v2.0.5
- pyOpenSSL v16.2.0
- pyparsing v2.2.0
- python-dateutil v2.5.3
- queuelib v1.4.2
- requests v2.11.1
- Scrapy v1.1.2
- service-identity v16.0.0
- simplejson v3.8.2
- six v1.10.0
- Twisted v16.4.0
- virtualenv v15.1.0
- w3lib v1.17.0
- Werkzeug v0.12
- zope.interface v4.3.3

## Docker アクション
{: #openwhisk_ref_docker}

Docker アクションは、Docker コンテナーでユーザー提供バイナリーを実行します。バイナリーは、[python:2.7.12-alpine](https://hub.docker.com/r/library/python) に基づく Docker イメージで実行されるため、バイナリーはこのディストリビューションと互換でなければなりません。

Docker スケルトンは、OpenWhisk 互換の Docker イメージをビルドするための便利な方法です。`wsk sdk install docker` CLI コマンドでスケルトンをインストールできます。

メイン・バイナリー・プログラムはコンテナー内部の `/action/exec` に置かれる必要があります。実行可能バイナリーは、`JSON` オブジェクトとしてデシリアライズ可能な単一コマンド・ライン引数ストリングを介して、入力引数を受け取ります。また、シリアライズされた `JSON` の単一行ストリングとして、`stdout` を介して結果を返す必要があります。

`dockerSkeleton` 内に含まれている `Dockerfile` を変更して、コンパイル・ステップや依存関係を組み込むこともできます。

## REST API
{: #openwhisk_ref_restapi}
REST API に関する情報は、[ここ](openwhisk_rest_api.html)を参照してください。


## システムしきい値
{: #openwhisk_syslimits}

### アクション
{{site.data.keyword.openwhisk_short}} には、1 つのアクションが使用できるメモリー量、1 分当たりの許容されるアクション起動数など、いくつかのシステム制限があります。

以下の表に、アクションのデフォルトの限度を示します。

| 限度 | 説明 | 構成対象 | 単位 | デフォルト |
| ----- | ----------- | ------------ | -----| ------- |
| timeout | N ミリ秒を超えてコンテナーを実行することはできません。 | アクション当たり |  ミリ秒 | 60000 |
| memory | N MB を超えるメモリーをコンテナーに割り振ることはできません。 | アクション当たり | MB | 256 |
| logs | コンテナーは、N MB を超えて stdout に書き込むことはできません。 | アクション当たり | MB | 10 |
| concurrent | 名前空間当たりに送信できる、実行中または実行用にキューに入れられているアクティベーションは N 個までです。 | 名前空間当たり | 数 | 1000 |
| minuteRate | 分当たり、名前空間当たりに送信できるアクティベーションは N 個までです。 | ユーザー当たり | 数 | 5000 |
| codeSize | アクション・コードの最大サイズ | 構成することはできません。アクション当たりの限度です。 | MB | 48 |
| parameters | 付加できるパラメーターの最大サイズです。 | 構成することはできません。アクション/パッケージ/トリガー当たりの限度です。 | MB | 1 |

### アクション当たりのタイムアウト (ms) (デフォルト: 60s)
{: #openwhisk_syslimits_timeout}
* タイムアウト限度の N は [100ms..300000ms] の範囲内で、アクション当たりのミリ秒数で設定されます。
* ユーザーは、アクションの作成時に限度を変更することができます。
* N ミリ秒を超えて実行したコンテナーは、終了されます。

### アクション当たりのメモリー (MB) (デフォルト: 256MB)
{: #openwhisk_syslimits_memory}
* メモリー限度の M は [128MB..512MB] の範囲内で、アクション当たりの MB 数で設定されます。
* ユーザーは、アクションの作成時に限度を変更することができます。
* コンテナーに限度を超えるメモリーを割り振ることはできません。

### アクション当たりのログ (MB) (デフォルト: 10MB)
{: #openwhisk_syslimits_logs}
* ログ限度の N は [0MB..10MB] の範囲内で、アクション当たりで設定されます。
* ユーザーは、アクションの作成または更新時に限度を変更することができます。
* 設定された限度を超えたログは切り捨てられ、アクティベーションの最後の出力として、アクティベーションが設定されたログ限度を超えたことを示す警告が追加されます。

### アクション当たりの成果物 (MB) (固定: 48MB)
{: #openwhisk_syslimits_artifact}
* アクションの最大コード・サイズは 48MB です。
* JavaScript アクションの場合は、ツールを使用して、依存関係を含むすべてのソース・コードを単一のバンドル・ファイルに連結することをお勧めします。

### アクティベーション当たりのペイロード・サイズ (MB) (固定: 1 MB)
{: #openwhisk_syslimits_activationsize}
* 最大 POST コンテンツ・サイズに、アクション呼び出しまたはトリガー発生用の付随するパラメーターを加えたものが 1 MB です。

### 名前空間当たりの同時呼び出し (デフォルト: 1000)
{: #openwhisk_syslimits_concur}
* 1 つの名前空間で実行中または実行用にキューに入れられているアクティベーションの数が 1000 を超えることはできません。
* デフォルト限度は、consul kvstore で whisk によって静的に構成可能です。
* ユーザーは現在この限度を変更できません。

### 分当たりの呼び出し数 (固定: 5000)
{: #openwhisk_syslimits_invocations}
* レート限度の N は 5000 に設定され、1 分の枠内のアクション呼び出し数を制限します。
* ユーザーがアクションの作成時にこの限度を変更することはできません。
* この限度を超える CLI または API 呼び出しは、HTTP 状況コード `429: TOO MANY REQUESTS` に対応するエラー・コードを受け取ります。

### パラメーターのサイズ (固定: 1 MB)
{: #openwhisk_syslimits_parameters}
* アクション/パッケージ/トリガーの作成または更新に関するパラメーターのサイズ限度は 1 MB です。
* この限度をユーザーが変更することはできません。
* パラメーターが大き過ぎるエンティティーを作成または更新しようとすると、拒否されます。

### Docker アクション当たりのオープン・ファイル数の制限 (固定: 64:64)
{: #openwhisk_syslimits_openulimit}
* オープン・ファイルの最大数は 64 です (ハード制限とソフト制限の両方)。
* docker run コマンドは、引数 `--ulimit nofile=64:64` を使用します。
* オープン・ファイル数の制限について詳しくは、[docker run](https://docs.docker.com/engine/reference/commandline/run) の資料を参照してください。

### Docker アクション当たりのプロセスの制限 (固定: 512:512)
{: #openwhisk_syslimits_proculimit}
* ユーザーが使用可能なプロセスの最大数は 512 です (ハード制限とソフト制限の両方)。
* docker run コマンドは、引数 `--ulimit nproc=512:512` を使用します。
* プロセスの最大数の制限について詳しくは、[docker run](https://docs.docker.com/engine/reference/commandline/run) の資料を参照してください。

### トリガー

次の表に示すように、トリガーには分当たりの発生頻度の制限が課されます。

| 限度 | 説明 | 構成対象 | 単位 | デフォルト |
| ----- | ----------- | ------------ | -----| ------- |
| minuteRate | 分当たり、名前空間当たりに起動できるトリガーは N 個までです。 | ユーザー当たり | 数 | 5000 |

### 分当たりのトリガー数 (固定: 5000)
* 発生頻度の限度 N は 5000 に設定され、1 分の枠内のトリガー発生数を制限します。
* ユーザーがトリガーの作成時にこの限度を変更することはできません。
* この限度を超える CLI または API 呼び出しは、HTTP 状況コード `429: TOO MANY REQUESTS` に対応するエラー・コードを受け取ります。
