---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# 使用 Eclipse Orion {{site.data.keyword.webide}} 编辑代码
{: #web_ide}

上次更新时间：2016 年 9 月 9 日
{: .last-updated}

Eclipse Orion {{site.data.keyword.webide}} 是基于浏览器的开发环境，可在其中针对 Web 进行开发。您可以借助内容辅助、代码完成和错误检查功能，在 JavaScript、HTML 和 CSS 中进行开发。{{site.data.keyword.webide}} 可使用几乎任何语言，并为大部分[文件类型（在新窗口中打开链接）](https://hub.jazz.net/docs/overview/#dev_support){: new_window}提供语法突出显示功能。源代码控制功能通过 Git 或 Jazz SCM 内置其中，因此您可以在本地部署代码并调试应用程序。
{:shortdesc}

最重要的是，{{site.data.keyword.webide}} 由 Web 提供支持。您无需进行任何安装、维护和扩展。您可以在具有因特网连接的任何地方进行开发。

## 设置编辑器
{: #editorsetup}

{{site.data.keyword.webide}} 可进行定制，因此您可以选择满足开发需要的颜色方案、技术工具和设置。要查看和修改设置，请从左侧菜单中，单击**设置**图标 <img class="inline" src="./images/webide_settings_icon.png"  alt="“设置”图标">。

如果在编辑时经常需要更改某些设置，您可以从编辑器右上角的**本地编辑器设置**图标 <img class="inline" src="./images/webide_local_settings_icon.png"  alt="“本地编辑器设置”图标"> 快速访问这些设置。

![本地编辑器设置](images/webide_local_editor_settings.png)

缺省情况下，始终显示编辑器样式和字体大小的设置。要在菜单中包含其他编辑器设置，请遵循以下步骤：

1. 单击**本地编辑器设置**图标 <img class="inline" src="./images/webide_local_settings_icon.png"  alt="“本地编辑器设置”图标">。

2. 单击**编辑器设置**。

3. 要在**本地编辑器设置**菜单中包含或排除某个设置，请单击该设置旁边的圆圈。

![编辑器设置切换](images/webide_editor_settings_toggle.png)


## 编辑代码
{: #editcode}

{{site.data.keyword.webide}} 包含两个主要部分。第一个部分是左侧的文件导航器，以树结构显示您的项目文件。从文件导航器中，可以创建、重命名、删除以及管理文件和文件夹。

**提示：**要将文件上传到文件导航器中，请将文件从您的计算机拖动到文件导航器中。

第二个部分是右侧的编辑器窗格。编辑器提供多种编码功能，包括内容辅助和语法验证。

![Web IDE](images/webide.png)

### 使用多个文件
1. 要同时使用两个文件，请单击编辑器顶部的**更改分割编辑器方式**图标 <img class="inline" src="./images/webide_split_editor_icon.png"  alt="“分割编辑器”图标">。
2. 从打开的菜单中，选择视图。

 选择视图之后，如果文件已在编辑器中打开，那么该文件将显示在两个编辑器视图中。

 要打开或更改其中一个编辑器视图中显示的文件，请执行以下操作：
 1. 将光标移至您要更改的编辑器视图中。
 2. 在文件导航器中，单击某个文件。

### 键盘快捷键
{{site.data.keyword.webide}} 中的大部分命令仅通过键盘快捷键即可访问。

要查看编辑器中的键盘快捷键列表，请按 Alt+Shift+?。如果使用的是 Mac OS，请按 Ctrl+Shift+?。

## 管理源代码
{: #sourcecontrol}

{{site.data.keyword.webide}} 与源代码管理工具相集成。要使用 Git 存储库，请单击 **Git 存储库**图标 <img class="inline" src="./images/webide_git_icon.png"  alt="“Git 存储库”图标">。有关更多信息，请参阅[使用 Git 进行源代码控制（在新窗口中打开链接）](https://hub.jazz.net/docs/git/){: new_window}。


## 从您的工作空间部署应用程序
{: #deploy}

1. 要部署应用程序，请从运行栏选择或[创建（在新窗口中打开链接）](https://hub.jazz.net/tutorials/livesync/#launch_configuration){: new_window}启动配置。
1. 单击“部署”图标 <img class="inline" src="./images/webide_deploy_button.png"  alt="“部署”图标">。这时将使用工作空间的当前内容以及启动配置中定义的环境来部署应用程序的实例。 
2. 部署应用程序之后，您可以使用运行栏停止、重新启动或调试应用程序，以及查看日志等等。
![运行栏](images/webide_runbar.png)

<!-- LH: I'm commenting out the following list because I think this information is obvious from the UI. I also updated the preceding sentence to mention a few things that you can do from the run bar.

 * Stop the app: <img  class="inline" src="./images/webide_stop_button.png"  alt="The stop icon">
 * Open the deployed app: <img class="inline" src="./images/webide_open_app_url.png"  alt="The open app URL icon">
 * View the logs of the deployed app: <img class="inline" src="./images/webide_view_logs.png"  alt="The view logs icon">
 * Open the app's Dashboard: <img  class="inline" src="./images/webide_open_dashboard.png"  alt="The open dashboard icon">
 * If you are developing a Node.js app, enable Live Edit mode: <img  class="inline"  src="./images/webide_enable_live_edit.png"  alt="The enable live edit slider">
 * With Live Edit mode enabled, restart the app quickly, without redeployment: <img  class="inline" src="./images/webide_live_edit_restart.png"  alt="The Live Edit restart icon">
 * With Live Edit mode enabled, access the debugger: <img  class="inline" src="./images/webide_debug_icon.png"  alt="The debug icon"> -->

 ## 在 {{site.data.keyword.webide}} 以外进行编辑
{: #editlocal}

要使用 {{site.data.keyword.webide}} 以外的编辑器，请设置 {{site.data.keyword.Bluemix_live}}，以便您可以在任何工具中直接使用项目文件。{{site.data.keyword.Bluemix_live_notm}} 是一种命令行应用程序，其将本地文件系统中的更改与 {{site.data.keyword.jazzhub}} 中的云工作空间同步。 

### 开始之前 

下载并安装 [{{site.data.keyword.Bluemix_live_notm}} 命令行界面（在新窗口中打开链接）](http://livesyncdownload.ng.bluemix.net){: new_window}。

### 将本地环境与 {{site.data.keyword.Bluemix_notm}} 同步
{: #edit_local_download}

1. 打开命令行窗口。
2. 登录到 {{site.data.keyword.Bluemix_notm}}：

	```
	bl login
	```
	{: pre}

3. 系统提示时，输入您的 IBM 标识和密码。
4. 查看您的 {{site.data.keyword.Bluemix_notm}} 项目列表： 

	```
	bl projects
	```
	{: pre}

4. 将本地环境与 {{site.data.keyword.Bluemix_notm}} 上的项目同步：

	```
	bl sync projectName
	```
	{: pre}

其中 `projectName` 是您的 {{site.data.keyword.Bluemix_notm}} 应用程序名称。

完成编辑后，请输入 `q` 以结束同步。

### 启用桌面同步功能以在本地编辑代码

“桌面同步”功能类似于命令行的“实时编辑”方式。您需要使用“桌面同步”功能来调试命令行。
1. 在另一个命令行窗口中，启用“桌面同步”功能：

	```
	cd localDirectory
	bl start
	```
	{: codeblock}

2. 使用您在 {{site.data.keyword.webide}} 中创建的启动配置。选择启动配置之后，“桌面同步”功能将在本地环境中启用。在您刚刚打开的命令行窗口中，您可以查看应用程序的 URL、调试 URL、管理 URL 以及查看 {{site.data.keyword.Bluemix_live_notm}} 状态。

3. 刷新浏览器，并验证您是否可以查看本地工作空间的静态文件中保存的更改。 

### 禁用桌面同步功能

1. 在第二个命令行窗口中，输入 `bl stop`。
2. 在第一个命令行窗口中，输入 `q`。
