---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 设置时间过滤器
{: #set_time_filter}

通过配置*时间选取器*，查看和过滤某个时间段内的 {{site.data.keyword.Bluemix}} 日志。
{:shortdesc}

可以在“发现”页面中配置*时间选取器*。缺省情况下，时间选取器设置为最近 15 分钟。 

要搜索包含特定时间的条目，请完成以下步骤：

1. 在“发现”页面的菜单栏中，单击时间选取器 ![时间选取器](images/k4_time_picker_icon.jpg "时间选取器")。

2. 设置时间间隔。 

    可以定义以下类型的时间间隔：
    
    * 快速：这些是预定义时间间隔，包含最常用的“相对”和“绝对”时间间隔，例如*今天*和*本月*。 
    
        ![时间选取器的“快速”选项](images/k4_time_picker_quick.jpg "时间选取器的“快速”选项")
    
    * 相对：可以为这些时间间隔指定开始日期和时间以及结束日期和时间。可以按小时四舍五入。
    
        ![时间选取器的“相对”选项](images/k4_time_picker_relative.jpg "时间选取器的“相对”选项")
    
    * 绝对：这些是介于开始日期和结束日期之间的时间间隔。
    
        ![时间选取器的“绝对”选项](images/k4_time_picker_absolute.jpg "时间选取器的“绝对”选项")
      

配置时间间隔后，Kibana 中的显示的数据对应于该时间范围内的条目。



