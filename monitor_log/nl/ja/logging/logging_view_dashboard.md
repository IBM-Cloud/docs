---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Bluemix ダッシュボードからの CF アプリ・ログの分析
{: #analyzing_logs_bmx_ui}

{{site.data.keyword.Bluemix}} では、Cloud Foundry アプリケーションごとにある**「ログ」**タブを使用して、ログの表示、フィルター操作、および分析を行うことができます。アプリケーションの最新アクティビティーを表示するには、{{site.data.keyword.Bluemix}} ダッシュボードを使用してください。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} Public では、統合ロギング・サービスが提供されています。ユーザーが Cloud Foundry でアプリケーションを実行すると、ロギング・サービスは、アプリケーションと対話するシステム・コンポーネントからのログ・データ、アプリケーションについてのログ・データを取り込むことに加えて、ユーザーが stdout と stderr を使用する場合はアプリケーション内部からもログ・データを取り込みます。

{{site.data.keyword.Bluemix_notm}} アプリケーションのログは、以下のようなパターンの固定フォーマットで表示されます。

<code><var class="keyword varname">コンポーネント </var>/<var class="keyword varname">インスタンス ID </var>     <var class="keyword varname">メッセージ </var>     <var class="keyword varname">タイム・スタンプ</var></code>
   
ログ・フォーマットの詳細については、『[Cloud Foundry アプリ・ログのログ・フォーマット](logging_view_dashboard.html#log_format_cf)』を参照してください。

**注:** {{site.data.keyword.Bluemix_notm}} Public では、ログ・データはデフォルトで 7 日間保管されます。1 日当たり 1 GB までのデータを検索できます。



##  Bluemix ログ・タブへの移動
{: #launch_logs_tab_bmx_ui}

Cloud Foundry アプリケーションのデプロイメントまたはランタイムのログを表示するには、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} にログインし、{{site.data.keyword.Bluemix_notm}} **「アプリ」**ダッシュボードでアプリ名をクリックします。 

    アプリの詳細ページが表示されます。
    
2. ナビゲーション・バーで、**「ログ」**をクリックします。

    「ログ」タブが開きます。 
    
    **「ログ」**タブでは、アプリの最近のログを表示したり、リアルタイムでログを追尾したりできます。また、コンポーネント (ログ・タイプ)、アプリ・インスタンス ID、およびエラーで、ログをフィルター操作できます。



## Cloud Foundry アプリ・ログのログ・フォーマット
{: #log_format_cf}

各ログ項目には、以下のフィールドが含まれています。

<dl>
<dt><strong>タイム・スタンプ</strong></dt>
<dd>
<p>ログ・ステートメントの時刻。タイム・スタンプは、ミリ秒単位まで定義されます。</p>
</dd>

<dt><strong>コンポーネント</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>ログを生成したコンポーネント。</p>
<p>各コンポーネント・タイプの後に、1 個のスラッシュと、アプリケーション・インスタンスを示す数字が続きます。0 は最初のインスタンスに割り当てられる数字、1 は 2 番目のインスタンスに割り当てられる数字であり、以下同様になります。
フィルター操作してダッシュボードで表示できるのは 1 つのみのアプリケーション・インスタンスであることに注意してください。</p>
<p>以下のリストは、異なるタイプのコンポーネントの概要を示しています。</p>

<dl>
<dt><strong>LGR</strong></dt>
<dd>Loggregator: LGR コンポーネントは、Cloud Foundry の内部からログを転送する Cloud Foundry Loggregator についての情報を提供します。</dd>

<dt><strong>RTR</strong></dt>
<dd>ルーター: RTR コンポーネントは、アプリケーションへの HTTP 要求についての情報を提供します。</dd>

<dt><strong>STG</strong></dt>
<dd>ステージング: STG コンポーネントは、アプリケーションがどのようにステージまたは再ステージされるのかについての情報を提供します。</dd>

<dt><strong>APP</strong></dt>
<dd>アプリケーション: APP コンポーネントは、アプリケーションからのログを提供します。これは stderr および stdout がコーディングされる場所です。
</dd>

<dt><strong>API</strong></dt>
<dd>Cloud Foundry API: API コンポーネントは、アプリケーション状況を変更するユーザー要求の結果として生じる内部アクションについての情報を提供します。</dd>

<dt><strong>DEA</strong></dt>
<dd>Droplet Execution Agent: DEA コンポーネントは、アプリケーションの開始、停止、またはクラッシュについての情報を提供します。
<p>このコンポーネントが使用可能なのは、DEA に基づく Cloud Foundry アーキテクチャーにアプリケーションがデプロイされている場合のみです。</p></dd>

<dt><strong>CELL</strong></dt>
<dd>Diego セル: CELL コンポーネントは、アプリケーションの開始、停止、またはクラッシュについての情報を提供します。
<p>このコンポーネントが使用可能なのは、Diego に基づく Cloud Foundry アーキテクチャーにアプリケーションがデプロイされている場合のみです。</p></dd>

<dt><strong>SSH</strong></dt>
<dd>SSH: SSH コンポーネントは、**cf ssh** コマンドを使用してユーザーがアプリケーションにアクセスするたびに情報を提供します。
<p>このコンポーネントが使用可能なのは、Diego に基づく Cloud Foundry アーキテクチャーにアプリケーションがデプロイされている場合のみです。</p></dd>

</dl>
</dd>

<dt><strong>メッセージ</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Message</var>&gt;</code></pre>
<p>コンポーネントによって発行されたメッセージ。メッセージは、コンテキストによって異なります。</p>
</dd>
</dl>

以下の図は、Droplet Execution Agent (DEA) に基づく Cloud Foundry アーキテクチャーのさまざまなコンポーネント (ログ・タイプ) を示します。
![ DEA アーキテクチャーのログ・タイプ。](images/logging_F1.png "コンポーネント (ログ・タイプ ")Droplet Execution Agent (DEA) に基づいた Cloud Foundry アーキテクチャーの。")



