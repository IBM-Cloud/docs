---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Cloud Foundry 应用程序的 Kibana 日志格式
{: #kibana_log_format_cf}

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
| app_name | {{site.data.keyword.Bluemix_notm}} 应用程序的名称。 |
| application_id | {{site.data.keyword.Bluemix_notm}} 应用程序的唯一标识。 |
| host | 生成日志数据的应用程序的名称。 |
| instance_id | 生成日志数据的应用程序实例的实例标识。 |
| loglevel | 所记录事件的严重性。 |
| message | 组件发出的消息。<br> 消息根据上下文而变化。 |
| message_type | 将日志消息写入其中的流。<br> * **OUT** 是指 stdout 流<br> * **ERR** 是指 stderr 流。 |
| org_id | {{site.data.keyword.Bluemix_notm}} 组织的唯一标识 |
| org_name | 在其中对应用程序编译打包的 {{site.data.keyword.Bluemix_notm}} 组织的名称。 |
| origin | 事件源于的组件。 |
| source_id | 生成日志的组件。<br> 以下列表描述了每个组件的日志：<br> ***API**：记录的对请求更改应用程序状态的 API 调用的响应。<br> * **APP**：记录的来自应用程序的响应。<br> * **CELL**：记录的来自 Diego 单元的响应，用于指示应用程序启动、停止或崩溃情况。<br> * **LGR**：记录的来自 Loggregator 的响应，用于指示日志记录进程发生的问题。<br> * **RTR**：路由器将 HTTP 请求路由到应用程序时记录的来自路由器的响应。<br> * **SSH**：用户使用“cf ssh”命令访问应用程序容器时记录的来自 Diego 单元的响应。<br> * **STG**：对应用程序编译打包或重新编译打包时记录的来自 Diego 单元或 Droplet Execution Agent 的响应。 |
| space_name | 在其中对应用程序编译打包的 {{site.data.keyword.Bluemix_notm}} 空间的名称。 |
| timestamp | 所记录事件的时间。时间戳记定义为精确到毫秒。 |
{: caption="表 1. CF 应用程序的字段" caption-side="top"}


