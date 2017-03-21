---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 從 CLI 分析 CF 應用程式日誌
{: #analyzing_logs_cli}

在 {{site.data.keyword.Bluemix}} 中，您可以使用 **cf logs** 指令，透過指令行介面來檢視、過濾及分析日誌。使用指令行，以程式設計方式管理日誌。
{:shortdesc}

當您將應用程式部署在 {{site.data.keyword.Bluemix_notm}} 時，請使用 **cf logs** 指令來顯示來自 Cloud Foundry 應用程式以及來自與其互動之系統元件的日誌。**cf logs** 指令會顯示 Cloud Foundry 應用程式的 STDOUT 和 STDERR 日誌串流。

若要檢視感興趣的日誌，或排除不想要檢視的內容，您可以在 cf 指令行介面中使用 **cf logs** 指令搭配過濾選項，例如 **cut** 和 **grep**：

* 若要檢視 Cloud Foundry 應用程式的日誌，請參閱[檢視 Cloud Foundry 應用程式的日誌](logging_view_cli.html#full_log_cli)。
* 若要檢視 Cloud Foundry 應用程式最近的日誌記錄，請參閱[檢視 Cloud Foundry 應用程式最新的日誌項目](logging_view_cli.html#tailing_log_cli)。
* 若要檢視 Cloud Foundry 應用程式在特定時間範圍中的日誌記錄，請參閱[檢視某區段的日誌](logging_view_cli.html#partial_log_cli)。
* 若要檢視 Cloud Foundry 應用程式日誌中包含特定關鍵字的項目，請參閱[檢視包含特定關鍵字的日誌項目](logging_view_cli.html#partial_by_keyword_log_cli)。


## 檢視 Cloud Foundry 應用程式的日誌
{: #full_log_cli}

若要查看 Cloud Foundry 應用程式所有可用的日誌，請完成下列步驟：

1. 開啟終端機，並登入 {{site.data.keyword.Bluemix}}。

2. 從指令行執行下列指令，以顯示所有日誌：

   <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var></code></pre>
   
   
## 檢視 Cloud Foundry 應用程式最新的日誌項目
{: #tailing_log_cli}

若要查看 Cloud Foundry 應用程式最近的可用日誌，請完成下列步驟：

1. 開啟終端機，並登入 {{site.data.keyword.Bluemix}}。

2. 從指令行執行下列指令，以顯示所有日誌：

     <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent</code></pre>

<div class="note tip"><span class="tiptitle">提示：</span>當您在某個指令行視窗中執行 <span class="keyword cmdname">cf push</span> 或 <span class="keyword cmdname">cf start</span> 指令時，即可在另一個指令行視窗中輸入 <samp class="ph codeph">cf logs appname --recent</samp>，以即時查看日誌。</div>


## 檢視某區段的 Cloud Foundry 日誌
{: #partial_log_cli}

若要查看 Cloud Foundry 應用程式在某個時間範圍內的部分可用日誌，請完成下列步驟：

1. 開啟終端機，並登入 {{site.data.keyword.Bluemix}}。

2. 從指令行執行下列指令，以顯示所有日誌：

    <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent  | cut -c 29-40,46-</code></pre>
    
    如需 **cut** 選項的相關資訊，請輸入 **cut --help**。


## 檢視包含特定關鍵字的日誌項目
{: #partial_by_keyword_log_cli}

若要顯示包含 Cloud Foundry 應用程式特定關鍵字的日誌項目，請完成下列步驟：

1. 開啟終端機，並登入 {{site.data.keyword.Bluemix}}。

2. 從指令行執行下列指令，以顯示所有日誌：

    <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent | grep '<var class="keyword varname">keyword</var>'</code></pre>
    

例如，若要顯示包含關鍵字 **APP** 的日誌項目，您可以使用下列指令：

<pre class="pre screen"><code>cf logs appname --recent | grep '\[App'
</code></pre>

如需 **grep** 選項的相關資訊，請鍵入 **grep --help**。


## Cloud Foundry 應用程式日誌
{: #cf_app_logs_cli}

將 Cloud Foundry 應用程式部署在 {{site.data.keyword.Bluemix}} 之後，Cloud Foundry 應用程式將會有下列日誌：

<dl><dt><strong>buildpack.log</strong></dt>
<dd>
<p>此日誌檔會記錄精細的參考資訊事件，以進行除錯。您可以使用此日誌，對建置套件執行問題進行疑難排解。</p>

<p>若要在 <span class="ph filepath">buildpack.log</span> 檔案中產生資料，您必須使用下列指令來啟用建置套件追蹤：</p>

   <pre class="pre">cf set-env <var class="keyword varname">appname</var> JBP_LOG_LEVEL DEBUG</pre>
   
<p>若要檢視此日誌，請輸入下列指令：</p>

    <pre class="pre">cf files <var class="keyword varname">appname</var> app/.buildpack-diagnostics/buildpack.log</pre>

</dd>

<dt><strong>staging_task.log</strong></dt>
<dd><p>此日誌檔會記錄編譯打包作業的主要步驟之後的訊息。您可以使用此日誌，對編譯打包問題進行疑難排解。</p>

<p>若要檢視此日誌，請輸入下列指令：</p>

    <pre class="pre">cf files <var class="keyword varname">appname</var> logs/staging_task.log</pre>
</dd>
</dl>

**附註：**如需如何啟用應用程式記載的相關資訊，請參閱[針對運行環境錯誤進行除錯](/docs/debug/index.html#debugging-runtime-errors)。

