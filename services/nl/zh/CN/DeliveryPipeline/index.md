{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

#{{site.data.keyword.deliverypipeline}} 入门
{: #delivery-pipeline}  

*上次更新时间：2016 年 1 月 21 日*

要自动执行构建并部署到 {{site.data.keyword.Bluemix}}，请使用 IBM Continuous {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}（{{site.data.keyword.deliverypipeline}} 服务）。
{: shortdesc} 

在云中开发应用程序时，可以从多个构建类型中进行选择。您提供构建脚本，{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} 运行该脚本；无需设置构建系统。然后，只需单击一下，即可将应用程序自动部署到一个或多个 {{site.data.keyword.Bluemix_notm}} 空间、公共 Cloud Foundry 服务器或 IBM Containers for {{site.data.keyword.Bluemix_notm}} 上的 Docker 容器。  

构建作业会对 Git 或 Jazz 源代码控制管理 (SCM) 存储库中的应用程序源代码进行编译和打包。构建作业会生成可部署的工件，如 WAR 文件或 IBM Containers 的 Docker 容器。此外，还可以在构建内自动运行单元测试。每次源代码更改时，都将触发构建。  

部署作业从构建作业中获取输出，并将其部署到 IBM Containers 或 Cloud Foundry 服务器，如 {{site.data.keyword.Bluemix_notm}}。  

可以部署到一个或多个区域和服务。例如，您可以设置 {{site.data.keyword.deliverypipeline}} 服务，以便在一个区域中测试使用了 IBM Containers 的开发工件，并将其部署到多个区域中的生产环境。有关更多信息，请参阅[区域](../../overview/index.html#ov_intro__reg)。

1. 登录到 {{site.data.keyword.Bluemix_notm}}，然后为您的应用程序选择组织和空间。
1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”上，单击**创建应用程序**。
1. 选择 Web 或移动应用程序模板，选择入门模板，然后单击**继续**。为您的应用程序命名，然后单击**完成**。  
1. 在“开始编码”页面上，向下滚动并单击**查看应用程序概述**。  
1. 在 {{site.data.keyword.Bluemix_notm}} 应用程序“仪表板”上，通过单击**添加 GIT** 为应用程序创建 Git 托管的项目。确保已选中**使用入门模板应用程序包填充存储库并启用 {{site.data.keyword.deliverypipeline}}（构建和部署）**复选框，然后单击**继续**。   
1. 在创建 Git 存储库之后，单击**关闭**。“添加	GIT”链接会替换为“编辑代码”链接和您的 Git URL。  
1. 将 {{site.data.keyword.deliverypipeline}} 服务添加到一个或多个关联空间。添加此服务后，可以在 {{site.data.keyword.Bluemix_notm}} 空间中创建多阶段部署管道，方法是配置并运行包含构建、测试和部署作业的阶段。
    1. 在 {{site.data.keyword.Bluemix_notm}} 应用程序“仪表板”上，单击**添加服务或 API**。对于类别，请选中 **DevOps** 复选框，然后单击目录中的 **Delivery Pipeline**。
    2. 选择计划，然后单击**创建**。这将打开 {{site.data.keyword.deliverypipeline}}“仪表板”，其中显示先前创建的应用程序。     
  
在 {{site.data.keyword.deliverypipeline}}“仪表板”上，可以查看 {{site.data.keyword.jazzhub_short}} 项目及其状态。您可以检查构建、已部署应用程序和最近部署的状态，也可以查看最新日志和部署详细信息。  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks">
<h2 class="topictitle2" id="d68e338">相关链接</h2>
<aside>
<div class="linklist" id="general"><h3 class="linklistlabel">相关链接</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="（在新选项卡或窗口中打开）">{{site.data.keyword.Bluemix_notm}} 先决条件</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">教程和样本</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="（在新选项卡或窗口中打开）">克隆、编辑和部署应用程序</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="（在新选项卡或窗口中打开）">开发和部署 Node.js 应用程序</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="（在新选项卡或窗口中）">开发和部署 Java 应用程序</a></li>
<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/delivery%20pipeline%20service" rel="external" title="（在新选项卡或窗口中）">developerWorks: {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.deliverypipeline}} service</a></li>
</ul>
</div>
</aside>
</article>
