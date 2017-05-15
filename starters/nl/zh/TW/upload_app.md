---



copyright:

  years: 2015, 2017

lastupdated: "2017-04-19"



---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 上傳應用程式

登入 {{site.data.keyword.Bluemix}} 之後，即可使用 `bluemix app push` 指令來上傳應用程式。
{:shortdesc}

開始之前，您必須：
  1. 安裝 {{site.data.keyword.Bluemix}} 指令行介面。

  <a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="（在新分頁或視窗中開啟）"><img class="image" src="images/btn_bx_commandline.svg" alt="下載 {{site.data.keyword.Bluemix}} 指令行介面" /> </a> 

  2. 連接至 {{site.data.keyword.Bluemix}}。

  <pre class="pre"><code class="hljs">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></code></pre>

  3. 登入 {{site.data.keyword.Bluemix_notm}}。

  <pre class="pre"><code class="hljs">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></code></pre>

發出 **bluemix app push** 指令時，指令行介面會提供 {{site.data.keyword.Bluemix_notm}} 環境的工作目錄，而此環境使用建置套件來建置及執行應用程式。

  1. 從您的應用程式目錄，輸入 **bluemix app push** 指令與應用程式名稱。應用程式名稱在 {{site.data.keyword.Bluemix_notm}} 環境中必須是唯一的。

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -m 512m</code></pre>

  {{site.data.keyword.Bluemix_notm}} 包括內建的建置套件。
在部分案例中，即使是內建建置套件，您也必須提供 -c 選項，來指定用來啟動應用程式的指令。例如，您需要使用 -c 選項來推送 Node.js 應用程式：

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -c start_command</code></pre>

  此外，Node.js 應用程式必須包含有效的 package.json 檔案。

  所有其他外部建置套件都必須使用 -b 選項來推送。例如：

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -b buildpack_URL</code></pre>

  **提示：**使用 **bluemix app push** 指令時，此指令會將所有檔案及目錄從現行目錄複製到 Bluemix。確定應用程式目錄中只有所需的檔案。

  
  2. 如果您變更應用程式，請重新輸入 `bluemix app push` 指令，即可上傳那些變更。此指令會使用您先前的選項以及對提示的回應，以一小段新的程式碼來更新應用程式的所有執行中實例。

{{site.data.keyword.Bluemix}} CLI 已將 cf cli 組合在其安裝中。`bluemix app push` 指令會實際呼叫 `cf push`，以將應用程式上傳及部署至 {{site.data.keyword.Bluemix_notm}}。如需 cf push 的相關資訊，請參閱 [cf 指令](/docs/cli/reference/cfcommands/index.html)。如需建置套件的相關資訊，請參閱[使用社群建置套件](/docs/cfapps/byob.html)。


**提示：**您也可以從 DevOps Services 上傳或部署應用程式。請參閱[使用 Web IDE 在 Node.js 中開發 {{site.data.keyword.Bluemix_notm}} 應用程式](https://hub.jazz.net/tutorials/devopsweb/){: new_window}。
