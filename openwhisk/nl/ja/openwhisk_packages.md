---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} パッケージの使用と作成
{: #openwhisk_packages}
*最終更新日: 2016 年 3 月 28 日*

{{site.data.keyword.openwhisk}} では、パッケージを使用して関連するアクションのセットを 1 つにまとめ、それらのパッケージを他のユーザーと共有することができます。

パッケージには、*アクション*および*フィード*を含めることができます。
- アクションは、
{{site.data.keyword.openwhisk_short}} で実行するコードの一部分です。例えば、Cloudant パッケージには、Cloudant データベースに対してレコードの読み取りまたは書き込みを行うアクションが含まれます。
- フィードは、外部イベント・ソースを構成してトリガー・イベントを発生させるために使用します。例えば、Alarm パッケージには、
指定した頻度でトリガーを発生させることができるフィードが含まれます。

パッケージを含む、すべての {{site.data.keyword.openwhisk_short}} エンティティーは、*名前空間*に属し、エンティティーの完全修飾名は `/namespaceName[/packageName]/entityName` となります。
ネーミングのガイドラインについて詳しくは、
[エンティティー名](./openwhisk_reference.html#openwhisk_entities)を参照してください。

以下のセクションでは、パッケージの参照方法と、パッケージでのトリガーとフィードの使用方法を説明します。
また、独自のパッケージをカタログに提供することに関心がある場合は、パッケージの作成と共有に関するセクションをお読みください。

## パッケージの参照
{: #openwhisk_packagedisplay}

複数のパッケージが {{site.data.keyword.openwhisk_short}} に登録されています。
名前空間でパッケージのリストを取得して、パッケージ内のエンティティーをリストし、パッケージ内の個々のエンティティーの詳細を取得できます。

1. `/whisk.system` 名前空間でパッケージのリストを取得します。

  ```
  wsk package list /whisk.system
  ```
  {: pre}
  ```
  packages
  /whisk.system/alarms                                              shared
  /whisk.system/cloudant                                            shared
  /whisk.system/github                                              shared
  /whisk.system/samples                                             shared
  /whisk.system/slack                                               shared
  /whisk.system/util                                                shared
  /whisk.system/watson                                              shared
  /whisk.system/weather                                             shared
  ```
  {: screen}

2. `/whisk.system/cloudant` パッケージ内のエンティティーのリストを取得します。

  ```
  wsk package get --summary /whisk.system/cloudant
  ```
  {: pre}
  ```
  package /whisk.system/cloudant: Cloudant database service
     (params: {{site.data.keyword.Bluemix_notm}}ServiceName host username password dbname includeDoc overwrite)
   action /whisk.system/cloudant/read: Read document from database
   action /whisk.system/cloudant/write: Write document to database
   feed   /whisk.system/cloudant/changes: Database change feed
  ```
  {: screen}

  この出力は、Cloudant パッケージが 2 つのアクション `read` および `write` と、`changes` という 1 つのトリガー・フィードを提供していることを示しています。`changes` フィードは、指定された Cloudant データベースに文書が追加されると、トリガーを発生させます。

  Cloudant パッケージには、パラメーター `username`、`password`、
`host`、および `port` も定義されています。これらのパラメーターは、アクションとフィードが意味を持つようにするために指定する必要があります。例えば、これらのパラメーターを使用すると、アクションが特定の Cloudant アカウントで作動することが可能になります。

3. `/whisk.system/cloudant/read` アクションの説明を取得します。

  ```
  wsk action get --summary /whisk.system/cloudant/read
  ```
  {: pre}
  ```
  action /whisk.system/cloudant/read: Read document from database
     (params: dbname includeDoc id)
  ```
  {: screen}

  この出力は、Cloudant の `read` アクションに、取得するデータベースと文書 ID などの 3 つのパラメーターが必要であることを示しています。


## パッケージ内のアクションの起動
{: #openwhisk_package_invoke}

他のアクションと同様に、パッケージ内のアクションを起動することができます。
次のいくつかのステップで、異なるパラメーターを指定して `/whisk.system/samples` パッケージ内の `greeting` アクションを起動する方法を説明します。

1. `/whisk.system/samples/greeting` アクションの説明を取得します。

  ```
  wsk action get --summary /whisk.system/samples/greeting
  ```
  {: pre}
  ```
  action /whisk.system/samples/greeting: Print a friendly greeting
     (params: name place)
  ```
  {: screen}

  `greeting` アクションは 2 つのパラメーター `name` と `place` を取ることに注意してください。

2. パラメーターを指定せずにアクションを起動します。


  ```
  wsk action invoke --blocking --result /whisk.system/samples/greeting
  ```
  {: pre}
  ```
  {
      "payload": "Hello, stranger from somewhere!"
  }
  ```
  {: screen}

  パラメーターが指定されなかったため、出力は汎用メッセージです。

3. パラメーターを指定してアクションを起動します。


  ```
  wsk action invoke --blocking --result /whisk.system/samples/greeting --param name Mork --param place Ork
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Mork from Ork!"
  }
  ```
  {: screen}

  出力は、アクションに渡された `name` パラメーターと `place` パラメーターを使用することに注意してください。


## パッケージ・バインディングの作成と使用
{: #openwhisk_package_bind}

パッケージ内のエンティティーを直接使用することができますが、毎回同じパラメーターをアクションに渡している場合があります。パッケージにバインドしてデフォルト・パラメーターを指定することによって、
これを避けることができます。これらのパラメーターは、パッケージ内のアクションによって継承されます。

例えば、
`/whisk.system/cloudant` パッケージで、パッケージ・バインディングにデフォルトの `username`、
`password`、`dbname` の値を設定することができます。これらの値はパッケージ内のアクションに自動的に渡されます。

次の単純な例では、
`/whisk.system/samples` パッケージにバインドします。

1. `/whisk.system/samples` パッケージにバインドし、デフォルトの `place` パラメーター値を設定します。

  ```
  wsk package bind /whisk.system/samples valhallaSamples --param place Valhalla
  ```
  {: pre}
  ```
  ok: created binding valhallaSamples
  ```
  {: screen}

2. パッケージ・バインディングの説明を取得します。

  ```
  wsk package get --summary valhallaSamples
  ```
  {: pre}
  ```
  package /myNamespace/valhallaSamples
   action /myNamespace/valhallaSamples/greeting: Print a friendly greeting
   action /myNamespace/valhallaSamples/wordCount: Count words in a string
   action /myNamespace/valhallaSamples/helloWorld: Print to the console
   action /myNamespace/valhallaSamples/echo: Returns the input arguments, unchanged
  ```
  {: screen}

  `/whisk.system/samples` パッケージ内のすべてのアクションが `valhallaSamples` パッケージ・バインディングで使用可能であることに注意してください。

3. パッケージ・バインディングでアクションを起動します。

  ```
  wsk action invoke --blocking --result valhallaSamples/greeting --param name Odin
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Odin from Valhalla!"
  }
  ```
  {: screen}

  `valhallaSamples` パッケージ・バインディングを作成したときに設定した `place`
パラメーターを、アクションが継承している結果に注目してください。

4. アクションを起動して、デフォルトのパラメーター値を上書きします。

  ```
  wsk action invoke --blocking --result valhallaSamples/greeting --param name Odin --param place Asgard
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Odin from Asgard!"
  }
  ```
  {: screen}

  アクションの起動で指定された `place` パラメーター値によって、
`valhallaSamples` パッケージ・バインディングに設定されたデフォルト値が上書きされている点に注意してください。


## トリガー・フィードの作成と使用
{: #openwhisk_package_trigger}

フィードは、外部イベント・ソースのイベントによって {{site.data.keyword.openwhisk_short}} トリガーが発生するように構成するための便利な方法を提供します。この例は、
Alarm パッケージ内のフィードを使用して毎秒トリガーを発生させ、ルールを使用して毎秒アクションを起動する方法を示しています。

1. `/whisk.system/alarms` パッケージ内のフィードの説明を取得します。

  ```
  wsk package get --summary /whisk.system/alarms
  ```
  {: pre}
  ```
  package /whisk.system/alarms
   feed   /whisk.system/alarms/alarm
  ```
  {: screen}

  ```
  wsk action get --summary /whisk.system/alarms/alarm
  ```
  {: pre}
  ```
  action /whisk.system/alarms/alarm: Fire trigger when alarm occurs
     (params: cron trigger_payload)
  ```
  {: screen}

  `/whisk.system/alarms/alarm` フィードは、次の 2 つのパラメーターを使用します。
  - `cron`: トリガーを発生させるタイミングを示す crontab 仕様。
  - `trigger_payload`: 各トリガー・イベントに設定するペイロード・パラメーター値。

2. 8 秒ごとに発生するトリガーを作成します。


  ```
  wsk trigger create everyEightSeconds --feed /whisk.system/alarms/alarm -p cron '*/8 * * * * *' -p trigger_payload '{"name":"Mork", "place":"Ork"}'
  ```
  {: pre}
  ```
  ok: created trigger feed everyEightSeconds
  ```
  {: screen}

3. 以下のアクション・コードを含む「hello.js」ファイルを作成します。

  ```
  function main(params) {
      return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

4. アクションが存在することを確認してください。

  ```
  wsk action update hello hello.js
  ```
  {: pre}

5. `everyEightSeconds` トリガーが発生するたびに `hello` アクションを起動するルールを作成します。

  ```
  wsk rule create --enable myRule everyEightSeconds hello
  ```
  {: pre}
  ```
  ok: created rule myRule
  ok: rule myRule is activating
  ```
  {: screen}

6. アクティベーション・ログをポーリングして、アクションが起動中であることを確認します。

  ```
  wsk activation poll
  ```
  {: pre}

  トリガー、ルール、アクションのアクティベーションが 8 秒ごとに表示されます。アクションは、起動されるたびにパラメーター
`{"name":"Mork", "place":"Ork"}` を受け取ります。


## パッケージの作成
{: #openwhisk_packages_create}

パッケージは、関連するアクションとフィードのセットを編成するために使用します。
また、パッケージを使用すると、パッケージ内のすべてのエンティティーでパラメーターを共有することができます。

次の例で、単純なアクションを含むカスタム・パッケージを作成してみます。

1. 「custom」というパッケージを作成します。

  ```
  wsk package create custom
  ```
  {: pre}
  ```
  ok: created package custom
  ```
  {: screen}

2. パッケージの要約を取得します。

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /myNamespace/custom
  ```
  {: screen}

  パッケージが空であることに注意してください。

3. 以下のアクション・コードを含む「`identity.js`」というファイルを作成します。このアクションは、
すべての入力パラメーターを返します。

  ```
  function main(args) { return args; }
  ```
  {: codeblock}

4. `custom` パッケージ内に `identity` アクションを作成します。

  ```
  wsk action create custom/identity identity.js
  ```
  {: pre}
  ```
  ok: created action custom/identity
  ```
  {: screen}

  パッケージ内にアクションを作成する場合、アクション名の前にパッケージ名を付ける必要があります。パッケージのネスティングは許可されません。パッケージは、アクションのみを含むことができ、別のパッケージを含むことはできません。

5. パッケージの要約を再度取得します。

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /myNamespace/custom
   action /myNamespace/custom/identity
  ```
  {: screen}

  名前空間に `custom/identity` アクションが表示されるようになりました。

6. パッケージ内のアクションを起動します。

  ```
  wsk action invoke --blocking --result custom/identity
  ```
  {: pre}
  ```
  {}
  ```
  {: screen}


パッケージ内のすべてのエンティティーに、デフォルトのパラメーターを設定することができます。これを行うには、パッケージ内のすべてのアクションで継承されるパッケージ・レベルのパラメーターを設定します。これがどのように動作するかを確認するには、次の例に従ってください。

1. 2 つのパラメーター `city` と `country` を指定して `custom` パッケージを更新します。

  ```
  wsk package update custom --param city Austin --param country USA
  ```
  {: pre}
  ```
  ok: updated package custom
  ```
  {: screen}

2. パッケージのパラメーターとアクションのパラメーターを表示し、
パッケージ内の `identity` アクションが、パッケージからパラメーターを継承していることを確認します。

  ```
  wsk package get custom parameters
  ```
  {: pre}
  ```
  ok: got package custom, projecting parameters
  [
      {
          "key": "city",
          "value": "Austin"
      },
      {
          "key": "country",
          "value": "USA"
      }
  ]
  ```
  {: screen}

  ```
  wsk action get custom/identity parameters
  ```
  {: pre}
  ```
  ok: got action custom/identity, projecting parameters
  [
      {
          "key": "city",
          "value": "Austin"
      },
      {
          "key": "country",
          "value": "USA"
      }
  ]
  ```
  {: screen}

3. identity アクションをパラメーターを指定せずに起動して、アクションが本当にパラメーターを継承しているかどうか確認します。

  ```
  wsk action invoke --blocking --result custom/identity
  ```
  {: pre}
  ```
  {
      "city": "Austin",
      "country": "USA"
  }
  ```
  {: screen}

4. いくつかのパラメーターを指定して identity アクションを起動します。
起動パラメーターは、パッケージ・パラメーターとマージされ、パッケージ・パラメーターをオーバーライドします。

  ```
  wsk action invoke --blocking --result custom/identity --param city Dallas --param state Texas
  ```
  {: pre}
  ```
  {
      "city": "Dallas",
      "country": "USA",
      "state": "Texas"
  }
  ```
  {: screen}


## パッケージの共有
{: #openwhisk_packages_share}

パッケージを構成するアクションとフィードのデバッグおよびテストが完了したら、パッケージをすべての {{site.data.keyword.openwhisk_short}} ユーザーで共有することができます。
パッケージを共有することにより、ユーザーは、パッケージをバインドしたり、パッケージ内のアクションを起動したり、
{{site.data.keyword.openwhisk_short}} のルールやアクションのシーケンスを作成したりできるようになります。

1. すべてのユーザーでパッケージを共有します。

  ```
  wsk package update custom --shared
  ```
  {: pre}
  ```
  ok: updated package custom
  ```
  {: screen}

2. パッケージの `publish` プロパティーを表示して、このプロパティーが現在 true かどうかを確認します。

  ```
  wsk package get custom publish
  ```
  {: pre}
  ```
  ok: got package custom, projecting publish
  true
  ```
  {: screen}


これで、他のユーザーは、パッケージへのバインディングや、パッケージ内のアクションの直接起動を含め、`custom` パッケージを使用することができます。
他のユーザーは、パッケージをバインドしたり、パッケージ内のアクションを起動するために、パッケージの完全修飾名を認識している必要があります。
共有パッケージ内のアクションおよびフィードは、*パブリック* です。パッケージがプライベートの場合は、そのコンテンツもすべてプライベートになります。

1. パッケージの記述を取得し、パッケージとアクションの完全修飾名を表示します。

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /myNamespace/custom
   action /myNamespace/custom/identity
  ```
  {: screen}

  前述の例では、
`myNamespace` 名前空間で作業しています。この名前空間が、完全修飾名に含まれています。

