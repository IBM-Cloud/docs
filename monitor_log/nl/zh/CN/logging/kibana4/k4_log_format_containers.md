---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Docker 容器的 Kibana 日志格式
{: #kibana_log_format_containers}

可以配置 Kibana 以在*发现*页面中显示每个日志条目的以下字段：
{:shortdesc}

| 字段 | 描述 |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`<br> 所记录事件的时间。<br> 时间戳记定义为精确到毫秒。 |
| @version | 事件的版本。 |
| ALCH_TENANT_ID | {{site.data.keyword.Bluemix_notm}} 空间的标识。 |
| \_id | 日志文档的唯一标识。 |
| \_index | 日志条目的索引。 |
| \_type | 日志的类型；例如，*logs*。 |
| group_id | 组标识<br> *对于单个容器，值为 **0000**。<br> * 对于容器组，值为组的 GUID。  |
| host | 运行容器所在主机的主机名。 |
| instance | 对于单个容器，为实例的 GUID。对于容器组，为实例标识的列表。|
| log | 简短消息。 |
| message | 完整消息。 |
| path | 日志在容器内部的路径和日志名称。 |
| stream | 指定日志的类型：stdout 或 stderr |
| time | 事件发生时的日期和时间。时间戳记定义为精确到毫秒。|
| timestamp | 所记录事件的日期和时间。时间戳记定义为精确到毫秒。 |



