---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Kibana ログ・フォーマット
{: #kibana_formats}

ログ項目ごとに異なるフィールドを「*Discover*」ページで表示するように Kibana を構成できます。
{:shortdesc}



## Cloud Foundry アプリケーションの Kibana ログ・フォーマット
{: #kibana_log_format_cf}

各ログ項目の以下のフィールドを「*Discover*」ページで表示するように Kibana を構成できます。


| フィールド | 説明 |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> ログに記録されたイベントの時刻。<br> タイム・スタンプは、ミリ秒単位まで定義されます。 |
| @version | イベントのバージョン。 |
| ALCH_TENANT_ID | {{site.data.keyword.Bluemix_notm}} スペースの ID。 |
| \_id | ログ文書の固有 ID。 |
| \_index | ログ項目のインデックス。 |
| \_type | ログのタイプ (例: *syslog*)。 |
| app_name | {{site.data.keyword.Bluemix_notm}} アプリケーションの名前。 |
| application_id | {{site.data.keyword.Bluemix_notm}} アプリケーションの固有 ID。 |
| ホスト (host) | ログ・データを生成したアプリケーションの名前。 |
| instance_id | ログ・データを生成したアプリケーション・インスタンスのインスタンス ID。 |
| loglevel | ログに記録されたイベントの重大度。 |
| message | コンポーネントによって発行されたメッセージ。<br> メッセージは、コンテキストによって異なります。 |
| message_type | ログ・メッセージが書き込まれたストリーム。<br> * **OUT** は、STDOUT ストリームを指します。<br> * **ERR** は、STDERR ストリームを指します。 |
| org_id | {{site.data.keyword.Bluemix_notm}} 組織の固有 ID。 |
| org_name | アプリがステージ化されている {{site.data.keyword.Bluemix_notm}} 組織の名前。 |
| origin | イベントの発生元コンポーネント。 |
| source_id | ログを生成したコンポーネント。<br> 各コンポーネントからのログは、以下のリストのとおりです。<br> * **API**: アプリ状況の変更を要求する API 呼び出しへの応答がログに記録されます。<br> * **APP**: アプリからの応答がログに記録されます。<br> * **CELL**: アプリの開始、停止、またはクラッシュがいつ起こったのかを示す Diego セルからの応答がログに記録されます。<br> * **LGR**: ロギング処理での問題を示す Loggregator からの応答がログに記録されます。<br> * **RTR**: ルーターが HTTP 要求をアプリに転送したときのルーターからの応答がログに記録されます。<br> * **SSH**: ユーザーが「cf ssh」コマンドを使用してアプリ・コンテナーにアクセスしたときの Diego セルからの応答がログに記録されます。<br> * **STG**: アプリがステージ化または再ステージ化されたときの Diego セルまたは Droplet Execution Agent からの応答がログに記録されます。 |
| space_name | アプリがステージ化されている {{site.data.keyword.Bluemix_notm}} スペースの名前。 |
| timestamp | ログに記録されたイベントの時刻。タイム・スタンプは、ミリ秒単位まで定義されます。 |
{: caption="表 1. CF アプリ用のフィールド" caption-side="top"}



## Docker コンテナーの Kibana ログ・フォーマット
{: #kibana_log_format_containers}

各ログ項目の以下のフィールドを「*Discover*」ページで表示するように Kibana を構成できます。


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


## Message Hub の Kibana ログ・フォーマット
{: #kibana_log_format_messagehub}

各ログ項目の以下のフィールドを「*Discover*」ページで表示するように Kibana を構成できます。


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
