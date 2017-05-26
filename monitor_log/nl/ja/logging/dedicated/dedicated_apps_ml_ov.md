---



copyright:

  years: 2016, 2017

lastupdated: "2017-04-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

<!-- audience blue staging only begin -->

# Dedicated および Local における Cloud Foundry アプリのモニターとロギング
{: #dedicated_apps_ml_ov}


{{site.data.keyword.Bluemix_dedicated_notm}} および {{site.data.keyword.Bluemix_local_notm:}} では、Cloud Foundry アプリには標準装備のロギングが付属しています。アプリから収集されたデータは、{{site.data.keyword.Bluemix_notm}} コンソールで検討できます。
{:shortdesc}

Cloud Foundry アプリは、Cloud Foundry Loggregator を使用して、アプリ外部からログのモニターおよび転送を行います。アプリ内にエージェントをインストールする必要はありません。

## ハードウェア要件


| **要件** |    **1 台のノード**     | **3 台のノード (高可用性に対応)** |
|-----------------|-------------------|-------------------|
vCPU | 19 | 57 |
メモリー | 80 GB | 240 GB |
ローカル・ストレージ | 2.98 TB | 8.94 TB |
{: caption="表 1.  {{site.data.keyword.Bluemix_local_notm:}}" caption-side="top"} のロギングのハードウェア要件

## セットアップ

{{site.data.keyword.Bluemix}} Dedicated および {{site.data.keyword.Bluemix}} Local では、ログはデフォルトですべてのアプリでアクティブになります。標準ログの読み取りについての情報を表示するには、Cloud Foundry で実行されているアプリのロギングを参照してください。さらに、{{site.data.keyword.Bluemix}} Dedicated 環境および {{site.data.keyword.Bluemix}} Local 環境で拡張ロギングを有効にすることができます。

## ログ保持期間

{{site.data.keyword.Bluemix}} Dedicated および {{site.data.keyword.Bluemix}} Local の Cloud Foundry アプリでは、ログ・データはデフォルトで 30 日間保管されます。

## {{site.data.keyword.Bluemix}} Dedicated および {{site.data.keyword.Bluemix}} Local での Cloud Foundry アプリのログの表示
{: #dedicated_apps_ml_logs_dash}

{{site.data.keyword.Bluemix_notm}} Dedicated および {{site.data.keyword.Bluemix_notm}} Local で実行されているアプリのログを検討することができます。
{:shortdesc}

アプリのログを表示するには、以下の手順に従ってください。
1. 実行中のアプリを選択します。
2. **「ログ (Logs)」**をクリックします。**「ログ (Logs)」**ビューで、実行中のアプリからログを表示することができます。
4. **「拡張ビュー (Advanced View)」**ボタンをクリックします。**「拡張ビュー (Advanced View)」**には、Kibana を使用してログの詳細ビューが表示されます。Kibana は、ログとタイム・スタンプ付きデータを使用してカスタムの視覚化を作成する視覚化ツールです。詳細ビューの使用法について詳しくは、「[Kibana User Guide ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}」を参照してください。

次に、Kibana ダッシュボードをカスタマイズできます。詳しくは、『[Kibana での高度なログ分析](../kibana4/analyzing_logs_Kibana.html#analyzing_logs_Kibana)』を参照してください。

<!-- audience blue staging only end comment -->
