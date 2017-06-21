---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-27"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Bluemix コンソールからのログの分析
{: #analyzing_logs_bmx_ui}

{{site.data.keyword.Bluemix}} では、各 Cloud Foundry アプリまたは Docker コンテナーに対して使用可能なログ・タブでログの表示、フィルタリング、および分析を行うことができます。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} Public は、統合ロギング機能を提供します。例えば、Cloud Foundry (CF) でアプリケーションを実行すると、アプリケーションと対話するシステム・コンポーネントからのログ・データ、アプリケーションについてのログ・データが取り込まれ、さらには stdout と stderr を使用した場合はアプリケーション内からのログ・データも取り込まれます。

分析およびログの保存で使用可能なログ・データに関する以下の情報を考慮してください。

* {{site.data.keyword.Bluemix_notm}} Public では、ログ・データはデフォルトで 7 日間保管されます。 
* 1 日当たり 1 GB までのデータを保管できます。 
* デフォルトでは、{{site.data.keyword.Bluemix_notm}} コンソールから分析用に使用可能なログには、過去 24 時間のデータが含まれます。

**ヒント:** 過去 24 時間より前のカスタム期間のデータを分析する場合は、『[Kibana での高度なログ分析](logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana)』を参照してください。 

##  Cloud Foundry アプリのログへのナビゲート
{: #launch_logs_tab_bmx_ui_cf}

Cloud Foundry アプリのデプロイメントまたはランタイムのログを表示するには、以下の手順を実行します。

1. 「アプリ」ダッシュボードで Cloud Foundry アプリの名前をクリックします。 
    
2. アプリ詳細ページで**「ログ」**をクリックします。
    
    **「ログ」**タブでは、アプリの最近のログを表示したり、最新のログ (ログ・ファイルの末尾) をリアルタイムで確認することができます。また、コンポーネント (ログ・タイプ)、アプリ・インスタンス ID、およびエラーで、ログをフィルター操作できます。
    

##  Docker コンテナーのログへのナビゲート
{: #launch_logs_tab_bmx_ui_containers}

Docker コンテナーのデプロイメントまたはランタイム・ログを表示するには、以下のステップを実行します。

1. 「アプリ」ダッシュボードで単一コンテナーまたはコンテナー・グループをクリックします。 
    
2. アプリ詳細ページで**「モニターおよびログ (Monitoring and Logs)」**をクリックします。

3. **「ロギング」**タブを選択します。
    
    **「ロギング」**タブでは、コンテナーの最近のログを表示したり、最新のログ (ログ・ファイルの末尾) をリアルタイムで確認することができます。 

## CF アプリ・ログのログ・フォーマット
{: #log_format_cf}

{{site.data.keyword.Bluemix_notm}} Cloud Foundry アプリのログは、以下のようなパターンの固定フォーマットで表示されます。

<code><var class="keyword varname">コンポーネント</var>/<var class="keyword varname">インスタンス ID</var>/<var class="keyword varname">メッセージ</var>/<var class="keyword varname">タイム・スタンプ</var></code>

各ログ項目には、以下のフィールドが含まれています。

| フィールド | 説明 |
|-------|-------------|
| タイム・スタンプ | ログ・ステートメントの時刻。タイム・スタンプは、ミリ秒単位まで定義されます。 |
| コンポーネント | ログを生成したコンポーネント。各種コンポーネントのリストについては、『[CF アプリのログ・ソース](logging_cf_apps.html#logging_bluemix_cf_apps_log_sources)』を参照してください。<br> 各コンポーネント・タイプの後に、1 個のスラッシュと、アプリケーション・インスタンスを示す数字が続きます。0 は最初のインスタンスに割り当てられる数字、1 は 2 番目のインスタンスに割り当てられる数字であり、以下同様になります。 |
| メッセージ | コンポーネントによって発行されたメッセージ。メッセージは、コンテキストによって異なります。 |
{: caption="表 1. CF アプリのログ項目フィールド" caption-side="top"}


## コンテナー・ログのログ・フォーマット
{: #log_format_containers}

コンテナーのログは、以下のようなパターンの固定フォーマットで表示されます。

<code><var class="keyword varname">タイム・スタンプ</var>/<var class="keyword varname">マシン</var>/<var class="keyword varname">メッセージ</var>  </code>

各ログ項目には、以下のフィールドが含まれています。

| フィールド | 説明 |
|-------|-------------|
| 日時 | ログ・ステートメントの時刻。タイム・スタンプは、ミリ秒単位まで定義されます。 |
| マシン | コンテナーが実行されているホスト名。 |
| メッセージ | 発行されたメッセージ。メッセージは、コンテキストによって異なります。 |
{: caption="表 2. Docker コンテナーのログ項目フィールド" caption-side="top"}

