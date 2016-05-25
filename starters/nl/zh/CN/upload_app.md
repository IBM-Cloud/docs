---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 上传应用程序
*上次更新时间：2016 年 2 月 17 日*

登录到 {{site.data.keyword.Bluemix}} 后，可以使用 cf push 命令来上传应用程序。
{:shortdesc}

开始之前，您必须：
  1. 安装 {{site.data.keyword.Bluemix}} 和 Cloud Foundry 命令行界面。

  <a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="（在新选项卡或窗口中打开）"><img class="image" src="images/btn_bx_commandline.svg" alt="下载 {{site.data.keyword.Bluemix}} 命令行界面" /> </a>  <a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="（在新选项卡或窗口中打开）"><img class="image" src="images/btn_cf_commandline.svg" alt="下载 Cloud Foundry 命令行界面" /> </a>
  2. 连接到 {{site.data.keyword.Bluemix}}。

  <pre class="pre">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></pre>
  
  3. 登录到 {{site.data.keyword.Bluemix_notm}}。

  <pre class="pre">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></pre>

发出 **cf push** 命令时，**cf** 命令行界面将提供使用 buildpack 来构建并运行应用程序的 {{site.data.keyword.Bluemix_notm}} 环境的工作目录。

  1. 从应用程序目录中，输入带有应用程序名称的 **cf push** 命令。在 {{site.data.keyword.Bluemix_notm}} 环境中，应用程序名称必须是唯一的。

  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -m 512m</pre>
  
  {{site.data.keyword.Bluemix_notm}} 包含内置 buildpack。在某些情况下，即便是内置 buildpack，也必须提供 -c 选项来指定用于启动应用程序的命令。例如，需要使用 -c 选项来推送 Node.js 应用程序：
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -c start_command</pre>
  
  此外，Node.js 应用程序必须包含有效的 package.json 文件。

  所有其他外部 buildpack 都必须使用 -b 选项来推送。例如：

  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -b buildpack_URL</pre>
  
  **提示：**使用 **cf push** 命令时，**cf** 命令行界面会将当前目录中的所有文件和目录复制到 Bluemix 中。请确保应用程序目录中只包含必需的文件。

  cf push 命令会上传应用程序并将其部署到 {{site.data.keyword.Bluemix_notm}}。有关 cf push 的更多信息，请参阅 [cf 命令](../cli/reference/cfcommands/index.html)。有关 buildpack 的信息，请参阅[使用社区 buildpack](../cfapps/byob.html)。

  2. 如果更改了应用程序，可以通过再次输入 cf push 命令来上传这些更改。cf 命令行界面会使用您先前的选项并根据您对提示的响应，以新的代码段来更新任何运行中应用程序实例。


**提示：**您还可以从 DevOps Services 上传或部署应用程序。请参阅[在 Node.js 中使用 Web IDE 开发 {{site.data.keyword.Bluemix_notm}} 应用程序](https://hub.jazz.net/tutorials/devopsweb/){: new_window}。
