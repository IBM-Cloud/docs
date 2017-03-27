---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 在 Bluemix 中进行日志记录
{: #logging_bmx_ov}

{{site.data.keyword.Bluemix_notm}} 日志记录功能集成在平台中，并且会对云资源自动启用数据收集。缺省情况下，{{site.data.keyword.Bluemix_notm}} 会收集并显示应用程序、应用程序运行时以及运行这些应用程序的计算运行时的日志。
{:shortdesc}

您可以使用 {{site.data.keyword.Bluemix_notm}} 中的日志记录功能来了解云平台的行为以及其中所运行的资源。无需进行特殊检测，即可收集标准输出和标准错误日志。例如，可以使用日志来为应用程序提供审计跟踪，检测服务中的问题，识别漏洞，对应用程序部署和运行时行为进行故障诊断，检测运行应用程序的基础架构中的问题，在云平台中的组件之间跟踪应用程序，以及检测可用于提前制止可能影响服务 SLA 的操作的模式。

在云中运行应用程序时，可能无法通过 SSH 或 FTP 连接到运行应用程序的基础架构以访问日志，例如在 Cloud Foundry 中运行应用程序时。另一方面，您可以在 {{site.data.keyword.containershort}}（{{site.data.keyword.Bluemix_notm}} 中提供的另一个计算运行时）中运行应用程序, 在其中可以通过 SSH 进行连接并访问日志。不管使用的是哪种计算运行时，访问日志都至关重要；{{site.data.keyword.Bluemix_notm}} 提供了对云平台中的日志进行可视化和分析的通用经验。

{{site.data.keyword.Bluemix_notm}} 会记录由 Cloud Foundry 平台和 Cloud Foundry 应用程序生成的日志数据。在日志中，可以查看为应用程序生成的错误、警告和参考消息。有关在 Cloud Foundry 中进行日志记录的更多信息，请参阅[在 Bluemix 中为 Cloud Foundry 应用程序进行日志记录](logging_cf_apps.html#logging_bluemix_cf_apps)。

{{site.data.keyword.Bluemix_notm}} 会记录由 {{site.data.keyword.containershort}} 生成的日志数据。有关在 {{site.data.keyword.containershort}} 中进行日志记录的更多信息，请参阅[在 {{site.data.keyword.containershort}} 中进行日志记录](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_logs)。   


通过使用 {{site.data.keyword.Bluemix_notm}} 提供的日志记录功能，可以执行以下操作：

* 了解云资源及其执行和运行的方式。
* 定义趋势，以帮助确定需要采取措施的场景。
* 定义应用程序的数据跟踪，例如可以用于审计的跟踪。
* 减少在应用程序中找到问题并进行修复所需的时间和精力。 
* 监视应用程序在云平台中的部署。
* 检测服务或应用程序停机或崩溃情况。
* 关注应用程序执行和数据流。
* 识别应用程序中的漏洞。
* 检测基础架构中的问题。
* 检测应用程序运行时中的问题。
