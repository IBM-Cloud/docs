---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#內嵌部署至 {{site.data.keyword.Bluemix_notm}} 的 iFrame 流程 {: #embed-d2bm-iframe} 

*前次更新：2015 年 12 月 8 日* 

您可以將「部署至 {{site.data.keyword.Bluemix_notm}}」的流程作為 iFrame 內容，內嵌至支援標記的許多種內容。例如，您可以將 iFrame 內嵌至 Readme 檔、部落格、文章及網頁中。 

{: shortdesc} 

iFrame 流程適用於您維持公司品牌之時。當有人按一下您的內嵌 iFrame 時，他們會停留在您的內容中，而非重新導向至 bluemix.net 網站。如果您不在意公司品牌，則可以在內容中插入標準的[部署至 {{site.data.keyword.Bluemix_notm}} 按鈕](../develop/deploy_button.html)，而非插入 iFrame。 

##iFrame 流程中的步驟 {: #iframe-steps} 

1. 如果您沒有作用中的 {{site.data.keyword.Bluemix_notm}} 帳戶，請建立一個試用帳戶。 

2. 您可以選取地區、組織、空間及應用程式名稱。建議的應用程式名稱是依據前一個應用程式名稱、您的使用者名稱及時間所建構。 

3. 原始的公用 Git 儲存庫的主要分支會複製到新的專用 {{site.data.keyword.jazzhub_short}} 專案，並具有新的 Git 儲存庫。 

4. 如果應用程式需要建置檔，則會自動偵測建置檔，並建置應用程式。 

5. 應用程式會部署至您的 {{site.data.keyword.Bluemix_notm}} 組織。 

##iFrame 流程的範例 {: #iframe-example} 

<p>
<a class="xref" href="http://d2bm-iframe-sample.ng.bluemix.net/" target="_blank" title="（在新分頁或視窗中開啟）">IBM Bluemix D2BM iFrame 範例</a>提供公用 Git 儲存庫的 iFrame 流程範例。<div class="image"><img class="image" src="images/d2bm_iframe_sample2.png" alt="「部署至 Bluemix」iFrame 流程範例" /></div>
</p> 

<p>
若要檢視此範例的原始檔，請按一下<a class="xref" href="https://hub.jazz.net/project/idsorg/d2bm-iframe-sample/overview" target="_blank" title="（在新分頁或視窗中開啟）">原始檔</a>。
</p>

##內嵌 iFrame 流程 {: #embed-iframe}  

<ol>
<li>從 <a href="https://bluemix.net/deploy/embed.js" target="_blank">https://bluemix.net/deploy/embed.js</a> 中載入 JavaScript 公用程式。此公用程式會依賴 jQuery，並透過將下列 Script 標籤新增至您的文件中進行載入：
<pre class="pre">
<code>&lt;script type="text/javascript" src="https://bluemix.net/deploy/embed.js"&gt;&lt;/script&gt;</code>
</pre>
</li>
<li> 利用下列引數來實例化 <code>DeployToBluemixIFrame</code> 建構子：

<dl class="parml">
<dt class="pt dlterm">domNodeId</dt>
<dd class="pd">domNode 的 ID，您要在該處將 iFrame 插入內容中。</dd>

<dt class="pt dlterm">callback</dt>
<dd class="pd">iFrame 流程已完成或發生錯誤時，即會呼叫這個引數。引數會回應結果。下列程式碼 Snippet 顯示成功的結果回呼：</dd>

<dt class="pt dlterm">args</dt>
<dd class="pd">此物件包含小組件的輸入參數。以下是可用參數：

<dl class="parml">

<dt class="pt dlterm">repository</dt>
<dd class="pd">Git 儲存庫，用作複製及部署的來源。這是必要值。</dd>
	
<dt class="pt dlterm">app_name</dt>
<dd class="pd">預設應用程式名稱，用作 iFrame 內 <strong>app_name</strong> 欄位中的指定值。這是選用值。</dd>
	
    
<dt class="pt dlterm">region_id</dt>
<dd class="pd">預設目標地區的 ID。例如：<code>ibm:yp:us-south</code>。這是選用值。</dd>
	
<dt class="pt dlterm">organization_guid</dt>
<dd class="pd">預設目標組織的 GUID。若要尋找此值，請按一下<strong>管理組織</strong> > <i>organization_name</i>。組織的 URL 包含該組識的 GUID。這是選用值。</dd>
	
<dt class="pt dlterm">space_guid</dt>
<dd class="pd">預設目標空間的 GUID。若要尋找此值，請按一下<strong>管理組織</strong> > <i>space_name</i>。空間的 URL 包含該空間的 GUID。這是選用值。</dd>
	
<dt class="pt dlterm">auto_login</dt>
<dd class="pd">指定 iFrame 是否自動讓使用者登入。預設值為 <code>true</code>。這是選用值。</dd>
	
<dt class="pt dlterm">width</dt>
<dd class="pd">iFrame 的寬度。這是選用值。預設值為 <code>620</code>。</dd>
	
<dt class="pt dlterm">height</dt>
<dd class="pd">iFrame 的高度。這是選用值。預設值為 <code>470</code>。</dd>
</dl>

</dd>
</dl>
</li>
</ol>  

**提示：**若要將與 iFrame 的互動減到最少，您可以預先填入 **app_name**、**region_id**、**organization_guid**、**space_guid** 及 **auto_login** 欄位。
