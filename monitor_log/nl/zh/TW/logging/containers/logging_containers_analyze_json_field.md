---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 分析屬於容器日誌項目一部分的 JSON 訊息欄位
{: #logging_containers_analyze_json_field}

在 Kibana 中，若要分析容器日誌資料，您可以定義新搜尋，並套用 JSON 格式訊息欄位中所定義字串類型欄位的過濾器。
{:shortdesc}

請完成下列步驟，以在 Kibana 中分析 JSON 類型欄位：

1. 若要將 JSON 訊息欄位區隔為多個欄位，請將 JSON 格式的訊息記載到檔案，而非 STDOUT。 

    以 STDOUT 形式將 JSON 日誌項目傳送至容器的 Docker 日誌檔時，不會將它們剖析為 JSON。您無法依 @timestamp 欄位來排序訊息，以變更其順序。  

2. 將日誌檔新增至來自容器可供分析的非預設日誌清單。如需相關資訊，請參閱[收集容器中的非預設日誌資料](logging_containers_other_logs.html#logging_containers_collect_data)。 

3. 在 Kibana 中分析日誌。如需相關資訊，請參閱[使用 Kibana 執行進階日誌分析](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana)。

    **附註：**如果將欄位判斷為有效的 JSON，則會對其進行剖析，並根據它建立新欄位。在 Kibana 中，只能過濾及排序字串類型欄位值。
    
    所顯示的 @timestamp 欄位值會對應至 ElasticSearch 收到日誌項目時的時間戳記。反映在容器中產生日誌項目之時刻的時間戳記，會顯示為訊息欄位的一部分。
    


