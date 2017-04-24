---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 依日誌類型過濾日誌
{:#k4_filter_logs_by_log_type}

依日誌類型檢視及過濾 {{site.data.keyword.Bluemix}} 日誌。
{:shortdesc}

請完成下列步驟，以搜尋包括特定日誌類型的項目：

1. 在 Kibana 的「探索」頁面中，查看其顯示哪些資料子集。如需相關資訊，請參閱[識別 Kibana 探索頁面中顯示的資料](logging_kibana_analize_logs_interactively.html#k4_identify_data)。

2. 在*欄位清單* 中，選取 **type** 欄位。

    例如，在下圖中，只有一個日誌類型可供使用：*syslog*
    
    ![顯示日誌類型欄位的過濾清單](images/k4_filter_log_type_F1.jpg "顯示日誌類型欄位的過濾清單")
   
3. 若要新增過濾器，以搜尋特定日誌類型，請針對您要分析的日誌類型選擇放大鏡按鈕 ![內含模式的放大鏡按鈕](images/k4_include_field_icon.jpg "內含模式的放大鏡按鈕")。

    例如，若要新增過濾器，以包括 *syslog* 的日誌項目，請在*欄位清單* 區段中，選取值 *syslog* 可用的放大鏡按鈕 ![內含模式的放大鏡按鈕](images/k4_include_field_icon.jpg "內含模式的放大鏡按鈕")。下圖顯示包括日誌類型 *syslog* 項目的過濾器。

    ![包括 syslog 日誌類型項目的過濾器](images/k4_filter_log_type_F2.jpg "包括 syslog 日誌類型項目的過濾器")

    若要新增過濾器，以搜尋不包括特定日誌類型的項目，請選擇該值的放大鏡按鈕 ![排除模式的放大鏡按鈕](images/k4_exclude_field_icon.jpg "排除模式的放大鏡按鈕")。

     例如，若要新增過濾器，以排除 *syslog* 的日誌項目，請在*欄位清單* 區段中，選取值 *syslog* 可用的放大鏡按鈕 ![排除模式的放大鏡按鈕](images/k4_exclude_field_icon.jpg "排除模式的放大鏡按鈕")。下圖顯示排除日誌類型 *syslog* 項目的過濾器。
     
     ![排除 syslog 日誌類型項目的過濾器](images/k4_filter_log_type_F3.jpg "排除 syslog 日誌類型項目的過濾器")



