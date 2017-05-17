---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# よくある質問と回答
{: #logging_qa}

ここでは、{{site.data.keyword.Bluemix}} ロギング機能の使用に関するよくある質問に対する回答を示します。
{:shortdesc}

* [Kibana のマイ・コンテナーによって生成された JSON ログを表示できない場合、どうすればよいですか?](logging_qa.html#logging_qa_no_JSON_data_kibana)


## Kibana のマイ・コンテナーによって生成された JSON ログを表示できない場合、どうすればよいですか?
{: #logging_qa_no_JSON_data_kibana}

JSON ログが stdout として Docker ログに送信されると、それらは JSON としては解析されないため、@timestamp フィールドによってソートして順序を変更することはできません。
 

表示される @timestamp 値は、Elasticsearch によりログが受信された時刻のタイム・スタンプです。 

コンテナー中でのログ生成時刻を示すタイム・スタンプは、メッセージ・フィールドの一部として表示されます。

message フィールドを分離して複数のフィールドにするには、JSON を stdout ではなくファイルにログ記録します。その後、Kibana でログをソートします。

