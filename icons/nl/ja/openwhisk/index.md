---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 入門


{{site.data.keyword.openwhisk}} は、サーバーレス・コンピューティングまたは Function as a Service (FaaS) とも呼ばれる分散イベント・ドリブン計算サービスです。{{site.data.keyword.openwhisk_short}} は、イベントに応えて、または、Web アプリやモバイル・アプリからの HTTP を介した直接起動に応えて、アプリケーション・ロジックを実行します。イベントは、Bluemix サービス (Cloudant など) および外部ソースから提供できます。開発者は、アプリケーション・ロジックの開発と、オンデマンドで実行されるアクションの作成に専念できます。この新しいパラダイムの利点は、明示的にサーバーをプロビジョンしたり自動スケーリングについて心配したりしないでよいこと、また、サーバーが稼働しているが要求を処理しない場合のプロセッサー時間の支払いや、高可用性、更新、保守について心配しないですむことです。
HTTP 呼び出し、データベース状態変更、または、コードの実行をトリガーするその他のタイプのイベントがあるたびに、コードが実行されます。
課金は実行時間のミリ秒単位で行われ (最も近い 100ms に丸められます)、VM が有益な作業をしているかどうかに関係なく VM 使用の時間単位で課金されるのではありません。
{: shortdesc}

このプログラミング・モデルは、マイクロサービス、モバイル、IoT、およびその他の多くのアプリに最適です。これに備わっている自動スケーリングおよびロード・バランシングはすぐに使用可能であり、クラスター、ロード・バランサー、http プラグインなどを手動で構成する必要はありません。{{site.data.keyword.openwhisk}} で実行することになれば、ゼロ管理という利点もあります。これは、ハードウェア、ネットワーキング、およびソフトウェアのすべてが IBM によって保守されることを意味します。必要な作業は、実行したいコードを用意し、それを {{site.data.keyword.openwhisk}} に渡すことだけです。残りはまるで魔法のように完了します。サーバーレス・プログラミング・モデルについての優れた概説が、[Martin Fowler のブログ](https://martinfowler.com/articles/serverless.html)にあります。

[Apache OpenWHisk ソース・コード](https://github.com/openwhisk/openwhisk)を入手して、自身でシステムを実行することもできます。

{{site.data.keyword.openwhisk_short}} の動作について詳しくは、『[{{site.data.keyword.openwhisk_short}} 概要](./openwhisk_about.html)』を参照してください。

ブラウザーおよび CLI を使用して、{{site.data.keyword.openwhisk_short}} アプリケーションを開発できます。
この 2 つには、類似したアプリケーション開発機能がありますが、CLI では、デプロイメントおよび操作をより詳細に制御できます。

## ブラウザーで開発
{: #openwhisk_start_editor}

[ブラウザー](https://console.{DomainName}/openwhisk/editor){: new_window}で {{site.data.keyword.openwhisk_short}} を試して、アクションの作成、トリガーを使用したアクションの自動化、パブリック・パッケージの探索を行ってください。
OpenWhisk ユーザー・インターフェースのクイック・ツアーについては、[詳細](https://console.{DomainName}/openwhisk/learn){: new_window}ページを参照してください。

## CLI を使用して開発
{: #openwhisk_start_configure_cli}

{{site.data.keyword.openwhisk_short}} コマンド・ライン・インターフェース (CLI) を使用して、名前空間および許可鍵をセットアップできます。[「CLI の構成」](https://new-console.{DomainName}/openwhisk/cli){: new_window}に移動し、手順に従ってインストールしてください。

## 概要
{: #openwhisk_start_overview}
- [OpenWhisk の動作](./openwhisk_about.html)
- [サーバーレス・アプリケーションの一般的なユース・ケース](./openwhisk_use_cases.html)
- [OpenWhisk CLI のセットアップと使用](./openwhisk_cli.html)
- [iOS アプリからの OpenWhisk の使用](./openwhisk_mobile_sdk.html)

## プログラミング・モデル
{: #openwhisk_start_programming}
- [システムの詳細](./openwhisk_reference.html)
- [OpenWhisk 提供サービスのカタログ](./openwhisk_catalog.html)
- [アクション](./openwhisk_actions.html)
- [トリガーおよびルール](./openwhisk_triggers_rules.html)
- [フィード](./openwhisk_feeds.html)
- [パッケージ](./openwhisk_packages.html)
- [アノテーション](./openwhisk_annotations.html)
- [Web アクション](./openwhisk_webactions.html)
- [API ゲートウェイ](./openwhisk_apigateway.html)
- [エンティティー名](./openwhisk_reference.html#openwhisk_entities)
- [アクションの意味](./openwhisk_reference.html#openwhisk_semantics)
- [制限](./openwhisk_reference.html#openwhisk_syslimits)

## {{site.data.keyword.openwhisk_short}} Hello World 例
{: #openwhisk_start_hello_world}
{{site.data.keyword.openwhisk_short}} の入門として、まず次の JavaScript コード例を試してみてください。

```javascript
/**
 * Hello world as an OpenWhisk action.
 */
function main(params) {
    var name = params.name || 'World';
    return {payload:  'Hello, ' + name + '!'};
}
```
{: codeblock}

この例を使用するには、以下の手順を実行してください。

1. コードをファイルに保存します。例えば、*hello.js* などです。

2. {{site.data.keyword.openwhisk_short}} CLI コマンド・ラインから、次のコマンドを入力してアクションを作成します。

    ```
    wsk action create hello hello.js
    ```
    {: pre}

3. 次に、以下のコマンドを入力することによって、アクションを起動します。

    ```
    wsk action invoke hello --blocking --result
    ```
    {: pre}  

    このコマンドの出力は以下のとおりです。

    ```json
  {
      "payload": "Hello, World!"
    }
    ```
    
    ```
    wsk action invoke hello --blocking --result --param name Fred
    ```
    {: pre}  

    このコマンドの出力は以下のとおりです。

    ```json
  {
      "payload": "Hello, Fred!"
    }
    ```

{{site.data.keyword.openwhisk_short}} のイベント・ドリブン機能を使用して、イベントに応えてこのアクションを起動することもできます。[アラーム・サービス例](./openwhisk_packages.html#openwhisk_packages_trigger)に従って、周期的イベントが生成されるたびに `hello` アクションを起動するイベント・ソースを構成します。


## API リファレンス
{: #openwhisk_start_api notoc}
* [REST API の資料](./openwhisk_reference.html#openwhisk_ref_restapi)
* [REST API](https://new-console.{DomainName}/apidocs/98){:new_window}

## 関連リンク
{: #general notoc}
* [ディスカバー: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [IBM developerWorks の {{site.data.keyword.openwhisk_short}}](https://developer.ibm.com/openwhisk/){:new_window}
* [Apache {{site.data.keyword.openwhisk_short}} プロジェクト Web サイト](http://openwhisk.org){:new_window}
