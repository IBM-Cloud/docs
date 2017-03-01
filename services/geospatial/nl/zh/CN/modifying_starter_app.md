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

#修改入门模板应用程序并应用于 {{site.data.keyword.Bluemix_short}}
{: #modifying_starter_app}

您可以修改入门模板应用程序，然后将其重新部署至 {{site.data.keyword.Bluemix_short}} 以查看结果。
{:shortdesc}


简单修改是在入门模板应用程序中提高或除去事件限制，以便其运行更长时间。

1. 在文本编辑器或开发环境中打开 app.js。
2. 更改 eventTarget 变量，或者删除此行，以完全除去事件限制。<pre><code>var eventTarget = 100;</code></pre>
3. 如果要除去事件限制，还需要删除以下 if 语句：<pre><code>  
if (eventCount >= eventTarget) {
status_step[3] = "Completed";
		    console.log("\nTarget event count has been reached.  Geospatial Analytics service will be stopped.\n");
callback(null, null);
		    } 
	</code></pre> 
4. 使用 cf push 命令将已修改的应用程序重新部署到 {{site.data.keyword.Bluemix_short}}。<pre><code>  
	cf push myapp
	</code></pre>
5. 在浏览器中输入应用程序的 URL 或“路径”，或者从 {{site.data.keyword.Bluemix_short}} 仪表板启动。
