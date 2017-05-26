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

# 使用可能な資格情報
{: #available-credentials}

アプリケーションをサービスに接続するには、サービスと共に作成された資格情報を使用します。[compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) サンプル・アプリケーションでは、Node.js を使用して、資格情報を使って {{site.data.keyword.composeForScyllaDB}} サービスに接続する方法を示します。

フィールド名|説明
----------|-----------
`db_type`|サービスによって提供されるデータベースのタイプ。この場合は、`scylla`。
`uri_cli_1`|データベース・インスタンスに接続する代替の `cqlsh` シェル・コマンド・ライン。
`maps`|さまざまなドライバーが内部 IP アドレスを ScyllaDB データベースの外部 DNS 名に関連付けるために必要な情報を提供する ScyllaDB 接続マップ。
`name`|データベース・デプロイメント名。
`uri_cli`|データベース・インスタンスに接続する `cqlsh` シェル・コマンド・ライン。
`uri_direct_2`|サービスに接続するために使用できる代替 URI。形式は `uri` と同様です。
`uri_direct_1`|サービスに接続するために使用できる代替 URI。形式は `uri` と同様です。
`ca_certificate_base64`|アプリケーションが適切なサーバーに接続されていることを確認するために使用する自己署名証明書。証明書は base64 でエンコードされています。
`deployment_id`|Compose 内で作成された、サービスの内部 ID。
`uri_cli_2`|データベース・インスタンスに接続する代替の `cqlsh` シェル・コマンド・ライン。
`uri`|サービスに接続するときに使用する URI。スキーマ (`scylla:`)、パスワード、サーバーのホスト名、接続先のポート番号、データベース名が含まれます。
{: caption="表 1. Compose for ScyllaDB の資格情報" caption-side="top"}
