---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#モニターとロギング
{: #monitoringandlogging}

*最終更新日: 2016 年 5 月 11 日*

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

Cloud Foundry インフラストラクチャーを使用して {{site.data.keyword.Bluemix_notm}} でアプリを実行している場合、ログ・ファイルが自動的に作成されます。デプロイメントからランタイムまでのどのステージでも、エラーが発生した場合は、ログを調べて問題解決の糸口を探すことができます。

<!-- 2016.1.27: original shortdes: Log files are automatically created when you are using the Cloud Foundry infrastructure to run your apps on {{site.data.keyword.Bluemix_notm}}. You can view logs from the {{site.data.keyword.Bluemix_notm}} Dashboard, the cf command line interface, or external hosts. You can also filter the logs to see the parts that you are interested in. -->



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

Cloud Foundry アプリのログは次の 3 つの場所で表示できます。

  * [{{site.data.keyword.Bluemix_notm}} ダッシュボード](#viewing_logs_UI){:new_window}
  * [コマンド・ライン・インターフェース](#viewing_logs_cli){:new_window}
  * [外部ログ・ホスト](#thirdparty_logging){:new_window}

#### {{site.data.keyword.Bluemix_notm}} ダッシュボードからのログの表示
{: #viewing_logs_UI}

デプロイメントまたはランタイムのログを表示するには、以下の手順を実行します。
1. {{site.data.keyword.Bluemix_notm}} にログインし、ダッシュボードでアプリのタイルをクリックします。アプリの詳細ページが表示されます。
2. 左側のナビゲーション・バーで、**「ログ」**をクリックします。

**「ログ」**コンソールでは、アプリの最近のログを表示したり、最新のログ (ログ・ファイルの末尾) をリアルタイムで確認することができます。また、ログのタイプとチャネルでログをフィルターに掛けることもできます。

**注:** アプリのクラッシュおよびデプロイメントをまたいでログが継続的に保持されることはありません。



#### コマンド・ライン・インターフェースからのログの表示
{: #viewing_logs_cli}

コマンド・ライン・インターフェースからログを表示するには、以下のいずれかのオプションを選択します。

<ul>
<li>アプリのデプロイ時にログの末尾を表示する。
<p>**cf logs** コマンドを使用して、 {{site.data.keyword.Bluemix_notm}} へのアプリのデプロイ時にアプリのログ、およびアプリと対話するシステム・コンポーネントのログを表示します。cf コマンド・ライン・インターフェースで以下のコマンドを入力できます。cf logs について詳しくは、<a href="http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html" target="_blank">Log Types and Their Messages in Cloud Foundry</a> を参照してください。</p>
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


**注:** アプリケーションのロギングを有効にする方法については、『[ランタイム・エラーのデバッグ](../debug/index.html#debugging-runtime-errors)』を参照してください。




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



### 外部ログ・ホストの構成
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} は、限られた量のログ情報をメモリー内に保持します。情報がログに記録されると、古い情報が新しい情報に置き換えられます。すべてのログ情報を保持するには、外部ログ・ホスト (例えば、サード・パーティーのログ管理サービスまたはその他のホスト) にログを保存することができます。

アプリおよびシステムから外部ログ・ホストにログをストリーミングするには、以下の手順を実行します。

  1. ロギング・エンドポイントを決定します。 
     
	 Papertrail、Splunk、または Sumologic など、サード・パーティーのログ集約機能にログを送信できます。また、syslog ホスト、TLS (Transport Layer Security) で暗号化された syslog ホスト、または HTTPS POST エンドポイントにログを送信することもできます。ロギング・エンドポイントを取得する方法は、ログ・ホストによって異なります。

  2. ユーザー提供のサービス・インスタンスを作成します。
     
	 ```cf create-user-provided-service``` コマンド (または、短縮版コマンド ```cups``) を使用して、ユーザー提供のサービス・インスタンスを作成します。
	 ```
	 cf create-user-provided-service <service_name> -l <logging_endpoint>
	 ```
	 **service_name**
	 
	 ユーザー提供のサービス・インスタンスの名前。
	 
	 **logging_endpoint**
	 
	 {{site.data.keyword.Bluemix_notm}} がログを送信する先のロギング・エンドポイント。次の表を参照して、*logging_endpoint* を適切な値で置き換えてください。
	 
	 <table>
     <thead>
     <tr>
     <th>ロギング・エンドポイント</th>
     <th>コマンド</th>
	 <th>注</th>
     </tr>
     </thead>
     <tbody>
     <tr>
     <td>syslog ホスト</td>
     <td>`cf cups my-logs -l syslog://HOST:PORT`</td>
	 <td>例えば、Papertrail へのロギングを有効にするには、`cf cups my-logs -l syslog://<papertrail-url>` と入力します。 `<papertrail-url>` を、Papertrail からのロギング・エンドポイントの URL に置き換えてください。</td>
     </tr>
	 <tr>
     <td>syslog-tls ホスト</td>
     <td>`cf cups my-logs -l syslog-tls://HOST:PORT`</td>
	 <td>証明書は認証局によって信頼されている必要があります。自己署名証明書を使用しないでください。</td>
     </tr>
	 <tr>
     <td>HTTPS POST</td>
     <td>`cf cups my-logs -l https://HOST:PORT`</td>
	 <td>このエンドポイントは、パブリック・インターネットにあり、{{site.data.keyword.Bluemix_notm}} によってアクセス可能でなければなりません。</td>
     </tr>
     </tbody>
     </table>	
  3. サービス・インスタンスをアプリにバインドします。

	 サービス・インスタンスをアプリにバインドするには、以下のコマンドを使用します。 
	
	 ```
	 cf bind-service appname <service_name>
	```
	 **appname**
	 
	 アプリの名前。
	 
	 **service_name**
	 
	 ユーザー提供のサービス・インスタンスの名前。
	 
  4. アプリを再ステージングします。
     変更を有効にするため、```cf restage appname``` と入力します。 

#### 外部ホストからのログの表示
{: #viewing_logs_external}

	 
ログが生成されると、少し遅れて、外部ログ・ホストにあるメッセージを表示できます。それらは、{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースまたは cf コマンド・ライン・インターフェースで表示するメッセージに似たメッセージです。アプリに複数のインスタンスがある場合、ログは集約されるため、アプリのすべてのログを確認できます。それに加えて、ログは、アプリのクラッシュおよびデプロイメントをまたいで継続的に保持されます。

**注:** コマンド・ライン・インターフェースで表示するメッセージは、syslog フォーマットではなく、外部ログ・ホストで表示されるメッセージと完全には一致しないことがあります。 


