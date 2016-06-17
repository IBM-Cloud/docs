---

copyright:
  years: 2016

---

#	使用 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application
{: #using_mobilefoundation_p2}


建立 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 服務實例之後，請閱讀下列程序，以開始使用該服務。

## 必要條件
{: #prerequisites_p2}

在配置 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 服務實例之前，請考量下列各項。
* 只有 {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional（支援 OLTP）的 {{site.data.keyword.Bluemix_notm}} 方案才支援 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application。

* {{site.data.keyword.dashdbshort_notm}} 服務實例及其認證必須可供使用，您才能配置 {{site.data.keyword.mobilefoundation_short}} 服務實例的設定。

**附註**：{{site.data.keyword.dashdbshort_notm}} 服務實例可存在於 {{site.data.keyword.Bluemix_notm}} *組織* 的任何*空間*中。  

## 配置 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 服務實例
{: #configure_dashdb_p2}

###  首要步驟
{: #firststeps_p2}

建立 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 服務實例之後，請採取下列步驟，以開始使用該服務：

* 同意 {{site.data.keyword.mfp_full_notm}} 8.0.0.0 版的授權條款。

* 輸入您的 {{site.data.keyword.Bluemix_notm}} 認證。這樣做可授權服務在您的 {{site.data.keyword.Bluemix_notm}} 空間中執行變更，以及建立用來管理 {{site.data.keyword.mobilefirst_notm}} Server 的 {{site.data.keyword.containerlong}}。


### 設定 {{site.data.keyword.dashdbshort_notm}} 服務實例的連線
{: #connect_dashdb_p2}

建立 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 服務實例之後，就會看到*概觀* 頁面，您必須在此頁面中指定 {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional 服務實例的連線資訊。

* 指定 {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional 服務實例所在的 {{site.data.keyword.Bluemix_notm}} **組織**和**空間**。
* 如果您已建立多個 {{site.data.keyword.dashdbshort_notm}} 服務實例，請從下拉清單中，選擇您要與 {{site.data.keyword.mobilefoundation_short}} 服務實例搭配使用的 {{site.data.keyword.dashdbshort_notm}} 服務實例的**服務名稱**。
* 選擇所選取 {{site.data.keyword.dashdbshort_notm}} 服務實例的**認證**。

* 按一下**測試連線**以驗證您的 {{site.data.keyword.dashdbshort_notm}} 服務實例可供使用，再按一下**儲存**。

**附註**：您無法變更配置成供 {{site.data.keyword.mobilefoundation_short}} 服務實例使用的這個 {{site.data.keyword.dashdbshort_notm}} 服務實例。不過，您能夠在多個 {{site.data.keyword.mobilefoundation_short}} 服務實例之間使用相同的 {{site.data.keyword.dashdbshort_notm}} 服務實例，因為每一個 {{site.data.keyword.mobilefoundation_short}} 服務實例都會在所選取的 {{site.data.keyword.dashdbshort_notm}} 服務實例中建立自己的綱目。

* 幾秒過後，您就可以存取*概觀* 頁面，而此頁面提供指導教學及視訊，協助您開始使用 {{site.data.keyword.mobilefoundation_short}} 服務。

### 啟動 {{site.data.keyword.mobilefirst}} 伺服器
{: #start_mobilefoundation_p2}

* 若要以預設值啟動 {{site.data.keyword.mfserver_short_notm}}，請按一下**啟動基本伺服器**。

![啟動基本伺服器](images/start_basic_server.png "圖 1. 啟動基本伺服器")
{: screen}
* 此選項會使用下列設定佈建 {{site.data.keyword.mfserver_long_notm}}：
    -  1 GB 的記憶體及 64 GB 的儲存體。此大小就足以進行開發及控管測試活動。

    -	自動產生 *username* 及 *password*。您可以在伺服器啟動並執行時存取它們。

會啟動伺服器的佈建處理程序。此處理程序大約需要 10 分鐘的時間，並且會出現一個訊息視窗，指出此作業的進度。完成時，會顯示一個儀表板，您可以在其中查看：

  -	執行中伺服器的狀態（狀態、大小、儲存體）。

  -	為您建立的伺服器路徑。使用此路徑，可以從公用網際網路連接行動式伺服器。行動式應用程式會使用該路徑來存取伺服器。

  -	用來存取 {{site.data.keyword.mfp_oc_short_notm}} 的*使用者名稱* 和*密碼*。會隱藏*密碼*。按一下小眼睛圖示，即可進行視覺化。

*	按一下**啟動主控台**，以啟動 {{site.data.keyword.mfp_oc_short_notm}}。

![啟動主控台](images/launch_console.png "圖 2. 啟動主控台")
{: screen}

這個主控台會在儲存器內執行。利用這個主控台，您可以管理行動式應用程式及行動式裝置、使用伺服器作為行動式後端、傳送推送通知，以及執行其他作業。

### 重建 {{site.data.keyword.mobilefirst}} 伺服器
{: #recreate_mobilefoundation_p2}

*	按一下**重建**，以重建伺服器。

![重建](images/recreate.png "圖 3. 重建")
{: screen}

* 此動作會停止現有的伺服器，並予以刪除。隨即會建立新的伺服器實例。這個動作需要數分鐘的時間才能完成。

**附註**：所有來自舊版伺服器實例的資料（包括應用程式及配接器的相關資訊）都會持續保存在已配置的 {{site.data.keyword.dashdbshort_notm}} 服務實例中，這項資料在伺服器重建之後即可供使用。

##	設定進階配置
{: #using_mfs_advanced_p2}

使用*概觀* 頁面中的**使用進階配置啟動伺服器**頁面，以使用進階或自訂設定來建立伺服器。您也可以更新伺服器設定來自訂伺服器配置，方法是按一下**配置**標籤。{{site.data.keyword.mobilefoundation_short}} 可讓您存取一些進階設定。

*	從**拓蹼**標籤中，您可以選取儲存器的「拓蹼」大小。預設 1 GB 伺服器就足以進行開發及輕量型測試，但也可能需要更大的大小（例如，執行負載測試）。
  - 根據您的需求，選取正確的伺服器大小。

  - **節點數**會顯示已建立的節點數目。
      - 您可以配置您在 {{site.data.keyword.IBM_notm}} 儲存器群組中需要的最小及最大節點數。儲存器群組會提供高可用性及可擴充性。

      - {{site.data.keyword.mobilefirst}} 伺服器陣列可以透過在此處配置節點數目加以建立。

如需詳細資料，請參閱 [{{site.data.keyword.mobilefoundation_long}} 文件](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}。
