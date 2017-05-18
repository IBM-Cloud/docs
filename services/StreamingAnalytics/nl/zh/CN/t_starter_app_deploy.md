---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 在 {{site.data.keyword.Bluemix_short}} 上部署入门模板应用程序
{: #starterapps_deploy}

您可以将其中一个 {{site.data.keyword.streaminganalyticsshort}} 入门模板应用程序推送并部署到 {{site.data.keyword.Bluemix_short}} 云。
{:shortdesc}

开始之前，请先使得 {{site.data.keyword.Bluemix_short}} 准备好可以部署 {{site.data.keyword.streaminganalyticsshort}} 入门模板应用程序：

* [安装 cf 命令行工具](https://github.com/cloudfoundry/cli/releases)。
* 在 {{site.data.keyword.Bluemix_short}} 中创建应用程序，将 {{site.data.keyword.streaminganalyticsshort}} 服务添加到应用程序，并重新编译打包应用程序：

	* 要部署“事件检测”入门模板应用程序，可使用 {{site.data.keyword.sdk4node}} 运行时创建应用程序。
	* 要部署“NYC 交通”入门模板应用程序，可使用 Liberty for Java™ 运行时创建应用程序。


请记住为应用程序指定的名称，稍后需要此名称。

{{site.data.keyword.streaminganalyticsshort}} 提供两个样本应用程序，使您可以开始使用服务。


“事件检测”入门模板应用程序会分析实时流中的天气相关数据，并显示分析的状态和结果。
该应用程序以 {{site.data.keyword.sdk4node}} 编写。有关如何使用“事件检测”入门模板应用程序的更多详细信息，请参阅[检测实时数据流中的复杂事件](https://www.ibm.com/developerworks/library/ba-bluemix-detect-complex-events-from-data-stream-trs/index.html)。

“NYC 交通”入门模板应用程序会从公共 Web 站点读取并分析交通数据。该应用程序以 Liberty for Java™ 编写。有关如何使用“NYC 交通”入门模板应用程序的更多详细信息，请参阅 [{{site.data.keyword.streaminganalyticsfull}} Starter Application](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-starter-application/)。

要将入门模板应用程序下载并部署到 {{site.data.keyword.Bluemix_short}}：

1. 下载[事件检测](https://hub.jazz.net/project/streamscloud/EventDetection/overview)或 [NYC 交通](https://hub.jazz.net/project/streamscloud/NYCTraffic/overview)入门模板应用程序。
2. 在命令行上，转至项目目录。
  <pre><code>cd myapp</code></pre>
  {:pre}

3. 重命名项目目录，以匹配您为 {{site.data.keyword.Bluemix_short}} 中应用程序所提供的名称。
4. 连接到 {{site.data.keyword.Bluemix_short}}：
  <pre><code>cf api https://api.DomainName</code></pre>
  {:pre}

5. 登录到 {{site.data.keyword.Bluemix_short}} 并在提示时设置目标组织：

  <pre><code>cf login</code></pre>
  {:pre}

6. 部署应用程序：
  <pre><code>cf push myapp</code></pre>
  {:pre}

7. 转至可从 {{site.data.keyword.Bluemix_short}} 仪表板访问的应用程序概述页面，以验证应用程序已成功启动。
8. 启动应用程序，以在浏览器中进行查看。您可以在应用程序概述页面上，找到应用程序的 URL（或“路径”）。


既然您的应用程序已在运行中，那么您可以转至服务仪表板，以查看 {{site.data.keyword.streaminganalyticsshort}} 实例的状态并获取故障诊断信息。要访问服务仪表板，请转至 {{site.data.keyword.Bluemix_short}} 仪表板，并单击应用程序概述页面上的 {{site.data.keyword.streaminganalyticsshort}} 磁贴。

