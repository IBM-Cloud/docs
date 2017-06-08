---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-14"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 監視及記載
{: #monitoringandlogging}

{{site.data.keyword.Bluemix}} 是 {{site.data.keyword.IBM_notm}} 的雲端運算平台，用於建置、執行及管理應用程式和服務。{{site.data.keyword.Bluemix_notm}} 結合平台即服務 (PaaS) 與基礎架構即服務 (IaaS)。此外，{{site.data.keyword.Bluemix_notm}} 還具有豐富的雲端服務型錄，可以輕鬆地與 PaaS 及 IaaS 整合，以快速地建置商業應用程式。{{site.data.keyword.Bluemix_notm}} 包括跨平台的整合式記載及監視服務。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} 提供跨不同運算服務的記載及監視服務，例如 Cloud Foundry 及 {{site.data.keyword.containershort}}。您可以在任何運算運行環境中開發、執行及管理應用程式，而不會有一般與開發及啟動應用程式相關聯的基礎架構建置與維護複雜性。 

**附註：**美國南部地區及英國地區提供監視及記載功能。

您可以使用 {{site.data.keyword.Bluemix_notm}} 中的監視功能，以自動收集及測量環境及應用程式中的重要度量值。不需要特殊設備，即可收集度量值。例如，您可以使用效能度量值所提供的資訊來監視服務在雲端中的執行方式、偵測資源瓶頸，以及注意服務水準合約 (SLA)。例如，當您分析服務的效能資料時，可以偵測到可能會導致資源瓶頸因而影響用戶端服務 SLA 的狀況。提早採取動作，可以避免可能會對您的業務造成負面影響的狀況。  

您可以使用 {{site.data.keyword.Bluemix_notm}} 中的記載功能來瞭解雲端平台的行為，以及在其中執行的資源。不需要特殊設備，即可收集標準輸出和標準錯誤日誌。例如，您可以使用日誌來提供應用程式的審核追蹤、在服務中偵測問題、識別漏洞、疑難排解應用程式部署和運行環境行為、在應用程式執行所在的基礎架構中偵測問題、在雲端平台中的各元件之間追蹤應用程式，以及偵測可用來搶先處理可能影響服務 SLA 之動作的型樣。

## 監視運算基礎架構資源
{: #monitoring_sl_ov}

每部 {{site.data.keyword.Bluemix_notm}} 伺服器都包括監視及隨時可取得且可輕鬆閱讀的報告。如需相關資訊，請參閱[基礎架構監視 & 報告 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/cloud-computing/bluemix/infrastructure-monitoring){: new_window}。


## 在 {{site.data.keyword.Bluemix}} 中監視運算服務
{: #monitoring_bmx_ov}

依預設，{{site.data.keyword.Bluemix_notm}} 會收集及顯示 CPU 用量、記憶體使用率及網路 I/O 的效能度量值。這些度量值提供個別雲端資源的相關效能資訊。您可以透過 {{site.data.keyword.Bluemix_notm}} 使用者介面來監視這些資源在雲端環境中的效能。您可以檢視接近即時的資料及歷程資料。
 

您也可以配置及監視更多效能度量值。您可以在 {{site.data.keyword.Bluemix_notm}} 外部視覺化及分析這些度量值。例如，在 {{site.data.keyword.containershort}} 中執行應用程式時，您可以使用 Grafana 來監視更多度量值。您可以自訂視覺化及分析效能資料的每個容器實例或每個空間的儀表板。

![{{site.data.keyword.Bluemix_notm}} 中所執行容器的 Grafana 監視視圖](images/monitoring_default_container_grafana_view.jpg)

您可以使用 {{site.data.keyword.Bluemix_notm}} 平台監視來：

* 瞭解應用程式作業（例如，偵測潛在瓶頸或需要升級的時機）。
* 定義您可用來計劃雲端平台中未來應用程式需求的趨勢。

如需監視 Cloud Foundry 上所執行的應用程式的相關資訊，請參閱[監視 Cloud Foundry 上所執行的應用程式](monitoring_cf_apps.html#monitoring_bluemix_apps)。

如需在 {{site.data.keyword.containershort}} 中監視的相關資訊，請參閱[在 {{site.data.keyword.containershort}} 中監視](/docs/containers/monitoringandlogging/container_ml_monitor.html#container_ml_monitor)。   

## {{site.data.keyword.Bluemix}} 中的記載功能
{: #logging_bmx_ov}

{{site.data.keyword.Bluemix_notm}} 記載功能已整合在平台中，並且自動啟用雲端資源的資料收集。依預設，{{site.data.keyword.Bluemix_notm}} 會收集及顯示應用程式、應用程式運行環境以及這些應用程式執行所在運算運行環境的日誌。
 

當您在雲端中執行應用程式時，可能會無法透過 SSH 或 FTP 連接至執行應用程式的基礎架構來存取日誌，例如當應用程式在 Cloud Foundry 中執行時。另一方面，您可以在 {{site.data.keyword.Bluemix_notm}} 提供的另一個運算運行環境 {{site.data.keyword.containershort}} 中執行應用程式，在這裡，您就可以使用 SSH 來存取日誌。無論運算運行環境為何，存取日誌都很重要，{{site.data.keyword.Bluemix_notm}} 可讓您以常見的方法，在雲端平台中視覺化及分析日誌。

{{site.data.keyword.Bluemix_notm}} 會記錄 Cloud Foundry 平台和 Cloud Foundry 應用程式所產生的日誌資料。在日誌中，您可以檢視針對應用程式所產生的錯誤、警告及參考訊息。如需 Cloud Foundry 中記載功能的相關資訊，請參閱 [{{site.data.keyword.Bluemix}} 中 Cloud Foundry 應用程式的記載功能](logging_cf_apps.html#logging_bluemix_cf_apps)。

{{site.data.keyword.Bluemix_notm}} 會記錄 {{site.data.keyword.containershort}} 所產生的日誌資料。如需 {{site.data.keyword.containershort}} 中記載功能的相關資訊，請參閱 [{{site.data.keyword.containershort}} 中的記載功能](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_logs)。   


使用 {{site.data.keyword.Bluemix_notm}} 所提供的記載功能，您可以：

* 查看雲端資源及其執行和運行方式。
* 定義趨勢，以協助您識別需要您採取動作的情境。
* 定義應用程式的資料追蹤，例如，可用來進行審核的資料追蹤。
* 減少在應用程式中尋找問題並進行修復所需的時間及工作量。 
* 監視應用程式在雲端平台中的部署情況。
* 偵測服務或應用程式關閉或損毀情況。
* 追蹤應用程式執行和資料流程。
* 識別應用程式中的漏洞。
* 偵測基礎架構中的問題。
* 偵測應用程式運行環境中的問題。


