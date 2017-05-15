---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 在 Kibana 中以查詢來過濾 Cloud Foundry 應用程式日誌
{: #logging_kibana_query}

使用 Kibana 來建立查詢，以在您的日誌中搜尋重要詞彙，並依那些詞彙進行過濾。Kibana 可讓您在儀表板上以視覺化方式比較查詢。您可以從 Cloud Foundry 應用程式的**日誌**標籤存取 Kibana 儀表板。
{:shortdesc}

完成下列作業，以在 Kibana 儀表板上建立 Cloud Foundry 應用程式日誌的查詢：

1. 存取 Cloud Foundry 應用程式的**日誌**標籤。 

    1. 在 {{site.data.keyword.Bluemix_notm}} **應用程式**儀表板上按一下應用程式名稱。
    2. 按一下**日誌**標籤。 
    
    即會顯示應用程式的日誌。

2. 存取應用程式的 Kibana 儀表板。按一下**進階視圖** ![「進階視圖」鏈結](images/logging_advanced_view.jpg "「進階視圖」鏈結")。即會顯示 Kibana 儀表板。

3. 在 Kibana 儀表板上，按一下**查詢** ![「查詢」圖示](images/logging_query.jpg "「查詢」圖示")，以顯示欄位。當您存取 Kibana 以從應用程式的**日誌**標籤檢視應用程式日誌時，會建立查詢來顯示應用程式之 application_id 的所有日誌。
	
    若要編輯查詢，請按一下**查詢**欄位，並輸入搜尋詞彙。

    * 若要搜尋關鍵字或部分關鍵字，請輸入一個單字，後面接著萬用字元符號 \*，例如 `Java*`。 
	* 若要搜尋特定詞組，請用雙引號輸入該詞組，例如 `"Java/1.8.0"`。
	* 若要建立較複雜的搜尋，您可以使用邏輯術語 AND 和 OR，例如 `"Java/1.8.0" OR "Java/1.7.0"`。
	* 若要搜尋特定欄位內的值，請以下列格式輸入您的搜尋內容：*log_field_name:search_term*，例如 `instance_id:1`。
	* 若要搜尋特定日誌欄位中某範圍的值，請以下列格式輸入您的搜尋內容：*log_field_name:[start_of_range TO end_of_range]*，例如 `instance_id:[1 TO 2]`。

4. 如果您要比較兩個不同查詢的結果，可以新增另一個查詢詞彙至儀表板。若要新增另一個查詢，請按一下**查詢**欄位結尾的 **+** 圖示。

    ![查詢欄位](images/logging_query_field.jpg "查詢欄位")
	
    即會顯示包含萬用字元 \* 的新建**查詢**欄位。此查詢會要求 Kibana 包含所有項目。
	
    ![其他查詢欄位](images/logging_additional_query_field.jpg "其他查詢欄位")
	
    您的儀表板已更新，以反映新建查詢的結果。**依時間排列事件**窗格會顯示這兩項查詢的圖形表示法，並且在括弧中顯示各查詢的詞彙數。 
	
    ![儀表板，其中顯示這兩項查詢的圖形](images/logging_dashboard_queries.jpg "儀表板，其中顯示這兩項查詢的圖形")
	
5. 按一下新建**查詢**欄位，以編輯其內容並新增查詢條件，例如 `instance_id:1`。使用**依時間排列事件**窗格來比較查詢的結果。

    ![儀表板，其中顯示這兩項查詢的圖形](images/logging_dashboard_queries2.jpg "儀表板，其中顯示這兩項查詢的圖形")

6. 若要刪除查詢，請將滑鼠移至您要刪除的**查詢**欄位上方，以顯示**刪除**圖示。按一下**刪除**圖示。

    ![含有刪除圖示的查詢欄位](images/logging_delete_query.jpg "含有刪除圖示的查詢欄位")

7. 若要使用可辨識的名稱來儲存此儀表板，請按一下**儲存**圖示 ![「儲存」圖示](images/logging_save.jpg "「儲存」圖示")，並且為儀表板輸入名稱。 

    **附註：**如果您嘗試用來儲存儀表板的名稱包含空格，將不會進行儲存。請輸入不含空格的名稱，然後按一下**儲存**圖示。

    ![儲存儀表板名稱](images/logging_save_dashboard.jpg "儲存儀表板名稱")


