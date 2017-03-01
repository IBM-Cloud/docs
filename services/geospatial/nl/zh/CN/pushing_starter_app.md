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

#将入门模板应用程序推送至 {{site.data.keyword.Bluemix_short}}
{: #pushing_starter_app}


 
部署入门模板应用程序并快速了解如何使用 {{site.data.keyword.geospatialshort_Geospatial}} 服务：
{:shortdesc}

1. 如果尚未完成，请[安装 cf 命令行工具](docs/starters/install_cli.html)。
2. [获取代码](https://hub.jazz.net/project/streamscloud/geo-starter/overview)：{{site.data.keyword.geospatialshort_Geospatial}} 入门模板应用程序。 
3. 重命名包含应用程序文件的目录以匹配在 {{site.data.keyword.Bluemix_short}} 中为应用程序指定的名称。例如，如果应用程序的名称为 myapp，那么将目录重命名为 myapp。
4. 在命令行上，切换到重命名的目录。
<pre><code>cd myapp</code></pre>
5. 连接到 {{site.data.keyword.Bluemix_short}}：
<pre><code>cf api https://api.DomainName</code></pre>
6. 登录到 {{site.data.keyword.Bluemix_short}}，然后在提示时设置目标组织并部署应用程序。
<pre><code>
cf logincf push myapp
</code></pre>

##接下来执行的操作

* 转至可从 {{site.data.keyword.Bluemix_short}} 仪表板访问的应用程序概述页面，以验证应用程序已成功启动。
* 启动应用程序，以在浏览器中进行查看。可以在应用程序概述页面上找到应用程序的 URL（或“路径”）。样本应用程序的网页显示有关应用程序代码中 REST API 调用的状态和 {{site.data.keyword.geospatialshort_Geospatial}} 检测到的事件的信息。
