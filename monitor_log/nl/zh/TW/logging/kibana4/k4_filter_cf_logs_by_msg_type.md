---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 依訊息類型過濾 CF 應用程式日誌
{:#k4_filter_cf_logs_by_msg_type}

您可以在 Kibana 中，依訊息類型檢視及過濾 Cloud Foundry 應用程式日誌。
{:shortdesc}


請完成下列步驟，以搜尋包括特定訊息類型的項目：

1. 在 Kibana 的「探索」頁面中，查看其顯示哪些資料子集。如需相關資訊，請參閱[識別 Kibana 探索頁面中顯示的資料](logging_kibana_analize_logs_interactively.html#k4_identify_data)。

2. 在*欄位清單* 中，選取 **message_type** 欄位。

    下圖顯示在 CF 應用程式日誌中找到的 *message_type* 欄位的值：
    
    ![顯示 message_type 欄位的過濾清單](images/k4_filter_by_msg_type_f1.jpg "顯示 message_type 欄位的過濾清單")     

3. 若要新增過濾器，以搜尋包括特定 *message_type* 的項目，請選擇該值的放大鏡按鈕 ![內含模式的放大鏡按鈕](images/k4_include_field_icon.jpg "內含模式的放大鏡按鈕")。

    例如，若要新增過濾器，以包括 message_type 值 *OUT* 的日誌項目，請在*欄位清單* 區段中，選取值 *OUT* 可用的放大鏡按鈕 ![內含模式的放大鏡按鈕](images/k4_include_field_icon.jpg "內含模式的放大鏡按鈕")。下圖顯示已啟用 message_type 值 *OUT* 的過濾器。
    
    ![包括欄位值的過濾器](images/k4_filter_by_msg_type_f2.jpg "包括欄位值的過濾器")

    若要新增過濾器，以搜尋不包括特定 *message_type* 的項目，請選擇該值的放大鏡按鈕 ![排除模式的放大鏡按鈕](images/k4_exclude_field_icon.jpg "排除模式的放大鏡按鈕")。
    
    例如，若要新增過濾器，以排除 message_type 值 *OUT* 的日誌項目，請在*欄位清單* 區段中，選取值 *CELL* 可用的放大鏡按鈕 ![排除模式的放大鏡按鈕](images/k4_exclude_field_icon.jpg "排除模式的放大鏡按鈕")。下圖顯示排除 message_type 值 *OUT* 項目的過濾器。

    ![排除欄位值的過濾器](images/k4_filter_by_msg_type_f3.jpg "排除欄位值的過濾器")

