---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 常見問題與解答
{: #logging_qa}

以下是關於使用 {{site.data.keyword.Bluemix}} 記載功能的常見問題與解答。{:shortdesc}

* [如果在 Kibana 中看不到我的容器所產生的 JSON 日誌，我該怎麼辦](logging_qa.html#logging_qa_no_JSON_data_kibana)


## 如果在 Kibana 中看不到我的容器所產生的 JSON 日誌，我該怎麼辦
{: #logging_qa_no_JSON_data_kibana}

以 stdout 形式將 JSON 日誌傳送至 Docker 日誌時，不會將它們剖析為 JSON，因此，無法依 @timestamp 欄位排序來變更其順序。 

所顯示的 @timestamp 值是 ElasticSearch 收到日誌時的時間戳記。 

反映在容器中產生日誌之時刻的時間戳記，會顯示為訊息欄位的一部分。

若要將訊息欄位區隔為多個欄位，請將 JSON 記載到檔案，而非 stdout。然後，在 Kibana 中排序日誌。
