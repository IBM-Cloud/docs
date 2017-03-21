---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 在 Kibana 中依實例 ID 過濾 Cloud Foundry 應用程式日誌
<!-- for example, Uploading your data -->
{: #logging_kibana_instance_id}
<!-- Provide an appropriate ID above -->

在 Kibana 儀表板上，依應用程式的實例 ID (instance_id) 來檢視及過濾 {{site.data.keyword.Bluemix_notm}} 實例日誌。您可以從 Cloud Foundry 應用程式的**日誌**標籤存取 Kibana 儀表板。
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
完成下列作業，以在 Kibana 儀表板上，依 instance_id 檢視及過濾 Cloud Foundry 應用程式日誌：

1. 存取 Cloud Foundry 應用程式的**日誌**標籤。 

    1. 在 {{site.data.keyword.Bluemix_notm}} **應用程式**儀表板上按一下應用程式名稱。
    2. 按一下**日誌**標籤。 
    
    即會顯示應用程式的日誌。

2. 存取應用程式的 Kibana 儀表板。按一下**進階視圖** ![進階視圖鏈結](images/logging_advanced_view.jpg)。即會顯示 Kibana 儀表板。

3. 在 Kibana 儀表板上，按一下**移至儲存的預設值**圖示 ![移至儲存的預設值圖示](images/logging_default_dash.jpg)，以顯示某空間的所有日誌。在**所有事件**視窗中，按一下右移鍵圖示，以顯示所有欄位。 

    ![「所有事件」視窗，其中含有右移鍵圖示](images/logging_all_events_no_fields.jpg)

4. 在**欄位**窗格中選取 **application_id** 和 **instance_id**，以在**所有事件**視窗中顯示 application_id 和 instance_id 欄位。

    ![「所有事件」視窗，其中已選取 application_id 和 instance_id 欄位](images/logging_all_events_app_instance_select.jpg)

5. 在**所有事件**視窗中，按一下日誌事件列，以顯示該事件的詳細資料。選擇顯示您要過濾之 instance_id 的事件。

    ![「所有事件」視窗，其中顯示所選取日誌事件的詳細資料](images/logging_selected_log_event.jpg)

6. 新增過濾器，以併入或排除某應用程式 ID 的相關資訊。 

    * 若要新增包括特定應用程式 ID 相關資訊的過濾器，請在表格的 application_id 列中按一下**放大鏡**圖示 ![放大鏡圖示](images/logging_magnifying_glass.jpg)。 
    
           ![application_id 欄位的過濾條件](images/logging_application_id_filter.jpg)
    
    * 若要新增排除特定應用程式 ID 相關資訊的過濾器，請在表格的 application_id 列中按一下**排除**圖示 ![排除圖示](images/logging_exclusion_icon.png)。 
    
           ![排除某應用程式 ID 的過濾條件](images/logging_application_id_exclude_filter.jpg)
    
    新的過濾條件已新增至 Kibana 儀表板。
 

7. 新增過濾器，以併入或排除某應用程式實例 ID 的相關資訊。 

    * 若要新增包括特定實例 ID 相關資訊的過濾器，請在表格的 instance_id 列中按一下**放大鏡**圖示 ![放大鏡圖示](images/logging_magnifying_glass.jpg)。 

    ![instance_id 欄位的過濾條件](images/logging_instance_id_filter.jpg)

     * 若要新增排除特定實例 ID 相關資訊的過濾器，請在表格的 instance_id 列中按一下**排除**圖示 ![排除圖示](images/logging_exclusion_icon.png)。 
    
           ![排除某實例 ID 的過濾條件](images/logging_application_instance_id_exclude_filter.jpg)
    
    新的過濾條件已新增至 Kibana 儀表板。

9. 儲存儀表板。完成建立過濾器之後，按一下**儲存**圖示 ![儲存圖示](images/logging_save.jpg)，並且為儀表板輸入名稱。 

    **附註：**如果您嘗試用來儲存儀表板的名稱包含空格，將不會進行儲存。請輸入不含空格的名稱，然後按一下**儲存**圖示。

    ![儲存儀表板名稱](images/logging_save_dashboard.jpg)。

您已建立依 instance_id 過濾日誌項目的儀表板。您隨時都可以按一下**資料夾**圖示 ![資料夾圖示](images/logging_folder.jpg)，並依名稱選取儀表板，以載入已儲存的儀表板。 
