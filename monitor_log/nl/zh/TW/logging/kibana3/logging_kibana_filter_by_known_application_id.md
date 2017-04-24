---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 在 Kibana 中依已知的應用程式 ID 過濾 Cloud Foundry 應用程式日誌
<!-- for example, Uploading your data -->
{: #logging_kibana_known_application_id}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

如果您知道 Cloud Foundry 應用程式的應用程式 ID，就可以在 Kibana 儀表板上，依應用程式的應用程式 ID (application_id)，快速檢視及過濾日誌。您可以從 Cloud Foundry 應用程式的**日誌**標籤存取 Kibana 儀表板。
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
完成下列作業，以在 Kibana 儀表板上，依已知的應用程式 ID 檢視及過濾 Cloud Foundry 應用程式日誌：

1. 存取 Cloud Foundry 應用程式的**日誌**標籤。 

    1. 在 {{site.data.keyword.Bluemix_notm}} **應用程式**儀表板上按一下應用程式名稱。
    2. 按一下**日誌**標籤。 
    
    即會顯示應用程式的日誌。

2. 存取應用程式的 Kibana 儀表板。按一下**進階視圖** ![進階視圖鏈結](images/logging_advanced_view.jpg)。即會顯示 Kibana 儀表板。

3. 在 Kibana 儀表板上，按一下**資料夾**圖示 ![資料夾圖示](images/logging_folder.jpg)，以顯示列出所有最近儀表板的功能表。 

    **附註：**除了您命名儲存的儀表板之外，此功能表也會根據下列格式，列出未命名的儀表板：*ALCH_TENANT_ID_application_id*。 

    ![儀表板清單](images/logging_list_of_dashboards.jpg)

4. 選取名稱中包含已知 application_id 的儀表板。 

    儀表板會載入並顯示針對 application_id 過濾的資訊。

5. 您可以選擇性地新增更多欄位至過濾器區段，例如 **instance_id**，以啟用或停用依實例 ID 過濾記錄的功能。 
  
    1. 在**所有事件**視窗中，按一下日誌事件列，以顯示該事件的詳細資料。 
	
        ![「所有事件」視窗，其中顯示所選取日誌事件的詳細資料](images/logging_selected_log_event.jpg)
	
    2. 選擇顯示您要過濾之欄位值的事件。
	
    3. 新增過濾器。
    
        若要新增包括該特定欄位值相關資訊的過濾器，請在包含您要過濾之欄位的表格列中，按一下**放大鏡**圖示 ![放大鏡圖示](images/logging_magnifying_glass.jpg)。 
	
        若要新增排除該特定欄位值相關資訊的過濾器，請在包含您要過濾之欄位的表格列中，按一下**排除**圖示 ![排除圖示](images/logging_exclusion_icon.png)。  

        新的過濾條件已新增至 Kibana 儀表板。
	
	    ![instance_id 欄位的過濾條件](images/logging_instance_id_filter.jpg)
	
6. 請使用可辨識的名稱來儲存此儀表板。 

    按一下**儲存**圖示 ![儲存圖示](images/logging_save.jpg)，並且為儀表板輸入名稱。 

    **附註：**如果您嘗試用來儲存儀表板的名稱包含空格，將不會進行儲存。請輸入不含空格的名稱，然後按一下**儲存**圖示。

    ![儲存儀表板名稱](images/logging_save_dashboard.jpg)。


您已建立依應用程式 ID 和實例 ID 過濾日誌項目的儀表板。您隨時都可以按一下**資料夾**圖示 ![資料夾圖示](images/logging_folder.jpg)，並依名稱選取儀表板，以載入已儲存的儀表板。
