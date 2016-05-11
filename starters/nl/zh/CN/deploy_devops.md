---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:download: .download}

# 使用 Git 开始编码
*上次更新时间：2016 年 3 月 2 日*  

您可以创建托管的 Git 存储库，该存储库将自动部署到 {{site.data.keyword.Bluemix}}。然后，可以通过将更改推送到 Git 存储库来修改应用程序中运行的代码。
{:shortdesc}

1. 要开始操作，请单击应用程序的“概述”页面上的**添加 Git 存储库和管道**，或者单击 {{site.data.keyword.Bluemix_notm}}“典型经验”中的**添加 GIT**。 
2. 在打开的窗口中，确保已选中**使用入门模板应用程序包填充存储库并启用“构建和部署”管道**复选框。这将创建 Git 存储库。如果入门模板代码可用，系统会将代码装入到存储库中。此外，应用程序由 {{site.data.keyword.jazzhub}} 中运行的 Delivery Pipeline 服务来部署。  
3. 要更新应用程序，可以使用命令行或 Web IDE。
   **如果使用命令行，请执行以下操作：**
   a. 在应用程序“概述”页面上，使用 Git URL 克隆 Git 存储库。
   b. 在您最常用的编辑器中，更新代码。
   c. 在 Git 命令行界面中，推送更改。  
	    
   **如果使用 Web IDE，请执行以下操作：**  
   a. 在应用程序的“概述”页面上，单击**编辑代码**。您的项目将在 Web IDE 中打开。  
   b. 根据需要进行更改，然后使用内置 Git 支持进行推送。  
		
更新后的应用程序将重新部署到 {{site.data.keyword.Bluemix_notm}}。  

有关逐步指示信息，请参阅 [Set up Git integration and auto-deploy in DevOps Services](https://hub.jazz.net/tutorials/jazzeditor/#git_integration_and_autodeployment)。  

## 已添加 Git？请尝试 {{site.data.keyword.Bluemix_notm}} Live Sync  

如果您要构建 Node.js 应用程序，那么可以使用 {{site.data.keyword.Bluemix_notm}} Live Sync 快速更新 {{site.data.keyword.Bluemix_notm}} 上的应用程序实例，并像在桌面上进行操作一样进行开发。  

要了解有关 {{site.data.keyword.Bluemix_notm}} Live Sync 的更多信息，请参阅 [{{site.data.keyword.Bluemix_notm}} Live Sync](../develop/bluemixlive.html)。有关命令的更多详细信息，请参阅 [{{site.data.keyword.Bluemix_notm}} Live Sync CLI 文档](../cli/reference/bl/index.html)。要将 {{site.data.keyword.Bluemix_notm}} Live Sync 与 Web IDE 配合使用，请参阅[实时编辑](../develop/bluemixlive.html)。  

1. 下载并安装 {{site.data.keyword.Bluemix_notm}} Live Sync bl 命令行。 

<p>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/blive_setup.msi" target="_blank" title="（在新选项卡或窗口中打开）"><img class="image" src="images/bl_gs_icons_windows_b.svg" alt="下载 Windows bl 命令行按钮" /></a>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/BluemixLive.pkg" target="_blank" title="（在新选项卡或窗口中打开）"><img class="image" src="images/bl_gs_icons_mac-osx_b.svg" alt="下载 Mac bl 命令行按钮" /></a>
</p>

**重要信息：**bl 命令行工具仅适用于 Windows 7 和 8 以及 Mac OS X V10.9 或更高版本。 

2. 在命令行上，使用以下命令登录。系统将提示您输入 IBM® 标识和密码。```
bl login```

3. 通过输入以下命令，查看可用于 {{site.data.keyword.Bluemix_notm}} Live Sync 同步的项目的列表：```
bl projects```
在列表中找到匹配您应用程序的项目名称。项目名称的格式为 *alias* | *your application name*。 

4. 通过输入以下命令，将本地环境与 {{site.data.keyword.Bluemix_notm}} 上的项目同步。如果您是项目所有者，那么只需为 projectName 指定 your-application-name 即可。 
<!--- this command needs italicized parameters projectName localDirectory and yellow on 'local' -->
```
bl sync projectName -d localDirectory --verbose
```
此命令继续运行（同步也将继续），直到您输入“q”。--verbose 选项用于显示日志记录和状态信息。如果任何自变量中包含空格，那么需要为该名称加引号。

5. 在另一个命令行窗口中，在本地目录下，通过输入以下命令，以“实时编辑”方式将应用程序部署到 {{site.data.keyword.Bluemix_notm}}。```
bl start```  

更改本地目录中的文件时，系统会自动将更改传播到正在 {{site.data.keyword.Bluemix_notm}} 上运行的应用程序以及项目云工作空间中。如果需要重新启动 Node 应用程序，那么可以使用以下命令：```
bl start --restart
```
