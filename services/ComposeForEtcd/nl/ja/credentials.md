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

アプリケーションをサービスに接続するには、サービスと共に作成された資格情報を使用します。[compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) サンプル・アプリケーションでは、Node.js を使用して、資格情報を使って {{site.data.keyword.composeForEtcd}} サービスに接続する方法を示します。

フィールド名|説明
----------|-----------
`ca_certificate_base64`|アプリケーションが適切なサーバーに接続されていることを確認するために使用する自己署名証明書。証明書は base64 でエンコードされています。サンプル・アプリケーションで示されているように、鍵をデコードした後に使用する必要があります。
`deployment_id`|Compose 内で作成された、サービスの内部 ID。
`db_type`|サービスによって提供されるデータベースのタイプ。この場合は、`etcd`。
`name`|データベース・デプロイメント名。
`uri`|サービスに接続するときに使用する URI。`uri` には、スキーマ (`amqps:)、管理者ユーザー名とパスワード、サーバーのホスト名、接続先のポート番号、`vhost` 名が含まれます。

{: caption="表 1. Compose for etcd の資格情報" caption-side="top"}
