---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 在 Kibana 中過濾日誌
{:#kibana_filtering_logs}

在「探索」頁面中，您可以建立搜尋查詢及套用過濾器，以限制顯示用來進行分析的資訊。{:shortdesc}

* 您可以在「探索」頁面的搜尋列中，定義一個以上的搜尋查詢。搜尋查詢會定義一個日誌項目子集。請使用 Lucene 查詢語言來定義搜尋查詢。 

* 您可以從*欄位清單* 或表格項目中新增過濾器。而過濾器可以透過包含或排除資訊的方式來修正資料選取項目。您可以啟用或停用過濾器、反轉過濾動作、將過濾器切換為開啟或關閉，或是將它整個移除。 

定義新搜尋之後，請儲存它，以供日後在「探索」頁面中重複使用來進行分析，或是建立視覺化，以用在自訂儀表板中。如需相關資訊，請參閱[儲存搜尋](logging_kibana_filtering_logs.html#k4_save_search)。

當您執行新搜尋時，直方圖、表格及「欄位」清單會自動更新，以顯示搜尋結果。若要瞭解會顯示哪些資料，請參閱[識別探索頁面中顯示的資料](k4_identify_data.html#k4_identify_data)。

下列清單概述如何過濾日誌資料的情境：

* 您可以建立自訂搜尋來過濾日誌。如需相關資訊，請參閱[透過定義自訂查詢過濾日誌](k4_filter_queries.html#k4_filter_queries)。

* 您可以在日誌中搜尋欄位值中包括特定文字的項目。如需相關資訊，請參閱[針對欄位值中的特定文字過濾日誌](k4_filter_logs_spec_text.html#k4_filter_logs_spec_text)。
 
* 您可以在日誌中搜尋特定欄位值，或排除日誌中特定欄位值的項目。如需相關資訊，請參閱[針對特定欄位值過濾日誌](k4_filter_logs_spec_field.html#k4_filter_logs_spec_field)。

    * 您可以依日誌類型來過濾日誌。如需相關資訊，請參閱[依日誌類型過濾日誌](k4_filter_logs_by_log_type.html#k4_filter_logs_by_log_type)。
    * 您可以依來源來過濾 CF 應用程式日誌。如需相關資訊，請參閱[依來源過濾 CF 應用程式日誌](k4_filter_logs_by_source.html#k4_filter_logs_by_source)。
    * 您可以依實例 ID 來過濾日誌。如需相關資訊，請參閱[依實例 ID 過濾日誌](k4_filter_logs_by_instance_id.html#k4_filter_logs_by_instance_id)。   
    * 您可以依訊息類型來過濾日誌。如需相關資訊，請參閱[依訊息類型 ID 過濾日誌](k4_filter_cf_logs_by_msg_type.html#k4_filter_cf_logs_by_msg_type)。  
 
* 您可以過濾日誌，以顯示某時段內的項目。如需相關資訊，請參閱[設定時間過濾器](logging_kibana_set_time_filter.html#set_time_filter)。
     

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


## 重新載入搜尋
{: #k4_reload_search}

請完成下列步驟，以載入已儲存的搜尋：

1. 在「探索」頁面的工具列中，按一下**載入搜尋**按鈕 ![載入搜尋](images/k4_load_icon.jpg "載入搜尋")。

2. 選取您要載入的搜尋。 


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




