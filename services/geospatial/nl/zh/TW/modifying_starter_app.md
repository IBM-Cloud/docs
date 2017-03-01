---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#將入門範本應用程式修改至 {{site.data.keyword.Bluemix_short}}
{: #modifying_starter_app}

您可以修改入門範本應用程式，然後將它重新部署到 {{site.data.keyword.Bluemix_short}} 以查看結果。
{:shortdesc}


簡單的修改是提高或移除入門範本應用程式中的事件限制，讓它可以執行更久。

1. 在文字編輯器或開發環境中開啟 app.js。
2. 變更 eventTarget 變數，若要完全移除事件限制則請刪除此行。
	 <pre><code>var eventTarget = 100;</code></pre>
3. 如果您想要移除事件限制，則也需要刪除下列 if 陳述式：
	 <pre><code>  
	if (eventCount >= eventTarget) {
		    status_step[3] = "Completed";
		    console.log("\nTarget event count has been reached.  Geospatial Analytics service will be stopped.\n");
		    callback(null, null);
		    } 
	</code></pre> 
4. 使用 cf push 指令，將已修改的應用程式重新部署到 {{site.data.keyword.Bluemix_short}}。
	 <pre><code>  
	cf push myapp
	</code></pre>
5. 在瀏覽器輸入應用程式的 URL 或「路徑」，或是從 {{site.data.keyword.Bluemix_short}} 儀表板啟動它。
