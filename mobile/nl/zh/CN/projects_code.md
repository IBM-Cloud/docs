---

copyright:
  years: 2016, 2017
lastupdated: "2016-12-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 使用代码入门模板创建项目
{: #projects_code}

您可以使用{{site.data.keyword.Bluemix}} Mobile 仪表板中的[代码入门模板](starters.html#Code_Starter)，在 {{site.data.keyword.Bluemix_notm}} 环境中创建项目。此过程不适用于使用“UI 入门模板”的项目。请参阅[使用 UI 入门模板创建项目](projects_ui.html)，以获取适用于“UI 入门模板”的指示信息。
{:shortdesc}

完成以下步骤，以使用“代码入门模板”创建项目：

1. 在 {{site.data.keyword.Bluemix_notm}} 中创建新 Mobile 仪表板项目。

 选择 Mobile 目录后，从*入门*选项卡开始。有描述说明您可以使用的已选入门模板，以及创建项目的不同方式，具体取决于您需要多少帮助。如果您只是想要开始使用，请选择**创建项目**。

 如果您已具有项目，那么您可以从选择*项目*选项卡开始。从 {{site.data.keyword.Bluemix_notm}} Mobile 仪表板的**项目**视图中，您可以选择要使用的项目、使用项目的*操作*来删除项目或下载项目的代码，或者创建新项目。

	1. 在 {{site.data.keyword.Bluemix_notm}} 控制台上，在您使用 {{site.data.keyword.Bluemix_notm}} 徽标旁边的三条线展开菜单之后，选择 **Mobile**。 
	
	2. 选择**创建项目**。 

	  或者，您也可以选择**项目**选项卡，以查看已在移动环境中的项目，并通过单击**创建项目**，创建新项目。

	3. 单击**代码入门模板**。  

	4. 选择与您要创建的应用程序类型最匹配的入门模板，然后选择**创建项目**。有 **UI 入门模板**和**代码入门模板**。有关入门模板以及如何使用它们的更多信息，请参阅[入门模板](starters.html)。 
	
	5. 输入项目的名称并选择**创建**。
	
2. 在**项目概述**屏幕上进行选择。**项目概述**屏幕显示项目的相关信息，以及您可以添加到项目的可选服务，如 {{site.data.keyword.mobilepushshort}} 和 Authentication。  

	1. 可选：选择**添加**以向项目添加其中一个所列服务。编辑服务的**服务名称**，然后单击**创建**。当您向项目添加服务时，会链接到该服务的 {{site.data.keyword.Bluemix_notm}} 页面。通过提供服务所需的信息来配置该服务。
	
	2. 可选：针对您要添加到项目中的任何其他功能，重复步骤 *a*。

3. 可选：选择**数据**以连接 Cloudant NoSQL 数据库或 Object Storage 服务。
	1. 单击**创建**以配置新的 Cloudant NoSQL DB 或 Object Storage 服务。
	
	注：如果您创建 Object Storage 服务的实例，那么系统会将您引导至项目外，以创建该实例并添加所需的凭证。创建实例之后导航回项目，并选择**添加现有项**以将服务与项目相连接。
	
	如果您已经具有未连接到其他项目的现有实例，而您想要连接到此项目，请选择**添加现有项**。 
	
	2. 验证您要连接的 Cloudant NoSQL DB 或 Object Storage 服务的磁贴是否显示在项目的“数据”选项卡上。

4.  下载项目并完成设置。

    1. 单击**下载代码**并选择首选语言。
   
    2. 解压缩归档文件，并在 Markdown 查看器中查看 `README.md` 文件，以完成设置。

5.  试用您的应用程序！ 


