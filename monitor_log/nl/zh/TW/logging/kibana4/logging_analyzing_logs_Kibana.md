---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 使用 Kibana 執行進階日誌分析
{:#analyzing_logs_Kibana}

在 {{site.data.keyword.Bluemix}} 中，您可以使用 Kibana（一種開放程式碼分析與視覺化平台）在各種圖形（例如圖表和表格）中監視、搜尋、分析及視覺化您的資料。使用 Kibana 來執行進階分析作業。
{:shortdesc}

您可以使用下列任何方式來啟動 Kibana：

* 從 {{site.data.keyword.Bluemix_notm}}

    在 Kibana 中，您可以在特定 CF 應用程式的環境定義下，啟動至該特定應用程式的日誌。
    
    在 Kibana 中，您可以在特定 Docker 容器的環境定義下，啟動至該特定容器的日誌。 
    
    若為 CF 應用程式，用來過濾 Kibana 中可分析資料的查詢，會擷取 Cloud Foundry 應用程式的日誌項目。Kibana 預設顯示的日誌資訊，全都與單一 Cloud Foundry 應用程式及其所有實例相關。 
    
    若為容器，用來過濾 Kibana 中可分析資料的查詢，會擷取所有容器實例的日誌項目。Kibana 預設顯示的日誌資訊，全都與單一容器或容器群組及其所有實例相關。 
    
    如需相關資訊，請參閱[從 Bluemix 儀表板進入 Kibana 儀表板](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix)。

* 從直接瀏覽器鏈結

    您可能會想要啟動 Kibana，讓您看到的資料從所提供之 {{site.data.keyword.Bluemix_notm}} 空間內的服務聚集日誌。
    
    用來過濾儀表板顯示資料的查詢，會擷取 {{site.data.keyword.Bluemix_notm}} 組織中某個空間的日誌項目。Kibana 顯示的日誌資訊，包括部署在您登入之 {{site.data.keyword.Bluemix_notm}} 組織的空間內的所有資源記錄。 
    
    如需相關資訊，請參閱[從 Web 瀏覽器進入 Kibana 儀表板](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser)。
    
    當您從瀏覽器啟動 Kibana 時，可以選擇使用 Kibana 4 或 Kibana 3。**附註：**Kibana 3 已被淘汰。如需使用 Kibana 3 來分析日誌的相關資訊，請參閱[在 Kibana 3（已淘汰）中分析日誌](../logging_view_kibana3.html#analyzing_logs_Kibana3)。

<br>    

Kibana 是一種以瀏覽器為基礎的介面，您可以在這裡以互動方式分析資料及自訂儀表板，然後可以使用該儀表板來分析日誌資料，以及執行進階管理作業。 

Kibana 頁面顯示的資料受搜尋限制。預設資料集是由預先配置的索引型樣來定義。若要過濾資訊，您可以新增搜尋查詢，並將過濾器套用至預設資料集。然後，您可以儲存搜尋，以供日後重複使用。 

Kibana 包括可用來分析日誌的不同頁面：

| Kibana 頁面 | 說明 |
|-------------|-------------|
| 探索 | 請利用這個頁面來定義搜尋，並可透過表格及直方圖，以互動方式分析日誌。 |
| 視覺化 | 請利用這個頁面來建立圖形及表格等視覺化，讓您可以用來分析日誌資料及比較結果。  |
| 儀表板 | 請利用這個頁面，透過已儲存的視覺化及搜尋集合來分析日誌。  |

**附註：**透過「視覺化」頁面或「儀表板」頁面，一次只能分析 1 整天，但可以回溯 7 天。日誌資料預設會儲存 7 天。 

| Kibana 頁面 | 時段資訊 |
|-------------|-------------------------|
| 探索 | 最多可分析 7 天的資料。 |
| 視覺化 | 分析 24 小時內的資料。<br> 您可以過濾歷時 24 小時自訂時段的日誌資料。  |
| 儀表板 | 分析 24 小時內的資料。<br> 您可以過濾歷時 24 小時自訂時段的日誌資料。<br> 您設定的時間選取器會套用至內含在儀表板中的所有視覺化。 |


例如，以下示範如何使用 Kibana，透過不同頁面來顯示空間中的 CF 應用程式或容器相關資訊：

* 在「探索」頁面中，您可以定義新的搜尋查詢，並依查詢來套用過濾器。日誌資料會透過表格及直方圖來顯示。您可以使用這些視覺化，以互動方式來分析資料。如需相關資訊，請參閱[在 Kibana 中以互動方式分析日誌](logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively)。

    您可以從日誌欄位（例如 message_type 及 instance_ID）配置過濾器，並設定時段。您可以動態啟用或停用這些過濾器。表格及直方圖將會顯示符合您啟用之查詢和過濾準則的日誌項目。如需相關資訊，請參閱[在 Kibana 中過濾日誌](logging_kibana_filtering_logs.html#kibana_filtering_logs)。
    
* 在「視覺化」頁面中，您可以定義新的搜尋查詢及視覺化。

    若要分析資料，您可以根據現有搜尋或新搜尋來建立視覺化。Kibana 包括可用來分析資訊的各種視覺化類型，例如表格、趨勢及直方圖。每一種視覺化的目標都不同。部分視覺化會分組成數列，以提供一個以上查詢的結果。其他視覺化則會顯示文件或自訂資訊。如果搜尋查詢有所更新，可修正或變更視覺化中的資料。您可以將視覺化內嵌在網頁中或予以共用。如需相關資訊，請參閱[使用視覺化來分析日誌](logging_kibana_visualizations.html#logging_kibana_visualizations)。

* 在「儀表板」頁面中，您可以同步自訂、儲存及共用多個視覺化和搜尋。 

    您可以新增、移除及重新排列儀表板中的視覺化。如需相關資訊，請參閱[在 Kibana 中透過儀表板來分析日誌](logging_kibana_analize_logs_dashboard.html#kibana_analize_logs_dashboard)。
    
    自訂 Kibana 儀表板之後，您可以透過其視覺化來分析資料，並可儲存起來以供日後重複使用。如需相關資訊，請參閱[儲存 Kibana 儀表板](logging_kibana_analize_logs_dashboard.html#save_Kibana_dashboard)。

Kibana 中也有*設定*頁面，可讓您用來配置 Kibana，以及儲存、刪除、匯出和匯入搜尋、視覺化和儀表板。

如需相關資訊，請參閱 [Kibana 使用手冊![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}。

**附註：**支援 Kibana 4 和 Kibana 3。Kibana 3 已淘汰。


##  從 Bluemix 儀表板進入 Kibana 儀表板
{: #launch_Kibana_from_bluemix}

用來過濾 Kibana 顯示資料的查詢，會從您啟動 Kibana 的位置擷取 {{site.data.keyword.Bluemix_notm}} CF 應用程式或容器的日誌項目。 

若要在 Kibana 中查看 Cloud Foundry 應用程式或 Docker 容器的日誌，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}}，然後從 {{site.data.keyword.Bluemix_notm}} 儀表板按一下應用程式名稱或容器。 
    
2. 在 {{site.data.keyword.Bluemix_notm}} 使用者介面開啟日誌標籤。

    * 若為 CF 應用程式，請按一下導覽列中的**日誌**。 
    * 若為容器，請選取導覽列中的**監視及日誌**，然後按一下**記載**標籤。 
    
    即會開啟「日誌」標籤。 
    
3. 按一下**進階視圖**。即會開啟 **Kibana 4** 儀表板。

    根據預設值，**探索**頁面會載入，並選取預設索引型樣，且時間過濾器設為前 30 秒。搜尋查詢設定為比對 CF 應用程式或 Docker 容器的所有項目。

    如果「探索」頁面沒有顯示任何日誌項目，請調整時間選取器。如需相關資訊，請參閱[設定時間過濾器](logging_kibana_set_time_filter.html#set_time_filter)。

如需 Kibana 的相關資訊，請參閱 [Kibana 使用手冊](https://www.elastic.co/guide/en/kibana/current/index.html)。

##  從 Web 瀏覽器進入 Kibana 儀表板
{: #launch_Kibana_from_browser}

用來過濾 Kibana 中顯示資料的查詢，會擷取 {{site.data.keyword.Bluemix_notm}} 組織中某個空間的日誌項目。Kibana 顯示的日誌資訊，包括部署在您登入之 {{site.data.keyword.Bluemix_notm}} 組織的空間內的所有資源記錄。

請完成下列步驟，以從瀏覽器啟動 Kibana：

1. 開啟 [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName})，以登入 Kibana 使用者介面。

2. 選取您要用來分析日誌的 Kibana 版本。
    * 選取 **Kibana 4** 標籤，以使用 Kibana 4。「探索」頁面即會開啟。如需相關資訊，請參閱 [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively)。
    * 選取 **Kibana 3** 標籤，以使用 Kibana 3。預設的 Kibana 儀表板即會開啟。如需自訂 Kibana 3 儀表板的相關資訊，請參閱[此部落格文章](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/)。
     
        **附註：**Kibana 3 已被淘汰。

    如果「探索」頁面沒有顯示任何日誌項目，請調整時間選取器。如需相關資訊，請參閱[設定時間過濾器](logging_kibana_set_time_filter.html#set_time_filter)。

如需 Kibana 的相關資訊，請參閱 [Kibana 使用手冊 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}。

