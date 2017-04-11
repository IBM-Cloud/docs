---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Kibana log format for Message Hub
{: #kibana_log_format_messagehub}

You can configure Kibana to display in the *Discover* page the following fields for each log entry:
{:shortdesc}

| Field | Description |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> The time of the logged event. <br> The timestamp is defined up to the millisecond. |
| @version | Version of the event. |
| ALCH_TENANT_ID | ID of the {{site.data.keyword.Bluemix_notm}} space. |
| \_id | The unique id for your log document. |
| \_index | The index for your log entry. |
| \_type | The type of log; for example, *syslog*. |
| loglevel | The severity of the logged event, for example, **Info**. |
| module | This field is set to **MessageHub**. |


Example of a log entry:

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
_id:
    AVqu6vJl1zcfr8KYMI95
_type:
    logs
_index:
    logstash-2017.03.08

```
