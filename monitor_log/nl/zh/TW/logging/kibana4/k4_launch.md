---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 導覽至 Kibana 儀表板
{: #k4_launch}

您可以從 {{site.data.keyword.Bluemix}} 使用者介面啟動 Kibana，或直接從 Web 瀏覽器啟動 Kibana。
{:shortdesc}

從 {{site.data.keyword.Bluemix_notm}} 啟動 Kibana，以根據啟動 Kibana 所用之資源的環境定義來檢視及分析資料。例如，您可以在 Kibana 中於特定 CF 應用程式的環境定義下啟動至該特定應用程式的日誌，或者在 Kibana 中於特定 Docker 容器的環境定義下啟動至該特定容器的日誌。 
    
如果您要查看所提供 {{site.data.keyword.Bluemix_notm}} 空間內的服務的聚集日誌資料，請從直接瀏覽器鏈結啟動 Kibana。用來過濾儀表板顯示資料的查詢，會擷取 {{site.data.keyword.Bluemix_notm}} 組織中某個空間的日誌項目。Kibana 顯示的日誌資訊，包括部署在您登入之 {{site.data.keyword.Bluemix_notm}} 組織的空間內的所有資源記錄。 

如需 Kibana 的相關資訊，請參閱 [Kibana User Guide ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}。
    

##  從 Bluemix 儀表板導覽至 Kibana 儀表板
{: #launch_Kibana_from_bluemix}

用來過濾 Kibana 顯示資料的查詢，會從您啟動 Kibana 的位置擷取 {{site.data.keyword.Bluemix_notm}} CF 應用程式或容器的日誌項目。 

若要在 Kibana 中查看 Cloud Foundry 應用程式或 Docker 容器的日誌，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}}，然後從 {{site.data.keyword.Bluemix_notm}} 儀表板按一下應用程式名稱或容器。 
    
2. 在 {{site.data.keyword.Bluemix_notm}} 使用者介面開啟日誌標籤。

    * 若為 CF 應用程式，請按一下導覽列中的**日誌**。 
    * 若為容器，請選取導覽列中的**監視及日誌**，然後按一下**記載**標籤。 
    
    即會開啟「日誌」標籤。 
    
3. 按一下**進階視圖**。即會開啟 **Kibana 4** 儀表板。

    依預設，**探索**頁面會載入，並選取預設索引型樣，且時間過濾器設為前 30 秒。搜尋查詢設定為比對 CF 應用程式或 Docker 容器的所有項目。

    如果「探索」頁面沒有顯示任何日誌項目，請調整時間選取器。如需相關資訊，請參閱[設定時間過濾器](logging_kibana_set_time_filter.html#set_time_filter)。


##  從 Web 瀏覽器導覽至 Kibana 儀表板
{: #launch_Kibana_from_browser}

用來過濾 Kibana 中顯示資料的查詢，會擷取 {{site.data.keyword.Bluemix_notm}} 組織中某個空間的日誌項目。Kibana 顯示的日誌資訊，包括部署在您登入之 {{site.data.keyword.Bluemix_notm}} 組織的空間內的所有資源記錄。

請完成下列步驟，以從瀏覽器啟動 Kibana：

1. 開啟 [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName})，以登入 Kibana 使用者介面。

2. 選取您要用來分析日誌的 Kibana 版本。
    * 選取 **Kibana 4** 標籤，以使用 Kibana 4。「探索」頁面即會開啟。如需相關資訊，請參閱 [在 Kibana 中以互動方式分析日誌](logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively)。
    * 選取 **Kibana 3** 標籤，以使用 Kibana 3。預設的 Kibana 儀表板即會開啟。如需使用 Kibana 3 來分析日誌的相關資訊，請參閱[在 Kibana 3（已淘汰）中分析日誌](../logging_view_kibana3.html#analyzing_logs_Kibana3)。如需自訂 Kibana 3 儀表板的相關資訊，請參閱[此部落格文章 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/)。
     
        **附註：**Kibana 3 已被淘汰。

    如果「探索」頁面沒有顯示任何日誌項目，請調整時間選取器。如需相關資訊，請參閱[設定時間過濾器](logging_kibana_set_time_filter.html#set_time_filter)。


