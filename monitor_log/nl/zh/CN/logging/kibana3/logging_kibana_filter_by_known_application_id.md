---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 在 Kibana 中按已知应用程序标识过滤 Cloud Foundry 应用程序日志
<!-- for example, Uploading your data -->
{: #logging_kibana_known_application_id}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

如果您知道 Cloud Foundry 应用程序的应用程序标识，那么可以在 Kibana 仪表板上按应用程序的应用程序标识 (application_id) 快速查看和过滤日志。可以从 Cloud Foundry 应用程序的**日志**选项卡访问 Kibana 仪表板。
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
要在 Kibana 仪表板上按已知应用程序标识查看和过滤 Cloud Foundry 应用程序日志，请完成以下任务：

1. 访问 Cloud Foundry 应用程序的**日志**选项卡。 

    1. 单击 {{site.data.keyword.Bluemix_notm}} **应用程序**仪表板上的应用程序名称。
    2. 单击**日志**选项卡。 
    
    这将显示应用程序的日志。

2. 访问应用程序的 Kibana 仪表板。单击**高级视图** ![“高级视图”链接](images/logging_advanced_view.jpg)。这将显示 Kibana 仪表板。

3. 在 Kibana 仪表板上，单击**文件夹**图标 ![“文件夹”图标](images/logging_folder.jpg) 以显示用于列出所有最近仪表板的菜单。 

    **注：**除了按名称列出保存的仪表板外，该菜单还会根据以下格式列出未命名仪表板：*ALCH_TENANT_ID_application_id*。 

    ![仪表板列表](images/logging_list_of_dashboards.jpg)

4. 选择其名称中包含已知 application_id 的仪表板。 

    此仪表板将装入并显示针对 application_id 过滤的信息。

5. （可选）可以向过滤器部分添加更多字段（例如，**instance_id**）以启用或禁用按实例标识过滤记录的功能。 
  
    1. 在**所有事件**窗口中，单击日志事件行以显示该事件的详细信息。 
	
        ![显示所选日志事件详细信息的“所有事件”窗口](images/logging_selected_log_event.jpg)
	
    2. 选择显示要过滤的字段值的事件。
	
    3. 添加过滤器。
    
        要添加用于包含该特定字段值相关信息的过滤器，请单击表中包含待过滤字段的行中的**放大镜** ![“放大镜”图标](images/logging_magnifying_glass.jpg) 图标。 
	
        要添加用于排除该特定字段值相关信息的过滤器，请单击表中包含待过滤字段的行中的**排除** ![“排除”图标](images/logging_exclusion_icon.png) 图标。  

        新的过滤条件会添加到 Kibana 仪表板。
	
	    ![instance_id 字段的过滤条件](images/logging_instance_id_filter.jpg)
	
6. 使用可识别的名称保存此仪表板。 

    单击**保存**图标 ![“保存”图标](images/logging_save.jpg)，然后输入仪表板的名称。 

    **注：**如果尝试使用包含空格的名称来保存仪表板，那么不会保存该仪表板。请输入不包含空格的名称，然后单击**保存**图标。

    ![保存仪表板名称](images/logging_save_dashboard.jpg)。


您已创建用于按应用程序标识和实例标识过滤日志条目的仪表板。您可以通过单击**文件夹**图标 ![“文件夹”图标](images/logging_folder.jpg)，并按名称选择仪表板来随时装入保存的仪表板。
