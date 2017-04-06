---

copyright:
  years: 2016, 2017
lastupdated: "2017-3-3"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 開始使用 {{site.data.keyword.product-insights_short}}
{: #product-insights}

{{site.data.keyword.product-insights_full}} 會連接至內部部署的 IBM 軟體產品，以建置跨產品的庫存，並提供關於產品用量度量值的見解。

{:shortdesc}

{{site.data.keyword.product-insights_short}} 服務會在 IBM Bluemix 內執行，並接收來自已啟用之內部部署 IBM 軟體產品的資訊。這項資訊接著會顯示在服務實例儀表板內。若要使用服務，您必須有 Bluemix 帳戶，並在組織及空間中建立服務。您的已啟用內部部署產品的產品及用量資訊，會在該項獨特服務的範圍或環境定義中安全地儲存與檢視。 

提示：為了簡單起見，您可以一開始使用單一服務實例。

若要開始使用 {{site.data.keyword.product-insights_short}}，請完成下列步驟：

1.  在**管理**標籤中，按一下**登錄產品**按鈕，以檢視支援的產品清單，以及所需的版本層次。我們提供了每個產品類型的指示，以便您能將內部部署產品實例連接到 {{site.data.keyword.product-insights_short}} 服務。如果需要，請將您的已啟用內部部署 IBM 軟體產品更新至最低的必要層次。若為需要最低支援層次的產品，請安裝修正套件或臨時修正程式，以便啟用與 {{site.data.keyword.product-insights_short}} 的整合。 
2.  將您的已啟用內部部署 IBM 軟體產品連接至 {{site.data.keyword.product-insights_short}} 服務。在每個產品的配置過程中，您需要服務認證（亦即 apikey 和 apihost）。您可以在服務儀表板的**服務認證**標籤找到服務認證。 
3.  啟用並連接每個產品實例之後，您可能需要啟動或重新啟動產品或產品實例，它們才能提供產品及用量資訊給 {{site.data.keyword.product-insights_short}} 服務。 

如需啟用產品的詳細資料、每個產品所需的最低支援層次，以及如何啟用每個產品以和 {{site.data.keyword.product-insights_short}} 整合，請加入 {{site.data.keyword.product-insights_full}} [技術社群](https://developer.ibm.com/product-insights/)。

您可以在服務儀表板選取**管理**，來檢視您的庫存。  

* 在服務儀表板中，已連接的產品名稱會列在**產品**窗格中。 
* 若要顯示所有產品實例，請選取**檢視全部**。若要顯示產品的產品實例，請從**產品**窗格選取該產品，它們便會顯示在**實例**窗格。
* 若要顯示單一產品實例的詳細資料，請從**實例**窗格選取產品實例。**詳細資料**窗格隨即移入資料。**詳細資料**窗格會顯示產品實例的詳細資料，以及從實例傳送的用量資訊。
* **用量**標籤會以圖形格式顯示產品用量資訊。視產品而定，您可以指定想要檢視的資訊類型，以及取樣期間。
* **詳細資料**標籤會顯示產品實例資訊；包括產品資訊、環境資訊及元件資訊。
* 在其**服務**標籤的**警告器**標籤中，提供了可能對現行產品實例有益的其他服務詳細資料。在其**更新**標籤中，提供了產品實例版本層次及其貨幣的資訊。










