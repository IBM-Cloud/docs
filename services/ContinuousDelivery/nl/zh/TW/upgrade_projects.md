---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-21"

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 將 {{site.data.keyword.jazzhub_short}} 專案升級至工具鏈
{: #upgrade_projects}

{{site.data.keyword.jazzhub}} 將會逐漸發展成 {{site.data.keyword.contdelivery_full}}。進行該變更時，會將專案升級至工具鏈。 

您可以升級專案，或等待它自動升級。若要獲得最佳經驗，請盡快升級專案，以控制工具鏈的名稱，以及在其中建立它的組織。  
{: shortdesc}

## 工具鏈
{: #compare_toolchains}

工具鏈就像專案，但有一些重要差異：

- 專案只能有一個儲存庫及管線。視需要，工具鏈可以有任意數目的儲存庫及管線。
- 工具鏈可以包括專案中無法使用的工具（例如 Slack、Sauce Labs、PagerDuty 及 {{site.data.keyword.DRA_full}}）。
- 工具鏈的存取權是透過標準 Bluemix 組織進行管理。與專案不同，成員資格是在組織層次進行維護，而在專案中，成員資格是在專案層次進行維護。

您可以在 [YouTube![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://youtu.be/2SIPE1e7NJ4){: new_window} 上或從[開始使用 {{site.data.keyword.contdelivery_short}}](/docs/services/ContinuousDelivery/index.html) 中瞭解工具鏈。
[![YouTube 的外部鏈結](images/CD_video.png)](https://youtu.be/2SIPE1e7NJ4){: new_window}    

## 必要條件
{: #upgrade_prereqs}    

- 若要存取已升級專案的工具鏈，您需要 Bluemix ID。升級之前，您必須驗證您有作用中的 Bluemix ID。如果您沒有，請[註冊](https://console.ng.bluemix.net/registration/)。
- 確定 DevOps Services 專案擁有者正確無誤。從您專案建立的工具鏈將是該擁有者之 Bluemix 組織的一部分。

**重要事項：**工具鏈中的 Eclipse Orion {{site.data.keyword.webide}} 不同於與專案相關聯的 {{site.data.keyword.webide}}。如果您使用 {{site.data.keyword.webide}}，而且有未確定的變更，請先確定它們，再進行升級。  


## 從專案升級至工具鏈
{: #project_to_toolchain}

準備好升級專案時，會在專案的卡片及「概觀」頁面上顯示一則訊息。

![含「準備好進行升級」標籤之卡片的影像](images/card-project-to-upgrade.png)

![升級時間訊息](images/banner-ready-to-upgrade.png)

**提示：**您可以從「我的專案」頁面的功能表中找到準備好升級的專案： 

![「要升級的專案」功能表項目的影像](images/menu-projects-to-upgrade.png)

## 開始升級處理程序
{: #start_upgrade}

您可以先在 [YouTube![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://youtu.be/oaZVGveVxBg){: new_window} 上觀看作用中的升級處理程序，然後再開始升級處理程序。
[![YouTube 的外部鏈結](images/migration-video2.png)](https://youtu.be/oaZVGveVxBg){: new_window}    
若要將專案升級至工具鏈，請遵循下列步驟：

1. 若要開始升級處理程序，請按一下橫幅訊息上的**立即升級**。即會開啟「專案升級工具鏈」頁面。 

   ![升級頁面範例](images/project-upgrade-toolchain.png)

   如需升級處理程序的概觀，請閱讀該頁面上的說明。在此情況下，因為專案使用 GitHub.com 上的儲存庫，所以工具鏈將會連接至相同的 GitHub 儲存庫。此工具鏈會包括新的管線，而這個管線包含與專案管線相同的階段及工作。此外，此工具鏈將包含 {{site.data.keyword.contdelivery_short}} 中所執行 Eclipse Orion {{site.data.keyword.webide}} 的指標。

2. 若要自訂工具鏈，您可以配置一些設定：

   - 若要變更工具鏈的名稱，請編輯**名稱**欄位。

      ![名稱欄位](images/name-change.png)

   - 若要變更在其中建立工具鏈的 {{site.data.keyword.Bluemix_notm}} 組織，請從帳戶功能表中選取組織：

      ![Bluemix 組織選擇器](images/bluemix-organization-chooser.png)

   因為工具鏈是在組織層次進行管理，所以請一定要選取已經有或可新增需要存取此工具鏈之專案成員的組織。 
  
3. 按一下**建立**。即會建立新的工具鏈，並顯示其「概觀」頁面。

   ![已升級工具鏈的概觀](images/new-toolchain-page.png)

   - 若要存取 GitHub 儲存庫或關聯的問題追蹤器，請按一下 **GitHub** 或 **Issues**。
   
   - 若要存取管線，請按一下 **Delivery Pipeline**。  
   
   - 若要存取包含已移出至工作區之儲存庫內容的 {{site.data.keyword.webide}}，請按一下 **Eclipse Orion {{site.data.keyword.webide}}**。 

## 重新造訪專案
{: #revisit_projects}

您已經準備好使用新的工具鏈。您的專案現在會標示為「已升級」，並且會在「概觀」頁面上顯示確認訊息。

![含「已升級」標籤之專案卡的影像](images/card-upgraded-project.png)

![已升級的專案](images/banner-upgraded.png)

您可以從「我的專案」頁面的功能表中選取**已升級的專案**，來查看已升級的專案：

![「已升級的專案」功能表項目的影像](images/menu-upgraded-projects.png)

如果您需要回復升級，請刪除工具鏈。然後，當您回到專案的「概觀」頁面時，會再次顯示升級訊息，而您可以在準備好時重新升級。

## 後續步驟
{: #upgrade_next_steps}   

1. 檢查專案「概觀」頁面上的訊息，確認升級已完成：    

   ![已升級的專案](images/banner-upgraded.png)    

2. 將工具鏈的存取權授與團隊成員。    
    - 每一個團隊成員都必須具有有效的 Bluemix 帳戶。沒有帳戶的團隊成員必須進行[註冊 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/registration){:new_window}。
    - 將團隊成員新增至工具鏈所屬的組織。
3. 使用工具鏈中的工具，而不是 {{site.data.keyword.jazzhub_short}} 專案中的工具。例如，若要從瀏覽器編輯程式碼，請使用工具鏈中的 Web IDE。    

## 疑難排解
{: #upgrade_troubleshoot}    

如果您有任何疑問或問題，請傳送電子郵件至 [hub@jazz.net](mailto:hub@jazz.net)。請在電子郵件中，併入 {{site.data.keyword.jazzhub_short}} 專案及 {{site.data.keyword.contdelivery_short}} 工具鏈的 URL。

