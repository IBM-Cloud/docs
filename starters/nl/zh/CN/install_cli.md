{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:download: .download}
{:pre: .pre}
{:app_name: data-hd-keyref="app_name"}
{:app_key: data-hd-keyref="app_key"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:host: data-hd-keyref="host"}
{:org_name: data-hd-keyref="org_name"}
{:route: data-hd-keyref="route"}
{:space_name: data-hd-keyref="space_name"}
{:service_name: data-hd-keyref="service_name"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:user_ID: data-hd-keyref="user_ID"}

# 使用 Cloud Foundry 命令行界面部署应用程序
*上次更新时间：2015 年 11 月 11 日*

可以使用 Cloud Foundry 命令行界面来部署和修改应用程序和服务实例。{:shortdesc}

开始之前，请安装 cf 命令行界面。

<p>
<a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="（在新选项卡或窗口中打开）"><img class="image" src="images/btn_cf_commandline.svg" alt="下载 Cloud Foundry 命令行界面" /></a></p>

**限制：**Cygwin 不支持 Cloud Foundry 命令行界面。请在非 Cygwin 命令行窗口中使用 Cloud Foundry 命令行界面。

安装 cf 命令行界面后，可以开始执行以下操作：

  1. 下载入门模板代码。
  
    <p>
    <a class="xref" href="http://bluemix.net" target="_blank" title="（在新选项卡或窗口中打开）"><img class="image" src="images/btn_starter-code.svg" alt="下载入门模板代码" /></a></p>
  
  {:download}
  2. 将软件包解压缩到新目录，以设置开发环境。
  3. 切换到新目录。
  
  <pre class="pre">cd <var class="keyword varname">your_new_directory</var></pre>
  
  4. 连接到 {{site.data.keyword.Bluemix}}。
  
  <pre class="pre">cf api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></pre>
  
  5. 登录到 {{site.data.keyword.Bluemix_notm}}。
 
  <pre class="pre">cf login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></pre>
  
  6. 将应用程序部署到 {{site.data.keyword.Bluemix_notm}}。有关 cf push 命令的更多信息，请参阅[上传应用程序](upload_app.html#upload_app__push)。
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var></pre>
  
  7. 通过在浏览器中输入以下 URL 来访问您的应用程序：
  
  <pre class="codeblock"><code><var class="keyword varname" data-hd-keyref="host">host</var>.<span class="keyword" data-hd-keyref="APPDomain">AppDomainName</span></code></pre>
