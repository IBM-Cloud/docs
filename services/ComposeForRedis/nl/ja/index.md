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

# Compose for Redis の概説
{: #getting-started-with-compose-for-redis}

Redis は、オープン・ソースでインメモリー型のキー/値ストアです。Redis には値として、単純なストリング、ハッシュ、リスト、セットを格納したり、強力なビットマップ、hyperloglog、地理空間インデックスを格納したりできます。Redis は、アプリケーション・キャッシュまたは高速応答用データ・ストアに向いています。{{site.data.keyword.composeForRedis_full}} で提供する構成は、高可用性とディスク上での永続性のために事前調整されており、追加のセキュリティー機能によってすべてがロックダウンされます。
{:shortdesc}

**注:** 2016 年 9 月 14 日より前にプロビジョンされた、現在もアクティブな Compose サービス・インスタンスは引き続き使用可能で、[https://www.compose.com/](https://www.compose.com) から直接アクセスできます。その時点以降にプロビジョンされた Compose サービス・インスタンスは、Bluemix アカウント内で直接アクセスして使用します。

{{site.data.keyword.composeForRedis}} の使用を開始するには、以下の手順を実行します。

1. [{{site.data.keyword.composeForRedis}} インスタンスを作成します](https://console.ng.bluemix.net/catalog/services/compose-for-redis/)。

  サービスのインスタンスを作成するときは、必ずサービスの名前と資格情報名の両方を選択してください。サービスをバインドしないでおきます。サービスをプロビジョンするときに指定される資格情報を使用して、アプリケーションをサービスに接続できます。*使用可能な資格情報*セクションには、各種の資格情報値がリストされています。

2. {{site.data.keyword.composeForRedis}} サービスに接続します。

  アプリケーションをサービスに接続するには、サービスと共に作成された[資格情報](./credentials.html)を使用します。サンプル・アプリケーションでは、Node.js を使用して {{site.data.keyword.composeForRedis}} サービスに接続する方法を示します。

  [compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs) サンプル・アプリケーションをダウンロードし、README ファイル内の指示に従ってください。そして、Bluemix 内のアプリケーション詳細ページで、**「アプリの表示 (View APP)」**をクリックします。
