---



copyright:

  years: 2015，2017

lastupdated: "2017-01-12"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:prereq: .prereq}
{:download: .download}
{:pre: .pre}
{:app_name: data-hd-keyref="app_name"}
{:app_key: data-hd-keyref="app_key"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:host: data-hd-keyref="host"}
{:org_name: data-hd-keyref="org_name"}
{:route: data-hd-keyref="route"}
{:space_name: data-hd-keyref="space_name"}
{:service_name: data-hd-keyref="service_name"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:user_ID: data-hd-keyref="user_ID"}

# 使用指令行介面下載、修改及重新部署 Cloud Foundry 應用程式

使用 Cloud Foundry 指令行介面，以下載、修改及重新部署 Cloud Foundry 應用程式和服務實例。
{:shortdesc}

開始之前，請下載並安裝 Cloud Foundry 指令行介面。 

<p>
<a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="（在新分頁或視窗中開啟）"><img class="image" src="images/btn_cf_commandline.svg" alt="下載 Cloud Foundry 指令行介面" /> </a>
  </p>

**限制：**Cygwin 不支援指令行工具。在指令行視窗（而非 Cygwin 指令行視窗）中，使用此工具。
{:prereq}

安裝指令行介面之後，即可開始：

  1. {: download} 將您應用程式的程式碼下載至新的目錄，以設定開發環境。
  
    <a class="xref" href="http://bluemix.net" target="_blank" title="（在新分頁或視窗中開啟）"><img class="image" src="images/btn_starter-code.svg" alt="下載應用程式碼" /> </a>

  2. 切換至您程式碼所在的目錄。

  <pre class="pre">cd <var class="keyword varname">your_new_directory</var></pre>

  3.  適當地變更應用程式碼。例如，如果您是使用 {{site.data.keyword.Bluemix}} 範例應用程式，而且您的應用程式包含 `src/main/webapp/index.html` 檔案，則可以修改它，並編輯 "Thanks for creating ..." 指出新內容。請先確定應用程式在本端執行，再將它部署回 {{site.data.keyword.Bluemix_notm}}。

    記下 `manifest.yml` 檔案。將應用程式部署回 {{site.data.keyword.Bluemix_notm}} 時，此檔案用來決定您應用程式的 URL、記憶體配置、實例數以及其他決定性參數。您可以在 Cloud Foundry 文件中[深入閱讀資訊清單檔 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html "外部鏈結圖示"){: new_window}。

    也請注意 `README.md` 檔案，內含建置指示這類詳細資料（適用時）。

    附註：如果您的應用程式是 Liberty 應用程式，則必須先建置它，再重新部署。

  4. 連接並登入 {{site.data.keyword.Bluemix_notm}}。

  <pre class="pre">cf api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></pre>

  <pre class="pre">cf login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></pre>

  如果您要使用聯合 ID，請使用 `-sso` 選項。

  <pre class="pre">cf login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var> -sso</pre>

  5. 從 <var class="keyword varname">your_new_directory</var> 中，使用 `cf push` 指令以將應用程式重新部署至 {{site.data.keyword.Bluemix_notm}}。如需 `cf push` 指令的相關資訊，請參閱[上傳應用程式](/docs/starters/upload_app.html)。

  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var></pre>

  6. 瀏覽至 https://<var class="keyword varname" data-hd-keyref="app_name">app_name</var>.<span class="keyword" data-hd-keyref="APPDomain">AppDomainName</span>，以存取應用程式。
