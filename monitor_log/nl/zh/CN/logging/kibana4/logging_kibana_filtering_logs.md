---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 在 Kibana 中过滤日志
{:#kibana_filtering_logs}

在“发现”页面中，可以创建搜索查询，并应用过滤器来限制显示以供分析的信息。
{:shortdesc}

* 可以在“发现”页面的搜索栏中定义一个或多个搜索查询。一个搜索查询会定义一部分日志条目。使用 Lucene 查询语言来定义搜索查询。 

* 可以从*字段列表*或从表条目添加过滤器。过滤器通过包含或排除信息来优化数据选择内容。可以启用或禁用过滤器，反转过滤操作，将过滤器切换为开启或关闭，或者完全除去过滤器。 

定义新搜索后，保存该搜索，以便可加以复用，以在“发现”页面中用于未来的分析，或者用于创建可以在定制仪表板中使用的可视化。有关更多信息，请参阅[保存搜索](logging_kibana_filtering_logs.html#k4_save_search)。

执行新搜索时，直方图、表和字段列表会自动更新，以显示搜索结果。要了解显示哪些数据，请参阅[确定在“发现”页面中显示的数据](k4_identify_data.html#k4_identify_data)。

以下列表概述了有关如何过滤日志中数据的场景：

* 可以创建定制搜索来过滤日志。有关更多信息，请参阅[通过定义定制查询来过滤日志](k4_filter_queries.html#k4_filter_queries)。

* 可以搜索日志以查找在字段值中包含特定文本的条目。有关更多信息，请参阅[针对字段值中的特定文本过滤日志](k4_filter_logs_spec_text.html#k4_filter_logs_spec_text)。
 
* 可以搜索日志以查找特定字段值，也可以排除日志中包含特定字段值的条目。有关更多信息，请参阅[针对特定字段值过滤日志](k4_filter_logs_spec_field.html#k4_filter_logs_spec_field)。

    * 可以按日志类型过滤日志。有关更多信息，请参阅[按日志类型过滤日志](k4_filter_logs_by_log_type.html#k4_filter_logs_by_log_type)。
    * 可以按源过滤 CF 应用程序日志。有关更多信息，请参阅[按源过滤 CF 应用程序日志](k4_filter_logs_by_source.html#k4_filter_logs_by_source)。
    * 可以按实例标识过滤日志。有关更多信息，请参阅[按实例标识过滤日志](k4_filter_logs_by_instance_id.html#k4_filter_logs_by_instance_id)。   
    * 可以按消息类型过滤日志。有关更多信息，请参阅[按消息类型标识过滤日志](k4_filter_cf_logs_by_msg_type.html#k4_filter_cf_logs_by_msg_type)。  
 
* 可以过滤日志以显示某个时间段内的条目。有关更多信息，请参阅[设置时间过滤器](logging_kibana_set_time_filter.html#set_time_filter)。
     

## 开始新搜索
{: #k4_new_search}

要开始新搜索，请单击“发现”页面工具栏中的**新建搜索**按钮 ![新建搜索](images/k4_new_search_icon.jpg "新建搜索")。

## 保存搜索 
{: #k4_save_search}

保存搜索时，将保存搜索查询字符串和当前所选的索引模式。

要保存“发现”页面中的当前搜索，请完成以下步骤：

1. 在“发现”页面的工具栏中，单击**保存搜索**按钮 ![保存搜索](images/k4_save_search_icon.jpg "保存搜索")。

2. 输入搜索的名称。

3. 单击“保存”。 

## 删除搜索
{: #k4_delete_search}

要删除搜索，请在“设置”页面中完成以下步骤：

1. 在“设置”页面中，选择**对象**选项卡。

2. 在**搜索**选项卡中，选择要删除的搜索。

3. 单击**删除**。


## 导出搜索
{: #k4_export_search}

要导出搜索，请在“设置”页面中完成以下步骤：

1. 在“设置”页面中，选择**对象**选项卡。

2. 在**搜索**选项卡中，选择要导出的搜索。

3. 单击**导出**。

4. 保存文件。

## 导入搜索
{: #k4_import_search}

要导入搜索，请在“设置”页面中完成以下步骤：

1. 在“设置”页面中，选择**对象**选项卡。

2. 在**搜索**选项卡中，选择**导入**。

3. 选择文件并单击**打开**。

搜索将添加到搜索列表中。


## 重新装入搜索
{: #k4_reload_search}

要装入保存的搜索，请完成以下步骤：

1. 在“发现”页面的工具栏中，单击**装入搜索**按钮 ![装入搜索](images/k4_load_icon.jpg "装入搜索")。

2. 选择要装入的搜索。 


## 刷新搜索内容
{: #k4_refresh_search}

要手动刷新搜索内容，可以单击搜索栏中可用的放大镜。 

要自动刷新“发现”页面中显示的数据，可以配置刷新时间间隔。刷新时间间隔的当前值显示在“发现”页面的菜单栏中。缺省情况下，自动刷新设置为**关闭**。

要设置刷新时间间隔，请完成以下步骤：

1. 在“发现”页面中，单击菜单栏中可用的**时间过滤器**。

2. 单击**自动刷新** ![自动刷新](images/k4_auto_refresh_icon.jpg "自动刷新")。

3. 从列表中选择刷新时间间隔。 

    ![刷新时间间隔选项](images/k4_change_autorefresh.jpg "刷新时间间隔选项")


**注**：启用自动刷新时间间隔后，可以通过单击“暂停”按钮 ![暂停](images/k4_auto_refresh_pause_icon.jpg "暂停") 暂停刷新。




