---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 在 Kibana 中透過儀表板來分析日誌
{:#kibana_analize_logs_dashboard}

使用 Kibana 中的*儀表板*頁面，來顯示分組成各儀表板的視覺化集合。使用儀表板來分析您的日誌資料並比較結果。{:shortdesc}

{{site.data.keyword.Bluemix}} 中有不同類型的儀表板，您可以定義及自訂，以視覺化及分析資料。例如，下表列出一些常見的儀表板類型：

| 儀表板類型 | 說明 |
|-------------------|-------------|
| Single-cf-app 儀表板 | 此儀表板會顯示單一 Cloud Foundry 應用程式的資訊。 |
| 單一容器儀表板  | 此儀表板會顯示單一容器的資訊。  |
| 容器群組儀表板  | 此儀表板會顯示特定容器群組的資訊。  |
| Multi-cf-app 儀表板 | 此儀表板會顯示部署在相同 {{site.data.keyword.Bluemix_notm}} 空間中的所有 Cloud Foundry 應用程式的資訊。  | 
| Multi-container 儀表板 | 此儀表板會顯示部署在相同 {{site.data.keyword.Bluemix_notm}} 空間中的所有容器的資訊。  |
| 空間儀表板 | 此儀表板會顯示 {{site.data.keyword.Bluemix_notm}} 空間中可用的記載資料。  | 

若要將儀表板中的資料視覺化，您可以配置畫面。Kibana 包括可用來分析資訊的各種視覺化，例如表格、趨勢及直方圖。視覺化會以畫面形式新增至儀表板。您可以新增、移除及重新排列儀表板中的畫面。每一個畫面的目標都不同。部分畫面會分組成數列，以提供一個以上查詢的結果。其他畫面則會顯示文件或自訂資訊。每一個畫面都以搜尋為基礎。搜尋會定義畫面顯示的資料子集。例如，您可以配置長條圖、圓餅圖或表格，以將資料視覺化，並進行分析。  

下表列出您可以在「儀表板」頁面中執行的各種作業：

| 作業 | 相關資訊 |
|------|------------------|
| [建立新的儀表板](logging_kibana_analize_logs_dashboard.html#K4_dashboard_new) | 您可以建立多個儀表板。每一個儀表板都可以設計為包括不同的搜尋、視覺化，以及不同的日誌資料子集。  |
| [儲存儀表板](logging_kibana_analize_logs_dashboard.html#k4_dashboard_save) | 您可以儲存儀表板，以供稍後重複使用。 |
| [載入儀表板](logging_kibana_analize_logs_dashboard.html#k4_dashboard_reload) | 您可以上傳儀表板，以更新其資料、予以修改或分析資料。 |
| [刪除儀表板](logging_kibana_analize_logs_dashboard.html#k4_dashboard_delete) | 刪除不需要的儀表板。 |
| [匯出儀表板](logging_kibana_analize_logs_dashboard.html#k4_dashboard_export) | 您可以將儀表板匯出成 JSON 檔案。 |
| [匯入儀表板](logging_kibana_analize_logs_dashboard.html#k4_dashboard_import) | 您可以將儀表板匯入成 JSON 檔案。 |
| [共用儀表板](logging_kibana_analize_logs_dashboard.html#k4_dashboard_share) | 您可以透過 HTML 原始檔或透過 Kibana 儀表板來共用儀表板。 |
| [新增視覺化](logging_kibana_analize_logs_dashboard.html#k4_dashboard_add_visualization) | 您可以將現有視覺化或搜尋新增至儀表板。|

如需 Kibana 的相關資訊，請參閱 [Kibana 使用手冊 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}。



## 建立新的 Kibana 儀表板
{: #K4_dashboard_new}

請完成下列步驟，以建立新的儀表板：

1. 在「儀表板」頁面的工具列中，按一下**新建儀表板**按鈕 ![新建儀表板](images/k4_dash_new_icon.jpg "新建儀表板")。

2. 新增一個以上的搜尋及視覺化。如需相關資訊，請參閱[新增搜尋或視覺化](logging_kibana_analize_logs_dashboard.html#K4_dashboard_add_visualization)。

    當您新增搜尋或視覺化時，會在儀表板中新增畫面。

3. 將畫面拖放在您要放置的儀表板部分。
 
4. 儲存儀表板，以供日後重複使用。如需相關資訊，請參閱[儲存 Kibana 儀表板](logging_kibana_analize_logs_dashboard.html#k4_dashboard_save)。


## 新增搜尋或視覺化
{: #k4_dashboard_add_visualization}

請完成下列步驟，以新增現有視覺化或搜尋：

1. 在「儀表板」頁面的工具列中，按一下**新增視覺化**按鈕 ![新增視覺化](images/k4_dash_add_visualization_icon.jpg "新增視覺化")。

    **附註**：您可以新增視覺化及搜尋。 

2. 選取**視覺化**標籤，以新增視覺化，或選取**搜尋**標籤，以新增搜尋。

3. 按一下您要新增的搜尋或視覺化。

    該搜尋或視覺化的畫面即會新增至儀表板。



## 儲存 Kibana 儀表板
{: #k4_dashboard_save}

完成下列步驟，以在自訂 Kibana 儀表板之後予以儲存：

1. 在工具列中，按一下**儲存**按鈕 ![儲存儀表板](images/k4_dash_save_icon.jpg "儲存儀表板")。

2. 輸入儀表板的名稱。

    **附註：**如果您嘗試用來儲存儀表板的名稱包含空格，將不會進行儲存。

3. 按一下名稱欄位旁邊的**儲存**圖示。


## 刪除 Kibana 儀表板
{: #k4_dashboard_delete}

若要刪除視覺化，請在「設定」頁面中完成下列步驟：

1. 在「設定」頁面中，選取**物件**標籤。

2. 在**視覺化**標籤中，選取您要刪除的視覺化。

3. 按一下**刪除**。


## 載入 Kibana 儀表板
{: #k4_dashboard_reload}

請完成下列步驟，以載入已儲存的儀表板：

1. 在「儀表板」頁面的工具列中，按一下**載入已儲存的儀表板**按鈕 ![載入已儲存的儀表板](images/k4_dash_load_icon.jpg "載入已儲存的儀表板")。

2. 選取您要載入的儀表板。 


## 匯出 Kibana 儀表板
{: #k4_dashboard_export}

若要將儀表板匯出成 JSON 檔案，請在「設定」頁面中完成下列步驟：

1. 在「設定」頁面中，選取**物件**標籤。

2. 在**儀表板**標籤中，選取您要匯出的儀表板。

3. 按一下**匯出**。

4. 儲存檔案。


## 匯入 Kibana 儀表板
{: #k4_dashboard_import}

若要將儀表板匯入成 JSON 檔案，請在「設定」頁面中完成下列步驟：

1. 在「設定」頁面中，選取**物件**標籤。

2. 在**儀表板**標籤中，選取**匯入**。

3. 選取檔案，然後按一下**開啟**。

該儀表板即會新增至儀表板清單中。


## 共用 Kibana 儀表板
{: #k4_dashboard_share}

請完成下列步驟，以共用儀表板：

1. 在「儀表板」頁面的工具列中，按一下**共用儀表板**按鈕 ![共用儀表板](images/k4_dash_share_icon.jpg "共用儀表板")。

2. 選擇下列其中一個動作：

    * **內嵌此儀表板**：選取此選項可透過 HTML 原始檔來共用儀表板。 
    
        按一下「複製」按鈕 ![複製到剪貼簿](images/k4_copy_to_clipboard.jpg "複製到剪貼簿") 來複製 HTML 程式碼，以用來將儀表板內嵌在 HTML 原始檔中。 
        
        **附註**：若要查看儀表板，使用者必須能夠存取 Kibana。
	
    * **共用鏈結**：選取此選項可將 Kibana 中的儀表板與其他使用者共用。



