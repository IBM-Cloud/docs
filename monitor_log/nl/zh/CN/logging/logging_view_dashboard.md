---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-27"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 通过 Bluemix 控制台分析日志
{: #analyzing_logs_bmx_ui}

在 {{site.data.keyword.Bluemix}} 中，可以通过可用于每个 Cloud Foundry 应用程序或 Docker 容器的“日志”选项卡来查看、过滤和分析日志。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} Public 提供了集成的日志记录功能。例如，在 Cloud Foundry (CF) 中运行应用程序时，如果使用了 stdout 和 stderr，那么会从与应用程序交互的系统组件中捕获有关应用程序的日志数据，甚至捕获应用程序内的日志数据。

请考虑有关供分析的日志数据可用性和日志保留时间的以下信息：

* 在 {{site.data.keyword.Bluemix_notm}} Public 中，缺省情况下日志数据存储 7 天。 
* 每天最多可以存储 1 GB 的数据。 
* 缺省情况下，通过 {{site.data.keyword.Bluemix_notm}} 控制台可供分析的日志包含最近 24 小时的数据。

**提示：**要分析早于最近 24 小时的定制时间段内的数据，请参阅[使用 Kibana 进行高级日志分析](logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana)。 

##  导航至 Cloud Foundry 应用程序的日志
{: #launch_logs_tab_bmx_ui_cf}

要查看 Cloud Foundry 应用程序的部署或运行时日志，请完成以下步骤：

1. 在“应用程序”仪表板中，单击 Cloud Foundry 应用程序的名称。 
    
2. 在“应用程序详细信息”页面中，单击**日志**。
    
    在**日志**选项卡中，可以查看应用程序的最近日志或实时跟踪日志。此外，可以按组件（日志类型）、按应用程序实例标识以及按错误来过滤日志。
    

##  导航至 Docker 容器的日志
{: #launch_logs_tab_bmx_ui_containers}

要查看 Docker 容器的部署或运行时日志，请完成以下步骤：

1. 在“应用程序”仪表板中，单击单个容器或容器组。 
    
2. 在“应用程序详细信息”页面中，单击**监视和日志**。

3. 选择**日志记录**选项卡。
    
    在**日志记录**选项卡中，可以查看容器的最近日志或实时跟踪日志。 

## CF 应用程序日志的日志格式
{: #log_format_cf}

{{site.data.keyword.Bluemix_notm}} Cloud Foundry 应用程序的日志以固定格式显示，类似于以下模式：

<code><var class="keyword varname">Component</var>/<var class="keyword varname">instanceID</var>/<var class="keyword varname">message</var>/<var class="keyword varname">timestamp</var></code>

每个日志条目都包含以下字段：

| 字段 | 描述 |
|-------|-------------|
| 时间戳记 | 日志语句的时间。时间戳记定义为精确到毫秒。 |
| 组件 | 用于生成日志的组件。有关不同组件的列表，请参阅 [CF 应用程序的日志源](logging_cf_apps.html#logging_bluemix_cf_apps_log_sources)。<br> 每个组件类型后跟一个斜杠和一个数字，数字指示应用程序实例。0 表示分配给第一个实例的数字，1 表示分配给第二个实例的数字，依此类推。 |
| 消息 | 组件发出的消息。消息根据上下文而变化。 |
{: caption="表 1. CF 应用程序日志条目字段" caption-side="top"}


## 容器日志的日志格式
{: #log_format_containers}

容器的日志以固定格式显示，类似于以下模式：

<code><var class="keyword varname">timestamp</var>/<var class="keyword varname">machine</var>/<var class="keyword varname">message</var>  </code>

每个日志条目都包含以下字段：

| 字段 | 描述 |
|-------|-------------|
| 日期/时间 | 日志语句的时间。时间戳记定义为精确到毫秒。 |
| 机器 | 运行容器所在主机的主机名。 |
| 消息 | 发出的消息。消息根据上下文而变化。 |
{: caption="表 2. Docker 容器日志条目字段" caption-side="top"}

