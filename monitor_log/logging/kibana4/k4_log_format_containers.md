---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Kibana log format for Docker containers
{: #kibana_log_format_containers}

You can configure Kibana to display in the *Discover* page the following fields for each log entry:
{:shortdesc}

| Field | Description |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> The time of the logged event. <br> The timestamp is defined up to the millisecond. |
| @version | Version of the event. |
| ALCH_TENANT_ID | ID of the {{site.data.keyword.Bluemix_notm}} space. |
| \_id | The unique id for your log document. |
| \_index | The index for your log entry. |
| \_type | The type of log; for example, *logs*. |
| group_id | Group ID <br> * For a single container, the value is **0000**. <br> * For a container group, the value is the GUID of the group.  |
| host | Host name where the container runs. |
| instance | GUID of the instance for a single container. List of instance IDs for a container group.|
| log | Short message. |
| message | Full message. |
| path | Path and log name where the log is located inside the container. |
| stream | Specifies the type of log: stdout, stderr |
| time | The date and time of the event when it happened. The timestamp is defined up to the millisecond.|
| timestamp | The date and time of the logged event. The timestamp is defined up to the millisecond. |



