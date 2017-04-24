---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 依實例 ID 過濾日誌
{:#k4_filter_logs_by_instance_id}

依實例 ID 檢視及過濾 {{site.data.keyword.Bluemix}} 日誌。
{:shortdesc}

請完成下列步驟，以在 Kibana 儀表板上，依實例 ID 檢視及過濾日誌：

1. 在 Kibana 的「探索」頁面中，查看其顯示哪些資料子集。如需相關資訊，請參閱[識別 Kibana 探索頁面中顯示的資料](logging_kibana_analize_logs_interactively.html#k4_identify_data)。

2. 在*欄位清單* 中，選取下列其中一個欄位，以搜尋特定實例 ID：

    * **instance_ID**：此欄位列出 Cloud Foundry 應用程式的日誌中可用的不同實例 ID。 
    * **instance**：此欄位列出所有容器群組實例的不同 GUID。 

    例如，下圖顯示 CF 應用程式的不同實例值：
    
    ![顯示 instance_id 欄位的過濾清單](images/k4_filter_instanceid_f1.jpg "顯示 instance_id 欄位的過濾清單")
   
3. 若要新增過濾器，以搜尋特定日誌類型，請針對您要分析的日誌類型選擇放大鏡按鈕 ![內含模式的放大鏡按鈕](images/k4_include_field_icon.jpg "內含模式的放大鏡按鈕")。

   例如，若要新增過濾器，以包括 CF 應用程式實例 *2* 的項目，請在「欄位清單」區段中，選取值 *2* 可用的放大鏡按鈕 ![內含模式的放大鏡按鈕](images/k4_include_field_icon.jpg "內含模式的放大鏡按鈕")。下圖顯示包括實例 *2* 項目的過濾器。
    
    ![包括實例 2 之 instance_id 項目的過濾器](images/k4_filter_instanceid_f2.jpg "包括實例 2 之 instance_id 項目的過濾器")

    若要新增過濾器，以搜尋不包括特定實例 ID 的項目，請選擇該值的放大鏡按鈕 ![排除模式的放大鏡按鈕](images/k4_exclude_field_icon.jpg "排除模式的放大鏡按鈕")。

     例如，若要新增過濾器，以排除 CF 應用程式實例 *2* 的項目，請在「欄位清單」區段中，選取值 *2* 可用的放大鏡按鈕 ![排除模式的放大鏡按鈕](images/k4_exclude_field_icon.jpg "排除模式的放大鏡按鈕")。下圖顯示排除實例 *2* 項目的過濾器。
     
      ![排除實例 2 之 instance_id 項目的過濾器](images/k4_filter_instanceid_f3.jpg "排除實例 2 之 instance_id 項目的過濾器")

