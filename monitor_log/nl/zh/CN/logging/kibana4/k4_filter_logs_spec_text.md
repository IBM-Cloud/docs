---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 针对字段值中的特定文本过滤日志
{:#k4_filter_logs_spec_text}

查看和搜索在字段值中包含特定文本的条目。
{:shortdesc}

**注意：**只能对 Elasticsearch 分析器分析的字符串字段执行自由文本搜索。 
    
Elasticsearch 分析字符串字段的值时，会根据 Unicode Consortium 定义的单词边界来拆分文本，除去标点符号并将所有单词转化成小写。
    
要搜索在字段值中包含特定文本的条目，请完成以下步骤：

1. 查看 Kibana 的“发现”页面，以确定它显示的数据子集。有关更多信息，请参阅[确定在 Kibana 的“发现”页面中显示的数据]((logging_kibana_analize_logs_interactively.html#k4_identify_data)。

2. 确定缺省情况下 Elasticsearch 中分析的字段。

    要显示可用于搜索和过滤日志数据的已分析字段的完整列表，请[重新装入字段列表](logging_kibana_analize_logs_interactively.html#kibana_discover_view_reload_fields)。然后，在“发现”页面中可用的*字段列表*中，完成以下步骤：
    
    1. 单击“配置”图标 ![“配置”图标](images/k4_configure_icon.jpg "“配置”图标")。这将显示**所选字段**部分，在其中可以过滤字段。

        ![用于显示具有特定属性的字段的“配置”部分](images/k4_reset_filters.jpg "用于显示具有特定属性的字段的“配置”部分")
    
    2. 要确定已分析的字段，请在搜索字段**已分析**中选择**是**。

        ![已分析的属性](images/k4_reset_filters_analyze_options.jpg "已分析的属性")
    
        这将显示已分析字段的列表。
    
        ![已分析字段的列表](images/k4_list_analyzed_fields.jpg "已分析字段的列表")
        
         
    3. 检查要在其中查找自由文本的字段是否为缺省情况下 Elasticsearch 分析的字段。
    
3. 如果该字段已分析，请修改查询以在日志中搜索将该自由文本包含为字段值一部分的条目。

    
**示例**

如果通过 {{site.data.keyword.Bluemix}} UI 为 Cloud Foundry (CF) 应用程序启动了 Kibana，并且希望查找包含消息标识 *CWWKT0016I:* 的特定消息，请将搜索修改为包含该自由文本。
    
1. 检查装入的搜索查询以及在“发现”页面中显示的数据。
       
    ![缺省搜索查询](images/k4_filter_by_text_default_query.jpg "缺省搜索查询")
        
2. 要搜索消息标识 *CWWKT0016I*，请修改搜索查询，然后按 **Enter** 键：
    
    ```
	application_id:f52f6016-3aab-4b5c-aa2e-5493747cb978 AND message:"CWWKT0016I:" 
	```
        
    ![修改查询](images/k4_filter_by_text_modify_query.jpg "修改查询")
      
    
该表显示了 *message* 字段值中包含文本 *CWWKT0016I* 的 CF 应用程序条目。
    
![新搜索视图](images/k4_filter_by_text_result_query.jpg "新搜索视图")     	
        
 
 
