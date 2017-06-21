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

アプリケーションをサービスに接続するには、サービスと共に作成された資格情報を使用します。[compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs) サンプル・アプリケーションでは、Node.js を使用して、資格情報を使って {{site.data.keyword.composeForRedis}} サービスに接続する方法を示します。

フィールド名|説明
----------|-----------
`uri`|サービスに接続するときに使用する URI。スキーマ (redis:)、管理者ユーザー名とパスワード、サーバーのホスト名、接続先のポート番号が含まれます。
`uri_cli`|データベース・インスタンスに接続する `redis-cli` コマンド・ライン。
`deployment_id`|Compose 内で作成された、サービスの内部 ID。
`db_type`|サービスによって提供されるデータベースのタイプ。この場合は、`redis`。
`name`|データベース・デプロイメント名。
{: caption="表 1. Compose for Redis の資格情報" caption-side="top"}
