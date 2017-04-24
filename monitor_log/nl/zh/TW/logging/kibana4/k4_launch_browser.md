---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 從 Web 瀏覽器進入 Kibana 儀表板
{: #launch_Kibana_from_browser}

如果您需要在 {{site.data.keyword.Bluemix}} 空間分析日誌項目，請從瀏覽器啟動 Kibana。
{:shortdesc}

用來過濾 Kibana 顯示資料的查詢，會擷取 {{site.data.keyword.Bluemix_notm}} 組織中某個空間的日誌項目。Kibana 顯示的日誌資訊，包括部署在您登入之 {{site.data.keyword.Bluemix_notm}} 組織的空間內的所有資源記錄。

完成下列步驟，以從瀏覽器啟動 Kibana：

1. 開啟 [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName})，以登入 Kibana 使用者介面。

2. 選取您想用來分析日誌的 Kibana 版本。
    * 選取 **Kibana 4** 標籤，以使用 Kibana 4。會開啟探索頁面。如需相關資訊，請參閱 [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively)。
    * 選取 **Kibana 3** 標籤，以使用 Kibana 3。預設會開啟 Kibana 儀表板。如需自訂 Kibana 儀表板的相關資訊，請參閱[此部落格文章](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/)。
     
        **附註：**Kibana 3 已淘汰。

    如果探索頁面未顯示任何日誌項目，請調整時間選取器。如需相關資訊，請參閱[設定時間過濾器](logging_kibana_set_time_filter.html#set_time_filter)。

如需 Kibana 的相關資訊，請參閱 [Kibana User Guide ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}。
