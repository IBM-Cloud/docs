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

# Web 基本入门模板端到端教程
{: #tutorial}

以下端到端教程将引导您完成通过“Web 基本入门模板”创建项目的步骤（包括必须安装的工具）以及接下来运行项目代码的步骤。

## 安装开发者工具
{: #dev_tools}

请确保您已安装[必备开发者工具 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](get_code.html#prereq-dev-tools){: new_window}。


## 使用 {{site.data.keyword.dev_console}} 创建项目
{: #create-devex}

1. 在 {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} 中创建项目。

	1. 从 {{site.data.keyword.dev_console}} 中的**入门**页面，单击**创建项目**。

		或者，您可以从**项目**页面单击**创建项目**。

	2. 选择 **Web 应用程序**并单击**下一步**。

	3. 选择**基本 Web** 并单击**下一步**。

	4. 输入项目名称。对于本教程，请使用 `WebBasicProject`。   

	5. 输入主机名。对于本教程，请使用 `devhost` 

	6. 选择语言平台。对于本教程，请使用 `Swift`。
   
	7. 单击**创建**。

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

	* 选择模式：1 (Web)
	* 选择入门模板：1（“基本 Web”）
	* 选择语言：2 (Swift)
	* 输入项目的名称：`WebBasicProjectCLI`
	* 输入项目的主机名：`myhost`

4. 如果要向项目添加服务，请在问题提示处输入 `y` 并回答其余问题。

5. 成功保存 `WebBasicProjectCLI` 项目后，浏览到 `WebBasicProjectCLI` 文件夹。

6. 添加您自己的代码，构建项目或运行项目。
 
	1. 使用以下命令构建项目：
   
		```
 		bx dev build
 		```     
		{: codeblock}

	2. 使用以下命令运行项目：
 
		```
		bx dev run
		```
		{: codeblock}


## 运行 Web 项目
{: #run}

### 本地
{: #local notoc}

1. 安装节点依赖关系：

  ```
  npm install
  ```
  {: codeblock}

2. 将前端代码绑定到模块：

  ```
  node_modules/.bin/gulp
  ```
  {: codeblock}

3. 编译服务器：

  ```
  swift build
  ```
  {: codeblock}

4. 运行应用程序：

  ```
  .build/debug/WebBasicProjectCLI
  ```
  {: codeblock}

5. 在浏览器中打开 `http://localhost:8080`。


### 使用 {{site.data.keyword.dev_cli_short}}
{: #dev notoc}

1. 安装节点依赖关系：

  ```
  npm install
  ```
  {: codeblock}

2. 将前端代码绑定到模块：

  ```
  gulp
  ```
  {: codeblock}

3. 运行编译：

  ```
  bx dev run
  ```
  {: codeblock}

4. 在浏览器中打开 `http://localhost:8080`。


## 在 Xcode 中运行项目
{: #Xcode}

1. 创建 Xcode 项目。

	需要先使用 Swift 软件包管理器构建 Xcode 项目，然后才能使用 Xcode 进行开发。
	
	```
	swift project generate-xcodeproj
	```
	{: codeblock}

2. 将活动目标更改为可执行对象：

	然后，在 Xcode 中打开项目，确保活动目标可执行。您可以在单击下拉菜单时按住选项键，以选择所需的活动可执行对象。

3. 按**运行**。

4. 在浏览器中打开 `http://localhost:8080`。

