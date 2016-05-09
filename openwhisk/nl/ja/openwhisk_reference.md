---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock:.codeblock}
{:screen:.screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} システムの詳細
{: #openwhisk_reference}
*最終更新日: 2016 年 4 月 14 日*

以下のセクションでは、{{site.data.keyword.openwhisk}} システムについて詳しく説明します。
{: shortdesc}

## {{site.data.keyword.openwhisk_short}} のエンティティー
{: #openwhisk_entities}

### 名前空間とパッケージ

{{site.data.keyword.openwhisk_short}} のアクション、トリガー、およびルールは、名前空間と、オプションでパッケージに属します。

パッケージは、アクションとフィードを含むことができます。パッケージに別のパッケージを含めることはできないため、パッケージのネスティングはできません。また、エンティティーをパッケージに含める必要はありません。

Bluemix では、組織とスペースのペアが {{site.data.keyword.openwhisk_short}} 名前空間に相当します。
例えば、組織 `BobsOrg` とスペース `dev` は {{site.data.keyword.openwhisk_short}} 名前空間
`/BobsOrg_dev` に相当します。

ユーザー固有の名前空間の作成も、該当する権限があれば可能です。
名前空間 `/whisk.system` は、{{site.data.keyword.openwhisk_short}} システムで配布されるエンティティー用に予約済みです。


### 完全修飾名

エンティティーの完全修飾名は、`/namespaceName[/packageName]/entityName` です。
名前空間、パッケージ、エンティティーの区切りに `/` が使用されることに注意してください。
また、名前空間の前には必ず `/` を付けてください。

便宜上、ユーザーのデフォルト名前空間である名前空間は、省略できます。

例えば、ユーザーのデフォルト名前空間が `/myOrg` であるとします。
以下に、いくつかのエンティティーの完全修飾名と別名の例を示します。


| 完全修飾名 | 別名 | 名前空間 | パッケージ | 名前 |
| --- | --- | --- | --- | --- |
| `/whisk.system/cloudant/read` | - | `/whisk.system` | `cloudant` | `read` |
| `/myOrg/video/transcode` | `video/transcode` | `/myOrg` | `video` | `transcode` |
| `/myOrg/filter` | `filter` | `/myOrg` | - | `filter` |

中でも特に {{site.data.keyword.openwhisk_short}} CLI を使用する場合、この命名体系を使用します。

### エンティティー名

アクション、トリガー、ルール、パッケージ、名前空間を含むすべてのエンティティーの名前は、
以下のフォーマットに従った文字列になります。

* 先頭文字は、英数字、数字、またはアンダースコアーでなければなりません。
* 後続の文字には、英数字、数字、スペース、または `_`、`@`、`.`、`-` のどれでも含めることができます。
* 最後の文字をスペースにすることはできません。

より正確に言うと、名前は次の (Java メタキャラクター構文で表した) 正規表現に一致する必要があります。`\A([\w]|[\w][\w@ .-]*[\w@.-]+)\z`


## アクションのセマンティクス
{: #openwhisk_semantics}

以下のセクションでは、{{site.data.keyword.openwhisk_short}} アクションについて詳しく説明します。

### ステートレス

アクションの実装はステートレス、つまり*べき等* である必要があります。この特性はシステムによって強制されませんが、アクションで維持された状態が、呼び出しをまたがって使用可能である保証はありません。

さらに、アクションの複数のインスタンス化が存在して、それぞれのインスタンス化が固有の状態であることもあります。アクションの呼び出しは、これらの中で任意のインスタンス化にディスパッチされる可能性があります。

### 呼び出しの入力および出力

アクションに対する入力および出力は、キーと値のペアのディクショナリーです。キーはストリングで、値は有効な JSON 値です。

### アクションの呼び出し順序
{: #openwhisk_ordering}

アクションの呼び出しは順序付けられません。ユーザーがコマンド・ラインまたは REST API からアクションを 2 回呼び出した場合に、2 番目の呼び出しが最初の呼び出しより前に実行される可能性があります。アクションに副次作用がある場合、それらが検出される順序は一定ではありません。

さらに、アクションがアトミックに実行される保証はありません。2 つのアクションが並行して実行され、その副次作用がインターリーブする可能性があります。並行性の副次作用は実装に依存します。

### 最高 1 回 (At most once) のセマンティクス
{: #openwhisk_atmostonce}

システムでは、アクションの最高 1 回の呼び出しをサポートします。

呼び出し要求が受信されると、システムは要求を記録し、アクティベーションをディスパッチします。

システムは (非ブロッキング呼び出しの場合) アクティベーション ID を返し、呼び出しが受信されたことを確認します。
(おそらくネットワーク接続の障害により) この応答がなくても、呼び出しは受信されている可能性があります。

システムはアクションの呼び出しを 1 回試行します。これにより、以下の 4 つのいずれかの結果になります。
- *success (成功)* : アクションの呼び出しが正常に完了しました。
- *application error (アプリケーション・エラー)* : アクションの呼び出しは成功しましたが、引数の前提条件が満たされなかったなどの理由で、アクションが意図的にエラー値を返しました。
- *action developer error (アクション開発者エラー)* : アクションが呼び出されましたが、異常終了しました。例えば、アクションが例外をキャッチしなかったり、または、構文エラーがあったりしました。
- *whisk internal error (whisk 内部エラー)* : システムがアクションを呼び出せませんでした。
結果は、以下のセクションに示されているように、アクティベーション・レコードの `status` フィールドに記録されます。

正常に受信され、ユーザーに課金されるすべての呼び出しには、最終的にアクティベーション・レコードがあります。


## アクティベーション・レコード
{: #openwhisk_ref_activation}

各アクションの呼び出しおよびトリガーの発生により、アクティベーション・レコードが生成されます。

アクティベーション・レコードには、以下のフィールドが含まれています。

- *activationId* : アクティベーション ID。
- *start* および *end* : アクティベーションの開始と終了を記録するタイム・スタンプ。値は、[UNIX の時刻形式](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap04.html#tag_04_15)です。
- *namespace* および `name`: エンティティーの名前空間および名前。
- *logs* : アクティベーション中にアクションによって生成されたログを含むストリング配列。各配列エレメントは、アクションによって標準出力または標準エラー出力に出力された行に対応し、ログ出力の時刻とストリームを含みます。構造は、次のとおりです。```TIMESTAMP STREAM: LOG_OUTPUT```
- *response* : `success`、`status`、および `result` のキーを定義したディクショナリー。
  - *status* : アクティベーションの結果。「success (成功)」、「application error (アプリケーション・エラー)」、「action developer error (アクション開発者エラー)」、「whisk internal error (whisk 内部エラー)」のいずれかの値が可能です。
  - *success* : 状況が`「success」`の場合に限り、`true` になります。
- *result* : アクティベーションの結果を含むディクショナリー。アクティベーションが成功した場合、アクションによって返された値がこれに入ります。アクティベーションが成功しなかった場合、`result` に必ず `error` キーが含まれます。これには通常、失敗の説明が伴います。


## JavaScript アクション
{: #openwhisk_ref_javascript}

### 関数プロトタイプ

{{site.data.keyword.openwhisk_short}} JavaScript アクションは、現在はバージョン 0.12.9 の Node.js ランタイムで実行されます。

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

JavaScript 関数が、戻った後でもコールバック関数で実行を続行することはよくあります。これに対応するため、JavaScript アクションのアクティベーションは、*同期* にすることも*非同期* にすることもできます。

JavaScript アクションのアクティベーションは、main 関数が以下のいずれかの条件で終了する場合に**同期**となります。

- main 関数が ```return``` ステートメントを実行せずに終了する。
- main 関数が、```whisk.async()``` *以外の* 任意の値を返す ```return`` ステートメントを実行して終了する。

以下に、同期アクションの例を 2 つ示します。

```
// a synchronous action
function main() {
  return {payload: 'Hello, World!'};
}
```
{: codeblock}

```
// an action in which each path results in a synchronous activation
function main(params) {
  if (params.payload == 0) {
     return;
  } else if (params.payload == 1) {
     return whisk.done();    // indicates normal completion
  } else if (params.payload == 2) {
    return whisk.error();   // indicates abnormal completion
  }
}
```
{: codeblock}

JavaScript アクションのアクティベーションは、main 関数が ```return whisk.async();``` を呼び出して終了する場合に**非同期**となります。この場合、システムは、以下のいずれかをアクションが実行するまで、アクションがまだ実行中であると見なします。
- ```return whisk.done();```
- ```return whisk.error();```

以下は、非同期に実行されるアクションの例です。

```
function main() {
    setTimeout(function() {
        return whisk.done({done: true});
    }, 100);
    return whisk.async();
}
```
{: codeblock}

アクションは、ある入力では同期で、別の入力では非同期であることもあります。以下に例を示します。

```
  function main(params) {
      if (params.payload) {
         setTimeout(function() {
            return whisk.done({done: true});
         }, 100);
         return whisk.async();  // asynchronous activation
      }  else {
         return whisk.done();   // synchronous activation
      }
  }
```
{: codeblock}

- このケースで、`main` 関数は `whisk.async()` を返します。アクティベーションの結果が使用可能である場合、`whisk.done()` 関数が呼び出され、結果が JSON オブジェクトとして渡されます。これは、*非同期* アクティベーションと呼ばれます。

アクティベーションが同期か非同期かに関係なく、アクションの呼び出しにはブロッキングまたは非ブロッキングが可能です。

### 追加の SDK メソッド

`whisk.invoke()` 関数は、別のアクションを呼び出します。引数として、以下のパラメーターを定義したディクショナリーを使用します。

- *name* : 呼び出すアクションの完全修飾名。
- *parameters* : 呼び出されたアクションへの入力を表す JSON オブジェクト。省略された場合、デフォルトは空のオブジェクトです。
- *apiKey* : アクションの呼び出しに使用する許可キー。
デフォルトは `whisk.getAuthKey()` です。 
- *blocking* : アクションをブロッキング・モードと非ブロッキング・モードのどちらで呼び出すか。デフォルトは `false` で、非ブロッキングの呼び出しを指示します。
- *next* : 呼び出しの完了時に実行するオプションのコールバック関数。

`next` のシグニチャーは `function(error, activation)` です。ここで、以下が適用されます。

- 呼び出しが成功した場合、`error` は `false` です。失敗した場合は、true を表す値で、通常、エラーを記述するストリングになります。
- エラーの場合、`activation` は、失敗のモードによっては未定義であることがあります。
- `activation` は、定義されている場合には、以下のフィールドがあるディクショナリーです。
  - *activationId* : アクティベーション ID。
  - *result* : アクションがブロッキング・モードで呼び出された場合: アクション結果の JSON オブジェクト、あるいは `undefined`。

`whisk.trigger()` 関数は、トリガーを起動します。引数として、以下のパラメーターを含む JSON オブジェクトを使用します。

- *name* : 呼び出すトリガーの完全修飾名。
- *parameters* : トリガーへの入力を表す JSON オブジェクト。省略された場合、デフォルトは空のオブジェクトです。
- *apiKey* : トリガーの起動に使用する許可キー。デフォルトは `whisk.getAuthKey()` です。
- *next* : 起動完了時に実行されるオプションのコールバック。

`next` のシグニチャーは `function(error, activation)` です。ここで、以下が適用されます。

- 起動が成功した場合、`error` は `false` です。失敗した場合は、true を表す値で、通常、エラーを記述するストリングになります。
- エラーの場合、`activation` は、失敗のモードによっては未定義であることがあります。
- `activation` は、定義されている場合には、アクティベーション ID が入った `activationId` フィールドを含むディクショナリーです。

`whisk.getAuthKey()` 関数は、アクションの実行に使用されている許可キーを返します。通常、`whisk.invoke()` 関数と `whisk.trigger()` 関数で暗黙的に使用されるため、この関数を直接呼び出す必要はありません。

### ランタイム環境
{: #openwhisk_ref_runtime_environment}

JavaScript アクションは、Node.js バージョン 0.12.9 環境において、アクションで使用可能な以下のパッケージで実行されます。

- apn
- async
- body-parser
- btoa
- cloudant
- commander
- consul
- cookie-parser
- cradle
- errorhandler
- express
- express-session
- jade
- log4js
- merge
- moment
- mustache
- nano
- node-uuid
- oauth2-server
- process
- request
- rimraf
- semver
- serve-favicon
- socket.io
- superagent
- swagger-tools
- tmp
- watson-developer-cloud
- when
- xml2js
- xmlhttprequest
- yauzl


## Docker アクション
{: #openwhisk_ref_docker}

Docker アクションは、Docker コンテナーでユーザー提供バイナリーを実行します。このバイナリーは Ubuntu 14.04 LTD に基づく Docker イメージで実行されるため、バイナリーはこのディストリビューションと互換でなければなりません。

アクション入力の「payload」パラメーターがバイナリー・プログラムへの定位置引数として渡され、プログラムの実行からの標準出力は「result」パラメーターで返されます。

Docker スケルトンは、{{site.data.keyword.openwhisk_short}} 互換の Docker イメージをビルドするための便利な方法です。`wsk sdk install docker` CLI コマンドでスケルトンをインストールできます。

メインのバイナリー・プログラムは、`dockerSkeleton/client/clientApp` ファイルにコピーする必要があります。比較ファイルまたはライブラリーは、`dockerSkeleton/client` ディレクトリーに存在することができます。

また、`dockerSkeleton/Dockerfile` を変更して、コンパイル・ステップや依存関係を組み込むこともできます。例えば、アクションが Python スクリプトであれば、Python をインストールします。


## システムしきい値
{: #openwhisk_syslimits}

{{site.data.keyword.openwhisk_short}} には、アクションで使用するメモリーの量、1 時間当たりのアクション呼び出しの許容数など、システムしきい値がいくつかあります。以下の表に、デフォルトの限度を示します。

| 限度 | 説明 | 構成対象 | 単位 | デフォルト |
| ----- | ----------- | ------------ | -----| ------- |
| timeout | N ミリ秒を超えてコンテナーを実行することはできません。 | アクション当たり |  ミリ秒 | 60000 |
| memory | N MB を超えるメモリーをコンテナーに割り振ることはできません。 | アクション当たり | MB | 256 |
| concurrent | 名前空間当たり N 件を超える同時アクティベーションは許可されません。 | 名前空間当たり | 数 | 100 |
| minuteRate | 1 分当たりにこの数を超えるアクションをユーザーが呼び出すことはできません。 | ユーザー当たり | 数 | 120 |
| hourRate | 1 時間当たりにこの数を超えるアクションをユーザーが呼び出すことはできません。 | ユーザー当たり | 数 | 3600 |

### アクション当たりのタイムアウト (ms) (デフォルト: 60s)
* タイムアウト限度の N は [100ms..300000ms] の範囲内で、アクション当たりのミリ秒数で設定されます。
* ユーザーは、アクションの作成時に限度を変更することができます。
* N ミリ秒を超えて実行したコンテナーは、終了されます。

### アクション当たりのメモリー (MB) (デフォルト: 256MB)
* メモリー限度の M は [128MB..512MB] の範囲内で、アクション当たりの MB 数で設定されます。
* ユーザーは、アクションの作成時に限度を変更することができます。
* コンテナーに限度を超えるメモリーを割り振ることはできません。

### 名前空間当たりの同時呼び出し (数) (デフォルト: 100)
* 名前空間で同時に処理されるアクティベーションの数が 100 を超えることはできません。
* デフォルト限度は、consul kvstore で whisk によって静的に構成可能です。
* ユーザーは現在この限度を変更できません。


### 分/時間当たりの呼び出し (数) (固定: 120/3600)
* レート限度の N は 120/3600 に設定され、1 分/1 時間の枠内のアクション呼び出し数を制限します。
* ユーザーがアクションの作成時にこの限度を変更することはできません。
* この限度を超える CLI 呼び出しは、TOO_MANY_REQUESTS に対応するエラー・コードを受け取ります。
