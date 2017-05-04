---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 按源过滤 CF 应用程序日志
{:#k4_filter_logs_by_source}

通过 Kibana 仪表板按源类型查看和过滤 Cloud Foundry 应用程序日志。
{:shortdesc}

要搜索包含特定日志源的条目，请完成以下步骤：

1. 查看 Kibana 的“发现”页面，以确定它显示的数据子集。有关更多信息，请参阅[确定在 Kibana 的“发现”页面中显示的数据](logging_kibana_analize_logs_interactively.html#k4_identify_data)。

2. 在*字段列表*中，选择 **source_id** 字段。

    ![显示 source_id 字段的过滤列表](images/k4_filter_sourceid_F1.jpg "显示 source_id 字段的过滤列表")     

3. 要添加过滤器以搜索包含特定 source_id 的条目，请选择该值的放大按钮 ![包含方式下的“放大镜”按钮](images/k4_include_field_icon.jpg "包含方式下的“放大镜”按钮")。

    有关可用于 CF 应用程序的日志源的列表，请参阅 [CF 应用程序的日志源](../logging_cf_apps.html#logging_bluemix_cf_apps_log_sources)。

    例如，要添加过滤器以包含有关 CF 应用程序的启动、停止或崩溃的日志条目，请选择*字段列表*部分中可用于值 *CELL* 的“放大镜”按钮 ![包含方式下的“放大镜”按钮](images/k4_include_field_icon.jpg "包含方式下的“放大镜”按钮")。下图显示了用于已启用 source_id 值 *CELL* 的过滤器。
    
    ![包含字段值的过滤器](images/k4_filter_sourceid_F2.jpg "包含字段值的过滤器")

    要添加过滤器以搜索不包含特定 source_id 的条目，请选择该值的放大按钮 ![排除方式下的“放大镜”按钮](images/k4_exclude_field_icon.jpg "排除方式下的“放大镜”按钮")。
    
    例如，要添加过滤器以排除有关 CF 应用程序的启动、停止或崩溃的日志条目，请选择*字段列表*部分中可用于值 *CELL* 的“放大镜”按钮 ![排除方式下的“放大镜”按钮](images/k4_exclude_field_icon.jpg "排除方式下的“放大镜”按钮")。下图显示了排除 source_id 值 *CELL* 的条目的过滤器。

    ![排除字段值的过滤器](images/k4_filter_sourceid_F3.jpg "排除字段值的过滤器")




