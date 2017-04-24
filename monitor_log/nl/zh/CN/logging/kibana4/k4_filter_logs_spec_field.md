---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 针对特定字段值过滤日志
{:#k4_filter_logs_spec_field}

可以搜索包含特定字段值的条目。
{:shortdesc}

要搜索包含特定字段值的条目，请完成以下步骤：

1. 查看 Kibana 的“发现”页面，以确定它显示的数据子集。有关更多信息，请参阅[确定在 Kibana 的“发现”页面中显示的数据](logging_kibana_analize_logs_interactively.html#k4_identify_data)。

2. 在*字段列表*中，确定要为其定义过滤器的字段，并单击该字段。

    该字段最多显示 5 个值。每个值有两个“放大镜”按钮。 
    
    如果看不到值，请参阅[为字段列表中未列出的值添加过滤器](k4_add_filter_out_value.html#k4_add_filter_out_value)。

3. 要添加过滤器以搜索具有某个字段值的条目，请选择该值的放大按钮 ![包含方式下的“放大镜”按钮](images/k4_include_field_icon.jpg "包含方式下的“放大镜”按钮")。

    ![包含字段值的过滤器](images/k4_add_filter_for_field.jpg "包含字段值的过滤器")

    要添加过滤器以搜索不包含该字段值的条目，请选择该值的放大按钮 ![排除方式下的“放大镜”按钮](images/k4_exclude_field_icon.jpg "排除方式下的“放大镜”按钮")。

    ![排除字段值的过滤器](images/k4_add_filter_to_exclude_field.jpg "排除字段值的过滤器")

4. 选择以下任一选项以在 Kibana 中使用过滤器：

    <table>
      <tbody>
        <tr>
          <th align="center">选项</th>
          <th align="center">描述</th>
          <th align="center">其他信息</th>
        </tr>
        <tr>
          <td align="left">启用</td>
          <td align="left">选择此选项可启用过滤器。</td>
          <td align="left">添加过滤器时，会自动启用该过滤器。<br> 如果过滤器已禁用，请单击该过滤器以将其启用。</td>
        </tr>
        <tr>
          <td align="left">禁用</td>
          <td align="left">选择此选项可禁用过滤器。</td>
          <td align="left">添加过滤器后，如果要隐藏某个字段值的条目，请单击**禁用**。</td>
        </tr>
        <tr>
          <td align="left">锁定</td>
          <td align="left">选择此选项可在各个 Kibana 页面之间持久存储该过滤器。</td>
          <td align="left">可以在*发现*页面、*可视化*页面或*仪表板*页面中锁定过滤器。</td>
        </tr>
        <tr>
          <td align="left">切换</td>
          <td align="left">选择此选项可切换过滤器。</td>
          <td align="left">缺省情况下，将显示与过滤器匹配的条目。要显示不匹配的条目，请切换过滤器。</td>
        </tr>
        <tr>
          <td align="left">除去</td>
          <td align="left">选择此选项可除去过滤器。</td>
          <td align="left"></td>
        </tr>
      </tbody>
    </table>

 

 
 

