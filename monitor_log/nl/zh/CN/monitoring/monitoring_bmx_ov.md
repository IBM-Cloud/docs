---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 在 Bluemix 中进行监视
{: #monitoring_bmx_ov}

缺省情况下，{{site.data.keyword.Bluemix_notm}} 会收集并显示 CPU 使用率、内存利用率和网络 I/O 的性能度量值。这些度量值提供了有关各个云资源的性能的信息。您可以通过 {{site.data.keyword.Bluemix_notm}} UI 在云环境中监视这些资源的性能。还可以查看近实时数据和历史数据。{:shortdesc}

您可以使用 {{site.data.keyword.Bluemix_notm}} 中的监视功能从环境和应用程序自动收集并度量关键度量值。无需进行特殊检测，即可收集度量值。例如，可以使用性能度量值提供的信息来监视服务在云中的运行情况，检测资源瓶颈，并密切关注服务级别协议 (SLA)。分析服务的性能数据时，可以检测会导致资源瓶颈并因而影响客户的服务 SLA 的情况。通过及早采取措施，可以避免会对业务造成负面影响的情况。  

您还可以配置并监视更多性能度量值。您可以在 {{site.data.keyword.Bluemix_notm}} 外部可视化和分析这些度量值。例如，在 {{site.data.keyword.containershort}} 中运行应用程序时，可以使用 Grafana 来监视更多度量值。可以按要可视化和分析性能数据的容器实例或空间来定制仪表板。

![在 {{site.data.keyword.Bluemix_notm}} 中运行的容器的 Grafana 监视视图](images/monitoring_default_container_grafana_view.jpg)

可以使用 {{site.data.keyword.Bluemix_notm}} 平台监视执行以下操作：

* 深入了解应用程序操作，例如检测潜在瓶颈或何时需要升级。
* 定义可用于计划云平台中的未来应用程序需求的趋势。

有关监视在 Cloud Foundry 上运行的应用程序的更多信息，请参阅[监视在 Cloud Foundry 上运行的应用程序](monitoring_cf_apps.html#monitoring_bluemix_apps)。

有关在 {{site.data.keyword.containershort}} 中进行监视的更多信息，请参阅[在 {{site.data.keyword.containershort}} 中进行监视](/docs/containers/monitoringandlogging/container_ml_monitor.html#container_ml_monitor)。   

