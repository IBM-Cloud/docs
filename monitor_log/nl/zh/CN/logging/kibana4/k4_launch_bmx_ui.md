---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 通过 Bluemix 仪表板访问 Kibana 仪表板
{: #launch_Kibana_from_bluemix}

通过 {{site.data.keyword.Bluemix}} UI 启动 Kibana 可查看 Cloud Foundry 应用程序或 Docker 容器的特定日志。
{:shortdesc}

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

有关 Kibana 的更多信息，请参阅 [Kibana 用户指南 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}。

