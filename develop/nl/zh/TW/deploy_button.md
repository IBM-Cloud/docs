---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


#建立「部署至 {{site.data.keyword.Bluemix_notm}}」按鈕 {: #deploy-button} 

*前次更新：2016 年 3 月 2 日* 

「部署至 {{site.data.keyword.Bluemix}}」按鈕可讓您有效率地共用您的公用 Git 來源應用程式，讓其他人能夠試用程式碼，並將其部署至 IBM {{site.data.keyword.Bluemix_notm}}。此按鈕需要的配置最少，而且您可以將其插入到任何支援標記的地方。任何人按一下此按鈕，就可以在新的 Git 儲存庫中建立複製的程式碼副本，所以您的原始應用程式會保持原狀，不受任何影響。
{: shortdesc} 

**提示：**如果公司品牌很重要，您可以在內容中[內嵌「部署至 {{site.data.keyword.Bluemix_notm}}」的 iFrame 流程](../develop/deploy_button_embed.html)，而非插入按鈕。當有人建立您的公用 Git 來源應用程式的副本時，他們會停留在您的內容中，而非重新導向至 bluemix.net 網站。 

當有人按一下您的按鈕時，就會進行下列動作： 

1. 如果那個人沒有作用中的 {{site.data.keyword.Bluemix}} 帳戶，則必須建立試用帳戶。 

2. 那個人可以選取地區、組織、空間及應用程式名稱。建議的應用程式名稱是依據前一個應用程式名稱、那個人的使用者名稱以及時間來建構。 

3. 原始的公用 Git 儲存庫的主要分支會複製到新的專用 {{site.data.keyword.jazzhub_title}} 專案，並具有新的 Git 儲存庫。 

4. 如果應用程式需要建置檔，則會自動偵測建置檔，並建置應用程式。 

5. 如果配置管線進行建置及部署程序，則會使用 `pipeline.yml` 檔來部署應用程式。

6. 如果應用程式需要儲存器，則會使用 `pipeline.yml`（它會定義 **IBM Containers** 服務）及 Dockerfile（它定義映像檔）在 {{site.data.keyword.Bluemix_notm}} 儲存器中部署應用程式。 

7. 應用程式會部署至那個人的 {{site.data.keyword.Bluemix_notm}} 組織。 

##按鈕的範例 {: #button-examples} 

請參閱公用 {{site.data.keyword.jazzhub_short}} 儲存庫的應用程式按鈕範例：

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://hub.jazz.net/git/idsorg/sample-java-cloudant" target="_blank" title="（在新分頁或視窗中開啟）"><img class="image" src="images/deploy_buttonx2.png" alt="部署至 Bluemix" /></a>
</p> 

請參閱公用 GitHub 儲存庫的應用程式按鈕範例： 

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://github.com/ibmjstart/bluemix-node-mysql-uploader" target="_blank" title="（在新分頁或視窗中開啟）"><img class="image" src="images/deploy_buttonx2.png" alt="部署至 Bluemix" /></a>
</p> 

請參閱在 {{site.data.keyword.Bluemix_notm}} 儲存器中部署之應用程式的按鈕範例： 

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://github.com/Puquios/hello-containers" target="_blank" title="（在新分頁或視窗中開啟）"><img class="image" src="images/deploy_buttonx2.png" alt="部署至 Bluemix" /></a>
</p> 

##建立按鈕 {: #create-button}

若要建立「部署至 {{site.data.keyword.Bluemix_notm}}」按鈕，請執行下列動作： 

<ol>
<li> 複製並修改下列其中一個 Snippet 範本，並包括公用 Git 儲存庫。

<p></p>
<p>
<strong>提示</strong>：如果想要為 DevOps Services 專案指定建置輸入，請將分支參數新增至 Git URL。當您新增分支參數時，原始公用 Git 儲存庫（包括其所有分支）會複製到新的專用 DevOps Services 專案（含新的 Git 儲存庫）。指定的 Git 分支會設為建置工作的輸入。如果未指定分支，則依預設，建置工作的輸入會設為主分支。</p>
<ul>
<li>HTML：<p>
預設主要分支：
</p>
<pre class="codeblock">
&lt;a href="https://bluemix.net/deploy?repository=&lt;git_repository_URL>" # [required]&gt;&lt;img src="https://bluemix.net/deploy/button.png" alt="Deploy to Bluemix"&gt;&lt;/a&gt;
</pre>
<p>
指定的 Git 分支：
</p>
<pre class="codeblock">
&lt;a href="https://bluemix.net/deploy?repository=&lt;git_repository_URL&gt;&branch=&lt;git_branch>" # [required]&gt;&lt;img src="https://bluemix.net/deploy/button.png" alt="Deploy to Bluemix"&gt;&lt;/a&gt;
</pre>
</li>
<li>Markdown：
<p>
預設主要分支：
</p>
<pre class="codeblock">
[&#33;[Deploy to Bluemix]&#40;https://bluemix.net/deploy/button.png&#41;]&#40;https://bluemix.net/deploy?repository=&lt;git_repository_URL> # [required]&#41;
</pre>
<p>指定的 Git 分支：
</p>
<pre class="codeblock">
[&#33;[Deploy to Bluemix]&#40;https://bluemix.net/deploy/button.png&#41;]&#40;https://bluemix.net/deploy?repository=&lt;git_repository_URL> &branch=&lt;git_branch&gt; # [required]&#41;
</pre>
</li>
</ul>
</li>
<li>將 Snippet 插入部落格、文章、Wiki、Readme 檔中，或是您要推銷應用程式的任何地方。</li>
</ol>

##按鈕的 Snippet 考量 {: #button-snippet}

當您自訂「部署至 Bluemix」按鈕的 Snippet 時，請檢閱下列考量事項。 

* 這兩個範本都會使用 PNG 格式且為英文的外部按鈕影像預設路徑。 

    * 如果您偏好使用 SVG 影像來作為按鈕，而不使用 PNG，則有 SVG 版本可供使用。您可以將 Snippet 中使用的外部按鈕影像的路徑，變更為 `https://bluemix.net/deploy/button.svg`。
	
	* 如果您偏好針對按鈕使用較大的影像，有一個是原始大小兩倍大的 PNG 影像可以使用。您可以將 Snippet 中使用的外部按鈕影像的路徑，變更為 `https://bluemix.net/deploy/button_x2.png`。 
	
	* 如果您希望在本端儲存影像，則可以下載影像，並將它儲存在 Git 儲存庫中。請調整路徑來使用影像的相對位置。 
	
	* 如果您想要使用翻譯的按鈕版本，可以從遠端參照，或是從 [ftp://public.dhe.ibm.com/cloud/bluemix/deploy_button](ftp://public.dhe.ibm.com/cloud/bluemix/deploy_button) 下載。 
	
##按鈕的儲存庫考量 {: #button-repo} 

針對您將用於「部署至 Bluemix」按鈕中的專案儲存庫，請檢閱下列考量事項。 

<ul>
<li><code>manifest.yml</code> 不一定要在您的儲存庫中。不過，如果您的應用程式需要其他服務才能執行，則必須提供用來宣告那些服務的資訊清單檔。  

您可以利用資訊清單檔指定： 
    <ul>
    <li>唯一應用程式名稱。</li>  
    <li>宣告的服務：資訊清單延伸規格，可建立或尋找預期要在部署應用程式之前設定的必要或選用服務，例如資料快取服務。您可以使用 <a href="https://github.com/cloudfoundry/cli/releases">CF 指令行介面</a>來執行 <code>cf marketplace</code> 指令，或是瀏覽 <a href="https://console.ng.bluemix.net/?ssoLogout=true&cm_mmc=developerWorks-*-dWdevcenter-*-devops-services-_-lp#/store">{{site.data.keyword.Bluemix_notm}} 型錄</a>，以尋找合格的 {{site.data.keyword.Bluemix_notm}} 服務、標籤和方案清單。    
    <strong>附註：</strong>宣告的服務是標準 Cloud Foundry 資訊清單格式的 IBM 延伸規格。此延伸規格可能會隨著該特性的發展與改進，在未來的版本中修訂。<a href="http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#minimal-manifest" target="_blank">瞭解如何建立 <code>manifest.yml</code> 檔案。</a>  
<pre class="codeblock">
	---
    #Template manifest.yml

  declared-services:
    &lt;`arbitrary_service_instance_name`&gt;:  # [required]
      label: &lt;`actual_service_name`&gt; # [required] The actual service name from market place
      plan: Shared # [optional] If provided, used to fetch the declared service. Otherwise, defaults to 'Free' or 'free'.
  applications:
  - services
    - &lt;`arbitrary_service_instance_name`&gt;
    name: &lt;`appname`&gt;
    host: &lt;`apphostname`&gt;
</pre>

<pre class="codeblock">
	---
    #Example manifest.yml

  declared-services: 
      sample-java-cloudant-cloudantNoSQLDB: 
        label: cloudantNoSQLDB 
        plan: Shared 
  applications:
  - services
    - sample-java-cloudant-cloudantNoSQLDB
    name: My app
    host: myapp
</pre>
   </li>
   </ul>
	<li> 如果在部署應用程式之前必須建置儲存庫，則在部署之前會觸發自動建置儲存庫中的程式碼。在儲存庫的根目錄中偵測到建置 Script 檔時，即會進行自動建置。
	
	支援的建置器： 
	    <ul>
		<li> <a href="http://ant.apache.org/manual/using.html" target="_blank">Ant：</a>/<code>build.xml</code>，會將輸出建置到 <code>./output/</code> 資料夾</li>
		<li> <a href="http://docs.cloudfoundry.org/buildpacks/java/build-tool-int.html#gradle" target="_blank">Gradle：</a><code>/build.gradle</code>，會將輸出建置到 <code>. </code> 資料夾 </i>
		<li> <a href="http://gruntjs.com/getting-started#the-gruntfile" target="_blank">Grunt：</a><code>/Gruntfile.js</code>，會將輸出建置到 <code>.</code> 資料夾</li>
		<li> <a href="http://docs.cloudfoundry.org/buildpacks/java/build-tool-int.html#maven" target="_blank">Maven：</a><code>/pom.xml</code>，會將輸出建置到 <code>./target/</code> 資料夾</li>
	   </ul>
	</li>	
	<li>若要配置專案的管線，請在 <code>.bluemix</code> 目錄中併入 <code>pipeline.yml</code> 檔案。您可以手動建立 <code>pipeline.yml</code> 檔案，或從現有 DevOps Services 專案中產生檔案。若要從 {{site.data.keyword.jazzhub_short}} 專案中建立 pipeline.yml 檔案並將它新增至儲存庫中，請完成下列步驟。
<ol>
<li>在瀏覽器中開啟您的 DevOps Services 專案，然後按一下<b>建置並部署</b>。</li>
<li>使用建置及部署工作配置您的管線。</li>
<li>在瀏覽器中，將 <code>/yaml</code> 新增至專案管線 URL，然後按 Enter 鍵。
<br>範例：<code>https://hub.jazz.net/pipeline/<owner>/<project_name>/yaml</code></li>
<li>儲存產生的 <code>pipeline.yml</code> 檔案。</li>
<li>在專案的根目錄中，建立 <code>.bluemix</code> 目錄。</li>
<li>將 <code>pipeline.yml</code> 檔案上傳至 <code>.bluemix</code> 儲存庫。</li>
</ol> </li>
	<li>如果您利用 <stong>IBM Containers</strong> 在儲存器中部署應用程式，則必須在儲存庫的根目錄中併入 Dockerfile，以及在 <code>.bluemix</code> 目錄中併入 <code>pipeline.yml</code> 檔案。
	<ul>
	    <li> 若要進一步瞭解如何建立 Dockerfile，<a href="https://docs.docker.com/reference/builder/" target="_blank">請參閱 Docker 文件</a>。</li>
	    <li>您可以手動建立 <code>pipeline.yml</code> 檔案，或從現有 DevOps Services 專案中產生檔案。若要手動建立專用於儲存器的 <code>pipeline.yml</code>，<a href="https://github.com/Puquios/" target="_blank">請參閱 GitHub 中的範例</a>。</li>
        </ul>

 </li>
 </ul>
</ul>

如需疑難排解說明，請參閱[「部署至 Bluemix」按鈕未部署應用程式](../troubleshoot/index.html#deploytobluemixbuttondoesntdeployanapp){:new_window}。	
