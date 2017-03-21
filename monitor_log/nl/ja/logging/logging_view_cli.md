---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# CLI からの CF アプリ・ログの分析
{: #analyzing_logs_cli}

{{site.data.keyword.Bluemix}} では、**cf logs** コマンドを使用することによって、ログの表示、フィルター操作、および分析をコマンド・ライン・インターフェースを介して行うことができます。ログをプログラマチックに管理するには、コマンド・ラインを使用してください。
{:shortdesc}

**cf logs** コマンドを使用して、Cloud Foundry アプリからのログ、および、そのアプリを {{site.data.keyword.Bluemix_notm}} にデプロイする場合はそのアプリと対話するシステム・コンポーネントからのログを表示します。**cf logs** コマンドは、Cloud Foundry アプリケーションの STDOUT および STDERR ログ・ストリームを表示します。

関心のあるログを表示する場合、または表示しない内容を除外する場合、cf コマンド・ライン・インターフェースで **cut** や **grep** などのフィルター・オプションを指定して **cf logs** コマンドを使用できます。

* Cloud Foundry アプリのログを表示する場合は、『[Cloud Foundry アプリのログの表示](logging_view_cli.html#full_log_cli)』を参照してください。
* Cloud Foundry アプリの最新ログ・レコードを表示する場合は、『[Cloud Foundry アプリの最新ログ項目の表示](logging_view_cli.html#tailing_log_cli)』を参照してください。
* 特定の時刻範囲の Cloud Foundry アプリのログ・レコードを表示する場合は、『[ログの一部の表示](logging_view_cli.html#partial_log_cli)』を参照してください。
* 特定のキーワードを含む Cloud Foundry アプリのログ項目を表示する場合は、『[特定のキーワードを含むログ項目の表示](logging_view_cli.html#partial_by_keyword_log_cli)』を参照してください。


## Cloud Foundry アプリのログの表示
{: #full_log_cli}

特定の Cloud Foundry アプリの使用可能なすべてのログを表示するには、以下の手順を実行します。

1. 端末を開いて、{{site.data.keyword.Bluemix}} にログインします。

2. コマンド・ラインから次のコマンドを実行して、すべてのログを表示します。

   <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var></code></pre>
   
   
## Cloud Foundry アプリの最新ログ項目の表示
{: #tailing_log_cli}

特定の Cloud Foundry アプリの使用可能な最新ログを表示するには、以下の手順を実行します。

1. 端末を開いて、{{site.data.keyword.Bluemix}} にログインします。

2. コマンド・ラインから次のコマンドを実行して、すべてのログを表示します。

     <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent</code></pre>

<div class="note tip"><span class="tiptitle">ヒント:</span> 1 つのコマンド・ライン・ウィンドウで <span class="keyword cmdname">cf push</span> コマンドまたは <span class="keyword cmdname">cf start</span> コマンドを実行した場合、別のコマンド・ライン・ウィンドウで <samp class="ph codeph">cf logs appname --recent</samp> と入力して、リアルタイムにログを確認できます。
</div>


## Cloud Foundry ログの一部の表示
{: #partial_log_cli}

特定の Cloud Foundry アプリの使用可能なログのうち、特定の時刻範囲内にある部分を表示するには、以下の手順を実行します。

1. 端末を開いて、{{site.data.keyword.Bluemix}} にログインします。

2. コマンド・ラインから次のコマンドを実行して、すべてのログを表示します。

    <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent  | cut -c 29-40,46-</code></pre>
    
    **cut** オプションについて詳しくは、**cut --help** と入力してください。


## 特定のキーワードを含むログ項目の表示
{: #partial_by_keyword_log_cli}

特定のキーワードが含まれている、Cloud Foundry アプリのログ項目を表示するには、以下の手順を実行します。

1. 端末を開いて、{{site.data.keyword.Bluemix}} にログインします。

2. コマンド・ラインから次のコマンドを実行して、すべてのログを表示します。

    <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent | grep '<var class="keyword varname">keyword</var>'</code></pre>
    

例えば、キーワード「**APP**」が含まれているログ項目を表示するには、以下のコマンドを使用できます。

<pre class="pre screen"><code>cf logs appname --recent | grep '\[App'
</code></pre>

**grep** オプションについて詳しくは、**grep --help** と入力してください。


## Cloud Foundry アプリケーション・ログ
{: #cf_app_logs_cli}

{{site.data.keyword.Bluemix}} にデプロイした後の Cloud Foundry アプリケーションには、以下のログがあります。

<dl><dt><strong>buildpack.log</strong></dt>
<dd>
<p>このログ・ファイルは、デバッグ用の詳細な通知イベントを記録します。このログを使用して、ビルドパック実行の問題をトラブルシューティングすることができます。</p>

<p>データを <span class="ph filepath">buildpack.log</span> ファイルに生成するには、以下のコマンドを使用してビルドパックのトレースを有効にする必要があります。</p>

   <pre class="pre">cf set-env <var class="keyword varname">appname</var> JBP_LOG_LEVEL DEBUG</pre>
   
<p>このログを表示するには、以下のコマンドを入力します。</p>

    <pre class="pre">cf files <var class="keyword varname">appname</var> app/.buildpack-diagnostics/buildpack.log</pre>

</dd>

<dt><strong>staging_task.log</strong></dt>
<dd><p>このログ・ファイルは、ステージング・タスクの重要なステップ後のメッセージを記録します。このログを使用して、ステージングの問題をトラブルシューティングすることができます。</p>

<p>このログを表示するには、以下のコマンドを入力します。</p>

    <pre class="pre">cf files <var class="keyword varname">appname</var> logs/staging_task.log</pre>
</dd>
</dl>

**注:** アプリケーションのロギングを有効にする方法については、『[ランタイム・エラーのデバッグ](/docs/debug/index.html#debugging-runtime-errors)』を参照してください。

