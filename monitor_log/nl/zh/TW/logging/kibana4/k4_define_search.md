---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 定義自訂搜尋查詢
{:#k4_define_search}

您可以在「探索」頁面的搜尋列中，使用 Lucene 查詢語言來定義及儲存搜尋查詢。您可以為每一個搜尋套用過濾器，以精簡可用於分析的項目。{:shortdesc}

請完成下列作業，以定義自訂搜尋：

1. 存取 Cloud Foundry (CF) 應用程式或容器的**日誌**標籤。 

    1. 在 {{site.data.keyword.Bluemix}} 儀表板中，按一下應用程式名稱或容器。
    2. 若為 CF 應用程式，請按一下**日誌**標籤。若為容器，請按一下**監視及日誌**，然後選取**記載**標籤。
    
    即會顯示日誌。

2. 存取 Kibana。按一下**進階視圖** ![「進階視圖」鏈結](images/logging_advanced_view.jpg "「進階視圖」鏈結")。即會顯示 Kibana 儀表板。

    當您存取 Kibana 時，會套用預設搜尋。您可以看到啟動 Kibana 之資源實例清單的日誌。您可以針對該空間中的任何或所有 {{site.data.keyword.Bluemix_notm}} 資源過濾日誌。

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



## 刪除搜尋
{: #k4_delete_search}

若要刪除搜尋，請在「設定」頁面中完成下列步驟：

1. 在「設定」頁面中，選取**物件**標籤。

2. 在**搜尋**標籤中，選取您要刪除的搜尋。

3. 按一下**刪除**。


## 匯出搜尋
{: #k4_export_search}

若要匯出搜尋，請在「設定」頁面中完成下列步驟：

1. 在「設定」頁面中，選取**物件**標籤。

2. 在**搜尋**標籤中，選取您要匯出的搜尋。

3. 按一下**匯出**。

4. 儲存檔案。

 
## 匯入搜尋
{: #k4_import_search}

若要匯入搜尋，請在「設定」頁面中完成下列步驟：

1. 在「設定」頁面中，選取**物件**標籤。

2. 在**搜尋**標籤中，選取**匯入**。

3. 選取檔案，然後按一下**開啟**。

該搜尋即會新增至搜尋清單中。

## 重新整理搜尋的內容
{: #k4_refresh_search}

若要手動重新整理搜尋的內容，您可以按一下搜尋列中可用的放大鏡。 

若要自動重新整理「探索」頁面中顯示的資料，您可以配置重新整理間隔。重新整理間隔的現行值會顯示在「探索」頁面的功能表列中。依預設，自動重新整理設定為**關閉**。

請完成下列步驟，以設定重新整理間隔：

1. 在「探索」頁面中，按一下功能表列中可用的**時間過濾器**。

2. 按一下**自動重新整理** ![自動重新整理](images/k4_auto_refresh_icon.jpg "自動重新整理")。

3. 從清單中選擇重新整理間隔。 

    ![重新整理間隔選項](images/k4_change_autorefresh.jpg "重新整理間隔選項")


**附註**：啟用自動重新整理間隔之後，您可以按一下「暫停」按鈕 ![暫停](images/k4_auto_refresh_pause_icon.jpg "暫停") 來將它暫停。


## 重新載入搜尋
{: #k4_reload_search}

請完成下列步驟，以載入已儲存的搜尋：

1. 在「探索」頁面的工具列中，按一下**載入搜尋**按鈕 ![載入搜尋](images/k4_load_icon.jpg "載入搜尋")。

2. 選取您要載入的搜尋。 

## 開始新搜尋
{: #k4_new_search}

若要開始新搜尋，請按一下「探索」頁面工具列中的**新搜尋**按鈕 ![新搜尋](images/k4_new_search_icon.jpg "新搜尋")。

## 儲存搜尋 
{: #k4_save_search}

當您儲存搜尋時，會儲存搜尋查詢字串及目前選取的索引型樣。

請完成下列步驟，以在「探索」頁面中儲存目前的搜尋：

1. 在「探索」頁面的工具列中，按一下**儲存搜尋**按鈕 ![儲存搜尋](images/k4_save_search_icon.jpg "儲存搜尋")。

2. 輸入搜尋的名稱。

3. 按一下「儲存」。 
