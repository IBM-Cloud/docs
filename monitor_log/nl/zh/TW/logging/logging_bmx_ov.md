---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-29"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Bluemix 中的記載功能
{: #logging_bmx_ov}

{{site.data.keyword.Bluemix}} 記載功能已整合在平台中，並且自動啟用雲端資源的資料收集。依預設，{{site.data.keyword.Bluemix_notm}} 會收集及顯示應用程式、應用程式運行環境以及這些應用程式執行所在運算運行環境的日誌。
{:shortdesc}

您可以使用 {{site.data.keyword.Bluemix_notm}} 中的記載功能來瞭解雲端平台的行為，以及在其中執行的資源。不需要特殊設備，即可收集標準輸出和標準錯誤日誌。例如，您可以使用日誌來提供應用程式的審核追蹤、在服務中偵測問題、識別漏洞、疑難排解應用程式部署和運行環境行為、在應用程式執行所在的基礎架構中偵測問題、在雲端平台中的各元件之間追蹤應用程式，以及偵測可用來搶先處理可能影響服務 SLA 之動作的型樣。

當您在雲端中執行應用程式時，可能會無法透過 SSH 或 FTP 連接至執行應用程式的基礎架構來存取日誌，例如當應用程式在 Cloud Foundry 中執行時。另一方面，您可以在 {{site.data.keyword.Bluemix_notm}} 提供的另一個運算運行環境 {{site.data.keyword.containershort}} 中執行應用程式，在這裡，您就可以使用 SSH 來存取日誌。無論運算運行環境為何，存取日誌都很重要，{{site.data.keyword.Bluemix_notm}} 可讓您以常見的方法，在雲端平台中視覺化及分析日誌。

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

## CF 應用程式的記載功能
{: #logging_bmx_ov_cf}

{{site.data.keyword.Bluemix_notm}} 會記錄 Cloud Foundry 平台和 Cloud Foundry 應用程式所產生的日誌資料。在日誌中，您可以檢視針對應用程式所產生的錯誤、警告及參考訊息。如需 Cloud Foundry 中的記載功能相關資訊，請參閱 [Bluemix 中 Cloud Foundry 應用程式的記載功能](cfapps/logging_cf_apps.html#logging_bluemix_cf_apps)。

## 容器的記載功能
{: #logging_bmx_ov_containers}

{{site.data.keyword.Bluemix_notm}} 會記錄 {{site.data.keyword.containershort}} 所產生的日誌資料。如需 {{site.data.keyword.containershort}} 中的記載功能相關資訊，請參閱 [IBM Bluemix Container Service 的記載功能](containers/logging_containers_ov.html#logging_containers_ov)。  

**附註：**您可以針對在 {{site.data.keyword.IBM}} 所管理雲端基礎架構中部署的 Docker 容器，在 {{site.data.keyword.Bluemix_notm}} 中分析容器日誌。

## Bluemix 中的日誌分析
{: #logging_bmx_ov_ui}

在 {{site.data.keyword.Bluemix_notm}} 中，您可以檢視應用程式的最新日誌，或即時讀取日誌尾端的內容。

* 您可以透過使用者介面來檢視、過濾及分析日誌。如需相關資訊，請參閱[從 Bluemix 主控台分析日誌](logging_view_dashboard.html#analyzing_logs_bmx_ui)。

* 您可以藉由使用指令行，以程式設計方式管理日誌，來檢視、過濾及分析日誌。如需相關資訊，請參閱[從 CLI 分析日誌](logging_view_cli.html#analyzing_logs_cli)。

## 使用 Kibana 執行進階日誌分析
{: #logging_bmx_ov_kibana}

在 {{site.data.keyword.Bluemix_notm}} 中，您可以使用 Kibana（一種開放程式碼分析與視覺化平台）在各種圖形（例如圖表和表格）中監視、搜尋、分析及視覺化您的資料。如需相關資訊，請參閱[使用 Kibana 執行進階日誌分析](kibana4/analyzing_logs_Kibana.html#analyzing_logs_Kibana)。


