---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Dedicated および Local での CF アプリのロギング
{: #hybrid_apps_logs_ov}

{{site.data.keyword.Bluemix_dedicated_notm}} および {{site.data.keyword.Bluemix_local_notm}} では、Cloud Foundry アプリには標準装備のロギングが付属しています。アプリから収集されたデータは、{{site.data.keyword.Bluemix_notm}} コンソールで検討できます。
{:shortdesc}

Cloud Foundry アプリは、Cloud Foundry Loggregator を使用して、アプリ外部からログのモニターおよび転送を行います。アプリ内にエージェントをインストールする必要はありません。

## ハードウェア要件


| **要件** |    **1 台のノード**     | **3 台のノード (高可用性に対応)** |
|-----------------|-------------------|-------------------|
| vCPU | 19 | 57 |
| メモリー | 80 GB | 240 GB |
| ローカル・ストレージ | 2.98 TB | 8.94 TB |
{: caption="表 2. {{site.data.keyword.Bluemix_local_notm}} のロギングのハードウェア要件" caption-side="top"}

## セットアップ

{{site.data.keyword.Bluemix_dedicated_notm}} および {{site.data.keyword.Bluemix_local_notm}} では、ログはデフォルトですべてのアプリでアクティブになります。標準ログの読み取りについての情報を表示するには、[Cloud Foundry で実行されているアプリのロギング](../logging_cf_apps.html#logging_bluemix_cf_apps)を参照してください。さらに、{{site.data.keyword.Bluemix_dedicated_notm}} 環境および {{site.data.keyword.Bluemix_local_notm}} 環境で拡張ロギングを有効にすることができます。

* {{site.data.keyword.Bluemix_dedicated_notm}} 環境および {{site.data.keyword.Bluemix_local_notm}} 環境で拡張ロギングが有効になっていることを確認するには、[ログの表示](#hybrid_apps_logs_dash)の手順に従ってください。**「拡張ビュー」**ボタンがない場合、このフィーチャーは有効になっていません。

* 環境に拡張ロギングを追加するには、[{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) または [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) の資料の手順に従ってください。

## ログ保持期間

{{site.data.keyword.Bluemix_dedicated_notm}} および {{site.data.keyword.Bluemix_local_notm}} の Cloud Foundry アプリでは、ログ・データはデフォルトで 30 日間保管されます。

## Dedicated および Local での Cloud Foundry アプリのログの表示
{: #hybrid_apps_logs_dash}

{{site.data.keyword.Bluemix_dedicated_notm}} および {{site.data.keyword.Bluemix_local_notm}} で実行されているアプリのログを検討することができます。
{:shortdesc}

アプリのログを表示するには、以下の手順に従ってください。
1. 実行中のアプリを選択します。
2. **「ログ (Logs)」**をクリックします。**「ログ (Logs)」**ビューで、実行中のアプリからログを表示することができます。
4. **「拡張ビュー (Advanced View)」**ボタンをクリックします。**「拡張ビュー (Advanced View)」**には、Kibana を使用してログの詳細ビューが表示されます。Kibana は、ログとタイム・スタンプ付きデータを使用してカスタムの視覚化を作成する視覚化ツールです。拡張ビューの使用について詳しくは、[Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) の資料を参照してください。

次に、Kibana ダッシュボードをカスタマイズできます。詳しくは、『[Kibana でのログの分析](../logging_view_kibana3.html#analyzing_logs_Kibana3)』を参照してください。
