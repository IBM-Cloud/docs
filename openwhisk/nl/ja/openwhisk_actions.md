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

# {{site.data.keyword.openwhisk_short}} アクションの作成と起動
{: #openwhisk_actions}


アクションとは、{{site.data.keyword.openwhisk}} プラットフォームで実行されるステートレスなコード・スニペットです。アクションは、JavaScript 関数、Swift 関数、Python 関数、または Java メソッドとして、または、Docker コンテナーにパッケージした実行可能なカスタム・プログラムとして、作成できます。例えば、アクションを使用して、イメージ内の顔を検出したり、データベース変更に応答したり、一連の API 呼び出しを集約したり、ツイートを投稿したりできます。
{:shortdesc}
アクションは明示的に起動するか、イベントに応じて実行することができます。どちらの場合も、アクションを実行するたびに、固有のアクティベーション ID で識別されるアクティベーション・レコードができます。アクションへの入力とアクションの結果は、キーと値のペアからなるディクショナリー (キーはストリング、値は有効な JSON 値) です。アクションは、他のアクションの呼び出し、または、定義された一連のアクションから構成することもできます。

開発環境別にアクションの作成、起動、およびデバッグの方法が説明されているので、該当するものを参照してください。
* [JavaScript](#openwhisk_create_action_js)
* [Swift](#openwhisk_actions_swift)
* [Python](#openwhisk_actions_python)
* [Java](#openwhisk_actions_java)
* [Docker](#openwhisk_actions_docker)


## JavaScript アクションの作成と起動
{: #openwhisk_create_action_js}

以下のセクションでは、JavaScript でのアクションに関する作業を説明します。まず、単純なアクションを作成して起動します。その後、アクションにパラメーターを追加し、パラメーターを指定してそのアクションを起動します。次に、デフォルト・パラメーターを設定して起動します。その後、非同期アクションを作成して、最後にアクション・シーケンスを処理します。


### 単純な JavaScript アクションの作成と起動
{: #openwhisk_single_action_js}

以下のステップと例を見て、最初の JavaScript アクションを作成してください。

1. 以下の内容を持つ JavaScript ファイルを作成します。この例では、ファイル名は 'hello.js' です。

  ```javascript
  function main() {
      return {payload: 'Hello world'};
  }
  ```
  {: codeblock}
この JavaScript ファイルにさらに関数を含めることもできます。ただし、規約により、アクションのエントリー・ポイントを提供するために `main` という名前の関数が存在している必要があります。2. 以下の JavaScript 関数からアクションを作成します。この例では、アクションは「hello」という名前です。

  ```
  wsk action create hello hello.js
  ```
  {: pre}
  ```
  ok: created action hello
  ```

3. 作成したアクションをリストします。

  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  hello       private
  ```
作成したばかりの `hello` アクションが表示されているのを確認できます。4. アクションを作成した後、invoke コマンドを使用して、そのアクションを OpenWhisk においてクラウド内で実行できます。コマンドにフラグを指定することによって、*ブロッキング* 起動 (つまり、要求/応答スタイル) または*非ブロッキング* 起動のいずれかでアクションを起動できます。ブロッキング起動要求は、アクティベーション結果が使用可能になるのを*待機* します。待機時間は、60 秒と、アクションに構成された[制限時間](./openwhisk_reference.html#openwhisk_syslimits)のいずれか小さいほうです。アクティベーションの結果が待機時間内に使用可能になった場合、その結果が返されます。使用可能にならない場合、非ブロッキング要求の場合と同様に、アクティベーション処理はシステムで続行され、結果を後でチェックできるようにアクティベーション ID が返されます (アクティベーションのモニターに関するヒントについては、[ここ](#watching-action-output)を参照してください)。

  
次の例では、ブロッキングを示す `--blocking` パラメーターが使用されています。
  ```
  wsk action invoke --blocking hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 44794bd6aab74415b4e42a308d880e5b
  ```
  ```json
  {
      "result": {
          "payload": "Hello world"
      },
      "status": "success",
      "success": true
  }
  ```
コマンドの出力は、次の 2 つの重要な情報です。  * アクティベーション ID (`44794bd6aab74415b4e42a308d880e5b`)
  * 予期される待機時間内に使用可能になった場合は起動結果  
この例の結果は、JavaScript 関数によって返されたストリング `Hello world` です。アクティベーション ID は、後でログまたは起動結果を取り出すときに使用できます。  

5. アクションの結果をすぐに必要としない場合は、`--blocking` フラグを省略して非ブロッキング起動を行うことができます。結果は後でアクティベーション ID を使用して取得できます。次の例を参照してください。
  
  ```
  wsk action invoke hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 6bf1f670ee614a7eb5af3c9fde813043
  ```
  ```
  wsk activation result 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: pre}
  ```json
  {
      "payload": "Hello world"
  }
  ```

6. アクティベーション ID を記録しておくのを忘れた場合、最新のものから古いものへと順に並べられたアクティベーションのリストを取得できます。アクティベーションのリストを取得するには、次のコマンドを実行します。

  ```
  wsk activation list
  ```
  {: pre}
  ```
  activations
  44794bd6aab74415b4e42a308d880e5b         hello
  6bf1f670ee614a7eb5af3c9fde813043         hello
  ```
  

### アクションへのパラメーターの引き渡し
{: #openwhisk_adding_parameters_js}

アクションが起動されるときにパラメーターを渡すことができます。

1. アクションでパラメーターを使用します。例えば、「hello.js」ファイルを更新して、次のような内容にします。

  ```javascript
  function main(params) {
      return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

  入力パラメーターが 1 つの JSON オブジェクト・パラメーターとして `main` 関数に渡されます。この例で、`name` パラメーターと `place` パラメーターが `params` オブジェクトからどのように取り出されるのかに注意してください。

2. `hello` アクションを更新し、`name` パラメーター値と `place` パラメーター値を渡してアクションを起動します。次の例を参照してください。

  ```
  wsk action update hello hello.js
  ```
  {: pre}

3.  パラメーターは、明示的にコマンド・ラインに指定するか、必要なパラメーターが含むファイルを指定することによって指定できます。

  コマンド・ラインを使用して直接パラメーターを渡すには、以下に示すように、`--param` フラグにキー/値のペアを指定します。
  ```
  wsk action invoke --blocking --result hello --param name Bernie --param place Vermont
  ```
  {: pre}

  パラメーターの内容を含むファイルを使用するには、JSON フォーマットでそれらのパラメーターを含むファイルを作成します。次に、以下に示すように、ファイル名を `param-file` フラグに渡す必要があります。

  parameters.json という名前のサンプル・パラメーター・ファイル
  ```json
  {
      "name": "Bernie",
      "place": "Vermont"
  }
  ```
  {: codeblock}

  ```
  wsk action invoke --blocking --result hello --param-file parameters.json
  ```
  {: pre}

  ```json
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
呼び出しの結果のみを表示する `--result` オプションの使用に注意してください。### デフォルト・パラメーターの設定
{: #openwhisk_binding_actions}

複数の名前付きパラメーターを指定してアクションを起動できます。前の例では `hello` アクションは、個人を表す *name* パラメーターと出身地を表す *place* の 2 つのパラメーターを予期していました。

アクションに毎回すべてのパラメーターを渡すのではなく、特定のパラメーターをバインドすることができます。次の例は、*place* パラメーターをバインドして、アクションがデフォルトで場所「Vermont」を設定するようにします。

1. `--param` オプションを使用してパラメーター値をバインドするか、パラメーターを含むファイルを `--param-file` に渡してアクションを更新します。

  デフォルト・パラメーターを明示的にコマンド・ラインに指定するには、以下に示すように、`param` フラグにキー/値のペアを指定してください。

  ```
  wsk action update hello --param place Vermont
  ```
  {: pre}

  ファイルからパラメーターを渡すには、必要な内容を JSON フォーマットで含むファイルを作成する必要があります。次に、以下に示すように、ファイル名を `-param-file` フラグに渡します。

  parameters.json という名前のサンプル・パラメーター・ファイル
  ```json
  {
      "place": "Vermont"
  }
  ```
  {: codeblock}

  ```
  wsk action update hello --param-file parameters.json
  ```
  {: pre}

2. 今回は `name` パラメーターのみを渡してアクションを起動します。

  ```
  wsk action invoke --blocking --result hello --param name Bernie
  ```
  {: pre}
  ```json
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
アクションを起動するときに place パラメーターを指定する必要がなかったことに注意してください。パラメーターをバインドしても、起動時にそのパラメーターの値を指定すれば上書きできます。3. `name` 値と `place` 値の両方を渡してアクションを起動します。後者は、アクションにバインドされた値を上書きします。

  `--param` フラグを使用した場合
  ```
  wsk action invoke --blocking --result hello --param name Bernie --param place "Washington, DC"
  ```
  {: pre}
  `--param-file` フラグを使用した場合
  ファイル parameters.json:
  ```json
  {
      "name": "Bernie",
    "place": "Vermont"
  }
  ```
  {: codeblock}  
  ```
  wsk action invoke --blocking --result hello --param-file parameters.json
  ```
  {: pre}
  ```json
  {
      "payload": "Hello, Bernie from Washington, DC"
  }
  ```

### 非同期アクションの作成
{: #openwhisk_asynchrony_js}

非同期に実行される JavaScript 関数は、場合によって、`main` 関数が戻った後にアクティベーション結果を返す必要があります。アクションで Promise を返すことによって、これを行えます。

1. 以下の内容を `asyncAction.js` という名前のファイルに保存します。

  ```javascript
  function main(args) {
       return new Promise(function(resolve, reject) {
         setTimeout(function() {
           resolve({ done: true });
         }, 2000);
      })
   }
  ```
  {: codeblock}

  `main` 関数は Promise を戻し、アクティベーションがまだ完了していないが、今後完了すると見込まれていることを示しています。

  この場合、`setTimeout()` JavaScript 関数は、コールバック関数を呼び出す前に 2 秒間待機します。これは、非同期コードを表し、Promise のコールバック関数の中に入っていきます。

  Promise のコールバックは、resolve と reject という 2 つの引数を使用します。これらはどちらも関数です。`resolve()` の呼び出しは、Promise を完了し、アクティベーションが正常に実行されたことを示します。

  `reject()` の呼び出しでは、Promise を拒否し、アクティベーションの実行で異常が発生したことを示すことができます。

2. 以下のコマンドを実行して、アクションを作成して起動します。

  ```
  wsk action create asyncAction asyncAction.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result asyncAction
  ```
  {: pre}
  ```json
  {
      "done": true
  }
  ```
実行したのは非同期アクションのブロッキング起動であることに注意してください。3. アクティベーション・ログを取り出して、アクティベーションの完了にかかった時間を確認します。

  ```
  wsk activation list --limit 1 asyncAction
  ```
  {: pre}
  ```
  activations
  b066ca51e68c4d3382df2d8033265db0             asyncAction
  ```

  ```
  wsk activation get b066ca51e68c4d3382df2d8033265db0
  ```
  {: pre}
  ```json
  {
      "start": 1455881628103,
      "end":   1455881648126
  }
  ```
アクティベーション・レコード中の `start` と `end` のタイム・スタンプを比較することで、このアクティベーションの完了に 2 秒と少しかかったことが分かります。### 外部 API を呼び出すためのアクションの使用
{: #openwhisk_apicall_action}

ここまでの例では、JavaScript 関数はすべて自己完結型でした。外部 API を呼び出すアクションを作成することもできます。

次の例は、Yahoo Weather サービスを呼び出して、特定の場所での現在の状態を取得します。

1. 以下の内容を `weather.js` という名前のファイルに保存します。
  

  ```javascript
  var request = require('request');

  function main(params) {
      var location = params.location || 'Vermont';
      var url = 'https://query.yahooapis.com/v1/public/yql?q=select item.condition from weather.forecast where woeid in (select woeid from geo.places(1) where text="' + location + '")&format=json';

      return new Promise(function(resolve, reject) {
          request.get(url, function(error, response, body) {
              if (error) {
                  reject(error);
              }
              else {
                  var condition = JSON.parse(body).query.results.channel.item.condition;
                  var text = condition.text;
                  var temperature = condition.temp;
                  var output = 'It is ' + temperature + ' degrees in ' + location + ' and ' + text;
                  resolve({msg: output});
              }
          });
      });
  }
  ```
  {: codeblock}

  この例では、アクションは JavaScript `request` ライブラリーを使用して Yahoo Weather API への HTTP 要求を行い、JSON 結果からフィールドを抽出することに注意してください。[リファレンス](./openwhisk_reference.html#openwhisk_ref_javascript_environments)に、アクションで使用できる Node.js パッケージについての詳しい説明が記載されています。

  この例は、非同期アクションの必要性も示しています。アクションは Promise を戻して、関数が戻ったときにこのアクションの結果はまだ使用可能になっていないことを示します。代わりに、結果は、HTTP 呼び出しが完了した後に `request` コールバックで使用可能になり、引数として `resolve()` 関数に渡されます。

2. 以下のコマンドを実行して、アクションを作成して起動します。

  ```
  wsk action create weather weather.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result weather --param location "Brooklyn, NY"
  ```
  {: pre}
  ```json
  {
      "msg": "It is 28 degrees in Brooklyn, NY and Cloudy"
  }
  ```


### Node.js モジュールとしてのアクションのパッケージ化
{: #openwhisk_js_packaged_action}

単一の JavaScript ソース・ファイル内にすべてのアクション・コードを作成する代わりに、`npm` パッケージとしてアクションを作成できます。例として、以下のファイルが含まれたディレクトリーについて考えます。

まず、`package.json`:

```json
{
  "name": "my-action",
  "main": "index.js",
  "dependencies" : {
    "left-pad" : "1.1.3"
  }
}
```
{: codeblock}

次に、`index.js`:

```javascript
function myAction(args) {
    const leftPad = require("left-pad")
    const lines = args.lines || [];
    return { padded: lines.map(l => leftPad(l, 30, ".")) }
}

exports.main = myAction;
```
{: codeblock}

なお、アクションは `exports.main` を介して公開されます。アクション・ハンドラー自体の名前は、オブジェクトを受け入れ、オブジェクトを返す通常のシグニチャー (オブジェクトの `Promise`) に準拠している限り、任意のものにすることができます。Node.js 規則により、このファイルの名前は `index.js` にするか、または、package.json 内の `main` プロパティーとして任意のファイル名を指定する必要があります。

このパッケージから OpenWhisk アクションを作成するには、以下のようにします。

1. まず、すべての依存関係をローカルでインストールします。

  ```
  npm install
  ```
  {: pre}

2. 以下のように、すべてのファイル (すべての依存関係を含む) が入った `.zip` アーカイブを作成します。

  ```
  zip -r action.zip *
  ```
  {: pre}

3. 以下のように、アクションを作成します。

  ```
  wsk action create packageAction --kind nodejs:6 action.zip
  ```
  {: pre}

  なお、CLI ツールを使用して `.zip` アーカイブからアクションを作成する場合、`--kind` フラグの値を明示的に指定する必要があります。

4. 以下のように、アクションの起動は、他と同様に行うことができます。

  ```
  wsk action invoke --blocking --result packageAction --param lines "[\"and now\", \"for something completely\", \"different\" ]"
  ```
  {: pre}
  ```json
  {
      "padded": [
          ".......................and now",
          "......for something completely",
          ".....................different"
      ]
  }
  ```


最後に、ほとんどの `npm` パッケージは `npm install` で JavaScript ソースをインストールしますが、一部のパッケージはバイナリー成果物をインストールおよびコンパイルすることにも注意してください。現在、アーカイブ・ファイルのアップロードでは、バイナリー依存関係はサポートされず、JavaScript 依存関係のみがサポートされます。アーカイブにバイナリーの依存関係が含まれている場合、アクションの起動が失敗することがあります。

## アクション・シーケンスの作成
{: #openwhisk_create_action_sequence}

一連のアクションをチェーニングする 1 つのアクションを作成できます。

いくつかのユーティリティー・アクションが `/whisk.system/utils` という名前のパッケージに入って提供されており、初めてのシーケンスを作成するためにこれを使用できます。パッケージについて詳しくは、『[パッケージ](./openwhisk_packages.html)』セクションを参照してください。

1. `/whisk.system/utils` パッケージ内のアクションを表示します。

  ```
  wsk package get --summary /whisk.system/utils
  ```
  {: pre}
  ```
  package /whisk.system/utils: Building blocks that format and assemble data
   action /whisk.system/utils/head: Extract prefix of an array
   action /whisk.system/utils/split: Split a string into an array
   action /whisk.system/utils/sort: Sorts an array
   action /whisk.system/utils/echo: Returns the input
   action /whisk.system/utils/date: Current date and time
   action /whisk.system/utils/cat: Concatenates input into a string
  ```


  この例では、`split` アクションと `sort` アクションを使用します。

2. アクション・シーケンスを作成して、1 つのアクションの結果が次のアクションに引数として渡されるようにします。

  ```
  wsk action create sequenceAction --sequence /whisk.system/utils/split,/whisk.system/utils/sort
  ```
  {: pre}

  このアクション・シーケンスは、数行のテキストを 1 つの配列に変換し、行をソートします。

3. アクションを起動します。

  ```
  wsk action invoke --blocking --result sequenceAction --param payload "Over-ripe sushi,\nThe Master\nIs full of regret."
  ```
  {: pre}
  ```json
  {
      "length": 3,
      "lines": [
          "Is full of regret.",
          "Over-ripe sushi,",
          "The Master"
      ]
  }
  ```


  結果では行がソートされていることが分かります。

**注**: シーケンス中のアクション間で渡されるパラメーターは、デフォルト・パラメーターを除いて、明示的です。
したがって、アクション・シーケンスに渡されるパラメーターを使用できるのはシーケンス中の先頭アクションのみです。
シーケンス中の先頭アクションの結果が、シーケンス中の 2 番目のアクションへの入力 JSON オブジェクトになります (以下同様)。
このオブジェクトには、最初にシーケンスに渡されたパラメーターはどれも含まれません (ただし、先頭アクションがその結果にそれらのパラメーターを明示的に組み込んだ場合は除きます)。
あるアクションへの入力パラメーターは、そのアクションのデフォルト・パラメーターとマージされます。その際、入力パラメーターが優先され、一致するデフォルト・パラメーターはオーバーライドされます。
複数の名前付きパラメーターを指定したアクション・シーケンス呼び出しについて詳しくは、『[デフォルト・パラメーターの設定](./openwhisk_actions.html#openwhisk_binding_actions)』を参照してください。

## Python アクションの作成
{: #openwhisk_actions_python}

Python アクションの作成プロセスは、JavaScript アクションの場合と似ています。以下のセクションでは、単一 Python アクションの作成と起動、および、そのアクションへのパラメーターの追加について説明します。

### アクションの作成と起動
{: #openwhisk_actions_python_invoke}

アクションは、単に最上位の Python 関数です。つまり、`main` という名前のメソッドが必要です。例えば、以下の内容で `hello.py` という名前のファイルを作成します。

```python
def main(dict):
    name = dict.get("name", "stranger")
    greeting = "Hello " + name + "!"
    print(greeting)
    return {"greeting": greeting}
```
{: codeblock}

Python アクションは常にディクショナリーを取り込み、ディクショナリーを生成します。

次のように、この関数から `helloPython` という名前の OpenWhisk アクションを作成できます。

```
wsk action create helloPython hello.py
```
{: pre}

コマンド・ラインおよび `.py` ソース・ファイルを使用する場合、(JavaScript アクションとは対照的に) Python アクションを作成していることを指定する必要はありません。そのことはツールがファイル拡張子から判定します。

アクション起動は、Python アクションの場合と JavaScript アクションの場合で同じです。

```
wsk action invoke --blocking --result helloPython --param name World
```
{: pre}

```json
  {
      "greeting": "Hello World!"
  }
```



## Swift アクションの作成
{: #openwhisk_actions_swift}

Swift アクションの作成プロセスは、JavaScript アクションの場合と似ています。以下のセクションでは、単一 Swift アクションの作成と起動、および、そのアクションへのパラメーターの追加について説明します。

オンラインの [Swift Sandbox](https://swiftlang.ng.bluemix.net) を使用して、Xcode をマシンにインストールする必要なく Swift コードをテストすることもできます。

### アクションの作成と起動
{: #openwhisk_actions_invoke_swift}

アクションは、単にトップレベルの Swift 関数です。例えば、以下の内容で `hello.swift` という名前のファイルを作成します。

```swift
func main(args: [String:Any]) -> [String:Any] {
    if let name = args["name"] as? String {
        return [ "greeting" : "Hello \(name)!" ]
    } else {
        return [ "greeting" : "Hello stranger!" ]
    }
}
```
{: codeblock}

Swift アクションは常にディクショナリーを取り込み、ディクショナリーを生成します。

次のように、この関数から `helloSwift` という名前の {{site.data.keyword.openwhisk_short}} アクションを作成できます。

```
wsk action create helloSwift hello.swift
```
{: pre}

コマンド・ラインおよび `.swift` ソース・ファイルを使用する場合、(JavaScript アクションとは対照的に) Swift アクションを作成していることを指定する必要はありません。そのことはツールがファイル拡張子から判定します。

アクション起動は、Swift アクションの場合と JavaScript アクションの場合で同じです。

```
wsk action invoke --blocking --result helloSwift --param name World
```
{: pre}

```json
  {
      "greeting": "Hello World!"
  }
```


**重要:** Swift アクションは Linux 環境で実行されます。Linux 上の Swift はまだ発展途上であり、
{{site.data.keyword.openwhisk_short}} は通常は使用可能な最新リリースを使用しますが、それは必ずしも安定しているとは限りません。それに加えて、{{site.data.keyword.openwhisk_short}} で使用される Swift のバージョンは、安定したリリースの MacOS 用 XCode からの Swift のバージョンと不整合である可能性があります。

## Java アクションの作成
{: #openwhisk_actions_java}

Java アクションの作成プロセスは、JavaScript アクションおよび Swift アクションの作成と似ています。以下のセクションでは、単一 Java アクションの作成と起動、および、そのアクションへのパラメーターの追加について説明します。

Java ファイルをコンパイル、テスト、およびアーカイブするには、[JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) がローカルにインストールされている必要があります。

### アクションの作成と起動
{: #openwhisk_actions_java_invoke}

Java アクションは、以下とまったく同じシグニチャーを持つ `main` と呼ばれるメソッドを持つ Java プログラムです。
```java
public static com.google.gson.JsonObject main(com.google.gson.JsonObject);
```
{: codeblock}

例えば、以下の内容で `Hello.java` という Java ファイルを作成します。

```java
import com.google.gson.JsonObject;
public class Hello {
    public static JsonObject main(JsonObject args) {
        String name = "stranger";
        if (args.has("name"))
            name = args.getAsJsonPrimitive("name").getAsString();
        JsonObject response = new JsonObject();
        response.addProperty("greeting", "Hello " + name + "!");
        return response;
    }
}
```
{: codeblock}

次に、以下のように、`Hello.java` をコンパイルして JAR ファイル `hello.jar` を作成します。
```
javac Hello.java
```
{: pre}
```
jar cvf hello.jar Hello.class
```
{: pre}

**注:** Java ファイルをコンパイルする場合、[google-gson](https://github.com/google/gson) を Java CLASSPATH に指定する必要があります。

以下に示すように、この JAR ファイルから `helloJava` という OpenWhisk アクションを作成できます。

```
wsk action create helloJava hello.jar --main Hello
```
{: pre}

コマンド・ラインと `.jar` ソース・ファイルを使用する場合、Java アクションを作成していることを指定する必要はありません。ツールは、ファイル拡張子からそのことを判別します。

`--main` を使用して、メイン・クラスの名前を指定する必要があります。適格なメイン・クラスは、上で説明されているように静的 `main` メソッドを実装するクラスです。クラスがデフォルト・パッケージ内にない場合は、完全修飾 Java クラス名を使用してください (例: `--main com.example.MyMain`)。

Java アクションのアクション呼び出しは、Swift アクションおよび JavaScript アクションの場合と同じです。

```
wsk action invoke --blocking --result helloJava --param name World
```
{: pre}

```json
  {
      "greeting": "Hello World!"
  }
```

## Docker アクションの作成
{: #openwhisk_actions_docker}

{{site.data.keyword.openwhisk_short}} Docker アクションでは、任意の言語で独自のアクションを作成できます。

コードはコンパイルされて実行可能バイナリーになり、Docker イメージに組み込まれます。バイナリー・プログラムとシステムの対話は、`stdin` から入力を受け取り、`stdout` を通して応答することによって行われます。

前提条件として、Docker Hub アカウントを持っている必要があります。無料の Docker ID およびアカウントをセットアップするには、[Docker Hub](https://hub.docker.com){: new_window} にアクセスしてください。

以下の説明では、Docker ユーザー ID が `janesmith` であり、パスワードが `janes_password`　であると想定しています。CLI が既にセットアップ済みである場合、{{site.data.keyword.openwhisk_short}} で使用するためのカスタム・バイナリーをセットアップするには、3 つのステップが必要です。その後、アップロードされた Docker イメージをアクションとして使用できます。

1. Docker スケルトンをダウンロードします。次のように CLI を使用してダウンロードできます。

  ```
  wsk sdk install docker
  ```
  {: pre}
  ```
Docker スケルトンが現在のディレクトリーにインストールされました。
  ```
  ```
  ls dockerSkeleton/
  ```
  {: pre}
  ```
  Dockerfile      README.md       buildAndPush.sh example.c
  ```
このスケルトンは、Docker コンテナー・テンプレートであり、そこにカスタム・バイナリーの形でコードを注入できます。2. ブラック・ボックス・スケルトン内にカスタム・バイナリーをセットアップします。スケルトンには既に C プログラムが含まれているので、それを使用できます。

  ```
  cat dockerSkeleton/example.c
  ```
  {: pre}
  ```c
  #include <stdio.h>
  int main(int argc, char *argv[]) {
      printf("This is an example log message from an arbitrary C program!\n");
      printf("{ \"msg\": \"Hello from arbitrary C program!\", \"args\": %s }",
             (argc == 1) ? "undefined" : argv[1]);
  }
  ```
  {: codeblock}

  必要に応じてこのファイルを変更するか、または、追加コードおよび依存関係を Docker イメージに追加できます。
  後者の場合、必要に応じて `Dockerfile` を微調整して実行可能バイナリーをビルドする必要があります。
  そのバイナリーはコンテナー内部の `/action/exec` に置く必要があります。

  実行可能バイナリーはコマンド・ラインから単一の引数を受け取ります。それは、アクションへの引数を表す JSON オブジェクトのストリング・シリアライゼーションです。プログラムは `stdout` または `stderr` にログを記録することがあります。
  規約により、出力の最終行は、アクションの結果を表す、stringify によって文字列化された JSON オブジェクト*でなければなりません*。

3. Docker イメージをビルドし、提供されているスクリプトを使用してアップロードします。最初に `docker login` を実行して認証し、次に、選択したイメージ名でスクリプトを実行する必要があります。

  ```
  docker login -u janesmith -p janes_password
  ```
  {: pre}
  ```
  cd dockerSkeleton
  ```
  {: pre}
  ```
  ./buildAndPush.sh janesmith/blackboxdemo
  ```
  {: pre}

  example.c ファイルの部分は Docker イメージのビルド・プロセスの一環としてコンパイルされるので、ご使用のマシン上で C をコンパイルする必要はないことに注意してください。実際、このバイナリーは、互換ホスト・マシン上でコンパイルしないと、フォーマットが一致しないためにコンテナー内では稼働しない可能性があります。

  これで、Docker コンテナーを {{site.data.keyword.openwhisk_short}} アクションとして使用できます。

  ```
  wsk action create --docker example janesmith/blackboxdemo
  ```
  {: pre}

  アクションを作成するときには、`--docker` の使用に注意してください。現在は、すべての Docker イメージが Docker Hub でホストされると想定されています。
  このアクションは他の任意の {{site.data.keyword.openwhisk_short}} アクションとして起動される可能性があります。

  ```
  wsk action invoke --blocking --result example --param payload Rey
  ```
  {: pre}
  ```json
  {
      "args": {
          "payload": "Rey"
      },
      "msg": "Hello from arbitrary C program!"
  }
  ```

  Docker アクションを更新するには、buildAndPush.sh を実行して、最新イメージを Docker Hub にアップロードします。これにより、システムは、アクション用のコードの次回実行時に新規 Docker イメージをプルできるようになります。ウォーム・コンテナーがない場合、すべての新しい起動は新規 Docker イメージを使用します。
  ただし、前のバージョンの Docker イメージを使用しているウォーム・コンテナーがある場合は、`wsk action update` を実行しない限り、新しい起動はそのイメージを使用し続けます。これは、新しい起動には Docker プルを実行して新規 Docker イメージを取得する必要があることをシステムに指示します。

  ```
  ./buildAndPush.sh janesmith/blackboxdemo
  ```
  {: pre}

  ```
  wsk action update --docker example janesmith/blackboxdemo
  ```
  {: pre}

  『[リファレンス](./openwhisk_reference.html#openwhisk_ref_docker)』セクションに、Docker アクションの作成に関するさらに詳しい説明が記載されています。

## アクション出力の監視
{: #openwhisk_actions_polling}

{{site.data.keyword.openwhisk_short}} アクションは、さまざまなイベントに応じて他のユーザーによって起動されたり、アクション・シーケンスの一部として起動されたりする可能性があります。そのような場合には、起動をモニターすることが役立ちます。

{{site.data.keyword.openwhisk_short}} CLI を使用して、アクションが起動されたときの出力を監視できます。

1. シェルから次のコマンドを実行します。
  
  ```
  wsk activation poll
  ```
  {: pre}

  このコマンドは、アクティベーションからのログを継続的にチェックするポーリング・ループを開始します。

2. 別のウィンドウに切り替えて、アクションを起動します。

  ```
  wsk action invoke /whisk.system/samples/helloWorld --param payload Bob
  ```
  {: pre}
  ```
  ok: invoked /whisk.system/samples/helloWorld with id 7331f9b9e2044d85afd219b12c0f1491
  ```

3. ポーリング・ウィンドウでアクティベーション・ログを監視します。

  ```
  Activation: helloWorld (7331f9b9e2044d85afd219b12c0f1491)
    2016-02-11T16:46:56.842065025Z stdout: hello bob!
  ```

  同様に、ポーリング・ユーティリティーを実行すると、{{site.data.keyword.openwhisk_short}} で実行されているアクションのログをリアルタイムで確認できます。

## アクションの削除
{: #openwhisk_delete_action}

使用しないアクションを削除してクリーンアップすることができます。

1. アクションを削除するには、次のコマンドを実行します。
  
  ```
  wsk action delete hello
  ```
  {: pre}
  ```
  ok: deleted hello
  ```

2. 対象のアクションが、もうアクションのリストに含まれていないことを確認します。
  
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  ```
  {: pre}

## アクション・ボディー内のアクション・メタデータへのアクセス

アクション環境は、実行中のアクションに固有のいくつかのプロパティーを含んでいます。
これらによって、アクションは REST API を介して OpenWhisk アセットをプログラマチックに処理したり、
アクションに割り当てられた時間を使い切ってしまいそうなときに内部アラームを設定したりできます。
OpenWhisk Docker スケルトンを使用している場合、すべてのサポートされるランタイム (Node.js、Python、Swift、Java、および Docker アクション) で、以下のシステム環境変数を介してこれらのプロパティーにアクセスできます。

* `__OW_API_HOST` このアクションを実行している OpenWhisk デプロイメントの API ホスト
* `__OW_API_KEY` アクションを起動するサブジェクトの API キー (制限付き API キーである場合もあります)
* `__OW_NAMESPACE` *アクティベーション* の名前空間 (アクションの名前空間と同じでないこともあります)
* `__OW_ACTION_NAME` 実行しているアクションの完全修飾名
* `__OW_ACTIVATION_ID` 実行しているアクション・インスタンスのアクティベーション ID
* `__OW_DEADLINE` このアクションに割り当てられた期間全体をアクションが使い切ると推定されるおよその時刻 (エポック・ミリ秒で測定されます)
