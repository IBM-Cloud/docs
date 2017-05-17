---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# コンテナー・ログ項目の一部である JSON メッセージ・フィールドの分析
{: #logging_containers_analyze_json_field}

Kibana では、コンテナー・ログ・データを分析するために、新規検索を定義し、JSON フォーマットのメッセージ・フィールドに定義されているストリング・タイプ・フィールド用のフィルターを適用することができます。
{:shortdesc}

Kibana で JSON タイプ・フィールドを分析するには、以下のステップを実行します。

1. JSON メッセージ・フィールドを複数のフィールドに分割するには、STDOUT ではなく JSON フォーマットでメッセージをファイルに記録します。 

    JSON ログ項目が STDOUT としてコンテナーの Docker ログ・ファイルに送信されると、JSON として構文解析されません。@timestamp フィールドによってメッセージをソートして、順序を変更することができなくなります。  

2. コンテナーから分析に使用できるデフォルト以外のログのリストにログ・ファイルを追加します。詳しくは、『[コンテナーからの非デフォルト・ログ・データの収集](logging_containers_other_logs.html#logging_containers_collect_data)』を参照してください。 

3. Kibana でログを分析します。詳しくは、『[Kibana での高度なログ分析](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana)』を参照してください。

    **注:** フィールドが有効な JSON であると判別されると、構文解析され、そこから新規フィールドが作成されます。Kibana でフィルター操作したりソートしたりできるのは、ストリング・タイプのフィールド値のみです。
    
    表示される @timestamp フィールド値は、ログ項目が Elasticsearch によって受け取られたときのタイム・スタンプに相当します。ログ項目がコンテナー内に生成された時間を反映したタイム・スタンプは、メッセージ・フィールドの一部として表示されます。
    


