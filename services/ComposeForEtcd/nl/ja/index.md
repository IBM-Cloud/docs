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

# Compose for etcd の概説
{: #getting-started-with-compose-for-etcd}

etcd は、分散サーバー構成管理のためにサーバー・クラスターの調整と管理に必要な、常に正確なデータを保持するキー/値ストアです。etcd は、RAFT コンセンサス・アルゴリズムを使用して、クラスター内のデータの整合性を保証します。データに対する操作の実行順序を強制することで、クラスター内のすべてのノードにおいて同じ方法で同じ結果が得られるようにします。{{site.data.keyword.composeForEtcd_full}} は、etcd に保管された構成データの自動バックアップを追加します。直感的な管理インターフェースで、デプロイメントのモニター、スケーリング、管理を簡単に行えます。
{:shortdesc}

**注:** 2016 年 9 月 14 日より前にプロビジョンされた、現在もアクティブな Compose サービス・インスタンスは引き続き使用可能で、[https://www.compose.com/](https://www.compose.com) から直接アクセスできます。その時点以降にプロビジョンされた Compose サービス・インスタンスは、Bluemix アカウント内で直接アクセスして使用します。

{{site.data.keyword.composeForEtcd}} の使用を開始するには、以下の手順を実行します。

1. [{{site.data.keyword.composeForEtcd}} インスタンスを作成します](https://console.ng.bluemix.net/catalog/services/compose-for-etcd/)。

  サービスのインスタンスを作成するときは、必ずサービスの名前と資格情報名の両方を選択してください。サービスをバインドしないでおきます。サービスをプロビジョンするときに指定される資格情報を使用して、アプリケーションをサービスに接続できます。*使用可能な資格情報*セクションには、各種の資格情報値がリストされています。

2. {{site.data.keyword.composeForEtcd}} サービスに接続します。

アプリケーションをサービスに接続するには、サービスと共に作成された[資格情報](./credentials.html)を使用します。サンプル・アプリケーションでは、Node.js を使用して {{site.data.keyword.composeForEtcd}} サービスに接続する方法を示します。

[compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) サンプル・アプリケーションをダウンロードし、README ファイル内の指示に従ってください。そして、Bluemix 内のアプリケーション詳細ページで、**「アプリの表示 (View APP)」**をクリックして *examples* の内容を表示します。
