---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Cloud Foundry でのモニターとロギング
{: #monitoringandlogging}


アプリをモニターし、ログを確認することで、アプリケーション実行
およびデータ・フローをたどって、デプロイメントの理解を深めることができます。また、問題を見つけて修復するために必要な時間と労力を削減することもできます。
{:shortdesc}

{{site.data.keyword.Bluemix}} アプリケーションは、広く分散したマルチインスタンス・アプリケーションにすることができ、アプリケーションの実行およびそのデータを多くのサービスで共有できます。この複合環境では、アプリを管理するために、アプリのモニターとログの確認が重要になります。

## Cloud Foundry アプリのモニターとロギング
{: #monitoring_logging_bluemix_apps}

{{site.data.keyword.Bluemix_notm}} は、アプリの実行中にそのログ・ファイルを生成する組み込みのロギング・メカニズムを備えています。ログでは、アプリに対して生成されたエラー、警告、および情報の各メッセージを表示できます。また、ログ・メッセージをログ・ファイルに書き込むようにアプリを構成することもできます。
ログ・フォーマットおよびログの表示方法について詳しくは、
[『Cloud Foundry で実行されてい
るアプリのロギング』 ](#logging_for_bluemix_apps)を参照してください。

アプリをモニターすることで、アプリのデプロイメントの確認および制御を行うことができます。モニターにより、以下のタスクを実行できます。

* アプリ・インスタンスのパフォーマンス情報を収集およびモニターし、インスタンスが機能しているかどうかを確認する。
* アプリケーションの操作に関する洞察を得る (例えば、潜在的ボトルネックやアップグレードの必要性を検出する)。
* リソースの使用量および料金を推定する。

{{site.data.keyword.Bluemix_notm}} プラットフォームでのデプロイメントの運用を安定化するために、問題を速やかに検出し、原因を効率的に判別する必要があります。この目的を満たすには、アプリの設計時にトラブルシューティングに留意し、アプリを {{site.data.keyword.Bluemix_notm}} にデプロイしたら、モニターおよびロギング用のサービスまたはツールを使用します。

### Cloud Foundry で実行されているアプリのモニター
{: #monitoring_bluemix_apps}

Cloud Foundry インフラストラクチャーを使用して {{site.data.keyword.Bluemix_notm}} でアプリを実行している場合、正常性状況、リソース使用量、トラフィック・メトリックなどの最新のパフォーマンス情報を入手する必要があります。このパフォーマンス情報を使用して、適宜、意思決定やアクション実行を行うことができます。

{{site.data.keyword.Bluemix_notm}} アプリをモニターするには、以下のいずれかの方法を使用します。

* {{site.data.keyword.Bluemix_notm}} サービス。Monitoring and Analytics は、アプリケーション・パフォーマンスのモニターに使用できるサービスを提供します。また、このサービスは、ログ分析などの分析機能も提供します。詳しくは、[Monitoring and
Analytics](/docs/services/monana/index.html#gettingstartedtemplate) を参照してください。
* サード・パーティー・オプション。例えば、[New Relic ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](http://newrelic.com/){:new_window} です。

### Cloud Foundry で実行されているアプリのロギング
{: #logging_for_bluemix_apps}

Cloud Foundry インフラストラクチャーを使用して {{site.data.keyword.Bluemix_notm}} でアプリを実行している場合、ログ・ファイルが自動的に作成されます。デプロイメントからランタイムまでのどのステージでも、エラーが発生した場合は、ログを調べて問題解決の糸口を探すことができます。


<!-- 2016.1.27: original shortdes: Log files are automatically created when you are using the Cloud Foundry infrastructure to run your apps on {{site.data.keyword.Bluemix_notm}}. You can view logs from the {{site.data.keyword.Bluemix_notm}} Dashboard, the cf command line interface, or external hosts. You can also filter the logs to see the parts that you are interested in. -->



### ログのフォーマットと保持
{: #log_format}

{{site.data.keyword.Bluemix_notm}} Public Cloud Foundry アプリでは、ログ・データはデフォルトで 7 日間保管されます。1 日当たり 1 GB までのデータを検索できます。

{{site.data.keyword.Bluemix_notm}} アプリケーションのログは、以下のようなパターンの固定フォーマットで表示されます。

```
1         2         3         4         5
12345678901234567890123456789012345678901234567890--------------------------------------------------
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
<p>ログを生成したコンポーネント。</p>
<p>各コンポーネント・タイプの後に、1 個のスラッシュと、アプリケーション・インスタンスを示す数字が続きます。0 は最初のインスタンスに割り当てられる数字、1 は 2 番目のインスタンスに割り当てられる数字であり、以下同様になります。</p>
<p>以下のリストに、さまざまなタイプのコンポーネントの概要を示します。</p>

<dl>
<dt><strong>LGR</strong></dt>
<dd>Loggregator: LGR コンポーネントは、ロギング・サービスについての情報を提供します。</dd>

<dt><strong>RTR</strong></dt>
<dd>ルーター: RTR コンポーネントは、アプリケーションへの HTTP 要求についての情報を提供します。</dd>

<dt><strong>STG</strong></dt>
<dd>ステージング: STG コンポーネントは、アプリケーションがどのようにステージまたは再ステージされるのかについての情報を提供します。</dd>

<dt><strong>APP</strong></dt>
<dd>アプリケーション: APP コンポーネントは、アプリケーションについての情報を提供します。</dd>

<dt><strong>API</strong></dt>
<dd>Cloud Foundry API: API コンポーネントは、アプリケーション状況を変更するユーザー要求によって生じる内部アクションについての情報を提供します。</dd>

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

以下の図は、Droplet Execution Agent (DEA) に基づく Cloud Foundry アーキテクチャーのさまざまなコンポーネント (ログ・タイプ) を示します。 ![DEA アーキテクチャーのログ・タイプ。](images/logging_F1.png "Droplet Execution Agent (DEA) に基づく Cloud Foundry アーキテクチャーのコンポーネント (ログ・タイプ)。")


## ログの表示
{: #viewing_logs}

Cloud Foundry アプリのログは次の 4 つの場所で表示できます。

  * {{site.data.keyword.Bluemix_notm}} ダッシュボード
  * Kibana ダッシュボード
  * コマンド・ライン・インターフェース
  * 外部ログ・ホスト

### {{site.data.keyword.Bluemix_notm}} ダッシュボードからのログの表示
{: #viewing_logs_UI}

デプロイメントまたはランタイムのログを表示するには、以下の手順を実行します。
1. {{site.data.keyword.Bluemix_notm}} にログインし、アプリのタイルをクリックします。アプリの詳細ページが表示されます。
2. ナビゲーション・バーで、**「ログ」**をクリックします。

**「ログ」**コンソールでは、アプリの最近のログを表示したり、最新のログ (ログ・ファイルの末尾) をリアルタイムで確認することができます。また、ログのタイプとチャネルでログをフィルターに掛けることもできます。

**注:** アプリのクラッシュおよびデプロイメントをまたいでログが継続的に保持されることはありません。


### Kibana ダッシュボードからのログの表示
{: #viewing_logs_Kibana}

カスタム・ダッシュボードを作成して、スペースで実行されるアプリのログを、シンプルまたはクリエイティブな方法で表示します

1. Kibana ユーザー・インターフェースにログインするため、[https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) を開きます。
2. **「Kibana 3」**タブを選択します。
3. ログが何も表示されない場合は、ヘッダーにあるタイム・ピッカーを調整してください。
4. ダッシュボードを新規ダッシュボードとして保存します。
  1. ツールバーで、**「保存」**アイコンをクリックします。
  2. ダッシュボードの名前を入力します。
  3. 名前フィールドの横の**「保存」**アイコンをクリックします。

Kibana ダッシュボードのカスタマイズについて詳しくは、[このブログ投稿](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/)または [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) の資料を参照してください。


### コマンド・ライン・インターフェースからのログの表示
{: #viewing_logs_cli}

コマンド・ライン・インターフェースからログを表示するには、以下のいずれかのオプションを選択します。

<ul>
<li>アプリのデプロイ時にログの末尾を表示する。
<p>**cf logs** コマンドを使用して、 {{site.data.keyword.Bluemix_notm}} へのアプリのデプロイ時にアプリのログ、およびアプリと対話するシステム・コンポーネントのログを表示します。cf コマンド・ライン・インターフェースで以下のコマンドを入力できます。cf logs について詳しくは、『<a href="http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html" target=" _blank">Log Types and Their Messages in Cloud Foundry<img src="../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>』を参照してください。</p>
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

<dl><dt><strong>buildpack.log</strong></dt>
<dd>
<p>このログ・ファイルは、デバッグ用の詳細な通知イベントを記録します。このログを使用して、ビルドパック実行の問題をトラブルシューティングすることができます。</p>
<p>データを <span class="ph filepath">buildpack.log</span> ファイルに生成するには、以下のコマンドを使用してビルドパックのトレースを有効にする必要があります。<pre class="pre">cf set-env <var class="keyword varname">appname</var> JBP_LOG_LEVEL DEBUG</pre></p>
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


**注:** アプリケーションのロギングを有効にする方法については、『[ランタイム・エラーのデバッグ](/docs/debug/index.html#debugging-runtime-errors)』を参照してください。

### 外部ホストからのログの表示
{: #viewing_logs_external}


ログが生成されると、少し遅れて、外部ログ・ホストにあるメッセージを表示できます。それらは、{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースまたは cf コマンド・ライン・インターフェースで表示するメッセージに似たメッセージです。アプリに複数のインスタンスがある場合、ログは集約されるため、アプリのすべてのログを確認できます。それに加えて、ログは、アプリのクラッシュおよびデプロイメントをまたいで継続的に保持されます。

**注:** コマンド・ライン・インターフェースで表示するメッセージは、syslog フォーマットではなく、外部ログ・ホストで表示されるメッセージと完全には一致しないことがあります。




## コマンド・ライン・インターフェースからのログのフィルター操作
{: #filtering_logs}

関心のあるログを表示する場合、または表示しない内容を除外する場合、cf コマンド・ライン・インターフェースで **cut** や **grep** などのフィルター・オプションを指定して **cf logs** コマンドを使用できます。

* 完全な詳細ログではなく、一部を表示する場合、**cut** オプションを使用します。例えば、コンポーネントおよびメッセージの情報を表示するには、以下のコマンドを使用します。
```
cf logs appname --recent | cut -c 29-40,46-
```

**grep** オプションについて詳しくは、cut --help と入力してください。
* 特定のキーワードが含まれているログ項目を表示するには、**grep** オプションを使用します。例えば、キーワード「`[APP`」が含まれているログ項目を表示するには、以下のコマンドを使用できます。

```
cf logs appname --recent | grep '\[App'
```
**grep** オプションについて詳しくは、`grep --help` と入力してください。



## 外部ログ・ホストの構成
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} は、限られた量のログ情報をメモリー内に保持します。情報がログに記録されると、古い情報が新しい情報に置き換えられます。すべてのログ情報を保持するには、外部ログ・ホスト (例えば、サード・パーティーのログ管理サービスまたはその他のホスト) にログを保存することができます。

アプリおよびシステムから外部ログ・ホストにログをストリーミングするには、以下の手順を実行します。

  1. ロギング・エンドポイントを決定します。

	 Papertrail、Splunk、または Sumologic など、サード・パーティーのログ集約機能にログを送信できます。また、syslog ホスト、TLS (Transport Layer Security) で暗号化された syslog ホスト、または HTTPS POST エンドポイントにログを送信することもできます。ロギング・エンドポイントを取得する方法は、ログ・ホストによって異なります。

  2. ユーザー提供のサービス・インスタンスを作成します。

	 `cf create-user-provided-service` コマンド (または、短縮版コマンドの `cups`) を使用して、ユーザー提供のサービス・インスタンスを作成します。
	 ```
	 cf create-user-provided-service <service_name> -l <logging_endpoint>
	 ```
	 &lt;service_name&gt;
	 
	 ユーザー提供のサービス・インスタンスの名前。

	 &lt;logging_endpoint&gt;

	 {{site.data.keyword.Bluemix_notm}} がログを送信する先のロギング・エンドポイント。次の表を参照して、*logging_endpoint* を適切な値で置き換えてください。

	 <table>
	 <caption>表 1. ロギング・エンドポイントの値</caption>
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
	 cf bind-service <appname> <service_name>
	 ```
	 &lt;appname&gt;
	 
	 アプリの名前。

	 &lt;service_name&gt;

	 ユーザー提供のサービス・インスタンスの名前。

  4. アプリを再ステージングします。
     変更を有効にするために、`cf restage appname` を入力します。


### 例: Cloud Foundry アプリケーション・ログの Splunk へのストリーミング
{: #splunk}

この例では、Jane という開発者が、IBM Virtual Servers Beta および Ubuntu イメージを使用して仮想サーバーを作成します。
Jane は Cloud Foundry アプリケーション・ログを
{{site.data.keyword.Bluemix_notm}} から Splunk へストリームし
ようと試みます。

  1. まず、Splunk をセットアップします。

     a. Jane は、[Splunk Light のダウンロード・サイト ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.splunk.com/en_us/download/splunk-light.html){:new_window} から
Splunk Light をダウンロードして、次のコマンドを使用してこれをインストールします。
ソフトウェアは */opt/splunk* にインストールされます。

	    ```
        dpkg -i  ~/splunklight-6.3.0-aa7d4b1ccb80-linux-2.6-amd64.deb
        ```

     b. RFC5424 syslog テクノロジー・アドオンをイン
ストールして適用し、{{site.data.keyword.Bluemix_notm}} と統合します。アドオンのインストール手順について詳しくは、
[『Cloud Foundry ガイドライン』 ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.cloudfoundry.org/devguide/services/integrate-splunk.html){:new_window} を参照してください。

	    次のコマンドを使用してアドオンをインストールします。

	    ```
        cd /opt/splunk/etc/apps
        tar xvfz ~/rfc5424-syslog_11.tgz
        ```

        次に Jane は、*/opt/splunk/etc/apps/rfc5424/default/transforms.conf* を次のテキストで構成される新規の *transforms.conf* ファイルと置き換えて、アドオンを適用します。

	    ```
        [rfc5424_host]
        DEST_KEY = MetaData:Host
        REGEX = <\d+>\d{1}\s{1}\S+\s{1}(\S+)
        FORMAT = host::$1[rfc5424_header]
        REGEX = <(\d+)>\d{1}\s{1}\S+\s{1}\S+\s{1}(\S+)\s{1}(\S+)\s{1}(\S+)
        FORMAT = prival::$1 appname::$2 procid::$3 msgid::$4
        MV_ADD = true
        ```
        {:screen}

     c. Splunk のセットアップ後、Ubuntu マシン上の一部のポートをオープンして、着信 syslog ドレーン (ポート 5140) および Splunk Web UI (ポート 8000) を受け入れる必要があります。{{site.data.keyword.Bluemix_notm}} 仮想サーバーのファイアウォールがデフォルトでセットアップされているためです。

	    **注:** ここでは Jane の評価目的のために iptable 構成としているため、これは一時的なものです。実動における Bluemix 仮想サーバーでのファイアウォール設定を構成する方法について詳しくは、[『ネットワーク・セキュリティー・グループ』![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://new-console.ng.bluemix.net/docs/services/networksecuritygroups/index.html){:new_window} 資料を参照してください。

	   ```
	   iptables -A INPUT -p tcp --dport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --sport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
       iptables -A INPUT -p tcp --sport 8000 -j ACCEPT
	   ```
	   {:screen}

	   次に、Jane は次のコマンドを使用して Splunk を実行します。

       ```
	   /opt/splunk/bin/splunk start --accept-license
       ```

  2. Splunk 設定を構成して、{{site.data.keyword.Bluemix_notm}} から syslog ドレーンを受け入れます。syslog ドレーン用にデータ入力を作成する必要があります。

     a. Splunk Web インターフェースから、**「データ (Data)」>「データ入力 (Data inputs)」
**とクリックします。Splunk がサポー
トする入力タイプのリストが表示されます。

     b. syslog ドレーンが TCP プロトコルを使用するため、
**TCP** を選択します。

     c. **TCP** ペインの **「ポート」**フィールドで、**「5140」**と入力し、残りのフィールドは空白のまま残し、**「次へ」**をクリックします。

     d. **「ソース・タイプ」**リストから、
**「未カテゴリー化 (Uncategorized)」>「rfc5424_syslog」
**を選択します。

     e. **「方式 (Method)」**タイプに
**「IP」**を選択します。

     f. **「索引 (Index)」**フィールド
で、**「新規索引の作成 (Create a new index)」
**をクリックします。新規索引に「bluemix」という名前を付け、**「保存」**をクリックします。

     g. 最後に**「レビュー (Review)」**ウィンドウで、設定が正しいことを確認し、**「送信 (Submit)」**をクリックしてこのデータ入力を有効にします。

  3. {{site.data.keyword.Bluemix_notm}}で、syslog ドレーン・サービスを作成し、これをアプリにバインドします。

     a. cf cli から次のコマンドを使用して syslog ドレーン・サービスを作成します。

     ```
     cf cups splunk -l syslog://dummyhost:5140
     ```

     **注:** *dummyhost* は実名ではありません。実際のホスト名を非表示にするために使用されます。

     b. Jane は 自分のスペースで syslog ドレーン・サービスをアプリにバインドしてから、アプリを再ステージングします。

	 ```
     cf bind-service myapp splunk
     cf restage myapp
     ```


アプリを試行して、Splunk Web インターフェースで次の照会ストリングを入力します。

```
source="tcp:5140" index="bluemix" sourcetype="rfc5424_syslog"
```

Splunk Web インターフェースでログのストリームを確認します。Jane がインストール
する Splunk は Splunk Light ですが、1 日に 500 MB のログを保存することが可能です。

## {{site.data.keyword.Bluemix_dedicated_notm}} および {{site.data.keyword.Bluemix_local_notm}} での Cloud Foundry アプリのロギング
{: #hybrid_apps_logs_ov}


{{site.data.keyword.Bluemix_dedicated_notm}} および {{site.data.keyword.Bluemix_local_notm}} では、Cloud Foundry アプリには標準装備のロギングが付属しています。アプリから収集されたデータは、{{site.data.keyword.Bluemix_notm}} コンソールで検討できます。
{:shortdesc}

Cloud Foundry アプリは、Cloud Foundry Loggregator を使用して、アプリ外部からログのモニターおよび転送を行います。アプリ内にエージェントをインストールする必要はありません。

### ハードウェア要件


| **要件** |    **1 台のノード**     | **3 台のノード (高可用性に対応)** |
|-----------------|-------------------|-------------------|
| vCPU | 19 | 57 |
| メモリー | 80 GB | 240 GB |
| ローカル・ストレージ | 2.98 TB | 8.94 TB |
{: caption="表 2. {{site.data.keyword.Bluemix_local_notm}} のロギングのハードウェア要件" caption-side="top"}

### セットアップ

{{site.data.keyword.Bluemix_dedicated_notm}} および {{site.data.keyword.Bluemix_local_notm}} では、ログはデフォルトですべてのアプリでアクティブになります。標準ログの読み取りについての情報を表示するには、[Cloud Foundry で実行されているアプリのロギング](#logging_for_bluemix_apps)を参照してください。さらに、{{site.data.keyword.Bluemix_dedicated_notm}} 環境および {{site.data.keyword.Bluemix_local_notm}} 環境で拡張ロギングを有効にすることができます。

* {{site.data.keyword.Bluemix_dedicated_notm}} 環境および {{site.data.keyword.Bluemix_local_notm}} 環境で拡張ロギングが有効になっていることを確認するには、[ログの表示](#hybrid_apps_logs_dash)の手順に従ってください。**「拡張ビュー」**ボタンがない場合、このフィーチャーは有効になっていません。

* 環境に拡張ロギングを追加するには、[{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) または [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) の資料の手順に従ってください。

### ログ保持期間

{{site.data.keyword.Bluemix_dedicated_notm}} および {{site.data.keyword.Bluemix_local_notm}} の Cloud Foundry アプリでは、ログ・データはデフォルトで 30 日間保管されます。

## {{site.data.keyword.Bluemix_dedicated_notm}} および {{site.data.keyword.Bluemix_local_notm}} での Cloud Foundry アプリのログの表示
{: #hybrid_apps_logs_dash}

{{site.data.keyword.Bluemix_dedicated_notm}} および {{site.data.keyword.Bluemix_local_notm}} で実行されているアプリのログを検討することができます。
{:shortdesc}

アプリのログを表示するには、以下の手順に従ってください。
1. 実行中のアプリを選択します。
2. **「ログ (Logs)」**をクリックします。**「ログ (Logs)」**ビューで、実行中のアプリからログを表示することができます。
4. **「拡張ビュー (Advanced View)」**ボタンをクリックします。**「拡張ビュー (Advanced View)」**には、Kibana を使用してログの詳細ビューが表示されます。Kibana は、ログとタイム・スタンプ付きデータを使用してカスタムの視覚化を作成する視覚化ツールです。拡張ビューの使用について詳しくは、[Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) の資料を参照してください。

次に、Kibana ダッシュボードをカスタマイズできます。詳細情報については、[Kibana ダッシュボードでのログ表示のカスタマイズ](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_dash_logs_custom)を参照してください。
