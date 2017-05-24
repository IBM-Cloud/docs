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

# Compose for RethinkDB の概説
{: #getting-started-with-compose-for-rethinkdb}

{{site.data.keyword.composeForRethinkDB}} は、統合管理および探索コンソールを備えた、JSON 文書ベースの分散データベースを提供します。RethinkDB では ReQL 照会言語を使用します。この照会言語は、関数のチェーニングをベースに構築され、Java、JavaScript、Python、Ruby のクライアント・ライブラリーで使用できます。ReQL を使用すると、クラスターのノード間での分散結合および副照会といった、RethinkDB のサーバー・サイド機能を使用できます。また RethinkDB は、読み取り照会パフォーマンスを向上させる 2 次索引もサポートします。RethinkDB の最強機能 changefeeds を利用すると、多数の ReQL 照会をリアルタイム・フィードに変換できます。
{:shortdesc}

**注:** 2016 年 9 月 14 日より前にプロビジョンされた、現在もアクティブな Compose サービス・インスタンスは引き続き使用可能で、[https://www.compose.com/](https://www.compose.com) から直接アクセスできます。その時点以降にプロビジョンされた Compose サービス・インスタンスは、Bluemix アカウント内で直接アクセスして使用します。

{{site.data.keyword.composeForRethinkDB}} の使用を開始するには、以下の手順を実行します。

1. [{{site.data.keyword.composeForRethinkDB}} インスタンスを作成します](https://console.ng.bluemix.net/catalog/services/compose-for-rethinkdb/)。

  サービスのインスタンスを作成するときは、必ずサービスの名前と資格情報名の両方を選択してください。サービスをバインドしないでおきます。サービスをプロビジョンするときに指定される資格情報を使用して、アプリケーションをサービスに接続できます。*使用可能な資格情報*セクションには、各種の資格情報値がリストされています。

2. {{site.data.keyword.composeForRethinkDB}} サービスに接続します。

   アプリケーションをサービスに接続するには、サービスと共に作成された[資格情報](./credentials.html)を使用します。サンプル・アプリケーションでは、Node.js を使用して {{site.data.keyword.composeForRethinkDB}} サービスに接続する方法を示します。

   [compose-rethinkdb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rethinkdb-helloworld-nodejs) サンプル・アプリケーションをダウンロードし、README ファイル内の指示に従ってください。そして、Bluemix 内のアプリケーション詳細ページで、**「アプリの表示 (View APP)」**をクリックします。
