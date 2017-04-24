---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 在 Kibana 中通过仪表板分析日志
{:#kibana_analize_logs_dashboard}

使用 Kibana 中的*仪表板*页面可显示按仪表板分组的可视化集合。使用仪表板可分析日志数据并比较结果。
{:shortdesc}

在 {{site.data.keyword.Bluemix}} 中，可以定义和定制不同类型的仪表板，以可视化并分析数据。例如，下表列出了一些常用的仪表板类型：

| 仪表板类型 | 描述 |
|-------------------|-------------|
| 单 CF 应用程序仪表板 | 此仪表板用于显示单个 Cloud Foundry 应用程序的信息。 |
| 单容器仪表板  | 此仪表板用于显示单个容器的信息。  |
| 容器组仪表板  | 此仪表板用于显示特定容器组的信息。  |
| 多 CF 应用程序仪表板 | 此仪表板用于显示同一 {{site.data.keyword.Bluemix_notm}} 空间内部署的所有 Cloud Foundry 应用程序的信息。  | 
| 多容器仪表板 | 此仪表板用于显示同一 {{site.data.keyword.Bluemix_notm}} 空间内部署的所有容器的信息。  |
| 空间仪表板 | 此仪表板用于显示 {{site.data.keyword.Bluemix_notm}} 空间中可用的日志记录数据。  | 

要在仪表板中可视化数据，可以配置面板。Kibana 包含可用于分析信息的不同可视化，如表、趋势和直方图。可视化作为面板添加到仪表板。可以在仪表板中添加、除去和重新排列面板。每个面板的用途各不相同。一些面板组织成行，用于提供一个或多个查询的结果。另一些面板则显示文档或定制信息。每个面板基于一个搜索。搜索用于定义面板显示的数据子集。例如，可以配置条形图、饼图或表来对数据进行可视化和分析。  

下表列出了可在“仪表板”页面中执行的不同任务：

| 任务 | 更多信息 |
|------|------------------|
| [新建仪表板](logging_kibana_analize_logs_dashboard.html#K4_dashboard_new) | 可以创建多个仪表板。每个仪表板可以设计为包含不同的搜索、可视化和不同的日志数据子集。  |
| [保存仪表板](logging_kibana_analize_logs_dashboard.html#k4_dashboard_save) | 可以保存仪表板以供日后复用。 |
| [装入仪表板](logging_kibana_analize_logs_dashboard.html#k4_dashboard_reload) | 可以上传仪表板以更新其数据，修改仪表板或分析数据。 |
| [删除仪表板](logging_kibana_analize_logs_dashboard.html#k4_dashboard_delete) | 删除不需要的仪表板。 |
| [导出仪表板](logging_kibana_analize_logs_dashboard.html#k4_dashboard_export) | 可以将仪表板导出为 JSON 文件。 |
| [导入仪表板](logging_kibana_analize_logs_dashboard.html#k4_dashboard_import) | 可以将仪表板作为 JSON 文件导入。 |
| [共享仪表板](logging_kibana_analize_logs_dashboard.html#k4_dashboard_share) | 可以通过 HTML 源或通过 Kibana 仪表板来共享仪表板。 |
| [添加可视化](logging_kibana_analize_logs_dashboard.html#k4_dashboard_add_visualization) | 可以向仪表板添加现有可视化或搜索。|

有关 Kibana 的更多信息，请参阅 [Kibana 用户指南 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}。



## 新建 Kibana 仪表板
{: #K4_dashboard_new}

要创建新的仪表板，请完成以下步骤：

1. 在“仪表板”页面的工具栏中，单击**新建仪表板**按钮 ![新建仪表板](images/k4_dash_new_icon.jpg "新建仪表板")。

2. 添加一个或多个搜索和可视化。有关更多信息，请参阅[添加新的搜索或可视化](logging_kibana_analize_logs_dashboard.html#K4_dashboard_add_visualization)。

    添加搜索或可视化时，将在仪表板中添加面板。

3. 将面板拖放到仪表板中您希望将其定位到的部分。
 
4. 保存仪表板以供未来复用。有关更多信息，请参阅[保存 Kibana 仪表板](logging_kibana_analize_logs_dashboard.html#k4_dashboard_save)。


## 添加新的搜索或可视化
{: #k4_dashboard_add_visualization}

要添加现有可视化或搜索，请完成以下步骤：

1. 在“仪表板”页面的工具栏中，单击**添加可视化**按钮 ![添加可视化](images/k4_dash_add_visualization_icon.jpg "添加可视化")。

    **注**：可以添加可视化和搜索。 

2. 选择**可视化**选项卡以添加可视化，或者选择**搜索**选项卡以添加搜索。

3. 单击要添加的搜索或可视化。

    该搜索或可视化的面板会添加到仪表板。



## 保存 Kibana 仪表板
{: #k4_dashboard_save}

要保存定制后的 Kibana 仪表板，请完成以下步骤：

1. 在工具栏中，单击**保存**按钮 ![保存仪表板](images/k4_dash_save_icon.jpg "保存仪表板")。

2. 输入仪表板的名称。

    **注：**如果尝试使用包含空格的名称来保存仪表板，那么不会保存该仪表板。

3. 在“名称”字段旁边，单击**保存**图标。


## 删除 Kibana 仪表板
{: #k4_dashboard_delete}

要删除可视化，请在“设置”页面中完成以下步骤：

1. 在“设置”页面中，选择**对象**选项卡。

2. 在**可视化**选项卡中，选择要删除的可视化。

3. 单击**删除**。


## 装入 Kibana 仪表板
{: #k4_dashboard_reload}

要装入保存的仪表板，请完成以下步骤：

1. 在“仪表板”页面的工具栏中，单击**装入保存的仪表板**按钮 ![装入保存的仪表板](images/k4_dash_load_icon.jpg "装入保存的仪表板")。

2. 选择要装入的仪表板。 


## 导出 Kibana 仪表板
{: #k4_dashboard_export}

要将仪表板导出为 JSON 文件，请在“设置”页面中完成以下步骤：

1. 在“设置”页面中，选择**对象**选项卡。

2. 在**仪表板**选项卡中，选择要导出的仪表板。

3. 单击**导出**。

4. 保存文件。


## 导入 Kibana 仪表板
{: #k4_dashboard_import}

要将仪表板作为 JSON 文件导入，请在“设置”页面中完成以下步骤：

1. 在“设置”页面中，选择**对象**选项卡。

2. 在**仪表板**选项卡中，选择**导入**。

3. 选择文件并单击**打开**。

仪表板将添加到仪表板列表中。


## 共享 Kibana 仪表板
{: #k4_dashboard_share}

要共享仪表板，请完成以下步骤：

1. 在“仪表板”页面的工具栏中，单击**共享仪表板**按钮 ![共享仪表板](images/k4_dash_share_icon.jpg "共享仪表板")。

2. 选择以下其中一个操作：

    * **嵌入此仪表板**：选择此选项可通过 HTML 源共享仪表板。 
    
        单击“复制”按钮 ![复制到剪贴板](images/k4_copy_to_clipboard.jpg "复制到剪贴板")，以复制可用于在 HTML 源中嵌入仪表板的 HTML 代码。 
        
        **注**：要查看仪表板，用户必须能够访问 Kibana。
	
    * **共享链接**：选择此选项可与其他用户共享 Kibana 中的仪表板。



