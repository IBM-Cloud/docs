---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Bluemix 中的記載功能
{: #logging_bmx_ov}

{{site.data.keyword.Bluemix_notm}} 記載功能已整合在平台中，並且自動啟用雲端資源的資料收集。依預設，{{site.data.keyword.Bluemix_notm}} 會收集及顯示應用程式、應用程式運行環境以及這些應用程式執行所在運算運行環境的日誌。
{:shortdesc}

您可以使用 {{site.data.keyword.Bluemix_notm}} 中的記載功能來瞭解雲端平台的行為，以及在其中執行的資源。不需要特殊設備，即可收集標準輸出和標準錯誤日誌。例如，您可以使用日誌來提供應用程式的審核追蹤、在服務中偵測問題、識別漏洞、疑難排解應用程式部署和運行環境行為、在應用程式執行所在的基礎架構中偵測問題、在雲端平台中的各元件之間追蹤應用程式，以及偵測可用來搶先處理可能影響服務 SLA 之動作的型樣。

當您在雲端中執行應用程式時，可能會無法透過 SSH 或 FTP 連接至執行應用程式的基礎架構來存取日誌，例如當應用程式在 Cloud Foundry 中執行時。另一方面，您可以在 {{site.data.keyword.Bluemix_notm}} 提供的另一個計算運行環境 {{site.data.keyword.containershort}} 中執行應用程式，在這裡，您就可以使用 SSH 來存取日誌。無論計算運行環境為何，存取日誌都很重要，{{site.data.keyword.Bluemix_notm}} 可讓您以常見的方法，在雲端平台中視覺化及分析日誌。

{{site.data.keyword.Bluemix_notm}} 會記錄 Cloud Foundry 平台和 Cloud Foundry 應用程式所產生的日誌資料。在日誌中，您可以檢視針對應用程式所產生的錯誤、警告及參考訊息。如需在 Cloud Foundry 中記載的相關資訊，請參閱 [Bluemix 中 Cloud Foundry 應用程式的記載功能](logging_cf_apps.html#logging_bluemix_cf_apps)。

{{site.data.keyword.Bluemix_notm}} 會記錄 {{site.data.keyword.containershort}} 所產生的日誌資料。如需在 {{site.data.keyword.containershort}} 中記載的相關資訊，請參閱 [{{site.data.keyword.containershort}} 中的記載功能](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_logs)。   


使用 {{site.data.keyword.Bluemix_notm}} 所提供的記載功能，您可以：

* 查看雲端資源及其執行和運行方式。
* 定義趨勢，以協助您識別需要您採取動作的情境。
* 定義應用程式的資料追蹤，例如，可用來進行審核的資料追蹤。
* 減少在應用程式中尋找問題並進行修復所需的時間及工作量。 
* 監視應用程式在雲端平台中的部署情況。
* 偵測服務或應用程式於何時關閉或損毀。
* 追蹤應用程式執行和資料流程。
* 識別應用程式中的漏洞。
* 偵測基礎架構中的問題。
* 偵測應用程式運行環境中的問題。
