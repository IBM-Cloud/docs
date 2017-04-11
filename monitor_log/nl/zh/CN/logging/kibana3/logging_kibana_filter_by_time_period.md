---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 在 Kibana 中按时间过滤 Cloud Foundry 应用程序日志
<!-- for example, Uploading your data -->
{: #logging_kibana_time_filter}


在 Kibana 仪表板上按时间查看和过滤 {{site.data.keyword.Bluemix_notm}} 应用程序日志。可以从 Cloud Foundry 应用程序的**日志**选项卡访问 Kibana 仪表板。
{:shortdesc}

要在 Kibana 仪表板上按时间查看和过滤 Cloud Foundry 应用程序日志，请完成以下任务：

1. 访问 Cloud Foundry 应用程序的**日志**选项卡。 

    1. 单击 {{site.data.keyword.Bluemix_notm}} **应用程序**仪表板上的应用程序名称。
    2. 单击**日志**选项卡。 
    
    这将显示应用程序的日志。

2. 访问应用程序的 Kibana 仪表板。单击**高级视图** ![“高级视图”链接](images/logging_advanced_view.jpg)。这将显示 Kibana 仪表板。


3. 在 Kibana 仪表板上，单击**时间过滤器** ![Kibana 时间过滤器](images/logging_kibana_time_filter.jpg)，然后从下拉菜单中选择**定制**。这将显示以下窗口：

    ![Kibana 仪表板上的定制时间过滤器](images/logging_custom_time_filter.jpg)

4. 单击**开始时间**和**结束时间**字段以编辑过滤器的开始时间和结束时间。 
    
    要包含截至此刻的日志，请单击**现在**链接。对时间范围满意后，单击**应用**。 

现在，Kibana 仪表板将根据定制的时间过滤器显示进行日志记录的事件。
