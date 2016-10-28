---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Cloudant 入门
{: #getting-started-with-cloudant}
上次更新时间：2016 年 8 月 12 日
{: .last-updated}

{{site.data.keyword.cloudant}} 是以 JSON 格式存储数据的文档数据库即服务 (DBaaS)。在其构建过程中，考虑到了可扩展性、高可用性和耐久性。它提供丰富多样的建立索引选项，包括 map-reduce、Cloudant Query、full-text 和 geospatial 建立索引。通过其复制功能，可以轻松实现数据库集群、台式 PC 和移动设备之间的数据同步。{:shortdesc}

您可以从 Bluemix 仪表板上的服务启动页面来启动 {{site.data.keyword.cloudant}} 控制台。

要使用该服务，请遵循以下步骤：
<ol>
<li>使用 Bluemix 仪表板或 CloudFoundry 命令行界面来创建服务实例。<p>要使用仪表板创建实例，请遵循以下步骤：<ol>
<li>登录到 Bluemix。</li>
<li>在仪表板上，单击“数据和分析”面板中的“<code>使用数据</code>”链接。</li>
<li>单击“<code>新建服务</code>”按钮。</li>
<li>在服务列表中，单击 {{site.data.keyword.cloudant}} 按钮。</li>
<li>在 {{site.data.keyword.cloudant}} 信息页面中，单击“<code>选择 {{site.data.keyword.cloudant}}</code>”按钮。</li>
<li>在 {{site.data.keyword.cloudant}} 目录页上，为您需要的服务填充详细信息。准备好继续时，请单击“<code>创建</code>”按钮。</li>
<li>创建完 Cloudant 实例后，会显示该实例的仪表板。单击“<code>服务凭证</code>”链接可查看访问实例所需的所有详细信息。</li>
</ol>
</p>
<p>要使用 CloudFoundry 命令行界面创建实例，请遵循以下步骤：<ol>
<li>在系统上安装 CloudFoundry <code>cf</code> 工具。《<a href="https://console.ng.bluemix.net/docs/cli/index.html">Bluemix CLI 和开发工具指南</a>》中提供有关如何执行该操作的指示信息。</li>
<li>使用以下命令创建新的服务实例：<br/>
<pre><code>cf create-service</code></pre></li>
<li>将为您显示可用服务的列表。请从中选择一个，然后输入唯一的服务实例名称和计划。将为该实例建议一个随机名称，但可以将其更改为您喜欢的名称。</li>
<li>创建服务之后，您可以获取包含所有已创建服务的列表：<br/>
<pre><code>cf services</code></pre></li>
<li>在应用程序中使用服务之前，必须将服务绑定到应用程序。使用以下命令执行此操作：<br/>
<pre><code>cf bind-service</code></pre>
从结果列表中选择一个应用程序和一个服务。绑定操作成功时，<code>cf</code> 命令会通知您。</li>
</ol>
</p>
</li>
<li><p>创建服务实例后，将显示类似以下示例的 JSON 数据，并可在 Bluemix 仪表板中进行查看：<br/><pre><code>{
"cloudantNoSQLDB": {"name": "Cloudant-3s",
    "label": "cloudantNoSQLDB",
    "plan": "shared",
    "credentials": {
      "username": "someusername",
      "password": "secret",
      "host": "myhost-bluemix.cloudant.com",
      "port": 443,
      "url": "https://someusername:secret@myhost-bluemix.cloudant.com"
    }
    }
}</code></pre></p>
{: screen}
<p>此数据还会添加到绑定了该服务的任何 Bluemix 应用程序的 <code>VCAP_SERVICES</code> 环境变量。</p>
<p>服务凭证存储在 JSON 对象中，其中包含以下字段：<ul>
<li><code>key</code>：服务的名称 (cloudantNoSQLDB)</li>
<li><code>name</code>：用户提供的服务实例名称</li>
<li><code>host</code>：服务器的主机名</li>
<li><code>port</code>：正在其上运行服务的端口号，通常为 443</li>
<li><code>username</code>：用于认证的用户名</li>
<li><code>password</code>：用于认证的密码</li>
<li><code>url</code>：服务实例的 URL</li>
</ul></li>
<li><p>在 Bluemix 应用程序中，从 <code>VCAP_SERVICES</code> 环境变量中读取凭证。</p>
<p>在从 Bluemix 外部运行的应用程序中或在位于 Bluemix 不同地理空间区域的应用程序中，您可以从 Bluemix 仪表板检索凭证，并将其添加到应用程序的配置中。</p>
</li>
<li>要访问数据库，基本机制是通过 HTTPS 将请求发送到给定主机和端口，并使用用户名和密码进行认证。可以使用各种应用程序语言和平台来发送请求，包括：<ul>
<li><a href="https://github.com/cloudant/sync-android">Android</a></li>
<li><a href="https://github.com/cloudant/CDTDatastore">Apple iOS</a></li>
<li><a href="https://github.com/cloudant/java-cloudant">Java</a></li>
<li><a href="https://github.com/cloudant/objective-cloudant">Objective C 和 Swift</a></li>
<li><a href="https://github.com/cloudant/python-cloudant">Python</a></li>
</ul>
... 以及其他多种平台。有关更多信息，请参阅 <a href="https://cloudant.com/for-developers/">Cloudant Developer 主页</a>和<a href="http://docs.cloudant.com/libraries.html">客户端库</a>列表。</li>
<li>当应用程序准备就绪时，就可以将其部署到 Bluemix 环境中以用于验证。要部署应用程序，请使用以下命令：<br/>
<pre><code>cf push</code></pre></li>
<li>要取消服务实例与应用程序的绑定，请使用以下命令：<br/>
<pre><code>cf unbind-service</code></pre></li>
<li>要删除服务实例，请使用以下命令：<br/>
<pre><code>cf delete-service</code></pre></li>
</ol>

[API 参考](https://docs.cloudant.com/api.html)中提供了有关向数据库认证并发送请求的更多信息。

# 相关链接
{: #rellinks}

## 教程和样本
{: #samples}

* [Cloudant 客户机库](https://docs.cloudant.com/libraries.html)
* [在 Bluemix 上将 Cloudant 与 Liberty 搭配使用](https://developer.ibm.com/bluemix/2014/07/08/cloudant_on_bluemix/)
* [Cloudant 指南](https://docs.cloudant.com/guides.html)

## API 参考
{: #api}

* [Cloudant API 参考](https://docs.cloudant.com/api.html)

## 相关链接
{: #general}

* [Cloudant Web 站点和仪表板](https://cloudant.com/)
* [Cloudant 博客](https://cloudant.com/blog)
