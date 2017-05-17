---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-16"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 在 Kibana 中按消息类型过滤 Cloud Foundry 应用程序日志
{: #logging_kibana_message_type_filter}

在 Kibana 仪表板上按消息类型查看和过滤 {{site.data.keyword.Bluemix_notm}} 应用程序日志。可以从 Cloud Foundry 应用程序的**日志**选项卡访问 Kibana 仪表板。
{:shortdesc}

要在 Kibana 仪表板上按消息类型查看和过滤 Cloud Foundry 应用程序日志，请完成以下任务：

1. 访问 Cloud Foundry 应用程序的**日志**选项卡。 

    1. 单击 {{site.data.keyword.Bluemix_notm}} **应用程序**仪表板上的应用程序名称。
    2. 单击**日志**选项卡。 
    
    这将显示应用程序的日志。

2. 访问应用程序的 Kibana 仪表板。单击**高级视图** ![“高级视图”链接](images/logging_advanced_view.jpg "“高级视图”链接")。这将显示 Kibana 仪表板。

3. 在**所有事件**窗口中，单击向右箭头图标以显示所有字段。 

    ![具有向右箭头图标的“所有事件”窗口](images/logging_all_events_no_fields.jpg "具有向右箭头图标的“所有事件”窗口")

4. 在**字段**窗格中，选择 **message_type** 以在**所有事件**窗口中显示生成每个日志条目的组件。

    ![选择了 message_type 字段的“所有事件”窗口](images/logging_message_type.png "选择了 message_type 字段的“所有事件”窗口")

5. 在**所有事件**窗口中，单击日志事件行以显示该事件的详细信息。选择显示要过滤的 **message_type** 的事件。

    ![显示所选日志事件的详细信息的“所有事件”窗口](images/logging_message_type_add_filter.png "显示所选日志事件的详细信息的“所有事件”窗口")

6. 添加过滤器以包含或排除有关某个消息类型的信息。 

    * 要添加用于包含某种消息类型相关信息的过滤器，请单击表的 message_type 行中的**放大镜** ![“放大镜”图标](images/logging_magnifying_glass.jpg "“放大镜”图标") 图标。 
    
           ![message_type 字段的过滤条件](images/logging_message_type_filter.png "message_type 字段的过滤条件")
    
    * 要添加用于排除某种消息类型相关信息的过滤器，请单击表的 message_type 行中的**排除** ![“排除”图标](images/logging_exclusion_icon.png "“排除”图标") 图标。 
    
    新的过滤条件会添加到 Kibana 仪表板。

7. （可选）重复先前的步骤以添加其他消息类型的过滤器。要查看消息类型的完整列表，请参阅[日志格式](../logging_view_kibana3.html#kibana_log_format_cf)。

9. 保存仪表板。    
        
    完成创建过滤器的操作后，单击**保存**图标 ![“保存”图标](images/logging_save.jpg "“保存”图标")，然后输入仪表板的名称。 
      
    **注：**如果尝试使用包含空格的名称来保存仪表板，那么不会保存该仪表板。请输入不包含空格的名称，然后单击**保存**图标。
    
    ![保存仪表板名称](images/logging_save_dashboard.jpg "保存仪表板名称")。

您已创建用于按消息类型过滤日志条目的仪表板。您可以通过单击**文件夹**图标 ![“文件夹”图标](images/logging_folder.jpg "“文件夹”图标")，并按名称选择仪表板来随时装入保存的仪表板。
