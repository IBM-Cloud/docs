---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 監視 IBM Bluemix Container Service
{: #monitoring_bmx_containers_ov}

在 {{site.data.keyword.Bluemix}} 中，會自動從容器外部收集容器度量值，而不需要在容器內部安裝及維護代理程式。{:shortdesc}

容器內代理程式對短期的輕量型雲端實例及自動擴充群組（其中容器可快速建立及破壞）具有顯著的額外需要及設定時間。這種頻外資料收集方法可以免除這些挑戰，並去除使用者的監視負擔。

主機中執行的處理程序會針對度量值執行無代理程式監視。依預設，此處理程序（亦稱為搜索器）會不斷從所有容器收集下列度量值：

* CPU
* 記憶體
* 網路資訊

度量資料會收集在 Graphite 中，並顯示在 {{site.data.keyword.Bluemix_notm}} 使用者介面及 Grafana 中。 

您可以從 {{site.data.keyword.Bluemix_notm}} 使用者介面啟動 Grafana，或直接從瀏覽器啟動 Grafana。如需相關資訊，請參閱[在 Grafana 中分析度量值](../grafana/monitoring_analyzing_metrics_grafana.html#analyzing_metrics_grafana)。

Docker 使用慣例及群組帳戶資訊會用作收集監視資料的基本機制。

**度量值保留**

每分鐘最多收集一個資料點。會刪除未在 7 天內寫入的容器度量值。
    
**度量值排序**

顯示資料，並依容器 ID 進行排序。 

您可以從指令行執行 `cf ic ps` 指令，以檢視專用 {{site.data.keyword.Bluemix_notm}} 映像檔登錄中之容器的容器 ID 清單。

