---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 监视和日志记录
{: #monitoringandlogging}

{{site.data.keyword.Bluemix}} 是 {{site.data.keyword.IBM_notm}} 的云计算平台，用于构建、运行和管理应用程序与服务。{{site.data.keyword.Bluemix}} 集平台即服务 (PaaS) 与基础架构即服务 (IaaS) 于一体。此外，{{site.data.keyword.Bluemix}} 具有包含丰富云服务的目录，这些服务可以轻松与 PaaS 和 IaaS 相集成，用于迅速构建业务应用程序。{{site.data.keyword.Bluemix}} 包含用于整个平台的集成日志记录和监视服务。
{:shortdesc}

{{site.data.keyword.Bluemix}} 在不同的计算服务（例如，Cloud Foundry 和 {{site.data.keyword.containershort}}）之间提供了日志记录和监视服务。您可以在任何计算运行时中开发、运行和管理应用程序，而避开了在开发和启动应用程序时通常会牵涉到的构建和维护基础架构的复杂性。 

您可以使用 {{site.data.keyword.Bluemix}} 中的监视功能从环境和应用程序自动收集并度量关键度量值。无需进行特殊检测，即可收集度量值。例如，可以使用性能度量值提供的信息来监视服务在云中的运行情况，检测资源瓶颈，并密切关注服务级别协议 (SLA)。例如，分析服务的性能数据时，可以检测会导致资源瓶颈并因而影响客户的服务 SLA 的情况。通过及早采取措施，可以避免会对业务造成负面影响的情况。  

您可以使用 {{site.data.keyword.Bluemix}} 中的日志记录功能来了解云平台的行为以及其中所运行的资源。无需进行特殊检测，即可收集标准输出和标准错误日志。例如，可以使用日志来为应用程序提供审计跟踪，检测服务中的问题，识别漏洞，对应用程序部署和运行时行为进行故障诊断，检测运行应用程序的基础架构中的问题，在云平台中的组件之间跟踪应用程序，以及检测可用于提前制止可能影响服务 SLA 的操作的模式。

## 监视计算基础架构资源
{: #monitoring_sl_ov}

每个 {{site.data.keyword.Bluemix_notm}} 服务器都包含始终可用的监视功能和易于阅读的报告。有关更多信息，请参阅[基础架构监控和报告 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/cloud-computing/bluemix/infrastructure-monitoring){: new_window}。



## 在 {{site.data.keyword.Bluemix}} 中监视计算服务
{: #monitoring_bmx_ov}

缺省情况下，{{site.data.keyword.Bluemix}} 会收集并显示 CPU 使用率、内存利用率和网络 I/O 的性能度量值。这些度量值提供了有关各个云资源的性能的信息。您可以通过 {{site.data.keyword.Bluemix}} UI 在云环境中监视这些资源的性能。还可以查看近实时数据和历史数据。可以为其中任意度量值配置警报和通知。

您还可以配置并监视更多性能度量值。您可以在 {{site.data.keyword.Bluemix}} 外部对这些度量值进行可视化和分析。例如，在 {{site.data.keyword.containershort}} 中运行应用程序时，可以使用 Grafana 来监视更多度量值。您可以按要可视化和分析性能数据的空间或容器实例来定制仪表板。

![在 {{site.data.keyword.Bluemix}} 中运行的容器的 Grafana 监视视图](images/monitoring_default_container_grafana_view.jpg)

可以使用 {{site.data.keyword.Bluemix}} 平台监视执行以下操作：

* 深入了解应用程序运行情况，例如，检测潜在瓶颈或何时需要升级。
* 定义可用于计划云平台中的未来应用程序需求的趋势。

有关监视在 Cloud Foundry 上运行的应用程序的更多信息，请参阅[监视在 Cloud Foundry 上运行的应用程序](monitoring_cf_apps.html#monitoring_bluemix_apps)。

有关在 {{site.data.keyword.containershort}} 中进行监视的更多信息，请参阅[在 {{site.data.keyword.containershort}} 中进行监视](/docs/containers/monitoringandlogging/container_ml_monitor.html#container_ml_monitor)。   

## 在 {{site.data.keyword.Bluemix}} 中进行日志记录
{: #logging_bmx_ov}

{{site.data.keyword.Bluemix}} 日志记录功能集成在平台中，并且会对云资源自动启用数据收集。缺省情况下，{{site.data.keyword.Bluemix}} 会收集并显示应用程序、应用程序运行时以及运行这些应用程序的计算运行时的日志。 

在云中运行应用程序时，可能无法通过 SSH 或 FTP 连接到运行应用程序的基础架构以访问日志，例如在 Cloud Foundry 中运行应用程序时。另一方面，您可以在 {{site.data.keyword.containershort}}（{{site.data.keyword.Bluemix}} 中提供的另一个计算运行时）中运行应用程序，在其中可以通过 SSH 进行连接并访问日志。不管使用的是哪种计算运行时，访问日志都至关重要；{{site.data.keyword.Bluemix}} 提供了对云平台中的日志进行可视化和分析的通用经验。

{{site.data.keyword.Bluemix_notm}} 会记录由 Cloud Foundry 平台和 Cloud Foundry 应用程序生成的日志数据。在日志中，可以查看为应用程序生成的错误、警告和参考消息。有关在 Cloud Foundry 中进行日志记录的更多信息，请参阅[在 {{site.data.keyword.Bluemix}} 中为 Cloud Foundry 应用程序进行日志记录](logging_cf_apps.html#logging_bluemix_cf_apps)。

{{site.data.keyword.Bluemix_notm}} 会记录由 {{site.data.keyword.containershort}} 生成的日志数据。有关在 {{site.data.keyword.containershort}} 中进行日志记录的更多信息，请参阅[在 {{site.data.keyword.containershort}} 中进行日志记录](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_logs)。   


通过使用 {{site.data.keyword.Bluemix}} 提供的日志记录功能，可以执行以下操作：

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


