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

# Compose for MySQL の概説
{: #getting-started-with-compose-for-mysql}

ANSI SQL 99 の広範囲なサブセット、および JSON ドキュメント、全文検索、更新可能なビューなどの独自の幅広い拡張機能セットによって、
MySQL は開発者がアプリケーションに構想を描くための便利なパレットを提供します。
また管理者は、MySQL で使用できるデータベース管理ツールを幅広い選択肢の中から見つけることもできます。
{{site.data.keyword.composeForMySQL_full}} は、MySQL をユーザーの代わりに管理して、MySQL の機能を拡張することにより、
高可用性、冗長度、自動バックアップを備えた、使いやすい自動スケーリング・デプロイメント・システムを提供します。
{:shortdesc}

**注:** {{site.data.keyword.composeForMySQL_full}} には、Compose UI へのアクセス権限がありません。
詳しくは、「[Compose on Bluemix Support](https://help.compose.com/docs/bluemix-compose-support)」を参照してください。

{{site.data.keyword.composeForMySQL}} の使用を開始するには、以下の手順を実行します。

1. [{{site.data.keyword.composeForMySQL}} インスタンスを作成します](https://console.ng.bluemix.net/catalog/services/compose-for-mysql/)。

   サービスのインスタンスを作成するときは、サービスの名前と資格情報名の両方を選択します。サービスをバインドしないでおきます。サービスをプロビジョンするときに指定される資格情報を使用して、アプリケーションをサービスに接続できます。「使用可能な資格情報」セクションには、各種の資格情報値がリストされています。

2. {{site.data.keyword.composeForMySQL}} サービスに接続します。

  アプリケーションをサービスに接続するには、サービスと共に作成された資格情報を使用します。

  [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) サンプル・アプリケーションをダウンロードし、README ファイル内の指示に従ってください。その後、Bluemix コンソール内のアプリケーション詳細ページで、**「アプリの表示 (View APP)」**をクリックします。

  サンプル・アプリケーションでは、Node.js を使用して {{site.data.keyword.composeForMySQL}} サービスに接続する方法を示します。


## 使用可能な資格情報

フィールド名|説明
----------|-----------
`db_type`|サービスによって提供されるデータベースのタイプ。この場合は、`mysql`。
`name`|データベース・デプロイメント名。
`uri_cli`|データベース・インスタンスに接続する `mysql` シェル・コマンド・ライン。
`ca_certificate_base64`|アプリケーションが適切なサーバーに接続されていることを確認するために使用する自己署名証明書。証明書は base64 でエンコードされています。
`deployment_id`|Compose 内で作成された、サービスの内部 ID。
`uri`|サービスに接続するときに使用する URI。スキーマ (`mysql:`)、管理者ユーザー名とパスワード、サーバーのホスト名、接続先のポート番号、vhost 名が含まれます。
{: caption="Table 1. {{site.data.keyword.composeForMySQL}} credentials" caption-side="top"}


# 関連リンク
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose の記事](https://www.compose.com/articles/){:new_window}

## チュートリアルとサンプル
{: #samples}
* [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs){:new_window}

## 関連リンク
{: #general}
* [Compose のヘルプ](https://help.compose.com/docs){:new_window}
