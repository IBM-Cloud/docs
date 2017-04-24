---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Message Hub 的 Kibana 日誌格式
{: #kibana_log_format_messagehub}

您可以配置 Kibana，以在*探索* 頁面顯示每一個日誌項目的下列欄位：
{:shortdesc}

| 欄位 | 說明 |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> 記載事件的時間。<br> 時間戳記最多定義到毫秒。 |
| @version | 事件的版本。 |
| ALCH_TENANT_ID | {{site.data.keyword.Bluemix_notm}} 空間的 ID。 |
| \_id | 日誌文件的唯一 ID。 |
| \_index | 日誌項目的索引。 |
| \_type | 日誌類型；例如 *syslog*。 |
| loglevel | 所記載事件的嚴重性，例如 **Info**。 |
| module | 此欄位設為 **MessageHub**。 |


日誌項目的範例：

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
