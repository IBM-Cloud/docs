---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 在 Grafana 中分析度量值
{:#analyzing_metrics_grafana}

在 {{site.data.keyword.Bluemix}} 中，可以使用 Grafana（一种开放式源代码分析和可视化平台）通过各种图形（例如，图表和表）来对度量值进行监视、搜索、分析和可视化。使用 Grafana 可执行高级分析任务。
{:shortdesc}

您可以使用以下任何一种方法来启动 Grafana：

* 通过 {{site.data.keyword.Bluemix_notm}}

    可以在 Grafana 中特定 Docker 容器的上下文中启动到该特定容器的度量值。 
    
    有关更多信息，请参阅 [通过 {{site.data.keyword.Bluemix_notm}} 仪表板导航至 Grafana 仪表板](monitoring_analyzing_metrics_grafana.html#launch_grafana_from_bluemix)。

* 通过直接浏览器链接

    您可以启动 Grafana，这样就能看到来自所提供 {{site.data.keyword.Bluemix_notm}} 空间内服务的日志聚集数据。
    
    有关更多信息，请参阅[通过 Web 浏览器导航至 Kibana 仪表板](monitoring_analyzing_metrics_grafana.html#launch_grafana_from_browser)。
    
有关 Grafana 的更多信息，请参阅 [Grafana 用户指南 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://docs.grafana.org/guides/getting_started/){: new_window}。


##  通过 Bluemix 仪表板导航至 Grafana 仪表板
{: #launch_grafana_from_bluemix}

用于过滤 Grafana 中所显示数据的查询会检索从中启动 Grafana 的 {{site.data.keyword.Bluemix_notm}} 容器的数据。 

要在 Grafana 中查看 Docker 容器的度量值，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}}，然后在 {{site.data.keyword.Bluemix_notm}}“仪表板”中，单击容器。 
    
2. 在导航栏中，单击**监视和日志**。这将打开“监视”选项卡。 
    
3. 单击**高级视图**。这将打开 **Grafana** 仪表板。


##  通过 Web 浏览器导航至 Grafana 仪表板
{: #launch_grafana_from_browser}

用于过滤 Grafana 中所显示数据的查询会检索 {{site.data.keyword.Bluemix_notm}} 组织中空间的数据。Grafana 显示的度量值信息包括在您登录到的 {{site.data.keyword.Bluemix_notm}} 组织空间内部署的所有资源的记录。

要通过浏览器启动 Grafana，请完成以下步骤：

1. 打开 [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) 以登录到 Grafana 用户界面。

2. 选择 **Grafana**。
     

