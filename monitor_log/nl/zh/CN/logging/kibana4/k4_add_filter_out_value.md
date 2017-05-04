---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 为*字段列表*中未列出的值添加过滤器
{:#k4_add_filter_out_value}

要为*字段列表*中未显示的值添加过滤器，请通过查询来搜索包含该值的记录。然后，从“发现”页面中提供的表条目添加过滤器。
{:shortdesc}

要为在*字段列表*部分中显示的列表中不可用的值添加过滤器，请完成以下步骤：

1. 查看 Kibana 的“发现”页面，以确定它显示的数据子集。有关更多信息，请参阅[确定在 Kibana 的“发现”页面中显示的数据](logging_kibana_analize_logs_interactively.html#k4_identify_data)。

    例如，下图显示了*字段列表*中 CF 应用程序实例的值。 
    
    ![显示字段列表中的值](images/k4_add_filter_f1.jpg "显示字段列表中的值")
    
    您关注的是编号为 *3* 的实例，但该实例在显示的列表中不可用。

2. 在“发现”页面中，修改查询以搜索特定字段值。

    例如，要搜索实例 *3*，输入的查询如下所示：`application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:"3"`
    
    ![修改查询](images/k4_add_filter_f2.jpg "修改查询")
    
    在该表中，可以看到与查询匹配的所有记录。 
    
 3. 展开一条记录，并选择“放大镜”按钮 ![包含方式下的“放大镜”按钮](images/k4_include_field_icon.jpg "包含方式下的“放大镜”按钮") 以添加过滤器。
 
     例如，要为值为 *3* 的实例标识添加过滤器，请单击 *instance_id* 字段旁边的“放大镜”按钮 ![包含方式下的“放大镜”按钮](images/k4_include_field_icon.jpg "包含方式下的“放大镜”按钮")。
     
     ![显示表](images/k4_add_filter_f3.jpg "显示表")
     
4. 检查过滤器是否已添加。

    例如，下图显示了从表添加过滤器后，该过滤器已启用。
    
    ![显示过滤器](images/k4_add_filter_f4.jpg "显示过滤器")
    
    
