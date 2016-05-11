---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:prereq: .prereq}
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

# 使用命令行界面部署应用程序
*上次更新时间：2016 年 2 月 24 日*

可以使用命令行界面来部署和修改应用程序和服务实例。
{:shortdesc}

开始之前，请安装 {{site.data.keyword.Bluemix}} 和 Cloud Foundry 命令行界面。

<p>
<a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="（在新选项卡或窗口中打开）"><img class="image" src="images/btn_bx_commandline.svg" alt="下载 {{site.data.keyword.Bluemix}} 命令行界面" /> </a>  <a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="（在新选项卡或窗口中打开）"><img class="image" src="images/btn_cf_commandline.svg" alt="下载 Cloud Foundry 命令行界面" /> </a>
</p>

**限制：**Cygwin 不支持命令行工具。请在非 Cygwin 命令行窗口中使用命令行工具。
{:prereq}

安装这些命令行界面后，可以开始执行以下操作：

  1. {: download} 下载入门模板代码。 
      
    <a class="xref" href="http://bluemix.net" target="_blank" title="（在新选项卡或窗口中打开）"><img class="image" src="images/btn_starter-code.svg" alt="下载入门模板代码" /></a>  
  2. 将软件包解压缩到新目录，以设置开发环境。
  3. 切换到新目录。
  
  <pre class="pre">cd <var class="keyword varname">your_new_directory</var></pre>
  
   4.  根据需要对应用程序代码进行更改。我们建议先确保应用程序在本地运行，然后再将其部署回 {{site.data.keyword.Bluemix}}。<br><br>应该记下的一个文件是 `manifest.yml` 文件。将应用程序部署回 {{site.data.keyword.Bluemix}} 时，此文件用于确定应用程序的 URL、内存分配、实例数和其他关键参数。可以在 Cloud Foundry 文档中[阅读有关清单文件的更多信息](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){: new_window}。
  
  5. 连接到 {{site.data.keyword.Bluemix}}。
  
  <pre class="pre">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></pre>
  
  6. 登录到 {{site.data.keyword.Bluemix_notm}}。
 
  <pre class="pre">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></pre>
  
  7. 将应用程序部署到 {{site.data.keyword.Bluemix_notm}}。有关 cf push 命令的更多信息，请参阅[上传应用程序](./upload_app.html)。
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var></pre>
  
  8. 通过在浏览器中输入以下 URL 来访问您的应用程序：
  
  <pre class="codeblock"><code><var class="keyword varname" data-hd-keyref="host">host</var>.<span class="keyword" data-hd-keyref="APPDomain">AppDomainName</span></code></pre>
