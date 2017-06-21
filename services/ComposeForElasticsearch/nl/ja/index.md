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

# Compose for Elasticsearch の概説
{: #getting-started-with-compose-for-elasticsearch}

{{site.data.keyword.composeForElasticsearch_full}} は、フルテキスト検索エンジンの能力と JSON 文書データベースの索引作成の強みを組み合わせたものです。この組み合わせにより、大量のデータの多様な分析を可能にする、強力なツールを生み出します。Elasticsearch を利用することで、検索時の一致度をスコア化できるため、データ・セットを探索していて見逃しかねない類似一致やニアミスを検出できるようになります。
{:shortdesc}

**注:** 2016 年 9 月 14 日より前にプロビジョンされた、現在もアクティブな Compose サービス・インスタンスは引き続き使用可能で、[https://www.compose.com/](https://www.compose.com) から直接アクセスできます。その時点以降にプロビジョンされた Compose サービス・インスタンスは、Bluemix アカウント内で直接アクセスして使用します。

{{site.data.keyword.composeForElasticsearch}} の使用を開始するには、以下の手順を実行します。

1. [{{site.data.keyword.composeForElasticsearch}} インスタンスを作成します](https://console.ng.bluemix.net/catalog/services/compose-for-elasticsearch/)。

  サービスのインスタンスを作成するときは、必ずサービスの名前と資格情報名の両方を選択してください。サービスをバインドしないでおきます。サービスをプロビジョンするときに指定される資格情報を使用して、アプリケーションをサービスに接続できます。*使用可能な資格情報*セクションには、各種の資格情報値がリストされています。

2. {{site.data.keyword.composeForElasticsearch}} サービスに接続します。

  アプリケーションをサービスに接続するには、サービスと共に作成された[資格情報](./credentials.html)を使用します。サンプル・アプリケーションでは、Node.js を使用して {{site.data.keyword.composeForElasticsearch}} サービスに接続する方法を示します。

  [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) サンプル・アプリケーションをダウンロードし、README ファイル内の指示に従ってください。そして、Bluemix 内のアプリケーション詳細ページで、**「アプリの表示 (View APP)」**をクリックして *examples* 索引の内容を表示します。
