---



copyright:

  years: 2016, 2017

lastupdated: "2016-10-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

<!-- audience blue staging only begin -->

# 在 Dedicated 和 Local 中对 Cloud Foundry 应用程序进行监视和日志记录
{: #dedicated_apps_ml_ov}


在 {{site.data.keyword.Bluemix_dedicated_notm}} 和 {{site.data.keyword.Bluemix_local_notm:}} 中，Cloud Foundry 应用程序随附内置日志记录功能。您可以在 {{site.data.keyword.Bluemix_notm}} 控制台上查看从应用程序收集的数据。
{:shortdesc}

Cloud Foundry 应用程序使用 Cloud Foundry loggregator 从应用程序外部监视和转发日志。您无需在应用程序内部安装代理程序。

## 硬件需求


| **需求** |    **1 个节点**     | **3 个节点（针对高可用性）** |
|-----------------|-------------------|-------------------|
vCPU | 19 | 57 |
内存 | 80 GB | 240 GB |
本地存储器 | 2.98 TB | 8.94 TB |
{: caption="表 1. 记录 {{site.data.keyword.Bluemix_local_notm:} 的硬件需求}" caption-side="top"}

## 设置

在 {{site.data.keyword.Bluemix}} Dedicated 和 {{site.data.keyword.Bluemix}} Local 中，缺省情况下所有应用程序的日志都处于活动状态。要查看有关读取标准日志的信息，请参阅“为 Cloud Foundry 上运行的应用程序进行日志记录”。此外，还可以在 {{site.data.keyword.Bluemix}} Dedicated 和 {{site.data.keyword.Bluemix}} Local 环境中启用高级日志记录功能。

## 日志保留时间

在 {{site.data.keyword.Bluemix}} Dedicated 和 {{site.data.keyword.Bluemix}} Local Cloud Foundry 应用程序中，缺省情况下日志数据存储 30 天。

## 在 {{site.data.keyword.Bluemix}} Dedicated 和 {{site.data.keyword.Bluemix}} Local 中查看 Cloud Foundry 应用程序的日志
{: #dedicated_apps_ml_logs_dash}

您可以查看正在 {{site.data.keyword.Bluemix_notm}} Dedicated 和 {{site.data.keyword.Bluemix_notm}} Local 上运行的应用程序的日志。
{:shortdesc}

要查看应用程序日志，请执行以下步骤。
1. 选择正在运行的应用程序。
2. 单击**日志**。在**日志**视图中，可以查看正在运行的应用程序的日志。
4. 单击**高级视图**按钮。**高级视图**将使用 Kibana 来显示日志的更详细视图；Kibana 是使用日志和带时间戳记的数据来创建定制可视化的可视化工具。有关使用高级视图的更多信息，请参阅 [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) 文档。

接下来，可以定制 Kibana 仪表板。有关更多信息，请参阅[在 Kibana 仪表板中定制日志显示](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_dash_logs_custom)。

<!-- audience blue staging only end comment -->
