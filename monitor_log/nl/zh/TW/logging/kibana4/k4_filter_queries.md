---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 透過定義自訂搜尋查詢過濾日誌
{:#k4_filter_queries}

您可以在「探索」頁面的搜尋列中，使用 Lucene 查詢語言來定義及儲存搜尋查詢。您可以為每一個搜尋套用過濾器，以精簡可用於分析的項目。{:shortdesc}

請完成下列作業，以使用自訂搜尋來過濾日誌：

1. 存取 Cloud Foundry (CF) 應用程式或容器的**日誌**標籤。 

    1. 在 {{site.data.keyword.Bluemix}} 儀表板中，按一下應用程式名稱或容器。
    2. 若為 CF 應用程式，請按一下**日誌**標籤。若為容器，請按一下**監視及日誌**，然後選取**記載**標籤。
    
    即會顯示日誌。

2. 存取 Kibana。按一下**進階視圖** ![進階視圖鏈結](images/logging_advanced_view.jpg)。即會顯示 Kibana 儀表板。

    當您存取 Kibana 時，會套用預設搜尋。您可以看到啟動 Kibana 之資源實例清單的日誌。您可以針對該空間中的任何或所有 {{site.data.keyword.Bluemix_notm}} 資源過濾日誌。

對 Lucene 而言，正確的說法是「術語」，而不是「關鍵字」。

3. 在「探索」頁面中，查看其顯示哪些資料子集。如需相關資訊，請參閱[識別 Kibana 探索頁面中顯示的資料](logging_kibana_analize_logs_interactively.html#k4_identify_data)。然後，修改預設查詢來過濾項目。

    **附註：**請使用 Lucene 查詢語言來定義自訂查詢。如需相關資訊，請參閱 [Apache Lucene - 查詢剖析器語法 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html){: new_window}
    
    從 {{site.data.keyword.Bluemix_notm}} 啟動 Kibana 時，若要修改查詢及定義多個搜尋準則，您可以使用邏輯術語 **AND** 及 **OR**。這些運算子必須大寫。    
    
    * 若要搜尋關鍵字或部分關鍵字，請輸入一個單字，後面接著萬用字元符號 \*，例如 `Java*`。 
    * 若要搜尋特定詞組，請用雙引號輸入該詞組，例如 `"Java/1.8.0"`。
    * 若要建立較複雜的搜尋，您可以使用邏輯術語 AND 和 OR，例如 `"Java/1.8.0" OR "Java/1.7.0"`。
    * 若要搜尋特定欄位中的值，請以下列格式輸入您的搜尋內容：*log_field_name:search_term*，例如 `instance_id:"1"`。
    * 若要搜尋特定日誌欄位中某範圍的值，請以下列格式輸入您的搜尋內容：*log_field_name:[start_of_range TO end_of_range]*，例如 `instance_id:["1" TO "2"]`。

     例如，若為 CF 應用程式，您可以建立查詢 `application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:["0" TO "1"]`，只列出實例 *0* 及 *1* 的項目。 

4. 儲存查詢，以供稍後重複使用。如需相關資訊，請參閱[儲存搜尋](logging_kibana_filtering_logs.html#k4_save_search)。 

**附註：**如果您需要刪除查詢，請參閱[刪除搜尋](logging_kibana_filtering_logs.html#k4_delete_search)。



