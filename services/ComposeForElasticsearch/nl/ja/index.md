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

# Compose for Elasticsearch の概説
{: #getting-started-with-compose-for-elasticsearch}

{{site.data.keyword.composeForElasticsearch_full}} は、フルテキスト検索エンジンの能力と JSON 文書データベースの索引作成の強みを組み合わせたものです。この組み合わせにより、大量のデータの多様な分析を可能にする、強力なツールを生み出します。Elasticsearch を利用することで、検索時の一致度をスコア化できるため、データ・セットを探索していて見逃しかねない類似一致やニアミスを検出できるようになります。
{:shortdesc}

**注:** 2016 年 9 月 14 日より前にプロビジョンされた、現在もアクティブな Compose サービス・インスタンスは引き続き使用可能で、[https://www.compose.com/](https://www.compose.com) から直接アクセスできます。その時点以降にプロビジョンされた Compose サービス・インスタンスは、Bluemix アカウント内で直接アクセスして使用します。

{{site.data.keyword.composeForElasticsearch}} の使用を開始するには、以下の手順を実行します。

1. [{{site.data.keyword.composeForElasticsearch}} インスタンスを作成します](https://console.ng.bluemix.net/catalog/services/compose-for-elasticsearch/)。

  サービスのインスタンスを作成するときは、必ずサービスの名前と資格情報名の両方を選択してください。サービスをバインドしないでおきます。サービスをプロビジョンするときに指定される資格情報を使用して、アプリケーションをサービスに接続できます。*使用可能な資格情報*セクションには、各種の資格情報値がリストされています。

2. {{site.data.keyword.composeForElasticsearch}} サービスに接続します。

  アプリケーションをサービスに接続するには、サービスと共に作成された資格情報を使用します。サンプル・アプリケーションでは、Node.js を使用して {{site.data.keyword.composeForElasticsearch}} サービスに接続する方法を示します。

  [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) サンプル・アプリケーションをダウンロードし、README ファイル内の指示に従ってください。そして、Bluemix 内のアプリケーション詳細ページで、**「アプリの表示 (View APP)」**をクリックして *examples* 索引の内容を表示します。

## 使用可能な資格情報

フィールド名|説明
----------|-----------
`uri`|サービスに接続するときに使用する URI。スキーマ (`https:`)、管理者ユーザー名とパスワード、サーバーのホスト名、接続先のポート番号が含まれます。
`uri_direct_1`|サービスに接続するときに使用可能な代替 URI。形式は `uri` と同様です。
`uri_health`|1 番目の haproxy にクラスター・ヘルスを要求する、`curl` コマンド。
`uri_health_1`|2 番目の haproxy にクラスター・ヘルスを要求する、`curl` コマンド。
`ca_certificate_base64`|アプリケーションが適切なサーバーに接続されていることを確認するために使用する自己署名証明書。これは base64 でエンコードされています。サンプル・アプリケーションで示されているように、鍵をデコードした後に使用する必要があります。
`deployment_id`|Compose 内で作成された、サービスの内部 ID。
`db_type`|サービスによって提供されるデータベースのタイプ。この場合は、`elastic_search`。
`name`|データベース・デプロイメント名。
{: caption="Table 1. {{site.data.keyword.composeForElasticsearch}} credentials" caption-side="top"}

**注:** 2 つの `haproxy` ポータルは、Elasticsearch クラスターへのアクセスを提供します。クラスターに接続するために `uri` と `uri_direct_1` の両方を使用できます。アプリケーションで、接続障害の対応管理のために `uri` と `uri_direct_1` を切り替えます。

# 関連リンク
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose の記事](https://www.compose.com/articles/){:new_window}

## チュートリアルとサンプル
{: #samples}
* [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs){:new_window}

## 関連リンク
{: #general}
* [Compose のヘルプ](https://help.compose.com/docs){:new_window}
