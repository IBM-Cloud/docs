---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 在 Kibana 中使用視覺化來分析日誌 
{:#logging_kibana_visualizations}

請利用 Kibana 中的*視覺化* 頁面來建立圖形及表格等視覺化，讓您可以用來分析日誌資料及比較結果。{:shortdesc}

您可以使用個別視覺化來分析日誌。 

* 您可以從您定義並儲存在*探索* 頁面中的搜尋來建立視覺化，也可以從您在*視覺化* 頁面中定義的新查詢來建立視覺化。搜尋會定義視覺化顯示的資料子集。

* 您選擇的視覺化類型，會決定如何顯示資料以進行分析。

下表列出不同的視覺化類型：

| 視覺化類型 | 說明 |
|-----------------------|-------------|
| 區域圖 | 以圖形方式顯示定量資料。可用來比較兩組以上的聚集資料。 |
| 資料表 | 針對組合集成，以表格方式顯示原始資料。 |
| 折線圖 | 顯示時間型資料。可用來比較兩組以上的時間型的聚集資料。 |
| Markdown 小組件 | 可用來顯示文字資訊。 |
| 度量值 | 可用來顯示相符數，或是數值欄位的確切平均值。 |
| 圓餅圖 | 可用來顯示欄位的不同值。 | 
| 垂直長條圖 | 顯示時間型資料，以及非時間型資料。可用來將資料分組。 |

在「視覺化」頁面中，您可以執行下列任何作業：

| 作業 | 相關資訊 |
|------|------------------|
| [建立新的視覺化](logging_kibana_visualizations.html#logging_k4_visualizations_create) | 您可以從您定義並儲存在*探索* 頁面中的搜尋來建立視覺化，也可以從您在*視覺化* 頁面中定義的新查詢來建立視覺化。 |
| [儲存視覺化](logging_kibana_visualizations.html#logging_kibana_visualizations_save) | 您可以儲存視覺化，以供稍後重複使用。 |
| [載入視覺化](logging_kibana_visualizations.html#logging_kibana_visualizations_reload) | 您可以上傳視覺化，以更新其資料、予以修改、分析資料。 |
| [刪除視覺化](logging_kibana_visualizations.html#logging_kibana_visualizations_delete) | 刪除不需要的視覺化。 |
| [匯出視覺化](logging_kibana_visualizations.html#logging_kibana_visualizations_export) | 您可以將視覺化匯出成 JSON 檔案。  |
| [匯入視覺化](logging_kibana_visualizations.html#logging_kibana_visualizations_import) | 您可以將視覺化匯入成 JSON 檔案。  |
| [共用視覺化](logging_kibana_visualizations.html#logging_kibana_visualizations_share) | 您可以透過 HTML 原始檔或透過 Kibana 儀表板來共用視覺化。  |


## 在 Kibana 中從查詢建立視覺化
{:#logging_k4_visualizations_create}

請完成下列步驟，以從「視覺化」頁面中建立視覺化：

1. 啟動 Kibana，然後選取**視覺化**頁面。

2. 建立新的視覺化。在工具列中，按一下**新建視覺化**按鈕 ![新建視覺化](images/k4_visualization_new_icon.jpg "新建視覺化")。

3. 選取一個視覺化。
    
4. 選取搜尋來源。選擇下列其中一個選項：

    * 按一下**從新搜尋**。
    * 按一下**從已儲存的搜尋**。 
  
5. 配置查詢。

    * 如果您選取**從已儲存的搜尋**，請選取一個搜尋查詢。此查詢用來擷取用於視覺化的資料。 

        選取搜尋之後，視覺化建置器即會開啟，並針對選取的查詢載入資料。系統會顯示下列訊息：*此視覺化鏈結至已儲存的搜尋：your_search_name*。 
	
	**附註**：您對已儲存的搜尋所做的任何變更，會自動反映在視覺化中。若要停用您對鏈結至此視覺化的查詢所進行的自動更新，請按兩下此訊息：*此視覺化鏈結至已儲存的搜尋：your_search_name*。 

    * 如果您選取**從新搜尋**，請定義新的查詢。此查詢用來定義視覺化所擷取及使用的資料子集。

        如需相關資訊，請參閱[透過定義自訂查詢過濾日誌](k4_filter_queries.html#k4_filter_queries)。

6. 在視覺化建置器中，為 Y 軸選取度量值集成。

7. 在視覺化建置器中，選取儲存區類型。然後，選取一個儲存區集成。
  
8. 新增子儲存區來分解資料。

如需 Kibana 的相關資訊，請參閱 [Kibana 使用手冊 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}。
 
## 儲存視覺化
{:#logging_kibana_visualizations_save}

請完成下列步驟，以在「視覺化」頁面中儲存視覺化：

1. 在「視覺化」頁面的工具列中，按一下**儲存視覺化**按鈕 ![儲存視覺化](images/k4_visualization_save_icon.jpg "儲存視覺化")。

2. 輸入視覺化的名稱。

3. 按一下「儲存」。 

## 載入視覺化
{:#logging_kibana_visualizations_reload}

請完成下列步驟，以載入已儲存的視覺化：

1. 在「視覺化」頁面的工具列中，按一下**載入已儲存的視覺化**按鈕 ![載入已儲存的視覺化](images/k4_visualization_open_icon.jpg "載入已儲存的視覺化")。

2. 選取您要載入的視覺化。 



## 刪除視覺化
{:#logging_kibana_visualizations_delete}

若要刪除視覺化，請在「設定」頁面中完成下列步驟：

1. 在「設定」頁面中，選取**物件**標籤。

2. 在**視覺化**標籤中，選取您要刪除的視覺化。

3. 按一下**刪除**。


## 匯出視覺化
{:#logging_kibana_visualizations_export}

若要將視覺化匯出成 JSON 檔案，請在「設定」頁面中完成下列步驟：

1. 在「設定」頁面中，選取**物件**標籤。

2. 在**視覺化**標籤中，選取您要匯出的視覺化。

3. 按一下**匯出**。

4. 儲存檔案。

## 匯入視覺化
{:#logging_kibana_visualizations_import}

若要將視覺化匯入成 JSON 檔案，請在「設定」頁面中完成下列步驟：

1. 在「設定」頁面中，選取**物件**標籤。

2. 在**視覺化**標籤中，選取**匯入**。

3. 選取檔案，然後按一下**開啟**。

該視覺化即會新增至視覺化清單中。


## 共用視覺化
{:#logging_kibana_visualizations_share}

請完成下列步驟，以在「視覺化」頁面中共用視覺化：

1. 在「視覺化」頁面的工具列中，按一下**共用視覺化**按鈕 ![共用視覺化](images/k4_visualization_share_icon.jpg "共用視覺化")。

2. 選擇下列其中一個動作：

    * **內嵌此視覺化**：選取此選項可透過 HTML 原始檔來共用視覺化。 
    
        按一下「複製」按鈕 ![複製到剪貼簿](images/k4_copy_to_clipboard.jpg "複製到剪貼簿") 來複製 HTML 程式碼，以用來將視覺化內嵌在 HTML 原始檔中。 
	
	**附註**：若要查看視覺化，使用者必須能夠存取 Kibana。
	
    * **共用鏈結**：選取此選項可將 Kibana 中的視覺化與其他使用者共用。



