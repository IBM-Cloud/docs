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

# {{site.data.keyword.composeForRabbitMQ}} の概説
{: #getting-started-with-compose-for-rabbitmq}

RabbitMQ は、アプリケーションとデータベースの間のメッセージを非同期的に処理し、データ層とアプリケーション層の分離を可能にします。開発者は RabbitMQ を利用すると、カスタマイズ可能な永続性レベル、送達設定、確認済みパブリケーションを指定してメッセージをルーティングし、追跡し、キューに入れることができます。{{site.data.keyword.composeForRabbitMQ_full}} を使用すると、デプロイメントのモニタリング、ボタン・クリックによるスケーリング、ユーザー・セットアップ、ログ・ファイル・アクセスなどといった多数の管理機能を備えた、使いやすい管理インターフェースにアクセスできます。
{:shortdesc}

**注:** 2016 年 9 月 14 日より前にプロビジョンされた、現在もアクティブな Compose サービス・インスタンスは引き続き使用可能で、[https://www.compose.com/](https://www.compose.com) から直接アクセスできます。その時点以降にプロビジョンされた Compose サービス・インスタンスは、Bluemix アカウント内で直接アクセスして使用します。

{{site.data.keyword.composeForRabbitMQ}} の使用を開始するには、以下の手順を実行します。

1. [{{site.data.keyword.composeForRabbitMQ}} インスタンスを作成します](https://console.ng.bluemix.net/catalog/services/compose-for-rabbitmq/)。

  サービスのインスタンスを作成するときは、必ずサービスの名前と資格情報名の両方を選択してください。サービスをバインドしないでおきます。サービスをプロビジョンするときに指定される資格情報を使用して、アプリケーションをサービスに接続できます。*使用可能な資格情報*セクションには、各種の資格情報値がリストされています。

2. {{site.data.keyword.composeForRabbitMQ}} サービスに接続します。

  アプリケーションをサービスに接続するには、サービスと共に作成された資格情報を使用します。サンプル・アプリケーションでは、Node.js を使用して {{site.data.keyword.composeForRabbitMQ}} サービスに接続する方法を示します。

  [compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs) サンプル・アプリケーションをダウンロードし、README ファイル内の指示に従ってください。そして、Bluemix 内のアプリケーション詳細ページで、**「アプリの表示 (View APP)」**をクリックします。

## 使用可能な資格情報

フィールド名|説明
----------|-----------
``uri``|サービスに接続するときに使用する URI。スキーマ (`amqps:)、管理者ユーザー名とパスワード、サーバーのホスト名、接続先のポート番号、vhost 名が含まれます。
`uri_direct_1`|サービスに接続するときに使用可能な代替 URI。形式は `uri` と同様です。
`uri_admin`|データベースの管理インターフェースにアクセスするときに、ブラウザーでアクセスする必要がある URI。アクセスには、`uri` フィールドからの管理者ユーザー名とパスワードが必要です。
`uri_admin_1`|代替管理 URI - `uri_admin` を参照してください。
`uri_admin_2`|代替管理 URI - `uri_admin` を参照してください。
`uri_admin_3`|代替管理 URI - `uri_admin` を参照してください。
`uri_admin_4`|代替管理 URI - `uri_admin` を参照してください。
`ca_certificate_base64`|アプリケーションが適切なサーバーに接続されていることを確認するために使用する自己署名証明書。これは base64 でエンコードされています。サンプル・アプリケーションで示されているように、鍵をデコードした後に使用する必要があります。
`deployment_id`|Compose 内で作成された、サービスの内部 ID。
`db_type`|サービスによって提供されるデータベースのタイプ。この場合は、`rabbitmq`。
`name`|データベース・デプロイメント名。
{: caption="Table 1. {{site.data.keyword.composeForRabbitMQ}} credentials" caption-side="top"}

# 関連リンク
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose の記事](https://www.compose.com/articles/){:new_window}

## チュートリアルとサンプル
{: #samples}
[compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs){:new_window}

## 関連リンク
{: #general}
* [Compose のヘルプ](https://help.compose.com/docs){:new_window}
