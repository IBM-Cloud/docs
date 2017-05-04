---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 從 Bluemix 儀表板進入 Kibana 儀表板
{: #launch_Kibana_from_bluemix}

從 {{site.data.keyword.Bluemix}} 使用者介面啟動 Kibana，以查看 Cloud Foundry 應用程式或 Docker 容器的特定日誌。
{:shortdesc}

用來過濾 Kibana 顯示資料的查詢，會從您啟動 Kibana 的位置擷取 {{site.data.keyword.Bluemix_notm}} CF 應用程式或容器的日誌項目。 

若要在 Kibana 中查看 Cloud Foundry 應用程式或 Docker 容器的日誌，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}}，然後從 {{site.data.keyword.Bluemix_notm}} 儀表板按一下應用程式名稱或容器。 
    
2. 在 {{site.data.keyword.Bluemix_notm}} 使用者介面開啟日誌標籤。

    * 若為 CF 應用程式，請按一下導覽列中的**日誌**。 
    * 若為容器，請選取導覽列中的**監視及日誌**，然後按一下**記載**標籤。 
    
    即會開啟「日誌」標籤。 
    
3. 按一下**進階視圖**。即會開啟 **Kibana 4** 儀表板。

    根據預設值，**探索**頁面會載入，並選取預設索引型樣，且時間過濾器設為前 30 秒。搜尋查詢設為比對 CF 應用程式或 Docker 容器的所有項目。

    如果探索頁面未顯示任何日誌項目，請調整時間選取器。如需相關資訊，請參閱[設定時間過濾器](logging_kibana_set_time_filter.html#set_time_filter)。

如需 Kibana 的相關資訊，請參閱 [Kibana User Guide ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}。

