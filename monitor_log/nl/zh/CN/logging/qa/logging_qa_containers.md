---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 常见问题及解答
{: #logging_qa}

下面是对有关使用 {{site.data.keyword.Bluemix}} 日志记录功能的常见问题的解答。
{:shortdesc}

* [如果在 Kibana 中看不到我的容器生成的 JSON 日志该怎么办](logging_qa.html#logging_qa_no_JSON_data_kibana)


## 如果在 Kibana 中看不到我的容器生成的 JSON 日志该怎么办
{: #logging_qa_no_JSON_data_kibana}

JSON 日志作为 stdout 发送到 Docker 日志时，不会将这些日志解析为 JSON，因此无法按 @timestamp 字段对这些日志进行排序以更改其顺序。 

显示的 @timestamp 值是 ElasticSearch 收到日志时的时间戳记。 

反映在容器中生成日志的时间的时间戳记会显示为 message 字段的一部分。

要将 message 字段分成多个字段，请将 JSON 记录到文件，而不是记录到 stdout。然后，在 Kibana 中对日志排序。
