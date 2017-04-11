---

copyright:
  years: 2017
lastupdated: "2017-02-28"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# {{site.data.keyword.mqa}}（已弃用）入门
{: #gettingstartedtemplate}

**{{site.data.keyword.mqafull}} 服务已弃用。** 有关状态和日期的更多信息，请参阅[弃用 Bluemix Mobile Quality Assurance 博客条目![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/blogs/bluemix/?p=72728){: new_window}。
{:deprecated}

{{site.data.keyword.mqafull}} 为团队提供相应功能来捕获测试人员和在线用户体验，从而持续构建和交付高质量的移动应用程序。
{: shortdesc}

要快速启动和运行 {{site.data.keyword.mqa}} 服务，请遵循下列步骤：

1. 在创建<!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)--> {{site.data.keyword.mqa}} 服务的实例之后，即可访问 {{site.data.keyword.mqa}} Console，方法是单击 {{site.data.keyword.Bluemix}}“仪表板”**服务**部分中的磁贴。

	此时 {{site.data.keyword.mqa}} 服务即会启动。

2. 选择**添加 MQA 应用程序**并为该应用程序提供名称，将移动应用程序添加到 {{site.data.keyword.mqa}} 实例。

3. 下载 {{site.data.keyword.mqa}} [客户机 SDK ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/support/docview.wss?uid=swg27044490){: new_window} 并通过继续以下其中一个过程，完成对应用程序的安装操作：

	* [对 MQA 安装 Android 应用程序](mqa_inst_app_android.html)
	* [对 MQA 安装 iOS 应用程序](mqa_inst_app_ios.html)
	* [对 MQA 安装 Cordova 应用程序](mqa_inst_app_cord.html)

	使用单个 SDK 为预生产和生产应用程序配置监视功能。您可以使用 `MODE:` 参数为预生产方式指定 *QA*，或者为生产方式指定 *MARKET*。指定预生产方式，使内部测试人员可以提供有关应用程序所发生的错误和崩溃的详细信息。指定生产方式，使用户可以提供有关应用程序的详细信息。如果应用程序已处于生产阶段，那么 {{site.data.keyword.mqa}} 可方便直接在应用程序中获取用户反馈。

4. 对应用程序执行安装操作之后，可以选择 {{site.data.keyword.mqa}} 服务实例界面上的以下其中一个选项，来对其查看更详细的质量信息：

	<dl>
		<dt><strong>会话</strong></dt>
		<dd>查看有关会话期间的崩溃、错误、反馈和设备状态的信息。请参阅 IBM Knowledge Center 中的[查看会话详细信息 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/t_ViewingSessionDetails.html){: new_window}，以获取更多信息。</dd>
		<dt>![](/images/cap_crashicon.jpg) <strong>崩溃</strong></dt>
		<dd>查看有关导致崩溃的事件的信息。请参阅 IBM Knowledge Center 中的[崩溃报告 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_CrashReports.html){: new_window}，以获取更多信息。</dd>
		<dt>![](/images/cap_bugicon.jpg) <strong>错误</strong></dt>
		<dd>查看用户报告的信息，例如错误报告、截屏和设备详细信息。请参阅 IBM Knowledge Center 中的[错误报告 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_BugReports.html){: new_window}，以获取更多信息。</dd>
		<dt>![](/images/cap_feedbackicon.jpg) <strong>反馈</strong></dt>
		<dd>查看用户反馈响应，以了解反馈者和反馈时间。请参阅 IBM Knowledge Center 中的[用户反馈 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_UserFeedback.html){: new_window}，以获取更多信息。</dd>
		<dt><strong>观点分数（如果已配置）</strong></dt>
		<dd>查看随时间和版本变化的用户观点分数，以监视、衡量和提高应用程序质量。请参阅 IBM Knowledge Center 中的[用户观点 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/UserSentiment.html){: new_window}，以获取更多信息。</dd>
		<dt><strong>已注册的设备</strong></dt>
		<dd>查看测试会话期间使用的设备列表以及有关这些设备的信息。请参阅 IBM Knowledge Center 中的[查看设备信息 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/t_ManagingDevices.html){: new_window}，以获取更多信息。</dd>
	</dl>

	这些度量值包含以下数据：

	* 崩溃、错误、反馈和会话的预生产数据。
	* 崩溃、反馈、观点和会话的生产数据。

	![您可以查看应用程序质量度量的界面的截屏](images/quality_metrics_saas4.gif)

	通过查看应用程序的这些信息，可以确定是否进一步调查特定问题。例如，如果应用程序的崩溃率到达峰值，那么可以单击崩溃率以在此应用程序的崩溃报告上查看更详细信息。

5. 要查看应用程序的总观点分数，必须配置观点分析：

	1. 在*观点分数*部分中，单击链接以配置所选应用程序的观点分析。

	2. 在“应用程序详细信息”页面中，[配置观点分析 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/tEnablingUserSentiment.html){: new_window} 并保存更改。


# 相关链接
{: #rellinks notoc}

## 教程和样本
{: #samples notoc}

* [视频：Bluemix 中的 Mobile Quality Assurance 入门 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.youtube.com/watch?v=zHRfGatcKPM){: new_window}  
* [视频：Mobile Quality Assurance 中的观点分析 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.youtube.com/watch?v=uhkqb8BIn6k){: new_window}
* [developerWorks：添加 IBM Mobile QualityAssurance 以用作移动质量方案 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/developerworks/library/mo-mqa/index.html){: new_window}
* [developerWorks：构建有效的移动应用程序：专家面板中的五大提示 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/developerworks/library/mo-mqa-tips/index.html){: new_window}
* [developerWorks：构建不完美的移动应用程序 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/developerworks/library/mo-build-imperfect-mobile-app/){: new_window}
* [developerWorks：DevOps 应对移动应用程序挑战，提供最佳实践 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/developerworks/library/mo-bestdevops-mobileapps/index.html){: new_window}
* [样本：bluelist-mqa ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://hub.jazz.net/project/mobilecloud/bluelist-mqa/overview){: new_window}
