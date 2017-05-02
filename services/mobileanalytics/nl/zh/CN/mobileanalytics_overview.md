---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 关于 {{site.data.keyword.mobileanalytics_short}}  
{: aboutmobileanalytics}

{: shortdesc}
{{site.data.keyword.mobileanalytics_full}} 服务为移动应用程序开发人员和应用程序所有者提供关键应用程序使用情况和性能洞察。通过使用 {{site.data.keyword.mobileanalytics_short}}，应用程序所有者和开发人员能够了解在用户端发生的事情，他们可以利用此洞察，构建与用户高度相关的更好的应用程序，从而在众多的移动应用程序中脱颖而出。 

{: #overview}  
该服务包括 {{site.data.keyword.mobileanalytics_short}} Console，开发人员和应用程序所有者可以在这里监视移动应用程序性能，查看使用情况统计信息，并搜索设备日志。{{site.data.keyword.mobileanalytics_short}} 为 iOS 8+（仅限 Swift）和 Android 4+ 提供客户端 SDK。

<!-- Mobile Analytics Server SDKs - set of server SDKs to protect resources that are-->
<!--hosted on {{site.data.keyword.Bluemix_notm}}. Currently supported runtimes are-->
<!--Node.js and Java for Liberty.-->

使用 {{site.data.keyword.mobileanalytics_short}} 服务，可以：
<!-- and includes the following capabilities: -->
<!-- * Near real-time analytics for client activity. Exp -->
<!--* Network latency analytics. GA only -->
<!-- * Client log search and download. Exp -->
<!--* Server log search and download. GA only -->
<!-- Crash and stack trace search. Exp -->

<dl>
	<dt>获取即时洞察</dt>
		<dd>实时查看性能和使用情况度量。</dd>
	<dt>快速实现</dt>
		<dd>在 {{site.data.keyword.Bluemix}} 中创建服务实例，向项目添加 SDK，将两行代码粘贴到应用程序，且准备好收集许多预定义度量。</dd>
	<dt>收集所需的任何数据</dt>
		<dd>使用定制事件检测应用程序，发现用户如何与应用程序交互，跟踪采购并监视应用程序活动。  
</dd>
<dt>速览所有应用程序的度量</dt>
	<dd>{{site.data.keyword.mobileanalytics_short}} Console 提供<!-- both -->现成的<!--and custom-->图表，无需编写查询。</dd>
<dt>关注对您而言重要的事项</dt>
	<dd>根据时间、适配器、应用程序、应用程序版本、操作系统、操作系统版本或设备模型，过滤度量。</dd>
<dt>快速发现问题</dt>
	<dd>监视崩溃状态。对于重要度量设置警报触发器，并将警报路由到任何 REST 端点。</dd>
<dt>对根本原因进行故障诊断</dt>
	<dd>在应用程序中使用定制日志记录，自动上传日志，并通过控制台对它们进行搜索。向下钻取崩溃事件，以查看堆栈跟踪。</dd>
</dl>
 

## 使用度量和事件
{: #usingmetrics}

使用**预定义度量**，可以回答如下问题：

* 我有多少位新用户？  
* 有多少人正在积极地使用我的应用程序？  
* 人们使用我的应用程序有多频繁？ 
* 人们在一天中的什么时间使用我的应用程序？  
* 我的用户最喜欢用的是什么设备模型？ 
* 我应该何时淘汰对旧操作系统的支持？ 
* 哪些应用程序有性能问题？  

通过添加自己的**定制事件**，可以回答如下问题： 

* 哪些功能最常用，哪些不常用？  
* 用户在哪里进入我的应用程序，又在哪里离开？  
* 用户查看最多的活动是哪些？  
* 用户在应用程序中完成工作流（例如，转换漏斗）了吗？   

客户端日志和使用情况数据会自动收集，并根据需要发送到 Mobile Analytics 服务。开发者和管理员可使用 {{site.data.keyword.mobileanalytics_short}} 服务仪表板查看客户端 SDK 收集的数据。

## 数据可视化
{: data-visualization notoc}

分析服务收集的所有数据均可显示在 {{site.data.keyword.mobileanalytics_short}} 仪表板中，该仪表板可从 {{site.data.keyword.Bluemix_notm}} 仪表板访问，通过单击 IBM {{site.data.keyword.mobileanalytics_short}} 服务磁贴实例即可。<!--You can also create custom charts, based on data that is collected by the analytics service in the dashboard.-->除了简明的移动分析视图之外，分析功能还包括对如下数据执行原始搜索的功能：客户端日志、捕获的客户端崩溃数据以及您通过调用客户端 API 函数订阅到 {{site.data.keyword.mobileanalytics_short}} 服务而明确提供的任何其他数据。 

## {{site.data.keyword.mobileanalytics_short}} 常见问题 
{: #faq}

<dl>
	<dt>{{site.data.keyword.mobileanalytics_full}} 是什么？</dt>
		<dd>{{site.data.keyword.mobileanalytics_full}} 是一种服务，可以提供实时和历史信息，帮助您了解移动应用程序的执行和使用情况。使用 {{site.data.keyword.mobileanalytics_short}}，应用程序开发人员和应用程序所有者可以通过监视活动用户、会话、移动平台和应用程序崩溃的趋势，依据数据来制定决策。您还可以针对所选度量值设置警报，一旦触发警报，立即将消息发送至 REST 端点，包括推送服务或内部消息传递服务。</dd>
	<dt>我可以如何使用 {{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}}？</dt>
		<dd>作为移动应用程序产品经理，您可以查看有多少人使用您的应用程序（用户度量值），以及具体的使用时间（会话度量值）。这些信息以时间序列的形式呈现给您并且实时更新，让您能够看到您对应用程序的更改有怎样的效果。您可以进行过滤以查看特定的应用程序版本或操作系统，以制定淘汰决策和划分优先级的决策。</dd>
		<dd>作为移动应用程序市场营销人员，您可以使用用户和会话度量值，通过观察各项指标随时间变化的情况并将其与事件日期相关联，来监视参与情况、管理顾客流失率，并评估移动应用程序市场营销活动的效果。</dd>
		<dd>作为移动应用程序开发人员，您可以使用崩溃度量值来提早发现并解决移动应用程序性能问题，使其不至于影响用户使用或应用程序声誉。您既可以监视来自分析控制台的崩溃计数和崩溃比率，也可以优先处理受影响用户数量最多的问题。您可以设置在崩溃数超过给定阈值时是发送通知警报还是自动执行操作；也可以通过向下钻取崩溃实例以查看设备日志和应用程序堆栈跟踪来进行故障诊断。</dd>
	<dt>使用 Mobile Analytics 需要有数据分析技能吗？</dt>
		<dd>不需要，{{site.data.keyword.mobileanalytics_short}} 为业务利益相关方和应用程序开发人员提供了即取即用的分析控制台。无需任何查询技能。</dd>
	<dt>我能在自己的分析数据上执行定制查询吗？</dt>
		<dd>{{site.data.keyword.mobileanalytics_short}} 不允许定制查询，但未来考虑要实现此功能。</dd>
	<dt>如何将我的应用程序连接到 {{site.data.keyword.mobileanalytics_short}}？</dt>
		<dd>[下载开放式源代码 SDK for iOS 或 Android](install-client-sdk.html)，也可以将 {{site.data.keyword.mobileanalytics_short}} [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/) 用于其他平台。</dd>
	<dt>{{site.data.keyword.mobileanalytics_short}} 在哪些 Bluemix 地区可用？</dt>
		<dd>当前，Mobile Analytics 在美国南部和英国可用。此产品未来计划在其他地区上市，但具体时间表尚未确定。</dd>
	<dt>此服务成本是多少？</dt>
		<dd>每个月收集的前 1 亿个事件是免费的，此后，每 1 百万个事件需要支付 $1。</dd>
	<dt>什么是事件？</dt>
		<dd>当前报告的事件包括应用程序会话开始、应用程序会话结束（包括应用程序崩溃）、警报通知和日志条目。</dd>
	<dt>我如何估算该服务每月开销为多少？</dt>
		<dd>因为定价取决于每个客户端账户发送给服务的事件数，所以估算定价意味着估算事件。  
<p>
您所需支付的价格是您已连接到 {{site.data.keyword.mobileanalytics_short}} 的所有应用程序的事件总数。对于给定的应用程序，事件数取决于您在应用程序中实施的检测程度、用户数量以及用户活跃程度。   
</p>
<p>
使用此公式估算使用情况：每个应用程序每个月的事件 =（每日用户数）（每日每用户会话数）（每月天数）（每会话事件数）
</p>
<p>
每会话事件数可以为 2 到几百个不等，取决于开发人员为应用程序配置的网络调用、定制分析、日志捕获和警报定义。
</p>
	<dt>分析数据可以保留多长时间？</dt>
		<dd>数据保留时间不少于 30 天。</dd>
	<dt>让数据显示在 {{site.data.keyword.mobileanalytics_short}} Console 中需要花多长时间？</dt>
		<dd>数据在 {{site.data.keyword.mobileanalytics_short}} Console 中几乎是实时的，也就是说，在实际事件发生后几秒之内，数据就会显示出来。</dd>
	<dt>{{site.data.keyword.mobileanalytics_full}} 与 MobileFirst Platform Foundation 中的移动分析有什么差别？</dt>
		<dd>在这两种控制台中，用户和会话非常相似，但 MobileFirst Platform Foundation 随附的分析中还包含其他度量值和设置，客户机可以使用这些功能来管理自己的内部部署分析集群。此外，MobileFirst Platform Foundation 分析控制台将度量值零散提供给适配器和适配器程序，而在 {{site.data.keyword.mobileanalytics_short}} 服务中，这些度量值集成到网络请求图表和表中。</dd>
	<dt>我要在内部部署中使用 MobileFirst Platform Foundation 来开发应用程序，但不想托管自己的分析集群。我可以改为使用 {{site.data.keyword.mobileanalytics_full}} 吗？</dt>
		<dd>可以。您有两个选项：如果要使用 MobileFirst Platform Foundation 7.x 或 8.0，并且您的应用程序受 MobileFirst Platform SDK 检测，那么您可以配置 MobileFirst 服务器使其将分析数据报告给 {{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}}。请阅读[配置 Mobile Analytics 和 Mobile Foundation Bluemix 服务 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://mobilefirstplatform.ibmcloud.com/blog/2016/07/11/analytics-bm-service/){: new_window} 博客帖子以了解详细信息。或者，您也可以使用 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} SDK 来检测您的应用程序，并直接报告给 {{site.data.keyword.mobileanalytics_short}} 服务。</dd>
	<!-- <dt>My instance of  {{site.data.keyword.mobileanalytics_short}} does not look like the screen shots in the catalog. What's going on?</dt> -->
		<!-- <dd>Most likely you are using the Classic view interface for {{site.data.keyword.Bluemix_notm}}. Classic view is deprecated, so {{site.data.keyword.mobileanalytics_short}} runs best in the new {{site.data.keyword.Bluemix_notm}} interface. If you are in Classic view, you will see a link in the {{site.data.keyword.Bluemix_notm}} header that says <strong>Try the new {{site.data.keyword.Bluemix_notm}}</strong>. Click that link to use the new interface.</dd> -->
</dl>


# 相关链接
{: #rellinks notoc}

## SDK
{: #sdk notoc}
<!-- Links to SDK download and SDK Developer Guide -->
* [Android SDK ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window} 
* [iOS SDK ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}

