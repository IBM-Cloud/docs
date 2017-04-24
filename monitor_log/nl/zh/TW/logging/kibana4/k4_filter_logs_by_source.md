---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 依來源過濾 CF 應用程式日誌
{:#k4_filter_logs_by_source}

透過 Kibana 儀表板，依來源類型 Cloud Foundry 應用程式日誌來檢視及過濾。
{:shortdesc}

請完成下列步驟，以搜尋包括特定日誌來源的項目：

1. 在 Kibana 的「探索」頁面中，查看其顯示哪些資料子集。如需相關資訊，請參閱[識別 Kibana 探索頁面中顯示的資料](logging_kibana_analize_logs_interactively.html#k4_identify_data)。

2. 在*欄位清單* 中，選取 **source_id** 欄位。

    ![顯示 source_id 欄位的過濾清單](images/k4_filter_sourceid_F1.jpg "顯示 source_id 欄位的過濾清單")     

3. 若要新增過濾器，以搜尋包括特定 source_id 的項目，請選擇該值的放大鏡按鈕 ![內含模式的放大鏡按鈕](images/k4_include_field_icon.jpg "內含模式的放大鏡按鈕")。

    如需 CF 應用程式可用的日誌來源清單，請參閱 [CF 應用程式的日誌來源](../logging_cf_apps.html#logging_bluemix_cf_apps_log_sources)。

    例如，若要新增過濾器，以包括關於 CF 應用程式啟動、停止或當機的日誌項目，請在*欄位清單* 區段中，選取值 *CELL* 可用的放大鏡按鈕 ![內含模式的放大鏡按鈕](images/k4_include_field_icon.jpg "內含模式的放大鏡按鈕")。下圖顯示已啟用 source_id 值 *CELL* 的過濾器。
    
    ![包括欄位值的過濾器](images/k4_filter_sourceid_F2.jpg "包括欄位值的過濾器")

    若要新增過濾器，以搜尋不包括特定 source_id 的項目，請選擇該值的放大鏡按鈕 ![排除模式的放大鏡按鈕](images/k4_exclude_field_icon.jpg "排除模式的放大鏡按鈕")。
    
    例如，若要新增過濾器，以排除關於 CF 應用程式啟動、停止或當機的日誌項目，請在*欄位清單* 區段中，選取值 *CELL* 可用的放大鏡按鈕 ![排除模式的放大鏡按鈕](images/k4_exclude_field_icon.jpg "排除模式的放大鏡按鈕")。下圖顯示排除 source_id 值 *CELL* 項目的過濾器。

    ![排除欄位值的過濾器](images/k4_filter_sourceid_F3.jpg "排除欄位值的過濾器")




