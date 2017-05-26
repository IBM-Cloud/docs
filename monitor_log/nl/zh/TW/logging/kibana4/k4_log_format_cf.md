---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Cloud Foundry 應用程式的 Kibana 日誌格式
{: #kibana_log_format_cf}

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


