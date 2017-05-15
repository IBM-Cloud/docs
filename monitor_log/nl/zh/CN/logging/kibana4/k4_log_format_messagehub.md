---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Message Hub 的 Kibana 日志格式
{: #kibana_log_format_messagehub}

可以配置 Kibana 以在*发现*页面中显示每个日志条目的以下字段：
{:shortdesc}

| 字段 | 描述 |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`<br> 所记录事件的时间。<br> 时间戳记定义为精确到毫秒。 |
| @version | 事件的版本。 |
| ALCH_TENANT_ID | {{site.data.keyword.Bluemix_notm}} 空间的标识。 |
| \_id | 日志文档的唯一标识。 |
| \_index | 日志条目的索引。 |
| \_type | 日志的类型；例如，*syslog*。 |
| loglevel | 所记录事件的严重性；例如，**Info**。 |
| module | 此字段设置为 **MessageHub**。 |
{: caption="表 1. Message Hub 事件的字段" caption-side="top"}

日志条目的示例：

```
March 8th 2017, 17:15:16.454	

message:
    Creating topic ABC
@version:
    1
@timestamp:
    March 8th 2017, 17:15:16.454
loglevel:
    Info
module:
    MessageHub
ALCH_TENANT_ID:
    3d8d2eae-f3f0-44f6-9717-126113a00b51
&#95;id:
    AVqu6vJl1zcfr8KYMI95
&#95;type:
    logs
&#95;index:
    logstash-2017.03.08
```
