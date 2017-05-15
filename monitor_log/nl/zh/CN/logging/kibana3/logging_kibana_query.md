---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 在 Kibana 中通过查询过滤 Cloud Foundry 应用程序日志
{: #logging_kibana_query}

使用 Kibana 可创建查询以在日志中搜索关键项并按这些项进行过滤。通过 Kibana，可以在仪表板上直观地比较查询。可以从 Cloud Foundry 应用程序的**日志**选项卡访问 Kibana 仪表板。
{:shortdesc}

要在 Kibana 仪表板上创建针对 Cloud Foundry 应用程序日志的查询，请完成以下任务：

1. 访问 Cloud Foundry 应用程序的**日志**选项卡。 

    1. 单击 {{site.data.keyword.Bluemix_notm}} **应用程序**仪表板上的应用程序名称。
    2. 单击**日志**选项卡。 
    
    这将显示应用程序的日志。

2. 访问应用程序的 Kibana 仪表板。单击**高级视图** ![“高级视图”链接](images/logging_advanced_view.jpg "“高级视图”链接")。这将显示 Kibana 仪表板。

3. 在 Kibana 仪表板上，单击**查询** ![“查询”图标](images/logging_query.jpg "“查询”图标") 以显示该字段。访问 Kibana 以从应用程序的**日志**选项卡查看应用程序日志时，将创建查询来显示您应用程序 application_id 的所有日志。
	
    要编辑查询，请单击**查询**字段并输入搜索项。

    * 要搜索关键字或关键字的一部分，请输入词语并后跟通配符 *；例如，`Java*`。 
	* 要搜索特定短语，请输入该短语并用双引号括起；例如，`"Java/1.8.0"`。
	* 要创建更复杂的搜索，可以使用逻辑项 AND 和 OR；例如，`"Java/1.8.0" OR "Java/1.7.0"`。
	* 要搜索特定字段内的值，请输入以下格式的搜索：*log_field_name:search_term*；例如，`instance_id:1`。
	* 要搜索特定日志字段内某一范围的值，请输入以下格式的搜索：*log_field_name:[start_of_range TO end_of_range]*；例如，`instance_id:[1 TO 2]`。

4. 如果要比较两个不同查询的结果，可以向仪表板再添加一个查询项。要再添加一个查询，请单击**查询**字段末尾的 **+** 图标。

    ![“查询”字段](images/logging_query_field.jpg "“查询”字段")
	
    这将显示新的**查询**字段，其中包含通配符 *。此查询将指示 Kibana 包含所有条目。
	
    ![另一个“查询”字段](images/logging_additional_query_field.jpg "另一个“查询”字段")
	
    您的仪表板会使用新查询的结果进行更新。**按时间列出的事件**窗格会显示这两个查询的图形表示法，并在括号中显示每个查询的项数。 
	
    ![显示这两个查询的图形的仪表板](images/logging_dashboard_queries.jpg "显示这两个查询的图形的仪表板")
	
5. 单击新的**查询**字段以编辑其内容并添加查询条件；例如，`instance_id:1`。使用**按时间列出的事件**窗格以比较查询的结果。

    ![显示这两个查询的图形的仪表板](images/logging_dashboard_queries2.jpg "显示这两个查询的图形的仪表板")

6. 要删除查询，请将鼠标移至要删除的**查询**字段上方以显示**删除**图标。单击**删除**图标。

    ![具有“删除”图标的“查询”字段](images/logging_delete_query.jpg "具有“删除”图标的“查询”字段")

7. 要使用可识别的名称保存此仪表板，请单击**保存**图标 ![“保存”图标](images/logging_save.jpg "“保存”图标")，然后输入仪表板的名称。 

    **注：**如果尝试使用包含空格的名称来保存仪表板，那么不会保存该仪表板。请输入不包含空格的名称，然后单击**保存**图标。

    ![保存仪表板名称](images/logging_save_dashboard.jpg "保存仪表板名称")


