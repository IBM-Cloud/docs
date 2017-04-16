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

# {{site.data.keyword.composeForEtcd}} の概説
{: #getting-started-with-compose-for-etcd}

etcd は、分散サーバー構成管理のためにサーバー・クラスターの調整と管理に必要な、常に正確なデータを保持するキー/値ストアです。etcd は、RAFT コンセンサス・アルゴリズムを使用して、クラスター内のデータの整合性を保証します。データに対する操作の実行順序を強制することで、クラスター内のすべてのノードにおいて同じ方法で同じ結果が得られるようにします。{{site.data.keyword.composeForEtcd_full}} は、etcd に保管された構成データの自動バックアップを追加します。直感的な管理インターフェースで、デプロイメントのモニター、スケーリング、管理を簡単に行えます。
{:shortdesc}

**注:** 2016 年 9 月 14 日より前にプロビジョンされた、現在もアクティブな Compose サービス・インスタンスは引き続き使用可能で、[https://www.compose.com/](https://www.compose.com) から直接アクセスできます。その時点以降にプロビジョンされた Compose サービス・インスタンスは、Bluemix アカウント内で直接アクセスして使用します。

{{site.data.keyword.composeForEtcd}} の使用を開始するには、以下の手順を実行します。

1. [{{site.data.keyword.composeForEtcd}} インスタンスを作成します](https://console.ng.bluemix.net/catalog/services/compose-for-etcd/)。

  サービスのインスタンスを作成するときは、必ずサービスの名前と資格情報名の両方を選択してください。サービスをバインドしないでおきます。サービスをプロビジョンするときに指定される資格情報を使用して、アプリケーションをサービスに接続できます。*使用可能な資格情報*セクションには、各種の資格情報値がリストされています。

2. {{site.data.keyword.composeForEtcd}} サービスに接続します。

アプリケーションをサービスに接続するには、サービスと共に作成された資格情報を使用します。サンプル・アプリケーションでは、Node.js を使用して {{site.data.keyword.composeForEtcd}} サービスに接続する方法を示します。

[compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) サンプル・アプリケーションをダウンロードし、README ファイル内の指示に従ってください。そして、Bluemix 内のアプリケーション詳細ページで、**「アプリの表示 (View APP)」**をクリックして *examples* の内容を表示します。

## 使用可能な資格情報

フィールド名|説明
----------|-----------
`ca_certificate_base64`|アプリケーションが適切なサーバーに接続されていることを確認するために使用する自己署名証明書。証明書は base64 でエンコードされています。サンプル・アプリケーションで示されているように、鍵をデコードした後に使用する必要があります。
`deployment_id`|Compose 内で作成された、サービスの内部 ID。
`db_type`|サービスによって提供されるデータベースのタイプ。この場合は、`etcd`。
`name`|データベース・デプロイメント名。
``uri``|サービスに接続するときに使用する URI。``uri` には、スキーマ (``amqps:)、管理者ユーザー名とパスワード、サーバーのホスト名、接続先のポート番号、`vhost` 名が含まれます。

{: caption="Table 1. {{site.data.keyword.composeForEtcd}} credentials" caption-side="top"}

# 関連リンク
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose の記事](https://www.compose.com/articles/){:new_window}

## チュートリアルとサンプル
{: #samples}
* [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs){:new_window}

## 関連リンク
{: #general}
* [Compose のヘルプ](https://help.compose.com/docs){:new_window}
