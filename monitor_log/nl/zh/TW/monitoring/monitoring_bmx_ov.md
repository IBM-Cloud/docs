---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Bluemix 中的監視功能
{: #monitoring_bmx_ov}

依預設，{{site.data.keyword.Bluemix_notm}} 會收集及顯示 CPU 用量、記憶體使用率及網路 I/O 的效能度量值。這些度量值提供個別雲端資源的相關效能資訊。您可以透過 {{site.data.keyword.Bluemix_notm}} 使用者介面來監視這些資源在雲端環境中的效能。您可以檢視接近即時的資料及歷程資料。
{:shortdesc}

您可以使用 {{site.data.keyword.Bluemix_notm}} 中的監視功能，以自動收集及測量環境及應用程式中的重要度量值。不需要特殊設備，即可收集度量值。例如，您可以使用效能度量值所提供的資訊來監視服務在雲端中的執行方式、偵測資源瓶頸，以及注意服務水準合約 (SLA)。當您分析服務的效能資料時，可以偵測到可能會導致資源瓶頸因而影響用戶端服務 SLA 的狀況。提早採取動作，可以避免可能會對您的業務造成負面影響的狀況。  

您也可以配置及監視更多效能度量值。您可以在 {{site.data.keyword.Bluemix_notm}} 外部視覺化及分析這些度量值。例如，在 {{site.data.keyword.containershort}} 中執行應用程式時，您可以使用 Grafana 來監視更多度量值。您可以自訂視覺化及分析效能資料的每個容器實例或每個空間的儀表板。

![{{site.data.keyword.Bluemix_notm}} 中所執行容器的 Grafana 監視視圖](images/monitoring_default_container_grafana_view.jpg)

您可以使用 {{site.data.keyword.Bluemix_notm}} 平台監視來：

* 瞭解應用程式作業（例如，偵測潛在瓶頸或需要升級的時機）。
* 定義您可用來計劃雲端平台中未來應用程式需求的趨勢。

如需監視 Cloud Foundry 上所執行的應用程式的相關資訊，請參閱[監視 Cloud Foundry 上所執行的應用程式](monitoring_cf_apps.html#monitoring_bluemix_apps)。

如需在 {{site.data.keyword.containershort}} 中監視的相關資訊，請參閱[在 {{site.data.keyword.containershort}} 中監視](/docs/containers/monitoringandlogging/container_ml_monitor.html#container_ml_monitor)。   

