---

copyright:
  years: 2016
lastupdated: "2016-02-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# トリガーとルールの作成
{: #openwhisk_triggers}


{{site.data.keyword.openwhisk}} のトリガーとルールにより、プラットフォームにイベント・ドリブン機能がもたらされます。外部および内部のイベント・ソースからのイベントは、トリガーを通じてチャネル設定され、ルールによって許可されたアクションがこれらのイベントに対応します。
{: shortdesc}

## トリガーの作成
{: #openwhisk_triggers_create}

トリガーは、ある種のイベントに対して指定されたチャネルです。以下は、トリガーの例です。

- ロケーション更新イベントのトリガー。
- Web サイトへの文書アップロードのトリガー。
- 着信 E メールのトリガー。

トリガーは、キーと値のペアのディクショナリーを使用して*発生させる* (アクティブ化する) ことができます。このディクショナリーは、*イベント* と呼ばれることもあります。アクションと同様に、トリガーを発生させるたびに、アクティベーション ID が生成されます。

トリガーは、ユーザーが明示的に発生させることも、ユーザーの代わりに外部イベント・ソースによって発生させることもできます。
*フィード* は、{{site.data.keyword.openwhisk_short}} によってコンシューム可能なトリガー・イベントを発生させるように外部イベント・ソースを構成するための便利な方法です。フィードの例として、以下があります。
- データベースの文書に追加または変更があるたびにトリガー・イベントを発生させる Cloudant データ変更フィード。
- Git リポジトリーへのコミットごとにトリガー・イベントを発生させる Git フィード。

## ルールの使用
{: #openwhisk_rules_use}

ルールは 1 つのトリガーを 1 つのアクションに関連付けます。トリガーが発生するたびに、該当のアクションが、トリガー・イベントを入力として起動されます。

適切なルール・セットを使用して、単一のトリガー・イベントで複数のアクションを起動することや、
複数のトリガーからのイベントへの対応としてアクションを起動することが可能です。

例えば、システムに以下のアクションがあるとします。
- `classifyImage` アクション: イメージ内のオブジェクトを検出し、それらを分類します。
- `thumbnailImage` アクション: イメージのサムネール・バージョンを作成します。

また、以下のトリガーを発生させる 2 つのイベント・ソースがあるとします。
- `newTweet` トリガー: 新規ツイートが投稿されたときに発生します。
- `imageUpload` トリガー: Web サイトにイメージがアップロードされたときに発生します。

単一のトリガー・イベントが複数のアクションを起動するようにルールをセットアップし、複数のトリガーで同じアクションを起動するようにすることができます。
- `newTweet -> classifyImage` ルール。
- `imageUpload -> classifyImage` ルール。
- `imageUpload -> thumbnailImage` ルール。

この 3 つのルールでは、ツイートとアップロードされたイメージの両方のイメージを分類する、アップロードされたイメージを分類する、サムネール・バージョンを生成する、という動作を設定します。

## トリガーの作成と発生
{: #openwhisk_triggers_fire}

トリガーは、特定のイベントの発生時に発生させることも、手動で発生させることもできます。

例として、ユーザー・ロケーションの更新を送信するトリガーを作成し、そのトリガーを手動で発生させます。

1. 以下のコマンドを入力してトリガーを作成します。

  ```
wsk trigger create locationUpdate
  ```
  {: pre}

  ```
ok: created trigger locationUpdate
  ```
  {: screen}

2. トリガーのセットをリストして、トリガーが作成されたことを確認します。

  ```
wsk trigger list
  ```
  {: pre}

  ```
triggers
  /someNamespace/locationUpdate                            private
  ```
  {: screen}

  これで、名前を指定した「チャネル」が作成され、このチャネルに対してイベントを発生させることができます。

3. 次に、トリガー名とパラメーターを指定して、トリガー・イベントを発生させます。

  ```
  wsk trigger fire locationUpdate --param name Donald --param place "Washington, D.C."
  ```
  {: pre}

  ```
ok: triggered locationUpdate with id fa495d1223a2408b999c3e0ca73b2677
  ```
  {: screen}

発生したトリガーは、それに突き合わせる付随のルールがない場合は、目に見える効果はありません。
トリガーはパッケージ内に作成できません。名前空間の直下に作成する必要があります。

## ルールを使用したトリガーとアクションの関連付け
{: #openwhisk_rules_assoc}

トリガーをアクションに関連付けるために、ルールが使用されます。トリガー・イベントが発生するたびに、イベントのパラメーターを使用してアクションが起動されます。

例として、ロケーションの更新がポストされるたびに hello アクションを呼び出すルールを作成します。

1. 使用するアクション・コードを含む 'hello.js' ファイルを作成します。

  ```
function main(params) {
     return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

2. トリガーとアクションが存在することを確認します。

  ```
wsk trigger update locationUpdate
  ```
  {: pre}

  ```
wsk action update hello hello.js
  ```
  {: pre}

3. ルールを作成します。ルールは作成時に有効化されることに注意してください。つまり、ルールは即時にトリガーのアクティベーションに応答できるようになります。3 つのパラメーターは、ルールの名前、トリガー、およびアクションです。

  ```
  wsk rule create myRule locationUpdate hello
  ```
  {: pre}

  ルールを無効にすることをいつでも選択できます。
  ```
  wsk rule disable myRule
  ```
  {: pre}

4. locationUpdate トリガーを発生させます。イベントを発生させるたびに、イベントのパラメーターを使用して hello アクションが呼び出されます。
  ```
  wsk trigger fire locationUpdate --param name Donald --param place "Washington, D.C."
  ```
  {: pre}

  ```
ok: triggered locationUpdate with id d5583d8e2d754b518a9fe6914e6ffb1e
  ```
  {: screen}

5. 最新のアクティベーションをチェックして、アクションが呼び出されたことを確認します。

  ```
wsk activation list --limit 1 hello
  ```
  {: pre}

  ```
activations
  9c98a083b924426d8b26b5f41c5ebc0d             hello
  ```
  {: screen}

  ```
wsk activation result 9c98a083b924426d8b26b5f41c5ebc0d
  ```
  {: pre}
  ```
  {
     "payload": "Hello, Donald from Washington, D.C."
  }
  ```
  {: screen}

  hello アクションがイベント・ペイロードを受け取り、予期されるストリングを戻したことが分かります。

複数のルールを作成して、同じトリガーを異なるアクションに関連付けることができます。トリガーおよびルールは、パッケージに属することができません。
ただし、パッケージに属しているアクションに、ルールを関連付けることはできます。以下に例を示します。
  ```
  wsk rule create recordLocation locationUpdate /whisk.system/utils/echo
  ```
  {: pre}

また、ルールをシーケンスとともに使用することも可能です。例えば、ルール  `anotherRule`
で有効化されるアクション・シーケンス `recordLocationAndHello` を作成することができます。
  ```
  wsk action create recordLocationAndHello --sequence /whisk.system/utils/echo,hello
  wsk rule create anotherRule locationUpdate recordLocationAndHello
  ```
  {: pre}
 
