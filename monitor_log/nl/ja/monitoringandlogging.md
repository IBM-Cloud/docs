{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#モニターとロギング
{: #monitoringandlogging}

*最終更新日: 2015 年 12 月 8 日*

アプリをモニターし、ログを確認することで、アプリケーション実行
およびデータ・フローをたどって、デプロイメントの理解を深めることができます。また、問題を見つけて修復するために必要な時間と労力を削減することもできます。
{:shortdesc}

{{site.data.keyword.Bluemix}} アプリケーションは、広く分散したマルチインスタンス・アプリケーションにすることができ、アプリケーションの実行およびそのデータを多くのサービスで共有できます。この複合環境では、アプリを管理するために、アプリのモニターとログの確認が重要になります。

{{site.data.keyword.Bluemix_notm}} は、アプリの実行中にそのログ・ファイルを生成する組み込みのロギング・メカニズムを備えています。ログでは、アプリに対して生成されたエラー、警告、および情報の各メッセージを表示できます。また、ログ・メッセージをログ・ファイルに書き込むようにアプリを構成することもできます。ログ・フォーマットおよびログの表示方法について詳しくは、『[{{site.data.keyword.Bluemix_notm}} アプリのロギング (Logging for {{site.data.keyword.Bluemix_notm}} apps)](#logging_for_bluemix_apps)』を参照してください。

アプリをモニターすることで、アプリのデプロイメントの確認および制御を行うことができます。モニターにより、以下のタスクを実行できます。

* アプリ・インスタンスのパフォーマンス情報を収集およびモニターし、インスタンスが機能しているかどうかを確認する。
* アプリケーションの操作に関する洞察を得る (例えば、潜在的ボトルネックやアップグレードの必要性を検出する)。
* リソースの使用量および料金を推定する。

{{site.data.keyword.Bluemix_notm}} プラットフォームでのデプロイメントの運用を安定化するために、問題を速やかに検出し、原因を効率的に判別する必要があります。この目的を満たすには、アプリの設計時にトラブルシューティングに留意し、アプリを {{site.data.keyword.Bluemix_notm}} にデプロイしたら、モニターおよびロギング用のサービスまたはツールを使用します。

##Cloud Foundry で実行されているアプリのモニター
{: #monitoring_bluemix_apps}

Cloud Foundry インフラストラクチャーを使用して {{site.data.keyword.Bluemix_notm}} でアプリを実行している場合、正常性状況、リソース使用量、トラフィック・メトリックなどの最新のパフォーマンス情報を入手する必要があります。このパフォーマンス情報を使用して、適宜、意思決定やアクション実行を行うことができます。

{{site.data.keyword.Bluemix_notm}} アプリをモニターするには、以下のいずれかの方法を使用します。

* {{site.data.keyword.Bluemix_notm}} サービス。Monitoring and Analytics は、アプリケーション・パフォーマンスのモニターに使用できるサービスを提供します。また、このサービスは、ログ分析などの分析機能も提供します。詳しくは、[Monitoring and
Analytics](../services/monana/index.html) を参照してください。
* サード・パーティー・オプション。例えば、[New Relic](http://newrelic.com/){:new_window}。

##Cloud Foundry で実行されているアプリのロギング
{: #logging_for_bluemix_apps}

Cloud Foundry インフラストラクチャーを使用して {{site.data.keyword.Bluemix_notm}} でアプリを実行している場合、ログ・ファイルが自動的に作成されます。ログは、{{site.data.keyword.Bluemix_notm}} のダッシュボードまたは cf コマンド・ライン・インターフェースのいずれかによって表示できます。ログをフィルターに掛けて、関心のある部分を表示できます。

###ログ・フォーマット
{: #log_format}

{{site.data.keyword.Bluemix_notm}} アプリケーションのログは、以下のようなパターンの固定フォーマットで表示されます。

```
         1         2         3         4         5
12345678901234567890123456789012345678901234567890
--------------------------------------------------
yyyy-MM-ddTHH:mm:ss:SS-0500 [App/0]      OUT <message>
```
{:screen}

各ログ項目には、4 つのフィールドが含まれています。各フィールドの要旨については、以下のリストを参照してください。

<dl>
<dt><strong>タイム・スタンプ</strong></dt>
<dd>
<pre class="pre screen"><code>yyyy-MM-ddTHH:mm:ss:SS-0500</code></pre>
<p>桁: 1 から 27</p>
<p>ログ・ステートメントの時刻。タイム・スタンプは、ミリ秒単位まで定義されます。</p>
</dd>

<dt><strong>コンポーネント</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>桁: 29 から 40</p>
<p>ログを生成したコンポーネント。以下のリストに、すべてのコンポーネントの定義を示します。</p>

<dl>
<dt><strong>APP</strong></dt>
<dd>アプリケーション。コンポーネント APP の後には、スラッシュと、アプリケーション・インスタンスを示す数字が続きます。ここで、0 が最初のインスタンスで、1 が 2 番目のインスタンス、…というようになります。</dd>

<dt><strong>API</strong></dt>
<dd>Cloud Foundry API。</dd>

<dt><strong>DEA</strong></dt>
<dd>Droplet Execution Agent。</dd>

<dt><strong>LGR</strong></dt>
<dd>Loggregator。</dd>

<dt><strong>RTR</strong></dt>
<dd>ルーター。</dd>

<dt><strong>STG</strong></dt>
<dd>ステージング。</dd>
</dl>
</dd>

<dt><strong>Stream</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>桁: 42 から 44</p>
<p>ログ・メッセージが書き込まれたストリーム。<samp class="ph codeph">OUT</samp> は <samp class="ph codeph">stdout</samp> ストリームを示し、<samp class="ph codeph">ERR</samp> は <samp class="ph codeph">stderr</samp> ストリームを示します。</p>
</dd>

<dt><strong>メッセージ</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Message</var>&gt;</code></pre>
<p>桁: 46 から行の終わり</p>
<p>コンポーネントによって発行されたメッセージ。メッセージは、コンテキストによって異なります。</p>
</dd>

</dl>

###ログの表示
{: #viewing_logs}

{{site.data.keyword.Bluemix_notm}} のダッシュボードまたはコマンド・ライン・インターフェースのいずれかを使用して、ログを表示できます。

####{{site.data.keyword.Bluemix_notm}} のダッシュボードからのログの表示

**デプロイメント**または**ランタイム**のログを表示するには、以下のステップを実行します。
1. アプリのタイルをクリックします。アプリの詳細ページが表示されます。
2. 左側のナビゲーション・バーで、**「ログ」**をクリックします。

####コマンド・ライン・インターフェースからのログの表示

コマンド・ライン・インターフェースからログを表示するには、以下のいずれかのオプションを選択します。

<ul>
<li>アプリのデプロイ時にログの末尾を表示する。
<p>**cf logs** コマンドを使用して、 {{site.data.keyword.Bluemix_notm}} へのアプリのデプロイ時にアプリのログ、およびアプリと対話するシステム・コンポーネントのログを表示します。cf コマンド・ライン・インターフェースで以下のコマンドを入力できます。cf logs について詳しくは、 『[Log Types and Their Messages in Cloud Foundry](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}』を参照してください。</p>
<dl>
<dt><strong>cf logs <var class="keyword varname">appname</var> --recent</strong></dt>
<dd>最近のログを表示します。</dd>

<dt><strong>cf logs <var class="keyword varname">appname</var></strong></dt>
<dd>このコマンドを実行した時点から生成されたログを表示します。</dd>
</dl>
<div class="note tip"><span class="tiptitle">ヒント:</span> 1 つのコマンド・ライン・ウィンドウで <span class="keyword cmdname">cf push</span> コマンドまたは <span class="keyword cmdname">cf start</span> コマンドを実行した場合、別のコマンド・ライン・ウィンドウで <samp class="ph codeph">cf logs appname --recent</samp> と入力して、リアルタイムにログを確認できます。
</div>
</li>

<li>アプリのデプロイ後にログを表示する。

<p>アプリケーションのロギングが有効になっている場合、実行時にアプリで問題が発生した場合に、以下のアプリケーション・ログを表示できます。アプリケーション・ログは、エラーの原因判別に役立つことがあります。</p>

<dl><strong>buildpack.log</strong></dt>
<dd>
<p>このログ・ファイルは、デバッグ用の詳細な通知イベントを記録します。このログを使用して、ビルドパック実行の問題をトラブルシューティングすることができます。</p>
<p>データを <span class="ph filepath">buildpack.log</span> ファイルに生成するには、以下のコマンドを使用してビルドパックのトレースを有効にする必要があります。<pre class="pre">cf set-env <var class="keyword varname">appname</var> JBP_LOG_LEVEL DEBUG</pre>
<p>
<p>このログを表示するには、以下のコマンドを入力します。<pre class="pre">cf files <var class="keyword varname">appname</var> app/.buildpack-diagnostics/buildpack.log</pre>
</p>
</dd>

<dt><strong>staging_task.log</strong></dt>
<dd><p>このログ・ファイルは、ステージング・タスクの重要なステップ後のメッセージを記録します。このログを使用して、ステージングの問題をトラブルシューティングすることができます。</p>
<p>このログを表示するには、以下のコマンドを入力します。<pre class="pre">cf files <var class="keyword varname">appname</var> logs/staging_task.log</pre>
</p>
</dd>
</dl>
</li></ul>


**注:** アプリケーションのロギングを有効にする方法については、『[ランタイム・エラーのデバッグ](../troubleshoot/debugging.html#debug_runtime)』を参照してください。

###ログのフィルタリング
{: #filtering_logs}

関心のあるログを表示する場合、または表示しない内容を除外する場合、cf コマンド・ライン・インターフェースで **cut** や **grep** などのフィルター・オプションを指定して **cf logs** コマンドを使用できます。

* 完全な詳細ログではなく、一部を表示する場合、**cut** オプションを使用します。例えば、コンポーネントおよびメッセージの情報を表示するには、以下のコマンドを使用します。
```
cf logs appname --recent | cut -c 29-40,46- 
```

**grep** オプションについて詳しくは、cut --help と入力してください。
* 特定のキーワードが含まれているログ項目を表示するには、**grep** オプションを使用します。例えば、キーワード「[APP」が含まれているログ項目を表示するには、以下のコマンドを使用できます。
```
cf logs appname --recent | grep '\[App'
```
**grep** オプションについて詳しくは、`grep --help` と入力してください。

###サード・パーティー・ロギングの構成
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} は、限られた量のログ情報をメモリー内に保持します。情報がログに記録されると、古い情報が新しい情報に置き換えられます。すべてのログ情報を保持するには、サード・パーティーのログ管理サービスにログを保存することができます。

アプリケーションおよびシステムからサード・パーティーのログ管理サービスにログをストリーミングするには、以下のステップを実行してください。

1. サード・パーティーのログ管理サービスを登録します。
    
    Papertail、Splunk Storm、SumoLogic、および Logentries などの、[Syslog プロトコル](http://tools.ietf.org/html/rfc5424){:new_window}をサポートするすべてのサード・パーティー・ログ管理サービスを使用できます。サード・パーティー・ログ管理サービスを登録し、次に {{site.data.keyword.Bluemix_notm}} 内のログの宛先を提供するようにサービスを構成します。構成を完了すると、サービスは通常、{{site.data.keyword.Bluemix_notm}} 内のログの宛先として Syslog URL を提供します。サード・パーティー・ログ管理サービスの構成方法について詳しくは、[Configuring Selected Third-Party Log Management Services ](http://docs.cloudfoundry.org/devguide/services/log-management-thirdparty-svc.html){:new_window}を参照してください。

2. ユーザー提供のサービス・インスタンスを作成します。
	
	{{site.data.keyword.Bluemix_notm}} 内のログをサード・パーティー・ログ管理サービスにストリーミングするには、最初にユーザー提供のサービス・インスタンスを作成する必要があります。以下のコマンドを使用して、ユーザー提供のサービス・インスタンスを作成します。ここで、service_name はユーザー提供のサービス・インスタンスの名前で、syslog_URL はサード・パーティーのロギング・サービスから取得する URL です。
	
	```
	cf create-user-provided-service <service_name> -l <syslog_URL>
	```
	
3. サービス・インスタンスをアプリケーションにバインドします。

	以下のコマンドを使用して、サービス・インスタンスをアプリケーションにバインドします。ここで、appname はアプリケーションの名前で、service_name はユーザー提供のサービス・インスタンスの名前です。
	
	```
	cf bind-service appname <service_name>
	```
	
	その後、変更を有効にするために、cf restage appname と入力して、アプリケーションの再ステージを行うよう求めるプロンプトが出されます。ログが生成されると、少し遅れて、同様のメッセージをサード・パーティー・ログ管理サービスで表示できます。


**注:** コマンド・ライン・インターフェースに表示されるログは、Syslog フォーマットになっておらず、サード・パーティー・ログ管理サービスに表示されるメッセージに完全に一致しない可能性があります。
