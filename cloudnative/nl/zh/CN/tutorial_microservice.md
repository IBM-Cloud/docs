---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 微服务基本入门模板端到端教程
{: #tutorial}

以下端到端教程将引导您完成通过“微服务基本入门模板”创建项目的步骤（包括必须安装的工具）以及接下来运行项目代码的步骤。

## 安装开发者工具
{: #dev_tools}

请确保您已安装[必备开发者工具 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](get_code.html#prereq-dev-tools){: new_window}。


## 使用 {{site.data.keyword.dev_console}} 创建项目
{: #create-devex}

1. 在 {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} 中创建项目。

	1. 从 {{site.data.keyword.dev_console}} 中的**入门**页面，单击**创建项目**。

		或者，您可以从**项目**页面单击**创建项目**。

	2. 选择**微服务**并单击**下一步**。

	3. 选择**基本**并单击**下一步**。

	4. 输入项目名称。对于本教程，请使用 `MicroserviceProject`。   

	5. 输入主机名。对于本教程，请使用 `devhost` 
   
	6. 单击**创建**。

2. 可选：添加数据功能。

	1. 在**项目概述**页面上，针对**数据**单击**查看**。

      或者，可在**功能 > 数据**页面上选择**创建**或**添加现有项**。

   2. 输入服务名称并单击**创建**。

3. 生成项目代码。

	1. 单击**项目概述**页面上的**获取代码**，以选择语言。
   
		或者，您可以在**代码**页面上单击。
      
	2. 单击**生成代码**。
   
	3. 项目代码完成生成后，单击**下载代码**以下载项目归档。

4. 可选：[更新项目](project_overview_page.html#update_language)以生成新语言。


## 使用 {{site.data.keyword.dev_cli_notm}} 创建项目
{: #create-cli}

1. 确保您已安装 [{{site.data.keyword.dev_cli_short}}](dev_cli.html)。

2. 在“终端”提示符处，浏览到所选的本地目录并运行以下命令。
  
	```
	bx dev create
	```
	{: codeblock}

3. 在系统提示时提供以下值：

	* 选择模式：4（“微服务”）
	* 选择入门模板：1（“基本”）
	* 选择平台：3 (Java)
	* 输入项目的名称：`MicroserviceProjectCLI`

4. 如果要向项目添加服务，请在问题提示处输入 `y` 并回答其余问题。

5. 成功保存 `MicroserviceProjectCLI` 后，浏览到 `MicroserviceProjectCLI` 文件夹。

6. 此时，可添加您自己的代码，构建或运行项目。
 
 
## 使用 {{site.data.keyword.dev_cli_notm}} 运行项目
{: #running-dev-plugin}

1. 要在当前项目目录中构建项目，请输入以下命令：

	```
	bx dev build
	```     
	{: codeblock}

2. 要在当前项目目录中构建和运行项目，请输入以下命令：

	```
	bx dev run
	```
	{: codeblock}	

3. 您可以使用 curl 在服务器上访问应用程序：

	```
	curl http://localhost:8080	
	```
	{: codeblock}
