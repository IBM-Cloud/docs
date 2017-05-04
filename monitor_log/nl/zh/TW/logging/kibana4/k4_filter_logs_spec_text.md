---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 針對欄位值中的特定文字過濾日誌
{:#k4_filter_logs_spec_text}

檢視及搜尋欄位值中包括特定文字的項目。{:shortdesc}

**注意：**您只能對由 Elasticsearch 分析器分析的字串欄位，進行任意文字搜尋。 
    
當 Elasticsearch 分析字串欄位的值時，它會依單字界限分割文字（如 Unicode Consortium 所定義）、移除標點符號，並將所有單字變成小寫。
    
請完成下列步驟，以搜尋欄位值中包括特定文字的項目：

1. 在 Kibana 的「探索」頁面中，查看其顯示哪些資料子集。如需相關資訊，請參閱[識別 Kibana 探索頁面中顯示的資料]((logging_kibana_analize_logs_interactively.html#k4_identify_data)。

2. 識別 ElasticSearch 中預設分析的欄位。

    若要顯示可用來搜尋及過濾日誌資料的分析欄位完整清單，請[重新載入欄位清單](logging_kibana_analize_logs_interactively.html#kibana_discover_view_reload_fields)。然後，在「探索」頁面可用的*欄位清單*中，完成下列步驟：
    
    1. 按一下配置圖示 ![配置圖示](images/k4_configure_icon.jpg "配置圖示")。即會顯示**選取的欄位** 區段，您可以在這裡過濾欄位。

        ![顯示包含特定屬性之欄位的「配置」區段](images/k4_reset_filters.jpg "顯示包含特定屬性之欄位的「配置」區段")
    
    2. 若要識別已分析的欄位，請針對**已分析**搜尋欄位選取**是**。

        ![已分析的屬性](images/k4_reset_filters_analyze_options.jpg "已分析的屬性")
    
        即會顯示已分析欄位的清單。
    
        ![已分析欄位的清單](images/k4_list_analyzed_fields.jpg "已分析欄位的清單")
        
         
    3. 檢查您要在其中尋找任意文字的欄位，是否為 ElasticSearch 預設分析的欄位。
    
3. 如果已分析該欄位，請修改查詢，以在日誌中搜尋欄位值中包括該任意文字的項目。

    
**範例**

如果您從 {{site.data.keyword.Bluemix}} 使用者介面為 Cloud Foundry (CF) 應用程式啟動 Kibana，而且您想要尋找包括訊息 ID *CWWKT0016I:* 的特定訊息，請修改搜尋為包括該任意文字。
    
1. 檢查所載入的搜尋查詢，以及顯示在「探索」頁面中的資料。
       
    ![預設搜尋查詢](images/k4_filter_by_text_default_query.jpg "預設搜尋查詢")
        
2. 若要搜尋訊息 ID *CWWKT0016I*，請修改搜尋查詢，然後按 **Enter** 鍵：
    
    ```
	application_id:f52f6016-3aab-4b5c-aa2e-5493747cb978 AND message:"CWWKT0016I:" 
	```
        
    ![修改查詢](images/k4_filter_by_text_modify_query.jpg "修改查詢")
      
    
此表格顯示 CF 應用程式中，*message* 欄位值中包含文字 *CWWKT0016I* 的項目。
    
![新搜尋視圖](images/k4_filter_by_text_result_query.jpg "新搜尋視圖")     	
        
 
 
