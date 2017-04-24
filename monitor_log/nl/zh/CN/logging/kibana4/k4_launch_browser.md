---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 通过 Web 浏览器访问 Kibana 仪表板
{: #launch_Kibana_from_browser}

如果需要在 {{site.data.keyword.Bluemix}} 空间中分析日志条目，请通过浏览器启动 Kibana。
{:shortdesc}

用于过滤 Kibana 中所显示数据的查询会检索 {{site.data.keyword.Bluemix_notm}} 组织中空间的日志条目。Kibana 显示的日志信息包括在您登录到的 {{site.data.keyword.Bluemix_notm}} 组织空间内部署的所有资源的记录。

要通过浏览器启动 Kibana，请完成以下步骤：

1. 打开 [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) 以登录到 Kibana 用户界面。

2. 选择要用于分析日志的 Kibana 版本。
    * 选择 **Kibana 4** 选项卡以使用 Kibana 4。这将打开“发现”页面。有关更多信息，请参阅 [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively)。
    * 选择 **Kibana 3** 选项卡以使用 Kibana 3。这将打开缺省 Kibana 仪表板。有关定制 Kibana 3 仪表板的更多信息，请参阅[此博客帖子](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/)。
     
        **注：**不推荐使用 Kibana 3。

    如果“发现”页面未显示任何日志条目，请调整时间选取器。有关更多信息，请参阅[设置时间过滤器](logging_kibana_set_time_filter.html#set_time_filter)。

有关 Kibana 的更多信息，请参阅 [Kibana 用户指南 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}。
