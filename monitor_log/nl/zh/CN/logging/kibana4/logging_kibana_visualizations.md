---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 在 Kibana 中使用可视化分析日志 
{:#logging_kibana_visualizations}

使用 Kibana 中的*可视化*页面可创建可视化，例如图形和表；可以使用可视化来分析日志数据并比较结果。
{:shortdesc}

可以单独使用可视化来分析日志。 

* 可以通过在*发现*页面中定义并保存的搜索来创建可视化，也可以通过在*可视化*页面中定义的新查询来创建可视化。搜索会定义可视化显示的数据子集。

* 选择的可视化类型确定了如何显示数据以供分析。

下表列出了不同的可视化类型：

| 可视化类型 | 描述 |
|-----------------------|-------------|
| 面积图 | 以图形方式显示量化数据。用于比较两组或更多组聚集的数据。 |
| 数据表 | 以表格形式显示组合聚集的原始数据。 |
| 折线图 | 显示基于时间的数据。用于比较两组或更多组基于时间的聚集数据。 |
| Markdown 窗口小部件 | 用于显示文本信息。 |
| 度量值 | 用于显示命中计数或数字字段的准确平均值。 |
| 饼图 | 用于显示字段的不同值。 | 
| 垂直条形图 | 显示基于时间的数据和非基于时间的数据。用于对数据分组。 |

在“可视化”页面中，可以执行以下任一任务：

| 任务 | 更多信息 |
|------|------------------|
| [新建可视化](logging_kibana_visualizations.html#logging_k4_visualizations_create) | 可以通过在*发现*页面中定义并保存的搜索来创建可视化，也可以通过在*可视化*页面中定义的新查询来创建可视化。 |
| [保存可视化](logging_kibana_visualizations.html#logging_kibana_visualizations_save) | 可以保存可视化以供未来复用。 |
| [装入可视化](logging_kibana_visualizations.html#logging_kibana_visualizations_reload) | 可以上传可视化以更新其数据，修改可视化或分析数据。 |
| [删除可视化](logging_kibana_visualizations.html#logging_kibana_visualizations_delete) | 删除不需要的可视化。 |
| [导出可视化](logging_kibana_visualizations.html#logging_kibana_visualizations_export) | 可以将可视化导出为 JSON 文件。  |
| [导入可视化](logging_kibana_visualizations.html#logging_kibana_visualizations_import) | 可以将可视化作为 JSON 文件导入。  |
| [共享可视化](logging_kibana_visualizations.html#logging_kibana_visualizations_share) | 可以通过 HTML 源或通过 Kibana 仪表板来共享可视化。  |


## 在 Kibana 中通过查询创建可视化
{:#logging_k4_visualizations_create}

要在“可视化”页面中创建可视化，请完成以下步骤：

1. 启动 Kibana，然后选择**可视化**页面。

2. 创建新的可视化。在工具栏中，单击**新建可视化**按钮 ![新建可视化](images/k4_visualization_new_icon.jpg "新建可视化")。

3. 选择可视化。
    
4. 选择搜索源。选择以下其中一个选项：

    * 单击**通过新搜索**。
    * 单击**通过保存的搜索**。 
  
5. 配置查询。

    * 如果选择**通过保存的搜索**，请选择一个搜索查询。该查询用于检索供可视化使用的数据。 

        选择搜索后，可视化构建器会打开，并装入所选查询的数据。这将显示以下消息：*此可视化已链接到保存的搜索：your_search_name*。 
	
	**注**：对保存的搜索进行的任何更改都会自动反映在可视化中。要禁用对链接到此可视化的查询进行的自动更新，请双击消息：*此可视化已链接到保存的搜索：your_search_name* 

    * 如果选择**通过新搜索**，请定义新查询。该查询用于定义由可视化检索并使用的数据子集。

        有关更多信息，请参阅[通过定义定制查询来过滤日志](k4_filter_queries.html#k4_filter_queries)。

6. 在可视化构建器中，为 Y 轴选择度量值聚集。

7. 在可视化构建器中，选择存储区类型。然后，选择一个存储区聚集。
  
8. 添加子存储区以划分数据。

有关 Kibana 的更多信息，请参阅 [Kibana 用户指南 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}。
 
## 保存可视化
{:#logging_kibana_visualizations_save}

要在“可视化”页面中保存可视化，请完成以下步骤：

1. 在“可视化”页面的工具栏中，单击**保存可视化**按钮 ![保存可视化](images/k4_visualization_save_icon.jpg "保存可视化")。

2. 输入可视化的名称。

3. 单击“保存”。 

## 装入可视化
{:#logging_kibana_visualizations_reload}

要装入保存的可视化，请完成以下步骤：

1. 在“可视化”页面的工具栏中，单击**装入保存的可视化**按钮 ![装入保存的可视化](images/k4_visualization_open_icon.jpg "装入保存的可视化")。

2. 选择要装入的可视化。 



## 删除可视化
{:#logging_kibana_visualizations_delete}

要删除可视化，请在“设置”页面中完成以下步骤：

1. 在“设置”页面中，选择**对象**选项卡。

2. 在**可视化**选项卡中，选择要删除的可视化。

3. 单击**删除**。


## 导出可视化
{:#logging_kibana_visualizations_export}

要将可视化导出为 JSON 文件，请在“设置”页面中完成以下步骤：

1. 在“设置”页面中，选择**对象**选项卡。

2. 在**可视化**选项卡中，选择要导出的可视化。

3. 单击**导出**。

4. 保存文件。

## 导入可视化
{:#logging_kibana_visualizations_import}

要将可视化作为 JSON 文件导入，请在“设置”页面中完成以下步骤：

1. 在“设置”页面中，选择**对象**选项卡。

2. 在**可视化**选项卡中，选择**导入**。

3. 选择文件并单击**打开**。

该可视化将添加到可视化列表中。


## 共享可视化
{:#logging_kibana_visualizations_share}

要在“可视化”页面中共享可视化，请完成以下步骤：

1. 在“可视化”页面的工具栏中，单击**共享可视化**按钮 ![共享可视化](images/k4_visualization_share_icon.jpg "共享可视化")。

2. 选择以下其中一个操作：

    * **嵌入此可视化**：选择此选项可通过 HTML 源共享可视化。 
    
        单击“复制”按钮 ![复制到剪贴板](images/k4_copy_to_clipboard.jpg "复制到剪贴板")，以复制可用于在 HTML 源中嵌入可视化的 HTML 代码。 
	
	**注**：要查看可视化，用户必须能够访问 Kibana。
	
    * **共享链接**：选择此选项可与其他用户共享 Kibana 中的可视化。



