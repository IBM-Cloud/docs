---
copyright:
  years: 2016
lastupdated: "2016-12-09"
---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Compose for ScyllaDB の概説
{: #getting-started-with-compose-for-scylladb}

ScyllaDB は、Cassandra ワイドカラム分散データベースをインプレースで置き換えたものです。ScyllaDB は、リソースをより有効に使用してベンチマークでのパフォーマンスが 10 倍に向上するように、Cassandra の Java ではなく C++ で記述されています。Cassandra のツールやデータ・ファイルとの互換性を保持することに加えて、
ScyllaDB ではセルフチューニングの機能が追加されます。{{site.data.keyword.composeForScyllaDB_full}} は、ScyllaDB をユーザーの代わりに管理して、その機能を拡張することにより、
高可用性、冗長度、自動バックアップを備えた、使いやすい自動スケーリング・デプロイメント・システムを提供します。
{:shortdesc}

**注:** {{site.data.keyword.composeForScyllaDB_full}} には、Compose UI へのアクセス権限がありません。
詳しくは、「[Compose on Bluemix Support](https://help.compose.com/docs/bluemix-compose-support)」を参照してください。

{{site.data.keyword.composeForScyllaDB}} の使用を開始するには、以下の手順を実行します。

1. [{{site.data.keyword.composeForScyllaDB}} インスタンスを作成します](https://console.ng.bluemix.net/catalog/services/compose-for-scylladb/)。

   サービスのインスタンスを作成するときは、サービスの名前と資格情報名の両方を選択します。サービスをバインドしないでおきます。サービスをプロビジョンするときに指定される資格情報を使用して、アプリケーションをサービスに接続できます。「使用可能な資格情報」セクションには、各種の資格情報値がリストされています。

2. {{site.data.keyword.composeForScyllaDB}} サービスに接続します。

   アプリケーションをサービスに接続するには、サービスと共に作成された資格情報を使用します。

   [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) サンプル・アプリケーションをダウンロードし、README ファイル内の指示に従ってください。その後、Bluemix コンソール内のアプリケーション詳細ページで、**「アプリの表示 (View APP)」**をクリックします。

   サンプル・アプリケーションでは、Node.js を使用して {{site.data.keyword.composeForScyllaDB}} サービスに接続する方法を示します。


## 使用可能な資格情報

フィールド名|説明
----------|-----------
`db_type`|サービスによって提供されるデータベースのタイプ。この場合は、`scylla`。
`uri_cli_1`|データベース・インスタンスに接続する代替の `cqlsh` シェル・コマンド・ライン。
`maps`|さまざまなドライバーが内部 IP アドレスを ScyllaDB データベースの外部 DNS 名に関連付けるために必要な情報を提供する ScyllaDB 接続マップ。
`name`|データベース・デプロイメント名。
`uri_cli`|データベース・インスタンスに接続する `cqlsh` シェル・コマンド・ライン。
`uri_direct_2`|サービスに接続するために使用できる代替 URI。形式は `uri` と同様です。
`uri_direct_1`|サービスに接続するために使用できる代替 URI。形式は `uri` と同様です。
`ca_certificate_base64`|アプリケーションが適切なサーバーに接続されていることを確認するために使用する自己署名証明書。証明書は base64 でエンコードされています。
`deployment_id`|Compose 内で作成された、サービスの内部 ID。
`uri_cli_2`|データベース・インスタンスに接続する代替の `cqlsh` シェル・コマンド・ライン。
`uri`|サービスに接続するときに使用する URI。スキーマ (`scylla:`)、パスワード、サーバーのホスト名、接続先のポート番号、データベース名が含まれます。
{: caption="Table 1. {{site.data.keyword.composeForScyllaDB}} credentials" caption-side="top"}


# 関連リンク
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose の記事](https://www.compose.com/articles/){:new_window}

## チュートリアルとサンプル
{: #samples}
* [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs){:new_window}

## 関連リンク
{: #general}
* [Compose のヘルプ](https://help.compose.com/docs){:new_window}
