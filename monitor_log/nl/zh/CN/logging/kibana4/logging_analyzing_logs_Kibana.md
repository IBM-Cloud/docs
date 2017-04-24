---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 使用 Kibana 进行高级日志分析
{:#analyzing_logs_Kibana}

在 {{site.data.keyword.Bluemix}} 中，可以使用 Kibana（一种开放式源代码分析和可视化平台）通过各种图形（例如，图表和表）来监视、搜索、分析和可视化数据。使用 Kibana 可执行高级分析任务。
{:shortdesc}

您可以使用以下任何一种方法来启动 Kibana：

* 通过 {{site.data.keyword.Bluemix_notm}}

    可以在 Kibana 中特定 CF 应用程序的上下文中启动到该特定应用程序的日志。
    
    可以在 Kibana 中特定 Docker 容器的上下文中启动到该特定容器的日志。 
    
    对于 CF 应用程序，用于过滤可在 Kibana 中进行分析的数据的查询会检索 Cloud Foundry 应用程序的日志条目。Kibana 缺省显示的日志信息全部与单个 Cloud Foundry 应用程序及其所有实例相关联。 
    
    对于容器，用于过滤可在 Kibana 中进行分析的数据的查询会检索容器的所有实例的日志条目。Kibana 缺省显示的日志信息全部与单个容器或容器组及其所有实例相关联。 
    
    有关更多信息，请参阅[通过 Bluemix 仪表板访问 Kibana 仪表板](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix)。

* 通过直接浏览器链接

    您可能希望启动 Kibana，以使您看到的数据从提供的 {{site.data.keyword.Bluemix_notm}} 空间内的服务聚集日志。
    
    用于过滤仪表板中所显示数据的查询会检索 {{site.data.keyword.Bluemix_notm}} 组织中空间的日志条目。Kibana 显示的日志信息包括在您登录到的 {{site.data.keyword.Bluemix_notm}} 组织空间内部署的所有资源的记录。 
    
    有关更多信息，请参阅[通过 Web 浏览器访问 Kibana 仪表板](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser)。
    
    通过浏览器启动 Kibana 时，可以选择使用 Kibana 4 或 Kibana 3。**注：**不推荐使用 Kibana 3。有关使用 Kibana 3 来分析日志的信息，请参阅[在 Kibana 3 中分析日志（不推荐）](../logging_view_kibana3.html#analyzing_logs_Kibana3)。

<br>    

Kibana 是一种基于浏览器的界面，在其中可以通过交互方式分析数据以及定制仪表板，随后可使用这些仪表板来分析日志数据并执行高级管理任务。 

Kibana 页面显示的数据受搜索约束。缺省数据集由预配置的索引模式进行定义。要过滤信息，可以添加新的搜索查询，并将过滤器应用于缺省数据集。然后，可以保存搜索以供未来复用。 

Kibana 包含可用于分析日志的不同页面：

| Kibana 页面 | 描述 |
|-------------|-------------|
| 发现 | 使用此页面可定义搜索，并通过表和直方图以交互方式分析日志。 |
| 可视化 | 使用此页面可创建可视化，例如图形和表；可以使用可视化来分析日志数据并比较结果。  |
| 仪表板 | 使用此页面可通过保存的可视化和搜索的集合来分析日志。  |

**注：**通过“可视化”页面或“仪表板”页面，一次只能分析一个整天的数据，尽管可以追溯 7 天。缺省情况下日志数据会存储 7 天。 

| Kibana 页面 | 时间段信息 |
|-------------|-------------------------|
| 发现 | 分析最长 7 天的数据。 |
| 可视化 | 分析 24 小时时间段的数据。<br> 可以过滤长度为 24 小时的定制时间段的日志数据。  |
| 仪表板 | 分析 24 小时时间段的数据。<br> 可以过滤长度为 24 小时的定制时间段的日志数据。<br> 设置的时间选取器会应用于仪表板中包含的所有可视化。 |


例如，下面说明了可以如何使用 Kibana 通过不同页面来显示有关空间中 CF 应用程序或容器的信息：

* 在“发现”页面中，可以定义新搜索查询并按查询应用过滤器。日志数据将通过表和直方图显示。可以使用这些可视化以交互方式分析数据。有关更多信息，请参阅[在 Kibana 中以交互方式分析日志](logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively)。

    可以通过日志字段（例如，message_type 和 instance_ID）来配置过滤器，并可以设置时间段。您可以动态启用或禁用这些过滤器。表和直方图将显示满足所启用的查询和过滤条件的日志条目。有关更多信息，请参阅[在 Kibana 中过滤日志](logging_kibana_filtering_logs.html#kibana_filtering_logs)。
    
* 在“可视化”页面中，可以定义新的搜索查询和可视化。

    要分析数据，可以基于现有搜索或新搜索来创建可视化。Kibana 包含可用于分析信息的不同类型的可视化，如表、趋势和直方图。每个可视化的用途各不相同。一些可视化组织成行，用于提供一个或多个查询的结果。另一些可视化则显示文档或定制信息。可视化中的数据可以是固定的，也可以在更新搜索查询时更改。可以在 Web 页面中嵌入可视化，也可以共享可视化。有关更多信息，请参阅[使用可视化分析日志](logging_kibana_visualizations.html#logging_kibana_visualizations)。

* 在“仪表板”页面中，可以同时定制、保存和共享多个可视化和搜索。 

    可以在仪表板中添加、除去和重新排列可视化。有关更多信息，请参阅[在 Kibana 中通过仪表板分析日志](logging_kibana_analize_logs_dashboard.html#kibana_analize_logs_dashboard)。
    
    定制 Kibana 仪表板后，可以通过其可视化对数据进行分析，然后保存以供未来复用。有关更多信息，请参阅[保存 Kibana 仪表板](logging_kibana_analize_logs_dashboard.html#save_Kibana_dashboard)。

在 Kibana 中还有*设置*页面，可用于配置 Kibana，以及保存、删除、导出和导入搜索、可视化和仪表板。

有关更多信息，请参阅 [Kibana 用户指南 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}。

**注：**支持 Kibana 4 和 Kibana 3。但不推荐使用 Kibana 3。


##  通过 Bluemix 仪表板访问 Kibana 仪表板
{: #launch_Kibana_from_bluemix}

用于过滤 Kibana 中所显示数据的查询会检索从中启动 Kibana 的 {{site.data.keyword.Bluemix_notm}} CF 应用程序或容器的日志条目。 

要在 Kibana 中查看 Cloud Foundry 应用程序或 Docker 容器的日志，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}}，然后在 {{site.data.keyword.Bluemix_notm}}“仪表板”中，单击应用程序名称或容器。 
    
2. 在 {{site.data.keyword.Bluemix_notm}} UI 中打开“日志”选项卡。

    * 对于 CF 应用程序，单击导航栏中的**日志**。 
    * 对于容器，选择导航栏中的**监视和日志**，然后单击**日志记录**选项卡。 
    
    这将打开“日志”选项卡。 
    
3. 单击**高级视图**。这将打开 **Kibana 4** 仪表板。

    缺省情况下，**发现**页面会装入所选的缺省索引模式，并将时间过滤器设置为最近 30 秒。搜索查询会设置为与 CF 应用程序或 Docker 容器的所有条目相匹配。

    如果“发现”页面未显示任何日志条目，请调整时间选取器。有关更多信息，请参阅[设置时间过滤器](logging_kibana_set_time_filter.html#set_time_filter)。

有关 Kibana 的更多信息，请参阅 [Kibana 用户指南](https://www.elastic.co/guide/en/kibana/current/index.html)。

##  通过 Web 浏览器访问 Kibana 仪表板
{: #launch_Kibana_from_browser}

用于过滤 Kibana 中所显示数据的查询会检索 {{site.data.keyword.Bluemix_notm}} 组织中空间的日志条目。Kibana 显示的日志信息包括在您登录到的 {{site.data.keyword.Bluemix_notm}} 组织空间内部署的所有资源的记录。

要通过浏览器启动 Kibana，请完成以下步骤：

1. 打开 [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) 以登录到 Kibana 用户界面。

2. 选择要用于分析日志的 Kibana 版本。
    * 选择 **Kibana 4** 选项卡以使用 Kibana 4。这将打开“发现”页面。有关更多信息，请参阅 [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively)。
    * 选择 **Kibana 3** 选项卡以使用 Kibana 3。这将打开缺省 Kibana 仪表板。有关定制 Kibana 3 仪表板的更多信息，请参阅[此博客帖子](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/)。
     
        **注：**不推荐使用 Kibana 3。

    如果“发现”页面未显示任何日志条目，请调整时间选取器。有关更多信息，请参阅[设置时间过滤器](logging_kibana_set_time_filter.html#set_time_filter)。

有关 Kibana 的更多信息，请参阅 [Kibana 用户指南 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}。

