---

copyright:
  years: 2016,2017
lastupdated: "2017-04-027"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Compose for RabbitMQ の概説
{: #getting-started-with-compose-for-rabbitmq}

RabbitMQ は、アプリケーションとデータベースの間のメッセージを非同期的に処理し、データ層とアプリケーション層の分離を可能にします。開発者は RabbitMQ を利用すると、カスタマイズ可能な永続性レベル、送達設定、確認済みパブリケーションを指定してメッセージをルーティングし、追跡し、キューに入れることができます。{{site.data.keyword.composeForRabbitMQ_full}} を使用すると、デプロイメントのモニタリング、ボタン・クリックによるスケーリング、ユーザー・セットアップ、ログ・ファイル・アクセスなどといった多数の管理機能を備えた、使いやすい管理インターフェースにアクセスできます。
{:shortdesc}

**注:** 2016 年 9 月 14 日より前にプロビジョンされた、現在もアクティブな Compose サービス・インスタンスは引き続き使用可能で、[https://www.compose.com/](https://www.compose.com) から直接アクセスできます。その時点以降にプロビジョンされた Compose サービス・インスタンスは、Bluemix アカウント内で直接アクセスして使用します。

{{site.data.keyword.composeForRabbitMQ}} の使用を開始するには、以下の手順を実行します。

1. [{{site.data.keyword.composeForRabbitMQ}} インスタンスを作成します](https://console.ng.bluemix.net/catalog/services/compose-for-rabbitmq/)。

  サービスのインスタンスを作成するときは、必ずサービスの名前と資格情報名の両方を選択してください。サービスをバインドしないでおきます。サービスをプロビジョンするときに指定される資格情報を使用して、アプリケーションをサービスに接続できます。*使用可能な資格情報*セクションには、各種の資格情報値がリストされています。

2. {{site.data.keyword.composeForRabbitMQ}} サービスに接続します。

  アプリケーションをサービスに接続するには、サービスと共に作成された[資格情報](./credentials.html)を使用します。サンプル・アプリケーションでは、Node.js を使用して {{site.data.keyword.composeForRabbitMQ}} サービスに接続する方法を示します。

  [compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs) サンプル・アプリケーションをダウンロードし、README ファイル内の指示に従ってください。そして、Bluemix 内のアプリケーション詳細ページで、**「アプリの表示 (View APP)」**をクリックします。
