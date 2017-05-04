---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 在 Grafana 分析度量值
{:#analyzing_metrics_grafana}

在 {{site.data.keyword.Bluemix}} 中，您可以使用 Grafana（一種開放程式碼分析與視覺化平台）在各種圖形（例如圖表和表格）中監視、搜尋、分析及視覺化您的度量值。使用 Grafana 來執行進階分析作業。
{:shortdesc}

您可以使用下列任何方式來啟動 Grafana：

* 從 {{site.data.keyword.Bluemix_notm}}

    在 Kibana 中，您可以在特定 Docker 容器度量值的環境定義下，啟動至該特定容器的日誌。 
    
    如需相關資訊，請參閱[從 {{site.data.keyword.Bluemix_notm}} 儀表板進入 Grafana 儀表板](monitoring_analyzing_metrics_grafana.html#launch_grafana_from_bluemix)。

* 從直接瀏覽器鏈結

    您可以啟動 Grafana 以便您看到的資料能從所提供的 {{site.data.keyword.Bluemix_notm}} 空間內的服務聚集日誌。
    
    如需相關資訊，請參閱[從 Web 瀏覽器進入 Kibana 儀表板](monitoring_analyzing_metrics_grafana.html#launch_grafana_from_browser)。
    


##  從 Bluemix 儀表板進入 Grafana 儀表板
{: #launch_grafana_from_bluemix}

用來過濾 Grafana 顯示資料的查詢，會從您啟動 Kibana 的位置擷取 {{site.data.keyword.Bluemix_notm}} 或容器的資料。 

若要在 Grafana 中查看 Docker 容器的度量值，請完成下列步驟：

1. 登入 {{site.data.keyword.Bluemix_notm}}，然後從 {{site.data.keyword.Bluemix_notm}} 儀表板按一下容器。 
    
2. 在導覽列中，按一下**監視及日誌**。即會開啟「監視」標籤。 
    
3. 按一下**進階視圖**。即會開啟 **Grafana** 儀表板。

如需 Grafana 的相關資訊，請參閱 [Grafana User Guide ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://docs.grafana.org/){: new_window}。


##  從 Web 瀏覽器進入 Grafana 儀表板
{: #launch_grafana_from_browser}

用來過濾 Grafana 顯示資料的查詢，會擷取 {{site.data.keyword.Bluemix_notm}} 組織中某個空間的資料。Grafana 顯示的度量值資訊，包括部署在您登入之 {{site.data.keyword.Bluemix_notm}} 組織的空間內的所有資源記錄。

完成下列步驟，以從瀏覽器啟動 Grafana：

1. 開啟 [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName})，以登入 Grafana 使用者介面。

2. 選取 **Grafana**。
     
如需 Grafana 的相關資訊，請參閱 [Grafana User Guide ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](http://docs.grafana.org/){: new_window}。
