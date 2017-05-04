---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 針對未列示在*欄位清單* 中的值新增過濾器
{:#k4_add_filter_out_value}

若要針對未顯示在*欄位清單* 中的值新增過濾器，請透過查詢來搜尋包括該值的記錄。然後，從「探索」頁面中可用的表格項目中新增過濾器。
{:shortdesc}

請完成下列步驟，以針對*欄位清單* 區段所顯示的清單中沒有的值，新增過濾器：

1. 在 Kibana 的「探索」頁面中，查看其顯示哪些資料子集。如需相關資訊，請參閱[識別 Kibana 探索頁面中顯示的資料](logging_kibana_analize_logs_interactively.html#k4_identify_data)。

    例如，下圖顯示*欄位清單* 中 CF 應用程式的實例值。 
    
    ![顯示「欄位清單」中的值](images/k4_add_filter_f1.jpg "顯示「欄位清單」中的值")
    
    您對實例號碼 *3* 感興趣，但它不在您可以看到的清單中。

2. 在「探索」頁面中修改查詢，以搜尋特定欄位值。

    例如，若要搜尋實例 *3*，則您輸入的查詢如下：
   `application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:"3"`
    
    ![修改查詢](images/k4_add_filter_f2.jpg "修改查詢")
    
    您可以在表格中看到符合查詢的所有記錄。 
    
 3. 展開某筆記錄，然後選取放大鏡按鈕 ![內含模式的放大鏡按鈕](images/k4_include_field_icon.jpg "內含模式的放大鏡按鈕")，以新增過濾器。
 
     例如，若要新增過濾器，以尋找包含值 *3* 的實例 ID，請按一下 *instance_id* 欄位旁的放大鏡按鈕 ![內含模式的放大鏡按鈕](images/k4_include_field_icon.jpg "內含模式的放大鏡按鈕")。
     
     ![顯示表格](images/k4_add_filter_f3.jpg "顯示表格")
     
4. 確認已新增過濾器。

    例如，下圖顯示您自表格新增過濾器之後，已啟用的過濾器。
    
    ![顯示過濾器](images/k4_add_filter_f4.jpg "顯示過濾器")
    
    
