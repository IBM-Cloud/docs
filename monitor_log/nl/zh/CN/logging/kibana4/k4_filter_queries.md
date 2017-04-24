---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 通过定义定制搜索查询来过滤日志
{:#k4_filter_queries}

在“发现”页面的搜索栏中，可以使用 Lucene 查询语言来定义并保存搜索查询。对于每个搜索，可以应用过滤器来优化可供分析的条目。
{:shortdesc}

要使用定制搜索来过滤日志，请完成以下任务：

1. 访问 Cloud Foundry (CF) 应用程序或容器的**日志**选项卡。 

    1.  在 {{site.data.keyword.Bluemix}}“仪表板”中单击应用程序名称或容器。
    2. 对于 CF 应用程序，单击**日志**选项卡。对于容器，单击**监视和日志**，然后选择**日志记录**选项卡。
    
    这将显示日志。

2. 访问 Kibana。单击**高级视图** ![“高级视图”链接](images/logging_advanced_view.jpg)。这将显示 Kibana 仪表板。

    访问 Kibana 时，将应用缺省搜索。您可以看到已为其启动 Kibana 的资源的实例列表的日志。可以过滤该空间中任何或全部 {{site.data.keyword.Bluemix_notm}} 资源的日志。

对于 Lucene，正确的术语是“项”，而不是“关键字”。

3. 查看“发现”页面，以确定它显示的数据子集。有关更多信息，请参阅[确定在 Kibana 的“发现”页面中显示的数据](logging_kibana_analize_logs_interactively.html#k4_identify_data)。然后，修改缺省查询以过滤条目。

    **注：**使用 Lucene 查询语言来定义定制查询。有关更多信息，请参阅 [Apache Lucene - Query Parser Syntax ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html){: new_window}
    
    如果 Kibana 是通过 {{site.data.keyword.Bluemix_notm}} 启动的，要修改查询并定义多个搜索条件，可以使用逻辑项 **AND** 和 **OR**。这些运算符必须为大写。    
    
    * 要搜索关键字或关键字的一部分，请输入词语并后跟通配符 *；例如，`Java*`。 
    * 要搜索特定短语，请输入该短语并用双引号括起；例如，`"Java/1.8.0"`。
    * 要创建更复杂的搜索，可以使用逻辑项 AND 和 OR；例如，`"Java/1.8.0" OR "Java/1.7.0"`。
    * 要搜索特定字段内的值，请输入以下格式的搜索：*log_field_name:search_term*；例如，`instance_id:"1"`。
    * 要搜索特定日志字段内某一范围的值，请输入以下格式的搜索：*log_field_name:[start_of_range TO end_of_range]*；例如，`instance_id:["1" TO "2"]`。

     例如，对于 CF 应用程序，可以创建查询 `application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:["0" TO "1"]`，此查询中仅列出实例 *0* 和 *1* 的条目。 

4. 保存查询，以便将来可以复用。有关更多信息，请参阅[保存搜索](logging_kibana_filtering_logs.html#k4_save_search)。 

**注：**如果需要删除查询，请参阅[删除搜索](logging_kibana_filtering_logs.html#k4_delete_search)。



