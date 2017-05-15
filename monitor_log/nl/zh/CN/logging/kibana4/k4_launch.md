---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 导航至 Kibana 仪表板
{: #k4_launch}

可以通过 {{site.data.keyword.Bluemix}} UI 或直接通过 Web 浏览器启动 Kibana。
{:shortdesc}

通过 {{site.data.keyword.Bluemix_notm}} 启动 Kibana 可在从中启动 Kibana 的资源的上下文中查看和分析数据。例如，可以在 Kibana 中特定 CF 应用程序的上下文中启动到该特定应用程序的日志，也可以在 Kibana 中特定 Docker 容器的上下文中启动到该特定容器的日志。 
    
如果要查看从提供的 {{site.data.keyword.Bluemix_notm}} 空间内各服务中聚集的日志数据，请通过直接浏览器链接启动 Kibana。用于过滤仪表板中所显示数据的查询会检索 {{site.data.keyword.Bluemix_notm}} 组织中空间的日志条目。Kibana 显示的日志信息包括在您登录到的 {{site.data.keyword.Bluemix_notm}} 组织空间内部署的所有资源的记录。 

有关 Kibana 的更多信息，请参阅 [Kibana 用户指南 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}。
    

##  通过 Bluemix 仪表板导航至 Kibana 仪表板
{: #launch_Kibana_from_bluemix}

用于过滤 Kibana 中所显示数据的查询会检索从中启动 Kibana 的 {{site.data.keyword.Bluemix_notm}} CF 应用程序或 Docker 容器的日志条目。 

要在 Kibana 中查看 Cloud Foundry 应用程序或 Docker 容器的日志，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}}，然后在 {{site.data.keyword.Bluemix_notm}}“仪表板”中，单击应用程序名称或容器。 
    
2. 在 {{site.data.keyword.Bluemix_notm}} UI 中打开“日志”选项卡。

    * 对于 CF 应用程序，单击导航栏中的**日志**。 
    * 对于容器，选择导航栏中的**监视和日志**，然后单击**日志记录**选项卡。 
    
    这将打开“日志”选项卡。 
    
3. 单击**高级视图**。这将打开 **Kibana 4** 仪表板。

    缺省情况下，**发现**页面会装入所选的缺省索引模式，并将时间过滤器设置为最近 30 秒。搜索查询会设置为与 CF 应用程序或 Docker 容器的所有条目相匹配。

    如果“发现”页面未显示任何日志条目，请调整时间选取器。有关更多信息，请参阅[设置时间过滤器](logging_kibana_set_time_filter.html#set_time_filter)。


##  通过 Web 浏览器导航至 Kibana 仪表板
{: #launch_Kibana_from_browser}

用于过滤 Kibana 中所显示数据的查询会检索 {{site.data.keyword.Bluemix_notm}} 组织中空间的日志条目。Kibana 显示的日志信息包括在您登录到的 {{site.data.keyword.Bluemix_notm}} 组织空间内部署的所有资源的记录。

要通过浏览器启动 Kibana，请完成以下步骤：

1. 打开 [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) 以登录到 Kibana 用户界面。

2. 选择要用于分析日志的 Kibana 版本。
    * 选择 **Kibana 4** 选项卡以使用 Kibana 4。这将打开“发现”页面。有关更多信息，请参阅 [在 Kibana 中以交互方式分析日志](logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively)。
    * 选择 **Kibana 3** 选项卡以使用 Kibana 3。这将打开缺省 Kibana 仪表板。有关使用 Kibana 3 来分析日志的信息，请参阅[在 Kibana 3 中分析日志（不推荐）](../logging_view_kibana3.html#analyzing_logs_Kibana3)。有关定制 Kibana 3 仪表板的更多信息，请参阅[此博客帖子 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/)。
     
        **注：**不推荐使用 Kibana 3。

    如果“发现”页面未显示任何日志条目，请调整时间选取器。有关更多信息，请参阅[设置时间过滤器](logging_kibana_set_time_filter.html#set_time_filter)。


