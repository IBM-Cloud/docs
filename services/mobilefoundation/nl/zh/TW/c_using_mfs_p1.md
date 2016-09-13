---

copyright:
  years: 2016

---

#	使用 Developer 方案
{: #using_mobilefoundation_p1}

前次更新：2016 年 8 月 4 日
{: .last-updated}

建立 {{site.data.keyword.mobilefoundation_short}}: Developer 服務實例之後，只要幾秒鐘，您就可以存取 {{site.data.keyword.Bluemix_notm}} 上的 `Overview` 頁面，而此頁面提供指導教學及視訊，協助您開始使用 {{site.data.keyword.mobilefoundation_short}} 服務。

## 啟動 {{site.data.keyword.mobilefirst}} 伺服器
{: #start_mobilefoundation_p1}
* 若要以預設值啟動 {{site.data.keyword.mfserver_short_notm}}，請按一下**啟動基本伺服器**。

此選項會使用下列設定佈建 {{site.data.keyword.mfserver_long_notm}}：
*	1 GB 的記憶體。此大小就足以進行開發、輕量型測試活動及小規模正式作業工作量。

*	自動產生 `username` 及 `password`。您可以在伺服器啟動並執行時存取它們。

即會啟動佈建處理程序。此處理程序大約需要 10 分鐘的時間，並且會出現一個訊息視窗，指出此作業的進度。完成時，會顯示一個儀表板，您可以在其中查看：
*	執行中伺服器的狀態（狀態、大小）。

*	為您建立的伺服器路徑。您可以使用行動應用程式中的這個路徑來連接至 {{site.data.keyword.mfserver_short_notm}}。

*	用來存取 {{site.data.keyword.mfp_oc_short_notm}} 的 `username` 和 `password`。會隱藏 `password`。按一下**顯示密碼**圖示，即可進行視覺化。

*	按一下**啟動主控台**，以啟動 {{site.data.keyword.mfp_oc_short_notm}}。


<!--This console runs inside the container.--> 利用這個主控台，您可以管理行動應用程式及行動裝置、使用伺服器作為行動後端、傳送推送通知，以及執行其他作業。

## 重建 {{site.data.keyword.mobilefirst}} 伺服器
{: #recreate_mobilefoundation_p1}

*	按一下**重建**，以重建伺服器。

* 此動作會停止現有的伺服器，並刪除資料。行動伺服器中的所有資料都會遺失。隨即會使用更新的版本（如果有的話）建立新的伺服器實例。這個動作需要數分鐘的時間才能完成。

##	設定進階配置
{: #using_mfs_advanced_p1}

使用 `Overview` 頁面中的**使用進階配置啟動伺服器**頁面，以使用進階或自訂設定來建立伺服器。您也可以更新伺服器設定來自訂伺服器配置，方法是按一下**配置**標籤。{{site.data.keyword.mobilefoundation_short}} 可讓您存取一些進階設定。

*	從**拓蹼**標籤中，您可以選取伺服器大小和所需的實例數目。預設 1 GB 伺服器就足以進行開發及控管測試。

  - 根據您的需求，選取正確的伺服器大小。

* **節點數**會顯示已建立的節點數目。在 {{site.data.keyword.mobilefoundation_short}}: Developer 中無法編輯此欄位。在 Developer 方案中，<!--in your {{site.data.keyword.IBM_notm}} container group-->節點數目預設為 **1**。

如需詳細資料，請參閱 [{{site.data.keyword.mobilefoundation_long}} 文件](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}。
