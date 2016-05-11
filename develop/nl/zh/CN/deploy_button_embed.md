---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#嵌入“部署到 {{site.data.keyword.Bluemix_notm}}”iFrame 流 {: #embed-d2bm-iframe} 

*上次更新时间：2015 年 12 月 8 日* 

您可以将“部署到 {{site.data.keyword.Bluemix_notm}}”流作为 iFrame 嵌入到支持标记的多种类型的内容中。例如，可以将 iFrame 嵌入到自述文件、博客、文章和网页中。 

{: shortdesc} 

希望保留公司标记时，iFrame 流会非常有用。用户单击嵌入的 iFrame 时，会停留在您的内容中，而不会重定向到 bluemix.net Web 站点。如果不涉及公司标记，那么可以将标准的[“部署到 {{site.data.keyword.Bluemix_notm}}”按钮](../develop/deploy_button.html)插入到您的内容中，而不使用 iFrame。 

##iFrame 流中的步骤 {: #iframe-steps} 

1. 如果您没有活动的 {{site.data.keyword.Bluemix_notm}} 帐户，请创建试用帐户。 

2. 可以选择区域、组织、空间和应用程序名称。建议的应用程序名称是从先前的应用程序名称、您的用户名和时间构建的。 

3. 会将原始公共 Git 存储库的主分支克隆到带有新 Git 存储库的专用 {{site.data.keyword.jazzhub_short}} 项目。 

4. 如果应用程序需要一个构建文件，那么会自动检测到该构建文件，并且会构建该应用程序。 

5. 应用程序将部署到您的 {{site.data.keyword.Bluemix_notm}} 组织。 

##iFrame 流的示例 {: #iframe-example} 

<p>
<a class="xref" href="http://d2bm-iframe-sample.ng.bluemix.net/" target="_blank" title="（在新选项卡或窗口中打开）">IBM Bluemix D2BM iFrame Sample</a> 提供了用于公共 Git 存储库的 iFrame 流示例。<div class="image"><img class="image" src="images/d2bm_iframe_sample2.png" alt="“部署到 Bluemix”iFrame 流样本" /></div>
</p> 

<p>
要查看此样本的源代码，请单击 <a class="xref" href="https://hub.jazz.net/project/idsorg/d2bm-iframe-sample/overview" target="_blank" title="（在新选项卡或窗口中打开）">source</a>。</p>

##嵌入 iFrame 流 {: #embed-iframe}  

<ol>
<li>从 <a href="https://bluemix.net/deploy/embed.js" target="_blank">https://bluemix.net/deploy/embed.js</a> 装入 JavaScript 实用程序。此实用程序依赖于 jQuery，并通过向文档添加以下脚本标记来装入：
<pre class="pre">
<code>&lt;script type="text/javascript" src="https://bluemix.net/deploy/embed.js"&gt;&lt;/script&gt;</code>
</pre>
</li>
<li> 使用以下自变量来实例化 <code>DeployToBluemixIFrame</code> 构造函数：<dl class="parml">
<dt class="pt dlterm">domNodeId</dt>
<dd class="pd">要将 iFrame 插入到内容中的 domNode 的标识。</dd>

<dt class="pt dlterm">callback</dt>
<dd class="pd">iFrame 流完成或者发生了错误时，将调用此自变量。此自变量会通过结果进行响应。以下代码片段显示了成功的结果回调：</dd>

<dt class="pt dlterm">args</dt>
<dd class="pd">包含窗口小部件的输入参数的对象。以下参数可用：<dl class="parml">

<dt class="pt dlterm">repository</dt>
<dd class="pd">要用作克隆和部署源的 Git 存储库。此值是必需的。</dd>
	
<dt class="pt dlterm">app_name</dt>
<dd class="pd">要用作 iFrame 内 <strong>app_name</strong> 字段中指定值的缺省应用程序名称。此值是可选的。</dd>
	
    
<dt class="pt dlterm">region_id</dt>
<dd class="pd">缺省目标区域的标识。例如：<code>ibm:yp:us-south</code>。此值是可选的。</dd>
	
<dt class="pt dlterm">organization_guid</dt>
<dd class="pd">缺省目标组织的 GUID。要找到此值，请单击<strong>管理组织</strong> > <i>organization_name</i>。组织的 URL 包含该组织的 GUID。此值是可选的。</dd>
	
<dt class="pt dlterm">space_guid</dt>
<dd class="pd">缺省目标空间的 GUID。要找到此值，请单击<strong>管理组织</strong> > <i>space_name</i>。空间的 URL 包含该空间的 GUID。此值是可选的。</dd>
	
<dt class="pt dlterm">auto_login</dt>
<dd class="pd">指定 iFrame 是否自动使用户登录。缺省值为 <code>true</code>。此值是可选的。</dd>
	
<dt class="pt dlterm">width</dt>
<dd class="pd">iFrame 的宽度。此值是可选的。缺省值为 <code>620</code>。</dd>
	
<dt class="pt dlterm">height</dt>
<dd class="pd">iFrame 的高度。此值是可选的。缺省值为 <code>470</code>。</dd>
</dl>

</dd>
</dl>
</li>
</ol>  

**提示：**要最大程度地减少与 iFrame 的交互，可以预填充 **app_name**、**region_id**、**organization_guid**、**space_guid** 和 **auto_login** 字段。
