---

 

copyright:

  years: 2015, 2016

 

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

# 使用指令行介面部署應用程式
*前次更新：2016 年 2 月 24 日*

您可以使用指令行介面來部署及修改應用程式和服務實例。
{:shortdesc}

開始之前，請先安裝 {{site.data.keyword.Bluemix}} 及 Cloud Foundry 指令行介面。

<p>
<a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="（在新分頁或視窗中開啟）"><img class="image" src="images/btn_bx_commandline.svg" alt="下載 {{site.data.keyword.Bluemix}} 指令行介面" /> </a>  <a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="（在新分頁或視窗中開啟）"><img class="image" src="images/btn_cf_commandline.svg" alt="下載 Cloud Foundry 指令行介面" /> </a>
</p>

**限制：**Cygwin 不支援指令行工具。在指令行視窗（而非 Cygwin 指令行視窗）中，使用這些工具。
{:prereq}

安裝指令行介面之後，即可開始：

  1. {: download} 下載入門範本程式碼。 
      
    <a class="xref" href="http://bluemix.net" target="_blank" title="（在新分頁或視窗中開啟）"><img class="image" src="images/btn_starter-code.svg" alt="下載入門範本程式碼" /> </a>
  
  2. 將套件擷取至新的目錄，以設定開發環境。
  3. 切換至您的新目錄。
  
  <pre class="pre">cd <var class="keyword varname">your_new_directory</var></pre>
  
   4.  適當地變更應用程式碼。建議先確定應用程式在本端執行，再將它部署回 {{site.data.keyword.Bluemix}}。<br><br>一個您應該記錄的檔案是 `manifest.yml` 檔案。將應用程式部署回 {{site.data.keyword.Bluemix}} 時，此檔案用來決定您應用程式的 URL、記憶體配置、實例數以及其他決定性參數。您可以[深入閱讀資訊清單檔](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){: new_window}（位於 Cloud Foundry 文件中）。
  
  5. 連接至 {{site.data.keyword.Bluemix}}。
  
  <pre class="pre">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></pre>
  
  6. 登入 {{site.data.keyword.Bluemix_notm}}。
 
  <pre class="pre">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></pre>
  
  7. 將您的應用程式部署至 {{site.data.keyword.Bluemix_notm}}。如需 cf push 指令的相關資訊，請參閱[上傳應用程式](./upload_app.html)。
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var></pre>
  
  8. 在瀏覽器輸入下列 URL 以存取您的應用程式：

  
  <pre class="codeblock"><code><var class="keyword varname" data-hd-keyref="host">host</var>.<span class="keyword" data-hd-keyref="APPDomain">AppDomainName</span></code></pre>
