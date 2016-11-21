---

copyright:
  years: 2016
lastupdated:  "2016-09-12"
---

#	使用 Professional 1 Application 方案
{: #using_mobilefoundation_p2}

<!--Last updated: 12 September 2016
{: .last-updated}-->

使用 Professional 1 Application 方案，使用者可以建立 1 個含有多個行動作業系統的行動應用程式。
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
    -  1 GB 的記憶體。此大小就足以進行開發、控管測試活動及小規模正式作業工作負載。

    -	自動產生 `username` 及 `password`。您可以在伺服器啟動並執行時存取它們。

會啟動伺服器的佈建處理程序。此處理程序大約需要 10 分鐘的時間，並且會出現一個訊息視窗，指出此作業的進度。完成時，會顯示一個儀表板，您可以在其中查看：

  -	執行中伺服器的狀態（狀態、大小）。

  -	為您建立伺服器路徑。您可以使用行動應用程式中的這個路徑來連接至 {{site.data.keyword.mfserver_short_notm}}。

  -	用來存取 {{site.data.keyword.mfp_oc_short_notm}} 的 `username` 和 `password`。會隱藏 `password`。按一下**顯示密碼**圖示，即可進行視覺化。

*	按一下**啟動主控台**，以啟動 {{site.data.keyword.mfp_oc_short_notm}}。


<!--This console runs inside the container.--> 使用這個主控台，您可以管理行動應用程式、配接器及行動裝置，使用伺服器作為行動後端、傳送推送通知，以及執行其他作業。



##  新增行動分析伺服器
{: #adding_analytics_server_prof}

 您現在可以在 {{site.data.keyword.mobilefirst}} 伺服器上監視您的行動應用程式，方法是將 Mobile Analytics 伺服器新增至
{{site.data.keyword.mobilefoundation_short}} 服務實例。

 Professional 方案會在一個容器群組中建立 Mobile Analytics 伺服器，使用者可以透過在容器群組中選取容器節點數來自訂配置。

 使用者也可以附加容器的磁區來持續保存資料。一旦磁區選定後就無法變更。20 GB 是使用者可用的預設檔案共用空間。如果使用者需要額外的儲存空間來持續保存分析資料，則需要購買額外的檔案共用，並且使用該檔案共用來建立磁區。然後，在部署分析伺服器時，便可以選取這個新的磁區。

 如需將磁區新增至 {{site.data.keyword.containerlong}} 的相關資訊，請參閱[使用 {{site.data.keyword.Bluemix_notm}} 儀表板將持續資料儲存在磁區中](https://new-console.ng.bluemix.net/docs/containers/container_volumes_ui.html){: new_window}。

* 按一下**新增分析**將 Mobile Analytics 伺服器新增至 {{site.data.keyword.mobilefoundation_short}} 服務實例。

即會啟動佈建處理程序。此處理程序大約需要 10 分鐘的時間，並且會出現一個訊息視窗，指出此作業的進度。  

* 從 {{site.data.keyword.mfp_oc_short_notm}} 啟動 MobileFirst Analytics 主控台。

* 介於 {{site.data.keyword.mfserver_short_notm}} 及 Mobile Analytics 伺服器的單一登入已啟用。使用相同的 LTPA 金鑰及使用者認證將 Mobile Analytics 伺服器配置為 {{site.data.keyword.mfserver_short_notm}} 伺服器。您可以使用與用來登入
{{site.data.keyword.mfp_oc_short_notm}} 相同的
`username` 及 `password` 來登入 Mobile Analytics 主控台。

如需 MobileFirst Analytics 的相關資訊，您可以參考 [MobileFirst Foundation Operational Analytics](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/analytics/)。

**附註：**當您刪除 {{site.data.keyword.mobilefoundation_short}} 服務實例時或當您嘗試重新建立
{{site.data.keyword.mfserver_short_notm}} 時，會移除 Mobile Analytics 伺服器。

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
