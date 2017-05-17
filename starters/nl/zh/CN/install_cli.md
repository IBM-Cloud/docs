---



copyright:

  years: 2015，2017

lastupdated: "2017-04-19"


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

# 使用命令行界面下载、修改和重新部署 Cloud Foundry 应用程序

使用 {{site.data.keyword.Bluemix_notm}} 命令行界面下载、修改和重新部署 Cloud Foundry 应用程序与服务实例。
{:shortdesc}

开始之前，请下载并安装 {{site.data.keyword.Bluemix_notm}} 命令行界面。 

<p>
<a class="xref" href="https://clis.ng.bluemix.net" target="_blank" title="（在新选项卡或窗口中打开）"><img class="image" src="images/btn_bx_commandline.svg" alt="下载 Bluemix 命令行界面" /> </a>
</p>

**限制：**Cygwin 不支持命令行工具。请在非 Cygwin 的命令行窗口中使用命令行工具。
{:prereq}

安装命令行界面后，可以开始执行以下操作：

  1. {: download} 将应用程序的编码下载到新目录，以设置开发环境。
  
    <a class="xref" href="http://bluemix.net" target="_blank" title="（在新选项卡或窗口中打开）"><img class="image" src="images/btn_starter-code.svg" alt="下载应用程序代码" /></a>

  2. 切换到代码所在的目录。

  <pre class="pre"><code class="hljs">cd <var class="keyword varname">your_new_directory</var></code></pre>

  3.  根据需要对应用程序代码进行更改。例如，如果要使用 {{site.data.keyword.Bluemix}} 样本应用程序，并且应用程序包含 `src/main/webapp/index.html` 文件，那么可以对其进行修改并编辑“Thanks for creating ...”以输入新内容。确保应用程序在本地运行，然后再将其部署回 {{site.data.keyword.Bluemix_notm}}。

    记录 `manifest.yml` 文件。将应用程序部署回 {{site.data.keyword.Bluemix_notm}} 时，此文件用于确定应用程序的 URL、内存分配、实例数和其他关键参数。您可以在 Cloud Foundry 文档中[阅读有关清单文件的更多信息](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){: new_window}。

    此外，请注意 `README.md` 文件，此文件包含详细信息，如构建指示信息（如果适用）。

    注：如果应用程序是 Liberty 应用程序，那么必须先对其进行构建，然后再重新部署。

  4. 连接并登录到 {{site.data.keyword.Bluemix_notm}}。

  <pre class="pre"><code class="hljs">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></code></pre>

  <pre class="pre"><code class="hljs">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></code></pre>

  如果使用的是联合标识，请使用 `-sso` 选项。

  <pre class="pre"><code class="hljs">bluemix login  -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var> -sso</code></pre>

  5. 在 <var class="keyword varname">your_new_directory</var> 中，使用 `bluemix app push` 命令将应用程序重新部署到 {{site.data.keyword.Bluemix_notm}}。有关 `bluemix app push` 命令的更多信息，请参阅[上传应用程序](/docs/starters/upload_app.html)。

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var></code></pre>

  6. 通过浏览到 https://<var class="keyword varname" data-hd-keyref="app_url">app_url</var>.<span class="keyword" data-hd-keyref="APPDomain">AppDomainName</span> 来访问应用程序。
