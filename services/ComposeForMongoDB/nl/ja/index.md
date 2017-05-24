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

# Compose for MongoDB の概説
{: #getting-started-with-compose-for-mongodb}

{{site.data.keyword.composeForMongoDB_full}} では、JSON データ・ストアとして多くの新規事業や企業に支持されている MongoDB の、強力な索引作成と照会、集約、幅広いドライバーのサポートを利用します。{{site.data.keyword.composeForMongoDB}} は、使いやすい自動スケーリング・デプロイメント・システムを提供します。高可用性と冗長性、自動およびオンデマンドのノンストップ・バックアップ、モニタリング・ツール、アラート・システムへの組み込み、パフォーマンス分析ビュー、その他の機能をすべて、整理されたシンプルなユーザー・インターフェースで提供します。
{:shortdesc}

**注:** 2016 年 9 月 14 日より前にプロビジョンされた、現在もアクティブな Compose サービス・インスタンスは引き続き使用可能で、[https://www.compose.com/](https://www.compose.com) から直接アクセスできます。その時点以降にプロビジョンされた Compose サービス・インスタンスは、Bluemix アカウント内で直接アクセスして使用します。

{{site.data.keyword.composeForMongoDB}} の使用を開始するには、以下の手順を実行します。

1. [{{site.data.keyword.composeForMongoDB}} インスタンスを作成します](https://console.ng.bluemix.net/catalog/services/compose-for-mongodb/)。

   サービスのインスタンスを作成するときは、必ずサービスの名前と資格情報名の両方を選択してください。サービスをバインドしないでおきます。サービスをプロビジョンするときに指定される資格情報を使用して、アプリケーションをサービスに接続できます。*使用可能な資格情報*セクションには、各種の資格情報値がリストされています。

2. {{site.data.keyword.composeForMongoDB}} サービスに接続します。

   アプリケーションをサービスに接続するには、サービスと共に作成された[資格情報](./credentials.html)を使用します。サンプル・アプリケーションでは、Node.js を使用して {{site.data.keyword.composeForMongoDB}} サービスに接続する方法を示します。

   [compose-mongodb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mongodb-helloworld-nodejs) サンプル・アプリケーションをダウンロードし、README ファイル内の指示に従ってください。そして、Bluemix 内のアプリケーション詳細ページで、**「アプリの表示 (View APP)」**をクリックします。
