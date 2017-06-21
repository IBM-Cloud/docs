---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Cloud Foundry アプリケーションの Kibana ログ・フォーマット
{: #kibana_log_format_cf}

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


