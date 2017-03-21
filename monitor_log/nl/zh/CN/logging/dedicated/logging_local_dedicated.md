---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 在 Dedicated 和 Local 中为 CF 应用程序进行日志记录
{: #hybrid_apps_logs_ov}

在 {{site.data.keyword.Bluemix_dedicated_notm}} 和 {{site.data.keyword.Bluemix_local_notm}} 中，Cloud Foundry 应用程序随附内置日志记录功能。您可以在 {{site.data.keyword.Bluemix_notm}} 控制台上查看从应用程序收集的数据。
{:shortdesc}

Cloud Foundry 应用程序使用 Cloud Foundry loggregator 从应用程序外部监视和转发日志。您无需在应用程序内部安装代理程序。

## 硬件需求


| **需求** |    **1 个节点**     | **3 个节点（针对高可用性）** |
|-----------------|-------------------|-------------------|
| vCPU | 19 | 57 |
| 内存 | 80 GB | 240 GB |
| 本地存储器 | 2.98 TB | 8.94 TB |
{: caption="表 2. 记录 {{site.data.keyword.Bluemix_local_notm}} 的硬件需求" caption-side="top"}

## 设置

在 {{site.data.keyword.Bluemix_dedicated_notm}} 和 {{site.data.keyword.Bluemix_local_notm}} 中，缺省情况下所有应用程序的日志都处于活动状态。要查看有关读取标准日志的信息，请参阅[为 Cloud Foundry 上运行的应用程序进行日志记录](../logging_cf_apps.html#logging_bluemix_cf_apps)。此外，还可以在 {{site.data.keyword.Bluemix_dedicated_notm}} 和 {{site.data.keyword.Bluemix_local_notm}} 环境中启用高级日志记录功能。

* 要确认是否在 {{site.data.keyword.Bluemix_dedicated_notm}} 和 {{site.data.keyword.Bluemix_local_notm}} 环境中启用了高级日志记录功能，请执行[查看日志](#hybrid_apps_logs_dash)中的步骤。如果没有**高级视图**按钮，说明此功能未启用。

* 要向环境添加高级日志记录功能，请执行 [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) 或 [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) 文档中的步骤。

## 日志保留时间

在 {{site.data.keyword.Bluemix_dedicated_notm}} 和 {{site.data.keyword.Bluemix_local_notm}} Cloud Foundry 应用程序中，缺省情况下日志数据存储 30 天。

## 在 Dedicated 和 Local 中查看 Cloud Foundry 应用程序的日志
{: #hybrid_apps_logs_dash}

您可以查看正在 {{site.data.keyword.Bluemix_dedicated_notm}} 和 {{site.data.keyword.Bluemix_local_notm}} 上运行的应用程序的日志。
{:shortdesc}

要查看应用程序日志，请执行以下步骤。
1. 选择正在运行的应用程序。
2. 单击**日志**。在**日志**视图中，可以查看正在运行的应用程序的日志。
4. 单击**高级视图**按钮。**高级视图**将使用 Kibana 来显示日志的更详细视图；Kibana 是使用日志和带时间戳记的数据来创建定制可视化的可视化工具。有关使用高级视图的更多信息，请参阅 [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) 文档。

接下来，可以定制 Kibana 仪表板。有关更多信息，请参阅[在 Kibana 中分析日志](../logging_view_kibana3.html#analyzing_logs_Kibana3)。
