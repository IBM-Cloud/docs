---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 通过 CLI 分析 CF 应用程序日志
{: #analyzing_logs_cli}

在 {{site.data.keyword.Bluemix}} 中，可以通过命令行界面使用 **cf logs** 命令来查看、过滤和分析日志。使用命令行以编程方式管理日志。
{:shortdesc}

将应用程序部署到 {{site.data.keyword.Bluemix_notm}} 中时，可使用 **cf logs** 命令来显示 Cloud Foundry 应用程序的日志以及与该应用程序进行交互的系统组件的日志。**cf logs** 命令显示 Cloud Foundry 应用程序的 STDOUT 和 STDERR 日志流。

要查看感兴趣的日志或排除不想查看的内容，可以在 cf 命令行界面中将 **cf logs** 命令与过滤选项（例如，**cut** 和 **grep**）一起使用：

* 要查看 Cloud Foundry 应用程序的日志，请参阅[查看 Cloud Foundry 应用程序的日志](logging_view_cli.html#full_log_cli)。
* 要查看 Cloud Foundry 应用程序的最新日志记录，请参阅[查看 Cloud Foundry 应用程序的最新日志条目](logging_view_cli.html#tailing_log_cli)。
* 要查看 Cloud Foundry 应用程序在特定时间范围内的日志记录，请参阅[查看日志的一部分](logging_view_cli.html#partial_log_cli)。
* 要查看 Cloud Foundry 应用程序日志中包含特定关键字的条目，请参阅[查看包含特定关键字的日志条目](logging_view_cli.html#partial_by_keyword_log_cli)。


## 查看 Cloud Foundry 应用程序的日志
{: #full_log_cli}

要查看可用于 Cloud Foundry 应用程序的所有日志，请完成以下步骤：

1. 打开终端并登录到 {{site.data.keyword.Bluemix}}。

2. 在命令行中，运行以下命令以显示所有日志：

   <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var></code></pre>
   
   
## 查看 Cloud Foundry 应用程序的最新日志条目
{: #tailing_log_cli}

要查看可用于 Cloud Foundry 应用程序的最新日志，请完成以下步骤：

1. 打开终端并登录到 {{site.data.keyword.Bluemix}}。

2. 在命令行中，运行以下命令以显示所有日志：

     <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent</code></pre>

<div class="note tip"><span class="tiptitle">提示：</span>在一个命令行窗口中运行 <span class="keyword cmdname">cf push</span> 或 <span class="keyword cmdname">cf start</span> 命令时，可以在另一个命令行窗口中输入 <samp class="ph codeph">cf logs appname --recent</samp> 来实时查看日志。</div>


## 查看 Cloud Foundry 日志的一部分
{: #partial_log_cli}

要查看某个时间范围内可用于 Cloud Foundry 应用程序的日志部分，请完成以下步骤：

1. 打开终端并登录到 {{site.data.keyword.Bluemix}}。

2. 在命令行中，运行以下命令以显示所有日志：

    <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent  | cut -c 29-40,46-</code></pre>
    
    有关 **cut** 选项的更多信息，请输入 **cut --help**。


## 查看包含特定关键字的日志条目
{: #partial_by_keyword_log_cli}

要显示包含特定关键字的 Cloud Foundry 应用程序日志条目，请完成以下步骤：

1. 打开终端并登录到 {{site.data.keyword.Bluemix}}。

2. 在命令行中，运行以下命令以显示所有日志：

    <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent | grep '<var class="keyword varname">keyword</var>'</code></pre>
    

例如，要显示包含关键字 **APP** 的日志条目，可以使用以下命令：

<pre class="pre screen"><code>cf logs appname --recent | grep '\[App'
</code></pre>

有关 **grep** 选项的更多信息，请键入 **grep --help**。






## Cloud Foundry 应用程序日志
{: #cf_app_logs_cli}

将 Cloud Foundry 应用程序部署到 {{site.data.keyword.Bluemix}} 后，将为该应用程序提供以下日志：

<dl><dt><strong>buildpack.log</strong></dt>
<dd>
<p>此日志文件会记录细颗粒度的参考事件，用于调试目的。您可以使用此日志来对 buildpack 执行问题进行故障诊断。</p>

<p>要将数据生成到 <span class="ph filepath">buildpack.log</span> 文件中，必须使用以下命令来启用 buildpack 跟踪：
</p>

   <pre class="pre">cf set-env <var class="keyword varname">appname</var> JBP_LOG_LEVEL DEBUG</pre>
   
<p>要查看此日志，请输入以下命令：
</p>

    <pre class="pre">cf files <var class="keyword varname">appname</var> app/.buildpack-diagnostics/buildpack.log</pre>

</dd>

<dt><strong>staging_task.log</strong></dt>
<dd><p>此日志文件会在编译打包任务的主要步骤之后记录消息。您可以使用此日志来对编译打包问题进行故障诊断。</p>

<p>要查看此日志，请输入以下命令：
</p>

    <pre class="pre">cf files <var class="keyword varname">appname</var> logs/staging_task.log</pre>
</dd>
</dl>

**注：**有关如何启用应用程序日志记录的信息，请参阅[调试运行时错误](/docs/debug/index.html#debugging-runtime-errors)。

