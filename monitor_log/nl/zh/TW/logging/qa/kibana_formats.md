---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Kibana 日誌格式
{: #kibana_formats}

您可以配置 Kibana，以在*探索* 頁面中顯示每一個日誌項目的不同欄位。
{:shortdesc}



## Cloud Foundry 應用程式的 Kibana 日誌格式
{: #kibana_log_format_cf}

您可以配置 Kibana，以在*探索* 頁面顯示每一個日誌項目的下列欄位：


| 欄位 | 說明 |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> 記載事件的時間。<br> 時間戳記最多定義到毫秒。 |
| @version | 事件的版本。 |
| ALCH_TENANT_ID | {{site.data.keyword.Bluemix_notm}} 空間的 ID。 |
| \_id | 日誌文件的唯一 ID。 |
| \_index | 日誌項目的索引。 |
| \_type | 日誌類型；例如 *syslog*。 |
| app_name | {{site.data.keyword.Bluemix_notm}} 應用程式的名稱。 |
| application_id | {{site.data.keyword.Bluemix_notm}} 應用程式的唯一 ID。 |
| host | 產生日誌資料的應用程式名稱。 |
| instance_id | 產生日誌資料之應用程式實例的實例 ID。 |
| loglevel | 所記載事件的嚴重性。 |
| message | 元件所發出的訊息。<br> 訊息會視環境定義而改變。 |
| message_type | 將日誌訊息寫入其中的串流。<br> * **OUT** 是指 stdout 串流。<br> * **ERR** 是指 stderr 串流。 |
| org_id | {{site.data.keyword.Bluemix_notm}} 組織的唯一 ID。 |
| org_name | 在其中編譯打包應用程式之 {{site.data.keyword.Bluemix_notm}} 組織的名稱。 |
| origin | 產生事件的元件。 |
| source_id | 產生日誌的元件。<br> 下列清單說明來自各元件的日誌：<br> * **API**：針對要求變更應用程式狀態之 API 呼叫所記載的回應。<br> * **APP**：已記載的應用程式回應。<br> * **CELL**：已記載的 Diego Cell 回應，指出應用程式開始、停止或當機的時間。<br> * **LGR**：已記載的日誌聚集器回應，指出記載程序的問題。<br> * **RTR**：當路由器將 HTTP 要求遞送至應用程式時，已記載的路由器回應。<br> * **SSH**：當使用者使用 `cf ssh` 指令來存取應用程式容器時，已記載的 Diego Cell 回應。<br> * **STG**：將應用程式編譯打包或重新編譯打包時，已記載的 Diego Cell 或 Droplet Execution Agent 回應。 |
| space_name | 在其中編譯打包應用程式之 {{site.data.keyword.Bluemix_notm}} 空間的名稱。 |
| timestamp | 記載事件的時間。時間戳記最多定義到毫秒。 |
{: caption="表 1. CF 應用程式的欄位" caption-side="top"}



## Docker 容器的 Kibana 日誌格式
{: #kibana_log_format_containers}

您可以配置 Kibana，以在*探索* 頁面顯示每一個日誌項目的下列欄位：


| 欄位 | 說明 |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> 記載事件的時間。<br> 時間戳記最多定義到毫秒。 |
| @version | 事件的版本。 |
| ALCH_TENANT_ID | {{site.data.keyword.Bluemix_notm}} 空間的 ID。 |
| \_id | 日誌文件的唯一 ID。 |
| \_index | 日誌項目的索引。 |
| \_type | 日誌類型；例如 *logs*。 |
| group_id | 群組 ID<br> *對於單一容器，值為 **0000**。<br> * 對於容器群組，值為群組的 GUID。  |
| host | 容器執行所在的主機名稱。 |
| instance | 單一容器的實例 GUID。容器群組的實例 ID 清單。|
| log | 短訊。 |
| message | 完整訊息。 |
| path | 日誌在容器內所位於的路徑及日誌名稱。 |
| stream | 指定日誌類型：stdout、stderr |
| time | 事件發生時的日期和時間。時間戳記最多定義到毫秒。|
| timestamp | 所記載事件的日期和時間。時間戳記最多定義到毫秒。 |
{: caption="表 1. Docker 容器的欄位" caption-side="top"}


## Message Hub 的 Kibana 日誌格式
{: #kibana_log_format_messagehub}

您可以配置 Kibana，以在*探索* 頁面顯示每一個日誌項目的下列欄位：


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
{: caption="表 1. Message Hub 事件的欄位" caption-side="top"}

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
&#95;id:
    AVqu6vJl1zcfr8KYMI95
&#95;type:
    logs
&#95;index:
    logstash-2017.03.08
```
