---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Docker コンテナーの Kibana ログ・フォーマット
{: #kibana_log_format_containers}

各ログ項目の以下のフィールドを「*Discover*」ページで表示するように Kibana を構成できます。
{:shortdesc}

| フィールド | 説明 |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> ログに記録されたイベントの時刻。<br> タイム・スタンプは、ミリ秒単位まで定義されます。 |
| @version | イベントのバージョン。 |
| ALCH_TENANT_ID | {{site.data.keyword.Bluemix_notm}} スペースの ID。 |
| \_id | ログ文書の固有 ID。 |
| \_index | ログ項目のインデックス。 |
| \_type | ログのタイプ (例、*logs*)。 |
| group_id | グループ ID<br> *単一コンテナーの場合、値は **0000** です。<br> * コンテナー・グループの場合、値はグループの GUID です。  |
| ホスト (host) | コンテナーが実行されるホスト名。 |
| インスタンス (instance) | 単一コンテナーのインスタンスの GUID。コンテナー・グループのインスタンス ID のリスト。|
| log | 簡略メッセージ。 |
| message | 完全なメッセージ。 |
| path | ログがコンテナー内にある場所のパスとログ名。 |
| stream | ログのタイプ (stdout、stderr) を指定します。 |
| time | イベント発生日時。タイム・スタンプは、ミリ秒単位まで定義されます。|
| timestamp | ログに記録されたイベントの日時。タイム・スタンプは、ミリ秒単位まで定義されます。 |
{: caption="表 1. Docker コンテナー用のフィールド" caption-side="top"}


