---



copyright:

  years: 2015, 2016



---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# 使用 {{site.data.keyword.deliverypipeline}} {: #pipeline-working}  

上次更新时间：2016 年 11 月 18 日
{: .last-updated}

要自动执行构建并部署到 {{site.data.keyword.Bluemix}}，请使用 {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}。
{: shortdesc}

使用 {{site.data.keyword.deliverypipeline}}，可以从多个构建类型中进行选择。您提供构建脚本，{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} 运行该脚本；无需设置构建系统。然后，只需单击一下，即可将应用程序自动部署到一个或多个 {{site.data.keyword.Bluemix_notm}} 空间、公共 Cloud Foundry 服务器或 IBM Containers for {{site.data.keyword.Bluemix_notm}} 上的 Docker 容器。  

构建作业会对 Git 存储库中的应用程序源代码进行编译和打包。构建作业会生成可部署的工件，如 WAR 文件或 IBM Containers 的 Docker 容器。此外，还可以在构建内自动运行单元测试。您可以设置构建作业，以便每次推送落实时，都触发构建。

部署作业从构建作业中获取输出，并将其部署到 IBM Containers 或 Cloud Foundry 服务器，如 {{site.data.keyword.Bluemix_notm}}。  

可以部署到一个或多个区域和服务。例如，您可以设置 {{site.data.keyword.deliverypipeline}} 以使用一个或多个服务，在一个区域中对服务测试，然后将服务部署到多个区域中的生产环境。有关更多信息，请参阅[区域](/docs/overview/whatisbluemix.html#ov_intro_reg)。

创建管道的方法有几种，包括将管道添加到现有应用程序以及在没有现有应用程序的情况下创建管道。如果组织中还没有 {{site.data.keyword.deliverypipeline}} 服务，那么您可以转至目录，单击 {{site.data.keyword.deliverypipeline}}，然后单击“创建”。

完成以下步骤，为现有应用程序设置 {{site.data.keyword.deliverypipeline}}：    

1. 在 {{site.data.keyword.Bluemix_notm}} 应用程序“仪表板”上，单击您的应用程序。
1. 从 {{site.data.keyword.Bluemix_notm}} 菜单栏上的“汉堡包”菜单中，单击**服务**，然后单击 **DevOps**。
1. 单击**管道**，然后单击**创建管道**。

要[创建管道（在新窗口中打开链接）](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window}（管道已配置为部署 Cloud Foundry 应用程序），请执行以下步骤：    

1. 单击 **Cloud Foundry**。  
1. 如果要对管道使用其他名称，请更改其缺省名称。 
1. 如果要对应用程序使用其他名称，请更改其缺省名称。这是管道部署到的应用程序的名称。 
1. 如果没有工具链，那么将为您创建具有缺省名称的工具链。如果要对工具链使用其他名称，请更改其名称。使用工具链，您可以通过与其他工具和服务相集成来扩展管道的功能。

 **提示**：管道和工具链属于组织。如果您属于具有工具链的组织，那么即便这些工具链不是您创建的，您也仍可以使用。
 
1. 选择要使用的工具链，或输入要创建的新工具链的名称。
1. 提供 GitHub 存储库的位置。

 **提示**：如果您未授权 {{site.data.keyword.Bluemix_notm}} 访问 GitHub，那么系统将提示您单击**授权**，以转至 GitHub Web 站点。如果您没有活动 GitHub 会话，那么系统会提示您登录。单击**授权应用程序**，以允许 {{site.data.keyword.Bluemix_notm}} 访问 GitHub 帐户。如果您具有活动 GitHub 会话但最近未输入过密码，那么系统可能会提示您输入 GitHub 密码以进行确认。

   * 如果您具有 GitHub 存储库且想要使用该存储库，那么对于存储库类型，请选择**链接**。搜索该存储库的位置，或者从可用存储库列表中选择该存储库。
   
   * 如果要创建空的 GitHub 存储库，那么对于存储库类型，请选择**新建**。输入存储库的名称。
   
   * 如果要创建 GitHub 存储库的克隆，那么对于存储库类型，请选择**复制**。搜索该存储库的位置，或者从可用存储库列表中选择该存储库。
   
   * 如果要派生 GitHub 存储库以便您可以通过拉出请求来提供更改，请选择**派生**。搜索该存储库的位置，或者从可用存储库列表中选择该存储库。
 
1. 单击**创建**。这将创建和配置管道，并将其显示在工具链的“概述”页面上。
 ![“管道”磁贴](images/cd_pipeline.png)

要创建不包含任何预配置阶段的[空管道（在新窗口中打开链接）](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window}，请执行以下操作：

1. 单击**定制**。
1. 如果要对管道使用其他名称，请更改其缺省名称。 
1. 如果没有工具链，那么将为您创建具有缺省名称的工具链。如果要对工具链使用其他名称，请更改其名称。使用工具链，您可以通过与其他工具和服务相集成来扩展管道的功能。
1. 选择要使用的工具链，或输入要创建的新工具链的名称。
1. 单击**创建**。这将创建空管道，并将其表示为工具链“概述”页面上的磁贴。

通过 {{site.data.keyword.deliverypipeline}} 磁贴，可更改配置，检查构建、已部署应用程序和最近部署的状态，查看最新日志和部署详细信息，也可以删除管道。  

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
