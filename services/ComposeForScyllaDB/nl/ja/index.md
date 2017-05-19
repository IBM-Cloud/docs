---

copyright:
  years: 2016,2017
lastupdated: "2017-04-27"
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

   アプリケーションをサービスに接続するには、サービスと共に作成された[資格情報](./credentials.html)を使用します。

   [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) サンプル・アプリケーションをダウンロードし、README ファイル内の指示に従ってください。その後、Bluemix コンソール内のアプリケーション詳細ページで、**「アプリの表示 (View APP)」**をクリックします。

   サンプル・アプリケーションでは、Node.js を使用して {{site.data.keyword.composeForScyllaDB}} サービスに接続する方法を示します。
