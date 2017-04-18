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

# {{site.data.keyword.composeForPostgreSQL}} の概説
{: #getting-started-with-compose-for-postgreSQL}

{{site.data.keyword.composeForPostgreSQL}} は、高度にカスタマイズ可能な、強力なオープン・ソースのオブジェクト関係データベースです。Postgres を使用すると、迅速で拡張が容易な開発が可能になります。C/C++、Perl、Python、TCL/TK、Delphi/Kylix、VB、PHP、ASP、Java など、使い慣れた言語で開発できます。JSON をサポートする機能が豊富なエンタープライズ・データベースを使用できるので、SQL と NoSQL の両領域のメリットが得られます。
{:shortdesc}

**注:** 2016 年 9 月 14 日より前にプロビジョンされた、現在もアクティブな Compose サービス・インスタンスは引き続き使用可能で、[https://www.compose.com/](https://www.compose.com) から直接アクセスできます。その時点以降にプロビジョンされた Compose サービス・インスタンスは、Bluemix アカウント内で直接アクセスして使用します。

Compose for PostgreSQL の使用を開始するには、以下の手順を実行します。

1. [{{site.data.keyword.composeForPostgreSQL}} インスタンスを作成します](https://console.ng.bluemix.net/catalog/services/compose-for-postgresql/)。

  サービスのインスタンスを作成するときは、必ずサービスの名前と資格情報名の両方を選択してください。サービスをバインドしないでおきます。サービスをプロビジョンするときに指定される資格情報を使用して、アプリケーションをサービスに接続できます。*使用可能な資格情報*セクションには、各種の資格情報値がリストされています。

2. {{site.data.keyword.composeForPostgreSQL}} サービスに接続します。

  アプリケーションをサービスに接続するには、サービスと共に作成された資格情報を使用します。サンプル・アプリケーションでは、Node.js を使用して {{site.data.keyword.composeForPostgreSQL}} サービスに接続する方法を示します。

  [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs) サンプル・アプリケーションをダウンロードし、README ファイル内の指示に従ってください。そして、Bluemix 内のアプリケーション詳細ページで、**「アプリの表示 (View APP)」**をクリックして *examples* 表の内容を表示します。

## 使用可能な資格情報

フィールド名|説明
----------|-----------
`uri`|サービスに接続するときに使用する URI。スキーマ (`postgres:`)、管理者ユーザー名とパスワード、サーバーのホスト名、接続先のポート番号、データベース名、SSL 接続を有効にする "?ssl=true" が含まれます。
`uri_cli`|データベース・インスタンスに接続する `psql` シェル・コマンド・ライン。
`ca_certificate_base64`|アプリケーションが適切なサーバーに接続されていることを確認するために使用する自己署名証明書。これは base64 でエンコードされています。サンプル・アプリケーションで示されているように、鍵をデコードした後に使用する必要があります。
`deployment_id`|Compose 内で作成された、サービスの内部 ID。
`db_type`|サービスによって提供されるデータベースのタイプ。この場合は、`postgresql`。
`name`|データベース・デプロイメント名。
{: caption="Table 1. {{site.data.keyword.composeForPostgreSQL}} credentials" caption-side="top"}

# 関連リンク
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose の記事](https://www.compose.com/articles/){:new_window}

## チュートリアルとサンプル
{: #samples}
* [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs){:new_window}

## 関連リンク
{: #general}
* [Compose のヘルプ](https://help.compose.com/docs){:new_window}
