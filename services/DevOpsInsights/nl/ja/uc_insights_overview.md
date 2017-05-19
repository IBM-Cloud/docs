---

copyright:
  years: 2017
lastupdated: "2017-03-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# DevOps Insights と IBM UrbanCode Deploy の統合 - 概要
{: #uc_insights_overview}

{{site.data.keyword.DRA_short}} の一部である Delivery Insights は、IBM UrbanCode Deploy インストールに関するデプロイメントの統計やメトリックなどの情報を表示します。
例えば、デプロイメントの期間、成功、失敗のグラフを、論理的に分類した環境別にすべてソートした状態で表示することができます。
{:shortdesc}

ツールチェーンも {{site.data.keyword.DRA_short}} もない場合は、まず {{site.data.keyword.DRA_short}} を設定する必要があります。

1. {{site.data.keyword.Bluemix}} カタログから、**「{{site.data.keyword.DRA_short}}」**をクリックし、価格設定プランを選択して、**「作成」**をクリックします。

1. **「管理」**タブをクリックした後、**「Delivery Insights for UrbanCode から開始 (Start with Delivery Insights for UrbanCode)」**の下で、**「ここから開始します」**をクリックします。
Delivery Insights がバックグラウンドで組織のためのツールチェーンを作成します。
オープン・ツールチェーンは複数のツール統合のコレクションであり、この例では、IBM UrbanCode Deploy と {{site.data.keyword.DRA_short}} はツールチェーンの一部です。
ツールチェーンについて詳しくは、[ツールチェーンを使用した作業](../ContinuousDelivery/toolchains_working.html)を参照してください。
1. **「Delivery Insights のセットアップ (Delivery Insights Setup)」**ページで、DevOps Connect 設定の手順を実行し、IBM UrbanCode Deploy サーバーを接続します。

<!--  1. Set up a system to run DevOps Connect. See [prerequisites](uc_insights_prereqs.html).
  1. Download DevOps Connect, which is provided in a runnable JAR file.
  1. Copy the script from the **Delivery Insights Setup** page and run it. This command starts DevOps Connect with a token that allows it to connect to your organization on {{site.data.keyword.Bluemix}}.
  1. Connect your IBM UrbanCode Deploy servers to DevOps connect. See [Connecting IBM UrbanCode Deploy servers to Delivery Insights](uc_insights_connect_ucd.html). -->


既にツールチェーンがある場合は、以下の手順を実行して Delivery Insights を追加します。

1. まだ {{site.data.keyword.DRA_short}} ツールがない場合は、それをツールチェーンに追加します。

1. ツールチェーンで、{{site.data.keyword.DRA_short}} ツールをクリックします。

1. **「Delivery Insights のセットアップ (Delivery Insights Setup)」**ページで、DevOps Connect 設定の手順を実行し、IBM UrbanCode Deploy サーバーを接続します。


Delivery Insights と DevOps Connect をセットアップすると、IBM UrbanCode Deploy サーバーからのデータを Delivery Insights で表示できるようになります。
[IBM UrbanCode Deploy サーバーを Delivery Insights に接続する](uc_insights_connect_ucd.html)を参照してください。


<!-- 
For questions or issues, see the [questions forum](https://developer.ibm.com/answers/?community=urbancode).
--> 

![UrbanCode Insights デモ・データからの 2 つのグラフ](images/uc_insights_demo_data.gif)

Delivery Insights で表示できる情報の中には、以下のものが含まれます。


- デプロイメントに関する統計。デプロイメントの期間や時間経過とともに変化するデプロイメント・ボリュームを含む。
- アプリケーション別、また環境別のデプロイメントの失敗率に関する統計。
- コンポーネントのデプロイメントに関する統計。失敗率、デプロイメント時刻、期間などを含む。

## システムの概要

Delivery Insights のトポロジーには、IBM UrbanCode Deploy や DevOps Connect ユーティリティーの 1 つ以上のオンプレミス・インストールが含まれます。<!-- (and optionally IBM UrbanCode Release) -->


以下の図は、それらのシステムの標準的なインストールを示しています。


![UrbanCode Insights のトポロジーの概要 (カスタマー・オンプレミス・システムと IBM Cloud Services を含む)](images/uc_insights_overview_topology_multi_ucd.png)

- **IBM UrbanCode Deploy** のインストール済み環境は、成功したデプロイメントと失敗したデプロイメントについての情報をメトリックとして提供します。
IBM UrbanCode Deploy には、IBM Bluemix DevOps Connect と通信するためのパッチが必要です。


<!--
- **IBM UrbanCode Release** is an optional part of the topology. You can use the environment mappings in IBM UrbanCode Release to set logical environments for reports.

-->

- **IBM Bluemix DevOps Connect** (旧称 IBM UrbanCode Sync Utility) は、IBM UrbanCode Deploy のオンプレミス・インストール済み環境と、IBM ホストのサービス (UrbanCode Insights など) との間の通信を調整します。<!-- and IBM UrbanCode Release -->
DevOps Connect は、オンプレミス・サーバーとのセキュア HTTPS 通信とトークン認証を使用することにより、UrbanCode Insights にデータを提供します。


  DevOps Connect が、トポロジー内の他のシステムと接続するためには、プラグインが必要です。


- {{site.data.keyword.DRA_short}} の一部である **Delivery Insights** は、IBM UrbanCode Deploy 上のデプロイメント・アクティビティーに関するメトリックを提供します。
これには、デプロイメントの回数や、環境グループごとの失敗率が含まれます。
権限は、{{site.data.keyword.Bluemix}} アカウントによって制御されます。

