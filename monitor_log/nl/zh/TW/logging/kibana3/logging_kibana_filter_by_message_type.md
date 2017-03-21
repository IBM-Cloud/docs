---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-16"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 在 Kibana 中依訊息類型過濾 Cloud Foundry 應用程式日誌
<!-- for example, Uploading your data -->
{: #logging_kibana_message_type_filter}
<!-- Provide an appropriate ID above -->

在 Kibana 儀表板上，依訊息類型檢視及過濾 {{site.data.keyword.Bluemix_notm}} 應用程式日誌。您可以從 Cloud Foundry 應用程式的**日誌**標籤存取 Kibana 儀表板。
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
完成下列作業，以在 Kibana 儀表板上，依訊息類型檢視及過濾 Cloud Foundry 應用程式日誌：

1. 存取 Cloud Foundry 應用程式的**日誌**標籤。 

    1. 在 {{site.data.keyword.Bluemix_notm}} **應用程式**儀表板上按一下應用程式名稱。
    2. 按一下**日誌**標籤。 
    
    即會顯示應用程式的日誌。

2. 存取應用程式的 Kibana 儀表板。按一下**進階視圖** ![進階視圖鏈結](images/logging_advanced_view.jpg)。即會顯示 Kibana 儀表板。

3. 在**所有事件**視窗中，按一下右移鍵圖示，以顯示所有欄位。 

    ![「所有事件」視窗，其中含有右移鍵圖示](images/logging_all_events_no_fields.jpg)

4. 在**欄位**窗格中選取 **message_type**，以在**所有事件**視窗中顯示產生各個日誌項目的元件。

    ![「所有事件」視窗，其中已選取 message_type 欄位](images/logging_message_type.png)

5. 在**所有事件**視窗中，按一下日誌事件列，以顯示該事件的詳細資料。選擇顯示您要過濾之 **message_type** 的事件。

    ![「所有事件」視窗，其中顯示所選取日誌事件的詳細資料](images/logging_message_type_add_filter.png)

6. 新增過濾器，以併入或排除某訊息類型的相關資訊。 

    * 若要新增包括某訊息類型相關資訊的過濾器，請在表格的 message_type 列中按一下**放大鏡**圖示 ![放大鏡圖示](images/logging_magnifying_glass.jpg)。 
    
           ![message_type 欄位的過濾條件](images/logging_message_type_filter.png)
    
    * 若要新增排除某訊息類型相關資訊的過濾器，請在表格的 message_type 列中按一下**排除**圖示 ![排除圖示](images/logging_exclusion_icon.png)。 
    
    新的過濾條件已新增至 Kibana 儀表板。

7. 您可以選擇性地重複前一個步驟，為其他訊息類型新增過濾器。若要查看完整的訊息類型清單，請參閱[日誌格式](../logging_view_kibana3.html#kibana_log_format_cf)。

9. 儲存儀表板。    
        
    完成建立過濾器之後，按一下**儲存**圖示 ![儲存圖示](images/logging_save.jpg)，並且為儀表板輸入名稱。 
      
    **附註：**如果您嘗試用來儲存儀表板的名稱包含空格，將不會進行儲存。請輸入不含空格的名稱，然後按一下**儲存**圖示。
    
    ![儲存儀表板名稱](images/logging_save_dashboard.jpg)。

您已建立依訊息類型過濾日誌項目的儀表板。您隨時都可以按一下**資料夾**圖示 ![資料夾圖示](images/logging_folder.jpg)，並依名稱選取儀表板，以載入已儲存的儀表板。
