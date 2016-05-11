# 创建移动应用程序
{: #mobile}
*上次更新时间：2016 年 1 月 28 日* 

使用 {{site.data.keyword.Bluemix}} Mobile Services，可以在不依赖于 IT 人员参与的情况下，将预构建、受管理且可扩展的云服务合并到您的移动应用程序中。您可以专注于移动应用程序的构建，而不用担心管理后端基础架构的复杂性。

<table><caption>表 1. MobileFirst&trade; Services Starter 样板</caption>
<tr>
	<td>每个移动服务都可以独立使用。您也可以将它们放在一起使用，从而获取最大好处。要开始操作，请使用 {{site.data.keyword.mobilefirstbp}} Starter 来创建您的应用程序。此样板会：<ul>
			<li>创建具有模板应用程序的 Node.js 运行时。您可以使用此应用程序来提供服务器端功能，例如 RESTful API 和静态文件。<!-- You can read more about operating this application in the Developing Mobile Backend section.--> </li>
			<li>
供应每个 {{site.data.keyword.Bluemix_notm}} Mobile Services 的实例，并将该服务绑定到 Node.js 应用程序。</li>
		</ul>
	</td>
	<td> <img src="images/mf_boiler_icon.png" alt="Bluemix 移动服务" width="500"> {{site.data.keyword.mobilefirstbp}} Starter 样板</td>
</tr>
</table>

在使用 {{site.data.keyword.mobilefirstbp}} Starter 样板创建您的应用程序之后，可以获取每个服务的 HelloWorld 样本，也可以配置您的现有应用程序以使用 {{site.data.keyword.Bluemix_notm}} 服务。


## 服务概述
{: #services-overview}
您可以通过 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobilefirstbp}} Starter 样板统一使用所有 {{site.data.keyword.Bluemix_notm}} Mobile Services，也可以从 {{site.data.keyword.Bluemix_notm}}“目录”中使用单个服务。下图概述了 {{site.data.keyword.Bluemix_notm}} Mobile Services 的所有组件。

![{{site.data.keyword.Bluemix_notm}} Mobile Services 体系结构](images/bms_architecture.jpg)

<table>
<caption>表 2. {{site.data.keyword.Bluemix_notm}} 和企业系统</caption>
<th>{{site.data.keyword.Bluemix_notm}}</th>
<th>企业系统</th>
<tr>
<td> <img src="images/i_js_64.png" alt="Node.js 运行时图标"> <b>Node.js</b><br/>Node.js 运行时（托管一个模板应用程序）是作为 {{site.data.keyword.mobilefirstbp}} Starter 样板的一部分来提供的。您可以使用该模板应用程序来提供服务器端功能，例如 RESTful API 和静态文件。<br/>例如，您可以在您所在公司的现有基础架构中扩展 Node.js 应用程序，以便处理定制逻辑或与 REST API 相连接。您在 {{site.data.keyword.Bluemix_notm}} 上创建的每个应用程序都具有唯一的应用程序标识。您的移动应用程序会将此标识与 SDK 配合使用，以访问与该应用程序相关联的服务。平台会将应用程序标识用作常用功能（例如测量和日志记录）的上下文。您可以在“开发移动后端”部分中阅读有关操作此应用程序的更多信息。</td>
<td valign="top"><b>信息提供者</b> <br/>您可以使用 {{site.data.keyword.Bluemix_notm}} 上托管的 Node.js 运行时来连接到任何种类的信息提供者：<ul>
	<li>企业后端</li>
	<li>数据库</li>
	<li>其他托管的第三方服务</li>
</ul>
</td>
</tr>
<tr>
<td><img src="images/catalog_icons-05.png" alt="{{site.data.keyword.amashort}}服务图标"> <b>{{site.data.keyword.amashort}}</b><br/>使用 {{site.data.keyword.amafull}} 服务可保护 {{site.data.keyword.Bluemix_notm}} 上托管的 Node.js 和 Java for Liberty 应用程序。为您的移动应用程序配备 {{site.data.keyword.amashort}} SDK 后，就可以要求用户必须登录才能访问 Node.js 或 {{site.data.keyword.Bluemix_notm}} Mobile Services。除安全功能外，{{site.data.keyword.amashort}} 还会收集分析数据，便于您监视移动应用程序性能以及收集客户机日志和使用情况统计信息。</td>
<td valign="top"><b>用户身份提供者</b> <br/>您可以使用以下身份提供者：<ul><li>Facebook</li><li>Google</li></ul></td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="Push Notifications 服务图标"> <b>{{site.data.keyword.mobilepushshort}}</b><br/>{{site.data.keyword.mobilepushfull}} 服务提供一个统一平台来发送和管理针对 iOS 和 Android 平台的移动推送通知。此服务会管理您的应用程序用户与其设备和设备平台之间的映射，还会处理将推送通知派送给设备。使用此服务，可以向移动应用程序用户发送广播、单点广播（根据设备标识）和基于标记（或基于主题）的推送通知。</td>
<td valign="top"><b>推送服务提供者</b><ul><li>Apple 推送通知服务</li><li>Google 云消息传递</li></ul></td>
</tr>
<tr>
<td><img src="images/cloudant64.png" alt="Cloudant 服务图标"> <b>Cloudant NoSQLDB</b><br/>Cloudant 是一种 NoSQL 数据库即服务 (DBaaS)。它从头开始构建，用于在全球范围内进行扩展，实现不间断运行，以及处理各种数据类型，例如 JSON、全文本和地理空间。</td>
<td>Cloudant.com</td>
</tr>
</table>
