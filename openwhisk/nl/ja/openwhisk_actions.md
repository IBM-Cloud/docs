---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} アクションの作成と起動
{: #openwhisk_actions}

*最終更新日: 2016 年 3 月 22 日*

アクションとは、{{site.data.keyword.openwhisk}} プラットフォームで実行されるステートレスなコード・スニペットです。JavaScript 関数、Swift 関数、または、Docker コンテナーにパッケージした実行可能なカスタム・プログラムをアクションにできます。例えば、アクションを使用して、イメージ内の顔を検出したり、一連の API 呼び出しを集約したり、ツイートを投稿したりできます。
{:shortdesc}

アクションは明示的に起動するか、イベントに応じて実行することができます。どちらの場合も、アクションを実行すると、固有のアクティベーション ID で識別されるアクティベーション・レコードができます。アクションへの入力とアクションの結果は、キーと値のペアからなるディクショナリー (キーはストリング、値は有効な JSON 値) です。

アクションは、他のアクションの呼び出し、または、定義された一連のアクションから構成できます。

## JavaScript アクションの作成と起動
{: #openwhisk_create_action_js}

以下のセクションでは、JavaScript でのアクションに関する作業を説明します。単純なアクションの作成と起動から始めて、アクションへのパラメーターの追加、パラメーターを指定したアクションの起動、デフォルト・パラメーターの設定と起動、非同期アクションの作成と進み、最後に、アクション・シーケンスを処理します。


### 単純な JavaScript アクションの作成と起動
{: #openwhisk_single_action_js}

以下のステップと例を見て、最初の JavaScript アクションを作成してください。

1. 以下の内容を持つ JavaScript ファイルを作成します。この例では、ファイル名は 'hello.js' です。
  
  ```
  function main() {
      return {payload: 'Hello world'};
  }
  ```
  {: codeblock}

  この JavaScript ファイルにさらに関数を含めることもできます。ただし、規約により、アクションのエントリー・ポイントを提供するために `main` という名前の関数が存在している必要があります。

2. 以下の JavaScript 関数からアクションを作成します。この例では、アクションは「hello」という名前です。

  ```
  wsk action create hello hello.js
  ```
  {: pre}
  ```
  ok: created action hello
  ```
  {: screen}

3. 作成したアクションをリストします。
  
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  hello       private
  ```
  {: screen}

  作成したばかりの `hello` アクションが表示されているのを確認できます。

4. アクションを作成した後、invoke コマンドを使用して、そのアクションを {{site.data.keyword.openwhisk_short}} においてクラウド内で実行できます。コマンドにフラグを指定することによって、アクションを*ブロッキング*起動または*非ブロッキング*起動のいずれかで起動できます。ブロッキング起動は、アクションの実行が完了するのを待ってから結果を返します。次の例では、ブロッキングを示す `-blocking` パラメーターが使用されています。

  ```
  wsk action invoke --blocking hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 44794bd6aab74415b4e42a308d880e5b
  response:
  {
      "result": {
          "payload": "Hello world"
      },
      "status": "success",
      "success": true
  }
  ```
  {: screen}

  コマンドの出力は、次の 2 つの重要な情報です。
  * アクティベーション ID (`44794bd6aab74415b4e42a308d880e5b`)
  * 起動結果

  この例の結果は、JavaScript 関数によって返されたストリング `Hello world` です。アクティベーション ID は、後でログまたは起動結果を取り出すときに使用できます。  

5. アクションの結果をすぐに必要としない場合は、`--blocking` フラグを省略して非ブロッキング起動を行うことができます。結果は後でアクティベーション ID を使用して取得できます。次の例を参照してください。

  ```
  wsk action invoke hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: screen}

  ```
  wsk activation result 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: pre}
  ```
  {
      "payload": "Hello world"
  }
  ```
  {: screen}

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
  {: screen}

### アクションへのパラメーターの引き渡し
{: #openwhisk_adding_parameters_js}

アクションが起動されるときにパラメーターを渡すことができます。

1. アクションでパラメーターを使用します。例えば、「hello.js」ファイルを更新して、次のような内容にします。
  
  ```
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
  ```
  wsk action invoke --blocking --result hello --param name 'Bernie' --param place 'Vermont'
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  {: screen}

  パラメーターの名前と値を指定する `--param` オプションと、起動結果のみを表示する `--result` オプションの使用に注意してください。

### デフォルト・パラメーターの設定
{: #openwhisk_binding_actions}

複数の名前付きパラメーターを指定してアクションを起動できます。前の例では `hello` アクションは、個人を表す *name* パラメーターと出身地を表す *place* の 2 つのパラメーターを予期していました。

アクションに毎回すべてのパラメーターを渡すのではなく、特定のパラメーターをバインドすることができます。次の例は、*place* パラメーターをバインドして、アクションがデフォルトで場所「Vermont」を設定するようにします。
 
1. アクションを更新し、`--param` オプションを使用してパラメーター値をバインドします。

  ```
  wsk action update hello --param place 'Vermont'
  ```
  {: pre}

2. 今回は `name` パラメーターのみを渡してアクションを起動します。

  ```
  wsk action invoke --blocking --result hello --param name 'Bernie'
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  {: screen}

  アクションを起動するときに place パラメーターを指定する必要がなかったことに注意してください。パラメーターをバインドしても、起動時にそのパラメーターの値を指定すれば上書きできます。

3. `name` 値と `place` 値の両方を渡してアクションを起動します。後者は、アクションにバインドされた値を上書きします。

  ```
  wsk action invoke --blocking --result hello --param name 'Bernie' --param place 'Washington, DC'
  ```
  {: pre}
  ```
  {  
      "payload": "Hello, Bernie from Washington, DC"
  }
  ```
  {: screen}

### 非同期アクションの作成
{: #openwhisk_asynchrony_js}

コールバック関数内で実行を続ける JavaScript 関数は、場合によって、`main` 関数が戻った後にアクティベーション結果を返す必要があります。これを行うには、アクション内で `whisk.async()` 関数および `whisk.done()` 関数を使用します。

1. 以下の内容を `asyncAction.js` という名前のファイルに保存します。

  ```
  function main() {
      setTimeout(function() {
          return whisk.done({done: true});
      }, 20000);
      return whisk.async();
  }
  ```
  {: codeblock}

  `main` 関数はすぐに戻り、このアクティベーションの実行を続行する必要があることを `whisk.async()` 戻り値が示すことに注意してください。

  この例では、`setTimeout()` JavaScript 関数は 20 秒待ってからコールバック関数を呼び出し、`whisk.done()` の呼び出しがアクティベーションの完了を示します。

2. 以下のコマンドを実行して、アクションを作成して起動します。

  ```
  wsk action create asyncAction asyncAction.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result asyncAction
  ```
  {: pre}
  ```
  {
      "done": true
  }
  ```
  {: screen}

  実行したのは非同期アクションのブロッキング起動であることに注意してください。

3. アクティベーション・ログを取り出して、アクティベーションの完了にかかった時間を確認します。

  ```
  wsk activation list --limit 1 asyncAction
  ```
  {: pre}
  ```
  activations
  b066ca51e68c4d3382df2d8033265db0             asyncAction
  ```
  {: screen}


  ```
  wsk activation get b066ca51e68c4d3382df2d8033265db0
  ```
  {: pre}
 ```
  {
      "start": 1455881628103,
      "end":   1455881648126,
      ...
  }
  ```
  {: screen}

  アクティベーション・レコード中の `start` と `end` のタイム・スタンプを比較することで、このアクティベーションの完了に 20 秒と少しかかったことが分かります。


### 外部 API を呼び出すためのアクションの使用
{: #openwhisk_apicall_action}

ここまでの例では、JavaScript 関数はすべて自己完結型でした。外部 API を呼び出すアクションを作成することもできます。

次の例は、Yahoo Weather サービスを呼び出して、特定の場所での現在の状態を取得します。 

1. 以下の内容を `weather.js` という名前のファイルに保存します。
  ```
    var request = require('request');
    
    function main(msg) {
        var location = msg.location || 'Vermont';
        var url = 'https://query.yahooapis.com/v1/public/yql?q=select item.condition from weather.forecast where woeid in (select woeid from geo.places(1) where text="' + location + '")&format=json';
    
        request.get(url, function(error, response, body) {
            var condition = JSON.parse(body).query.results.channel.item.condition;
            var text = condition.text;
            var temperature = condition.temp;
            var output = 'It is ' + temperature + ' degrees in ' + location + ' and ' + text;
            whisk.done({msg: output});
        });
    
        return whisk.async();
    }
  ```
  {: codeblock}

  この例では、アクションは JavaScript `request` ライブラリーを使用して Yahoo Weather API への HTTP 要求を行い、JSON 結果からフィールドを抽出することに注意してください。[リファレンス](./openwhisk_reference.html#runtime_ref_runtime_environment)に、アクションで使用できる Node.js パッケージについての詳しい説明が記載されています。
  
  この例は、非同期アクションの必要性も示しています。アクションは `whisk.async()` を戻して、関数が戻ったときにこのアクションの結果はまだ使用可能になっていないことを示します。代わりに、結果は、HTTP 呼び出しが完了した後に `request` コールバックで使用可能になり、引数として `whisk.done()` 関数に渡されます。

2. 以下のコマンドを実行して、アクションを作成して起動します。
  ```
  wsk action create weather weather.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result weather --param location 'Brooklyn, NY'
  ```
  {: pre}
  ```
  {
      "msg": "It is 28 degrees in Brooklyn, NY and Cloudy"
  }
  ```
  {: screen}

### アクション・シーケンスの作成
{: #openwhisk_create_action_sequence}

一連のアクションをチェーニングする 1 つのアクションを作成できます。

いくつかのユーティリティー・アクションが `/whisk.system/util` という名前のパッケージに入って提供されており、初めてのシーケンスを作成するためにこれを使用できます。パッケージについて詳しくは、『[パッケージ](./openwhisk_packages.html)』セクションを参照してください。

1. `/whisk.system/util` パッケージ内のアクションを表示します。
  
  ```
  wsk package get --summary /whisk.system/util
  ```
  {: pre}
  ```
  package /whisk.system/util
   action /whisk.system/util/cat: Concatenate array of strings, and split lines into an array
   action /whisk.system/util/head: Filter first K array elements and discard rest
   action /whisk.system/util/date: Get current date and time
   action /whisk.system/util/sort: Sort array
  ```
  {: screen}

  この例では、`cat` アクションと `sort` アクションを使用します。

2. アクション・シーケンスを作成して、1 つのアクションの結果が次のアクションに引数として渡されるようにします。
  
  ```
  wsk action create myAction --sequence /whisk.system/util/cat,/whisk.system/util/sort
  ```
  {: pre}

  このアクション・シーケンスは、数行のテキストを 1 つの配列に変換し、行をソートします。

3. アクション・シーケンスを起動する前に、次のような数行のテキストからなる 'haiku.txt' という名前のテキスト・ファイルを作成します。

  ```
  Over-ripe sushi,
  The Master
  Is full of regret.
  ```
  {: codeblock}

4. アクションを起動します。
  
  ```
  wsk action invoke --blocking --result myAction --param payload "$(cat haiku.txt)"
  ```
  {: pre}
  ```
  {
      "length": 3,
      "lines": [
          "Is full of regret.",
          "Over-ripe sushi,",
          "The Master"
      ]
  }
  ```
  {: screen}

  結果では行がソートされていることが分かります。

**注**: 複数の名前付きパラメーターを指定したアクション・シーケンス呼び出しについて詳しくは、『[デフォルト・パラメーターの設定](./openwhisk_actions.html##openwhisk_binding_actions)』を参照してください。

## Swift アクションの作成
{: #openwhisk_actions_swift}

Swift アクションの作成プロセスは、JavaScript アクションの場合と似ています。以下のセクションでは、単一 Swift アクションの作成と起動、および、そのアクションへのパラメーターの追加について説明します。

オンラインの [Swift Sandbox](https://swiftlang.ng.bluemix.net) を使用して、Xcode をマシンにインストールする必要なく Swift コードをテストすることもできます。

### アクションの作成と起動
{: #openwhisk_actions_invoke_swift}

アクションは、単にトップレベルの Swift 関数です。例えば、以下の内容で `hello.swift` という名前のファイルを作成します。

```
  func main(args: [String:Any]) -> [String:Any] {
      if let name = args["name"] as? String {
          return [ "greeting" : "Hello \(name)!" ]
      } else {
return [ "greeting" : "Hello stranger!" ]
      }
  }
```
{: codeblock}

JavaScript アクションと同様に、Swift アクションは常にディクショナリーを取り込み、ディクショナリーを生成することに注意してください。

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

```
  {
      "greeting": "Hello World!"
  }
```
{: screen}

**重要:** Swift アクションは Linux 環境で実行されます。Linux 上の Swift はまだ発展途上であり、
{{site.data.keyword.openwhisk_short}} は通常は使用可能な最新リリースを使用しますが、それは必ずしも安定しているとは限りません。それに加えて、{{site.data.keyword.openwhisk_short}} で使用される Swift のバージョンは、安定したリリースの MacOS 用 XCode からの Swift のバージョンと不整合である可能性があります。

## Docker アクションの作成
{: #openwhisk_actions_docker}

{{site.data.keyword.openwhisk_short}} Docker アクションでは、任意の言語で独自のアクションを作成できます。

コードはコンパイルされて実行可能バイナリーになり、Docker イメージに組み込まれます。バイナリー・プログラムとシステムの対話は、`stdin` から入力を受け取り、`stdout` を通して応答することによって行われます。

前提条件として、Docker Hub アカウントを持っている必要があります。無料の Docker ID およびアカウントをセットアップするには、[Docker Hub](https://hub.docker.com){: new_window} にアクセスしてください。

以下の説明では、ユーザー ID が「janesmith」であり、パスワードが「janes_password」であると想定しています。CLI が既にセットアップ済みである場合、{{site.data.keyword.openwhisk_short}} で使用するためのカスタム・バイナリーをセットアップするには、3 つのステップが必要です。その後、アップロードされた Docker イメージをアクションとして使用できます。

1. Docker スケルトンをダウンロードします。次のように CLI を使用してダウンロードできます。

  ```
  wsk sdk install docker
  ```
  {: pre}
  ```
  Docker スケルトンが現在のディレクトリーにインストールされました。
  ```
  {: screen}

  ```
  ls dockerSkeleton/
  ```
  {: pre}
  ```
  Dockerfile      README.md       buildAndPush.sh client          server
  ```
  {: screen}

  このスケルトンは、Docker コンテナー・テンプレートであり、そこにカスタム・バイナリーの形でコードを注入できます。

2. ブラック・ボックス・スケルトン内にカスタム・バイナリーをセットアップします。スケルトンには既に C プログラムが含まれているので、それを使用できます。

  ```
  cat ./dockerSkeleton/client/example.c
  ```
  {: pre}
  {: pre}
  ```
  #include <stdio.h>
  
  int main(int argc, char *argv[]) {
      printf("Hello %s from arbitrary C program!\n",
             (argc == 1) ? "anonymous" : argv[1]);
  }
  ```
  {: screen}

  必要に応じてこのファイルを変更できます。

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

  example.c ファイルの部分は Docker イメージのビルド・プロセスの一環としてコンパイルされるので、ご使用のマシン上で C をコンパイルする必要はないことに注意してください。

4. 提供された JavaScript ファイルではなく Docker イメージからアクションを作成するには、`--docker` を追加し、JavaScript ファイル名を Docker イメージ名に置き換えます。

  ```
  wsk action create --docker example janesmith/blackboxdemo
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result example --param payload Rey
  ```
  {: pre}
  ```
  {
      "msg": "Hello Rey from arbitrary C program!\n"
  }
  ```
  {: screen}


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
  {: screen}

3. ポーリング・ウィンドウでアクティベーション・ログを監視します。

  ```
  Activation: helloWorld (7331f9b9e2044d85afd219b12c0f1491)
    2016-02-11T16:46:56.842065025Z stdout: hello bob!
  ```
  {: screen}

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
  {: screen}

2. 対象のアクションが、もうアクションのリストに含まれていないことを確認します。
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  ```
  {: screen}
