---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 在 Bluemix 中对 Cloud Foundry 应用程序进行日志记录
{: #logging_bluemix_cf_apps}

在 {{site.data.keyword.Bluemix}} 中，可以通过 {{site.data.keyword.Bluemix}}“仪表板”、Kibana 以及命令行界面来查看、过滤和分析日志。此外，还可以将日志记录传送到外部日志管理工具。
{:shortdesc}

在云平台即服务 (PaaS)（如 {{site.data.keyword.Bluemix_notm}} 上的 Cloud Foundry）中运行应用程序时，无法通过 SSH 或 FTP 连接到运行应用程序的基础架构以访问日志。该平台由云提供者进行控制。在 {{site.data.keyword.Bluemix_notm}} 上运行的 Cloud Foundry 应用程序使用 Loggregator 组件从 Cloud Foundry 基础架构内部转发日志记录。Loggregator 会自动选取 STDOUT 和 STDERR 数据。可以通过 {{site.data.keyword.Bluemix}}“仪表板”、Kibana 以及命令行界面来可视化和分析这些日志。

下图显示了 {{site.data.keyword.Bluemix_notm}} 中 Cloud Foundry 应用程序的日志记录的高级别视图：

![CF 应用程序的高级别组件概览图](images/logging_cf_apps_ov.jpg)
 
使用 Cloud Foundry 基础架构在 {{site.data.keyword.Bluemix_notm}} 上运行应用程序时，会自动启用 Cloud Foundry 应用程序的日志记录。要查看 Cloud Foundry 运行时日志，必须将日志写入 STDOUT 和 STDERR。有关更多信息，请参阅[通过 CF 应用程序进行运行时应用程序日志记录](cfapps/logging_writing_to_log_from_cf_app.html#logging_writing_to_log_from_cf_app)。

可以选择以下任一方法来分析 Cloud Foundry 应用程序的日志：

* 在 {{site.data.keyword.Bluemix_notm}} 中分析日志以查看应用程序的最新活动。
    
    在 {{site.data.keyword.Bluemix}} 中，可以通过可用于每个 Cloud Foundry 应用程序的**日志**选项卡来查看、过滤和分析日志。有关更多信息，请参阅[通过 Bluemix 仪表板分析 CF 应用程序日志](logging_view_dashboard.html#analyzing_logs_bmx_ui)。
    
* 在 Kibana 中分析日志以执行高级分析任务。
    
    在 {{site.data.keyword.Bluemix}} 中，可以使用 Kibana（一种开放式源代码分析和可视化平台）通过各种图形（例如，图表和表）来监视、搜索、分析和可视化数据。有关更多信息，请参阅[在 Kibana 中分析日志](logging_view_kibana3.html#analyzing_logs_Kibana)。

* 通过 CLI 分析日志可使用命令以编程方式管理日志。
    
    在 {{site.data.keyword.Bluemix}} 中，可以通过命令行界面使用 **cf logs** 命令来查看、过滤和分析日志。有关更多信息，请参阅[通过命令行界面分析 Cloud Foundry 应用程序日志](logging_view_cli.html#analyzing_logs_cli)。

{{site.data.keyword.Bluemix_notm}} 会保留数量有限的日志信息。记录信息时，较新的信息会将旧的信息替换掉。如果您必须符合的组织或行业策略要求您保留部分或所有日志信息以用于审计或其他用途，那么可以将日志传送到外部日志主机，例如第三方日志管理服务或其他主机。有关更多信息，请参阅[配置外部日志主机](logging_view_external.html#viewing_logs_external)。



