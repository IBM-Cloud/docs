---



copyright:

  years: 2015, 2017

lastupdated: "2017-04-19"



---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 上传应用程序

登录到 {{site.data.keyword.Bluemix}} 后，可以使用 `bluemix app push` 命令来上传应用程序。
{:shortdesc}

开始之前，您必须：
  1. 安装 {{site.data.keyword.Bluemix}} 命令行界面。

  <a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="（在新选项卡或窗口中打开）"><img class="image" src="images/btn_bx_commandline.svg" alt="下载 {{site.data.keyword.Bluemix}} 命令行界面" /></a>

  2. 连接到 {{site.data.keyword.Bluemix}}。

  <pre class="pre"><code class="hljs">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></code></pre>

  3. 登录到 {{site.data.keyword.Bluemix_notm}}。

  <pre class="pre"><code class="hljs">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></code></pre>

发出 **bluemix app push** 命令时，命令行界面将提供使用 buildpack 来构建并运行应用程序的 {{site.data.keyword.Bluemix_notm}} 环境的工作目录。

  1. 从应用程序目录中，输入带有应用程序名称的 **bluemix app push** 命令。在 {{site.data.keyword.Bluemix_notm}} 环境中，应用程序名称必须是唯一的。


  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -m 512m</code></pre>

  {{site.data.keyword.Bluemix_notm}} 包含内置 buildpack。在某些情况下，即便是内置 buildpack，也必须提供 -c 选项来指定用于启动应用程序的命令。例如，需要使用 -c 选项来推送 Node.js 应用程序：

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -c start_command</code></pre>

  此外，Node.js 应用程序必须包含有效的 package.json 文件。

  所有其他外部 buildpack 都必须使用 -b 选项来推送。例如：

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -b buildpack_URL</code></pre>

  **提示：**使用 **bluemix app push** 命令时，该命令会将当前目录中的所有文件和目录复制到 Bluemix 中。请确保应用程序目录中只包含必需的文件。


  2. 如果更改了应用程序，可以通过再次输入 `bluemix app push` 命令来上传这些更改。该命令会使用您先前的选项并根据您对提示的响应，以新的代码段来更新任何运行中应用程序实例。

{{site.data.keyword.Bluemix}} CLI 在其安装中捆绑了 cf CLI。`bluemix app push` 命令实际上会调用 `cf push` 以将应用程序上传并部署到 {{site.data.keyword.Bluemix_notm}}。有关 cf push 的更多信息，请参阅 [cf 命令](/docs/cli/reference/cfcommands/index.html)。有关 buildpack 的信息，请参阅[使用社区 buildpack](/docs/cfapps/byob.html)。
