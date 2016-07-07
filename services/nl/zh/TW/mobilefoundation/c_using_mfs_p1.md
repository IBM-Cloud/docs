---

copyright:
  years: 2016

---

#	使用 Developer 方案
{: #using_mobilefoundation_p1}

*前次更新：2016 年 6 月 15 日*
{: .last-updated}

建立 {{site.data.keyword.mobilefoundation_short}}: Developer 服務實例之後，請同意 {{site.data.keyword.mfp_full_notm}} 8.0 版的授權條款以便開始使用。幾秒過後，您就可以存取 {{site.data.keyword.Bluemix_notm}} 上的`概觀` 頁面，而此頁面提供指導教學及視訊，協助您開始使用 {{site.data.keyword.mobilefoundation_short}} 服務。

## 啟動 {{site.data.keyword.mobilefirst}} 伺服器
{: #start_mobilefoundation_p1}
* 若要以預設值啟動 {{site.data.keyword.mfserver_short_notm}}，請按一下**啟動基本伺服器**。

此選項會使用下列設定佈建 {{site.data.keyword.mfserver_long_notm}}：
*	1 GB 的記憶體及 64 GB 的儲存空間。此大小就足以進行開發及輕量型測試活動。

*	自動產生 `username` 及 `password`。您可以在伺服器啟動並執行時存取它們。

即會啟動佈建處理程序。此處理程序大約需要 10 分鐘的時間，並且會出現一個訊息視窗，指出此作業的進度。完成時，會顯示一個儀表板，您可以在其中查看：
*	執行中伺服器的狀態（狀態、大小、儲存空間）。

*	為您建立的伺服器路徑。使用此路徑，可以從公用網際網路連接行動伺服器。行動應用程式會使用該路徑來存取伺服器。

*	用來存取 {{site.data.keyword.mfp_oc_short_notm}} 的`使用者名稱`和`密碼`。會隱藏`密碼`。按一下**顯示密碼**，即可進行視覺化。

*	按一下**啟動主控台**，以啟動 {{site.data.keyword.mfp_oc_short_notm}}。


這個主控台會在容器內執行。利用這個主控台，您可以管理行動應用程式及行動裝置、使用伺服器作為行動後端、傳送推送通知，以及執行其他作業。

## 重建 {{site.data.keyword.mobilefirst}} 伺服器
{: #recreate_mobilefoundation_p1}

*	按一下**重建**，以重建伺服器。

* 此動作會停止現有的伺服器，並予以刪除。行動伺服器中的所有資料都會遺失。隨即會建立新的伺服器實例。這個動作需要數分鐘的時間才能完成。

##	設定進階配置
{: #using_mfs_advanced_p1}

使用`概觀` 頁面中的**使用進階配置啟動伺服器**頁面，以使用進階或自訂設定來建立伺服器。您也可以更新伺服器設定來自訂伺服器配置，方法是按一下**配置**標籤。{{site.data.keyword.mobilefoundation_short}} 可讓您存取一些進階設定。

*	從**拓蹼**標籤中，您可以選取容器的大小。預設 1 GB 伺服器就足以進行開發及控管測試。

  - 根據您的需求，選取正確的伺服器大小。


* **節點數**會顯示已建立的節點數目。在 {{site.data.keyword.mobilefoundation_short}}: Developer 中無法編輯此欄位。{{site.data.keyword.IBM_notm}} 容器群組中的節點數目，在 Developer 方案中預設為 **1**。

如需詳細資料，請參閱 [{{site.data.keyword.mobilefoundation_long}} 文件](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}。
