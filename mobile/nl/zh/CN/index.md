# 创建移动应用程序
{: #mobile}

使用 {{site.data.keyword.Bluemix_notm}} Mobile Services，可以在不依赖于 IT 人员参与的情况下，将预构建、受管理且可扩展的云服务合并到您的移动应用程序中。您可以专注于移动应用程序的构建，而不用担心管理后端基础架构的复杂性。

<table><caption>表 1. Bluemix Mobile Services 样板</caption>
<tr>
	<td>每个 Bluemix Mobile Services 都可以独立使用。您也可以将它们放在一起使用，从而获取最大好处。要开始操作，请使用 Bluemix Mobile Services 样板来创建您的应用程序。此样板会：<ul>
			<li>创建具有模板应用程序的 Node.js 运行时。您可以使用此应用程序来提供服务器端功能，例如 RESTful API 和静态文件。您可以在“开发移动后端”部分中阅读有关操作此应用程序的更多信息。</li>
			<li>
供应每个 Bluemix Mobile Services 的实例，并将该服务绑定到 Node.js 应用程序。</li>
		</ul>
	</td>
	<td> <img src="images/mf_boiler_icon.png" alt="Bluemix Mobile Services" width="500"> Bluemix Mobile Services 样板</td>
</tr>
</table>

在使用 Bluemix Mobile Services 样本创建您的应用程序之后，可以获取每个服务的 HelloWorld 样本，也可以配置您的现有应用程序以使用 Bluemix 服务。


## 服务概述
{: #services-overview}
您可以通过 Bluemix Mobile Services 样板统一使用所有 Bluemix Mobile Services，也可以从 Bluemix“目录”中使用单个服务。下图列出了 Bluemix Mobile Services 的所有组件。

![Bluemix Mobile Services 体系结构](images/bms_architecture.jpg)

<table>
<caption>表 2. Bluemix 和企业系统</caption>
<th>Bluemix</th>
<th>企业系统</th>
<tr>
<td> <img src="images/i_js_64.png" alt="Node.js 运行时图标"> <b>Node.js</b><br/>一种 Node.js 运行时，其中托管一个模板应用程序，它是作为 Bluemix Mobile Services 样板的一部分来提供的。您可以使用该模板应用程序来提供服务器端功能，例如 RESTful API 和静态文件。<br/>例如，您可以在您所在公司的现有基础架构中扩展 Node.js 应用程序，以便处理定制逻辑或与 REST API 相连接。您在 Bluemix 上创建的每个应用程序都具有唯一的应用程序标识。您的移动应用程序会将此标识与 SDK 配合使用，以访问与该应用程序相关联的服务。平台会将应用程序标识用作常用功能（例如测量和日志记录）的上下文。您可以在“开发移动后端”部分中阅读有关操作此应用程序的更多信息。</td>
<td valign="top"><b>信息提供者</b> <br/>您可以使用 Bluemix 上托管的 Node.js 运行时来连接到任何种类的信息提供者：<ul>
	<li>企业后端</li>
	<li>数据库</li>
	<li>其他托管的第三方服务</li>
</ul>
</td>
</tr>
<tr>
<td><img src="images/catalog_icons-05.png" alt="Mobile Client Access 服务图标"> <b>Mobile Client Access</b><br/>使用 IBM Mobile Client Access for Bluemix 服务可保护 Bluemix 上托管的 Node.js 和 Java for Liberty 应用程序。为您的移动应用程序配备 Mobile Client Access SDK 后，就可以要求用户必须登录才能访问 Node.js 或 Bluemix Mobile Services。除安全功能外，Mobile Client Access 还会收集分析数据，便于您监视移动应用程序性能以及收集客户机日志和使用情况统计信息。</td>
<td valign="top"><b>用户身份提供者</b> <br/>您可以使用以下身份提供者：<ul><li>Facebook</li><li>Google</li></ul></td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="Push Notifications 服务图标"> <b>Push Notifications</b><br/>IBM Push Notifications for Bluemix 服务提供一个统一平台来发送和管理针对 iOS 和 Android 平台的移动推送通知。此服务会管理您的应用程序用户与其设备和设备平台之间的映射，还会处理将推送通知派送给设备。使用此服务，可以根据向移动应用程序用户推送的通知来发送广播、单点广播（根据用户标识和设备标识）和标记（或主题）。</td>
<td valign="top"><b>推送服务提供者</b><ul><li>Apple 推送通知服务</li><li>Google 云消息传递</li></ul></td>
</tr>
<tr>
<td><img src="images/cloudant64.png" alt="Cloudant 服务图标"> <b>Cloudant NoSQLDB</b><br/>Cloudant 是一种 NoSQL 数据库即服务 (DBaaS)。它从头开始构建，用于在全球范围内进行扩展，实现不间断运行，以及处理各种数据类型，例如 JSON、全文本和地理空间。</td>
<td>Cloudant.com</td>
</tr>
</table>
