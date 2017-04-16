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

# Compose for MongoDB の概説
{: #getting-started-with-compose-for-mongodb}

{{site.data.keyword.composeForMongoDB_full}} では、JSON データ・ストアとして多くの新規事業や企業に支持されている MongoDB の、強力な索引作成と照会、集約、幅広いドライバーのサポートを利用します。{{site.data.keyword.composeForMongoDB}} は、使いやすい自動スケーリング・デプロイメント・システムを提供します。高可用性と冗長性、自動およびオンデマンドのノンストップ・バックアップ、モニタリング・ツール、アラート・システムへの組み込み、パフォーマンス分析ビュー、その他の機能をすべて、整理されたシンプルなユーザー・インターフェースで提供します。
{:shortdesc}

**注:** 2016 年 9 月 14 日より前にプロビジョンされた、現在もアクティブな Compose サービス・インスタンスは引き続き使用可能で、[https://www.compose.com/](https://www.compose.com) から直接アクセスできます。その時点以降にプロビジョンされた Compose サービス・インスタンスは、Bluemix アカウント内で直接アクセスして使用します。

{{site.data.keyword.composeForMongoDB}} の使用を開始するには、以下の手順を実行します。

1. [{{site.data.keyword.composeForMongoDB}} インスタンスを作成します](https://console.ng.bluemix.net/catalog/services/compose-for-mongodb/)。

   サービスのインスタンスを作成するときは、必ずサービスの名前と資格情報名の両方を選択してください。サービスをバインドしないでおきます。サービスをプロビジョンするときに指定される資格情報を使用して、アプリケーションをサービスに接続できます。*使用可能な資格情報*セクションには、各種の資格情報値がリストされています。

2. {{site.data.keyword.composeForMongoDB}} サービスに接続します。

   アプリケーションをサービスに接続するには、サービスと共に作成された資格情報を使用します。サンプル・アプリケーションでは、Node.js を使用して {{site.data.keyword.composeForMongoDB}} サービスに接続する方法を示します。

   [compose-mongodb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mongodb-helloworld-nodejs) サンプル・アプリケーションをダウンロードし、README ファイル内の指示に従ってください。そして、Bluemix 内のアプリケーション詳細ページで、**「アプリの表示 (View APP)」**をクリックします。


## 使用可能な資格情報

フィールド名|説明
----------|-----------
`uri`|サービスに接続するときに使用する URI。`uri` には、スキーマ (`mongodb:`)、管理者ユーザー名とパスワード、サーバーのホスト名、接続先のポート番号、データベース名、SSL 接続を有効にする `?ssl=true` が含まれます。
`uri_cli`|データベース・インスタンスに接続する `mongo` シェル・コマンド・ライン。
`ca_certificate_base64`|アプリケーションが適切なサーバーに接続されていることを確認するために使用する自己署名証明書。証明書は base64 でエンコードされています。サンプル・アプリケーションで示されているように、鍵をデコードした後に使用する必要があります。
`deployment_id`|Compose 内で作成された、サービスの内部 ID。
`db_type`|サービスによって提供されるデータベースのタイプ。この場合は、`mongodb`。
`name`|データベース・デプロイメント名。
{: caption="Table 1. {{site.data.keyword.composeForMongoDB}} credentials" caption-side="top"}

# 関連リンク
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose の記事](https://www.compose.com/articles/){:new_window}

## チュートリアルとサンプル
{: #samples}
* [compose-mongodb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mongodb-helloworld-nodejs){:new_window}

## 関連リンク
{: #general}
* [Compose のヘルプ](https://help.compose.com/docs){:new_window}
