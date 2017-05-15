---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Docker 容器的 Kibana 日誌格式
{: #kibana_log_format_containers}

您可以配置 Kibana，以在*探索* 頁面顯示每一個日誌項目的下列欄位：
{:shortdesc}

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


