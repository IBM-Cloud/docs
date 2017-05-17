---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Message Hub の Kibana ログ・フォーマット
{: #kibana_log_format_messagehub}

各ログ項目の以下のフィールドを「*Discover*」ページで表示するように Kibana を構成できます。
{:shortdesc}

| フィールド | 説明 |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> ログに記録されたイベントの時刻。<br> タイム・スタンプは、ミリ秒単位まで定義されます。 |
| @version | イベントのバージョン。 |
| ALCH_TENANT_ID | {{site.data.keyword.Bluemix_notm}} スペースの ID。 |
| \_id | ログ文書の固有 ID。 |
| \_index | ログ項目のインデックス。 |
| \_type | ログのタイプ (例: *syslog*)。 |
| loglevel | ログに記録するイベントの重大度 (例えば、**Info**)。 |
| module | このフィールドは、**MessageHub** に設定されます。 |
{: caption="表 1. メッセージング・ハブ・イベント用のフィールド" caption-side="top"}

ログ項目の例:

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
