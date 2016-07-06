---

copyright:
  years: 2015, 2016

---
{:shortdesc: .shortdesc}

# 关于 {{site.data.keyword.mobileanalytics_short}}  
{: aboutmobileanalytics}
*上次更新时间：2016 年 4 月 21 日*
{: .last-updated}

{: shortdesc}
{{site.data.keyword.mobileanalytics_full}} 服务为移动应用程序开发人员和应用程序所有者提供关键应用程序使用情况和性能洞察。通过使用 {{site.data.keyword.mobileanalytics_short}}，应用程序所有者和开发人员能够了解在“用户端”发生的事情，他们可以利用此洞察，构建与用户高度相关的更好的应用程序，从而在众多的移动应用程序中脱颖而出。 

{: #overview}  
该服务包括 {{site.data.keyword.mobileanalytics_short}} 控制台，开发人员和应用程序所有者可以在这里监视移动应用程序性能、查看使用情况统计信息，并搜索设备日志。{{site.data.keyword.mobileanalytics_short}} 为 iOS 8+（仅限 Swift）和 Android 4+ 提供客户端 SDK。

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
<dt>一眼即能够查看所有应用程序的度量</dt>
	<dd>{{site.data.keyword.mobileanalytics_short}} 控制台提供现成的图表和定制图表，无需编写查询。</dd>
<dt>关注对您而言重要的事项</dt>
	<dd>根据时间、适配器、应用程序、应用程序版本、操作系统、操作系统版本或设备模型，过滤度量。</dd>
<dt>快速发现问题</dt>
	<dd>监视崩溃状态。对于重要度量设置警报触发器，并将警报路由到任何 REST 端点。</dd>
<dt>对根本原因进行故障诊断</dt>
	<dd>在应用程序中使用定制客户机日志记录，自动上传日志，并通过控制台对它们进行搜索。向下钻取崩溃事件，以查看堆栈跟踪。</dd>
</dl>
 

## 使用度量和事件
{: #usingmetrics}

使用**预定义度量**，可以回答如下问题：

*我有多少位新用户？*  
*有多少人正在积极使用我的应用程序？*  
*人们使用我的应用程序有多频繁？*  
*人们在一天中的哪个时间使用我的应用程序？*  
*我的用户最喜欢用的是什么设备模型？*  
*我应该何时淘汰对旧操作系统的支持？*  
*哪些应用程序有性能问题？*  

通过添加自己的**定制事件**，可以回答如下问题：  

*哪些功能最常用，哪些不常用？*  
*用户在哪里进入我的应用程序，又在哪里离开？*  
*用户查看最多的活动是哪些？*  
*用户在应用程序中完成工作流了吗？（例如，转换漏斗）*  

<!--Client-side logs and usage data are gathered automatically and sent to the Mobile Analytics -->
<!-- service on demand. Developers and -->
<!-- administrators can use the {{site.data.keyword.mobileanalytics_short}} service dashboard to view data that -->
<!-- is gathered by the client SDK. -->

<!--## Data visualization
{: data-visualization}

All data that is collected by the analytics service can be visualized through the {{site.data.keyword.mobileanalytics_short}} dashboard which is accessible from your {{site.data.keyword.Bluemix_notm}} dashboard by clicking your IBM {{site.data.keyword.mobileanalytics_short}} service tile instance. You can also create custom charts, based on data that is collected by the analytics service in the dashboard. In addition to an at-a-glance view of your mobile analytics, the analytics feature includes the capability to perform a raw search against client logs, captured client crash data, and any extra data that you explicitly provide through client API function calls that feed into the {{site.data.keyword.mobileanalytics_short}} service. -->

># 相关链接 {:class="linklist"}
<!-->## 教程和样本 {:id="samples"}-->
<!-->* [Link1](https://github.com/)-->
>
># 相关链接 {:class="linklist"}
>## 相关链接 {:id="general"}
## SDK
<!-- Links to SDK download and SDK Developer Guide -->
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core )  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)  
>
>{:elementKind="article" id="rellinks"}
