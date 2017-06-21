---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 分析作为容器日志条目一部分的 JSON message 字段
{: #logging_containers_analyze_json_field}

在 Kibana 中，要分析容器日志数据，可以定义新搜索，并对在 JSON 格式的 message 字段中定义的字符串类型字段应用过滤器。
{:shortdesc}

要在 Kibana 中分析 JSON 类型字段，请完成以下步骤：

1. 要将 JSON message 字段分成多个字段，请将 JSON 格式的消息记录到文件，而不是记录到 STDOUT。 

    JSON 日志条目作为 STDOUT 发送到容器的 Docker 日志文件时，不会将这些日志条目解析为 JSON。因此无法按 @timestamp 字段对消息进行排序以更改其顺序。  

2. 将日志文件添加到容器中可供分析的非缺省日志的列表。有关更多信息，请参阅[从容器收集非缺省日志数据](logging_containers_other_logs.html#logging_containers_collect_data)。 

3. 在 Kibana 中分析登录。有关更多信息，请参阅[使用 Kibana 进行高级日志分析](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana)。

    **注：**如果系统确定某个字段是有效的 JSON，那么会对该字段进行解析，并基于该字段来创建新字段。在 Kibana 中，只有字符串类型的字段值可用于过滤和排序。
    
    显示的 @timestamp 字段值对应于 Elasticsearch 收到日志条目时的时间戳记。反映在容器中生成日志条目的时间的时间戳记会显示为 message 字段的一部分。
    


