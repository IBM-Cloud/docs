---

copyright:
  years: 2016

---

#	使用 Professional 1 Application 方案
{: #using_mobilefoundation_p2}

前次更新：2016 年 8 月 4 日
{: .last-updated}

使用 Professional 1 Application 方案，使用者可以建立 1 個含有多個行動式作業系統的行動應用程式。
建立 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 服務實例之後，請閱讀下列程序，以開始使用該服務。

## 必要條件
{: #prerequisites_p2}

在配置 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 服務實例之前，請考量下列各項。
* 只有 {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional（支援 OLTP）的 {{site.data.keyword.Bluemix_notm}} 方案才支援 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application。

* 您應該具有 {{site.data.keyword.dashdbshort_notm}} 服務實例認證的存取權，才能配置 {{site.data.keyword.mobilefoundation_short}} 服務實例的設定。

**附註**：{{site.data.keyword.dashdbshort_notm}} 服務實例可存在於 {{site.data.keyword.Bluemix_notm}} `Organization` 的任何 `Space` 中或您具有存取權的任何其他 `Organization` 中。請確定您具有存取 {{site.data.keyword.dashdbshort_notm}} 服務實例所存在的 `Space` 的許可權。


## 新增資料庫連線
{: #configure_dashdb_p2}

###  首要步驟
{: #firststeps_p2}

建立 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 服務實例之後，請遵循下面的程序以開始使用。

### 設定 {{site.data.keyword.dashdbshort_notm}} 服務實例的連線
{: #connect_dashdb_p2}

建立 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 服務實例之後，就會看到*概觀* 頁面，您必須在此頁面中指定 {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional 服務實例的連線資訊。

1. 選取 {{site.data.keyword.dashdbshort_notm}} 服務實例所存在的 {{site.data.keyword.Bluemix_notm}} `Organization`。

+ 從所選取 `Organization` 中可用的空間清單，選取 {{site.data.keyword.dashdbshort_notm}} 服務實例所存在的 {{site.data.keyword.Bluemix_notm}} `Space`。

**附註：**如果您未看見，請列出 {{site.data.keyword.dashdbshort_notm}} 服務實例所存在的 `Organization` 和 `Space`，然後檢查您是否為該 `Organization` 和 `Space` 的成員。

+ 選取 {{site.data.keyword.dashdbshort_notm}} `Service Name` 和 `Credentials`，以連接至現有的 {{site.data.keyword.dashdbshort_notm}} 服務實例。

+  測試所指定的 {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional 服務實例的連線。

+  按一下**繼續**。此動作會在配置的 {{site.data.keyword.dashdbshort_notm}} 資料庫服務實例中建立必要的表格。

**附註**：您無法變更配置來供 {{site.data.keyword.mobilefoundation_short}} 服務實例使用的 {{site.data.keyword.dashdbshort_notm}} 服務實例。不過，您能夠在多個 {{site.data.keyword.mobilefoundation_short}} 服務實例之間使用相同的 {{site.data.keyword.dashdbshort_notm}} 服務實例，因為每一個 {{site.data.keyword.mobilefoundation_short}} 服務實例都會在所選取的 {{site.data.keyword.dashdbshort_notm}} 服務實例中建立自己的綱目。

* 幾秒過後，您就可以存取 `Overview` 頁面，而此頁面提供指導教學及視訊，協助您開始使用 {{site.data.keyword.mobilefoundation_short}} 服務。

## 啟動 {{site.data.keyword.mobilefirst}} 伺服器
{: #start_mobilefoundation_p2}

* 若要以預設值啟動 {{site.data.keyword.mfserver_short_notm}}，請按一下**啟動基本伺服器**。

* 此選項會使用下列設定佈建 {{site.data.keyword.mfserver_long_notm}}：
    -  1 GB 的記憶體。此大小就足以進行開發、控管測試活動及小規模正式作業工作量。

    -	自動產生 `username` 及 `password`。您可以在伺服器啟動並執行時存取它們。

會啟動伺服器的佈建處理程序。此處理程序大約需要 10 分鐘的時間，並且會出現一個訊息視窗，指出此作業的進度。完成時，會顯示一個儀表板，您可以在其中查看：

  -	執行中伺服器的狀態（狀態、大小）。

  -	為您建立伺服器路徑。您可以使用行動應用程式中的這個路徑來連接至 {{site.data.keyword.mfserver_short_notm}}。

  -	用來存取 {{site.data.keyword.mfp_oc_short_notm}} 的 `username` 和 `password`。會隱藏 `password`。按一下**顯示密碼**圖示，即可進行視覺化。

*	按一下**啟動主控台**，以啟動 {{site.data.keyword.mfp_oc_short_notm}}。


<!--This console runs inside the container.--> 使用這個主控台，您可以管理行動應用程式、配接器及行動裝置，使用伺服器作為行動後端、傳送推送通知，以及執行其他作業。

## 重建 {{site.data.keyword.mobilefirst}} 伺服器
{: #recreate_mobilefoundation_p2}

*	按一下**重建**，以重建伺服器。

* 此動作會停止現有的伺服器，並刪除資料。隨即會使用更新的版本（如果有的話）建立新的伺服器實例。這個動作需要數分鐘的時間才能完成。

**附註**：所有來自舊版伺服器實例的資料（包括應用程式及配接器的相關資訊）都會持續保存在已配置的 {{site.data.keyword.dashdbshort_notm}} 服務實例中，這項資料可用來重建您的伺服器。

##	設定進階配置
{: #using_mfs_advanced_p2}

使用 `Overview` 頁面中的**使用進階配置啟動伺服器**頁面，以使用進階或自訂設定來建立伺服器。您也可以更新伺服器設定來自訂伺服器配置，方法是按一下**配置**標籤。{{site.data.keyword.mobilefoundation_short}} 可讓您存取一些進階設定。

*	從**拓蹼**標籤中，您可以視需要選取伺服器大小和實例數目。預設 1 GB 伺服器就足以進行開發及輕量型測試。
  - 根據您的需求，選取正確的伺服器大小。

  - **節點數**會顯示已建立的節點數目。

      - {{site.data.keyword.mobilefirst}} 伺服器陣列可以透過在此處配置節點數目加以建立。

如需詳細資料，請參閱 [{{site.data.keyword.mobilefoundation_long}} 文件](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}。
