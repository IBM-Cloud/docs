---



copyright:

  years: 2015, 2016



---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# {{site.data.keyword.deliverypipeline}} 入门 {: #delivery-pipeline}  

上次更新时间：2016 年 9 月 15 日
{: .last-updated}

要自动执行构建并部署到 {{site.data.keyword.Bluemix}}，请使用 IBM Continuous {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}。
{: shortdesc}

此信息适用于 {{site.data.keyword.deliverypipeline}} 和 {{site.data.keyword.deliverypipeline}} Next。

使用 {{site.data.keyword.deliverypipeline}} 服务，可以从多个构建类型中进行选择。您提供构建脚本，{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} 运行该脚本；无需设置构建系统。然后，只需单击一下，即可将应用程序自动部署到一个或多个 {{site.data.keyword.Bluemix_notm}} 空间、公共 Cloud Foundry 服务器或 IBM Containers for {{site.data.keyword.Bluemix_notm}} 上的 Docker 容器。  

构建作业会对 Git 或 Jazz 源代码控制管理 (SCM) 存储库中的应用程序源代码进行编译和打包。构建作业会生成可部署的工件，如 WAR 文件或 IBM Containers 的 Docker 容器。此外，还可以在构建内自动运行单元测试。每次源代码更改时，都将触发构建。

部署作业从构建作业中获取输出，并将其部署到 IBM Containers 或 Cloud Foundry 服务器，如 {{site.data.keyword.Bluemix_notm}}。  

可以部署到一个或多个区域和服务。例如，您可以设置 {{site.data.keyword.deliverypipeline}} 服务，以便在一个区域中测试使用了 IBM Containers 的开发工件，并将其部署到多个区域中的生产环境。有关更多信息，请参阅[区域](../../overview/index.html#ov_intro__reg)。

创建管道的方法有几种，包括将管道添加到现有应用程序以及在没有现有应用程序的情况下创建管道。如果组织中还没有 {{site.data.keyword.deliverypipeline}} 服务，那么您可以转至该目录，单击 {{site.data.keyword.deliverypipeline}} 或 {{site.data.keyword.deliverypipeline}} Next，然后单击“创建”。

完成以下步骤，为现有应用程序设置 {{site.data.keyword.deliverypipeline}}：    

1. 在 {{site.data.keyword.Bluemix_notm}} 应用程序“仪表板”上“概述”选项卡的**持续交付**下，通过单击**添加 Git 存储库和管道**或**添加 Git**（取决于上下文），为应用程序创建 Git 托管的项目。
1. 确保已选中**使用入门模板应用程序包填充存储库并启用构建和部署管道**复选框，然后单击**继续**。您可能需要验证电子邮件地址才能继续。  
1. 在创建 Git 存储库之后，单击**关闭**。“添加	Git”按钮替换为“编辑代码”按钮和您的 Git URL。  
1. 要打开管道，请单击**编辑代码**，然后单击**构建和部署**。要第一次运行管道，请将更改推送至 Git 存储库。

添加此服务后，可以在 {{site.data.keyword.Bluemix_notm}} 空间中创建多阶段部署管道，方法是配置并运行包含构建、测试和部署作业的阶段。在 {{site.data.keyword.deliverypipeline}}“仪表板”上，可以查看 {{site.data.keyword.jazzhub_short}} 项目及其状态。您可以检查构建、已部署应用程序和最近部署的状态，也可以查看最新日志和部署详细信息。  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks" role="article">
<h2 class="topictitle2" id="d68e338">相关链接</h2>
<aside role="complementary" aria-labelledby="related_links">
<div class="linklist" id="general"><h3 class="linklistlabel" id="related_links">相关链接</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="（在新选项卡或窗口中打开）">{{site.data.keyword.Bluemix_notm}} 先决条件</a></li>
<li><img src="./sout.gif" alt=""><a href="https://www.ibm.com/devops/method/content/deliver/practice_delivery_pipeline/" rel="external" title="（在新选项卡或窗口中打开）">IBM Bluemix Garage 方法：Delivery Pipeline</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">教程和样本</h3>
<ul>

<!--
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="(Opens in a new tab or window)">Clone, edit, and deploy an app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Node.js app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Java app</a></li>
-->

<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/delivery%20pipeline%20service" rel="external" title="（在新选项卡或窗口中）">developerWorks: {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.deliverypipeline}} service</a></li>
</ul>
</div>
</aside>
</article>
