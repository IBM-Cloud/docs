---

copyright:
  years: 2015, 2017
lastupdated: "2017-5-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 將 {{site.data.keyword.jazzhub_short}} 專案升級至工具鏈
{: #upgrade_projects}

{{site.data.keyword.jazzhub}} 將會逐漸發展成 {{site.data.keyword.contdelivery_full}}。進行該變更時，會將專案升級至工具鏈。

您可以升級專案，或等待它自動升級。若要獲得最佳經驗，請確定您符合[必要條件](#upgrade_prereqs)，並盡快升級專案，以控制工具鏈的名稱，以及在其中建立它的組織。
{: shortdesc}

## 工具鏈
{: #compare_toolchains}

工具鏈就像專案，但有一些重要差異：

- 專案只能有一個儲存庫及管線。視需要，工具鏈可以有任意數目的儲存庫及管線。
- 工具鏈可以包含專案中無法使用的工具（例如 Slack、Sauce Labs、PagerDuty 及 {{site.data.keyword.DRA_full}}）。
- 工具鏈的存取權是透過標準 {{site.data.keyword.Bluemix_notm}} 組織進行管理。與專案不同，成員資格是在組織層次進行維護，而在專案中，成員資格是在專案層次進行維護。

您可以在 [YouTube![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://youtu.be/2SIPE1e7NJ4){: new_window} 上或從[開始使用 {{site.data.keyword.contdelivery_short}}](/docs/services/ContinuousDelivery/index.html) 中瞭解工具鏈。
[![指向 YouTube 的外部鏈結](images/CD_video.png)](https://youtu.be/2SIPE1e7NJ4){: new_window}

## 必要條件
{: #upgrade_prereqs}

- 若要存取已升級專案的工具鏈，您需要 {{site.data.keyword.Bluemix_notm}} ID。升級之前，您必須驗證您有作用中的 {{site.data.keyword.Bluemix_notm}} ID。如果您沒有，請[註冊](https://console.ng.bluemix.net/registration/)。
- 確定 {{site.data.keyword.jazzhub_short}} 專案擁有者正確無誤。從您專案建立的工具鏈將是該擁有者之 {{site.data.keyword.Bluemix_notm}} 組織的一部分。
- 如果您計劃開始升級，請確定您是每個在其中部署管線的組織及空間的成員。任何專案管理者都可以開始升級。不過，如果開始升級的管理者不是每個在其中部署管線的組織及空間的成員，則無法建立管線。開始升級的人員會變成工具鏈中儲存庫的擁有者。
- 工具鏈中的 Eclipse Orion {{site.data.keyword.webide}} 不同於與專案相關聯的 {{site.data.keyword.webide}}。如果您使用 {{site.data.keyword.webide}}，而且有未確定的變更，請先確定它們，再進行升級。


## 從專案升級至工具鏈
{: #project_to_toolchain}

**重要事項：**hub.jazz.net 及工具鏈中的專案都是在美國南部地區進行管理。如果您的專案已配置成將應用程式部署至不同地區，則在將專案升級至工具鏈之後，仍會將應用程式部署至該地區。

準備好升級專案時，會在專案的卡片及「概觀」頁面上顯示一則訊息。

![具有「準備好進行升級」標籤之卡片的影像](images/card-project-to-upgrade.png)

![升級時間訊息](images/banner-ready-to-upgrade.png)

**提示：**您可以從「我的專案」頁面的功能表中找到準備好升級的專案：

![「要升級的專案」功能表項目的影像](images/menu-projects-to-upgrade.png)

開始升級時，會鎖定您專案中的管線階段。您將無法執行或修改它們。如果您刪除工具鏈來回復升級，則會將管線解除鎖定。

如果您的專案使用在 JazzHub 上管理的 Git 儲存庫，則在開始升級之後，會鎖定儲存庫，確保移至工具鏈的資料的完整性。如果您刪除工具鏈來回復升級，則會將 JazzHub 上的儲存庫解除鎖定。

## 開始升級處理程序
{: #start_upgrade}

您可以先在 [YouTube![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://youtu.be/LSr2e3uvyLs){: new_window} 上觀看作用中的升級處理程序，然後再開始升級處理程序。
[![指向 YouTube 的外部鏈結](images/migration-video2.png)](https://youtu.be/LSr2e3uvyLs){: new_window}

若要將專案升級至工具鏈，請遵循下列步驟：

1. 若要開始升級處理程序，請按一下橫幅訊息上的**立即升級**。即會開啟「專案升級工具鏈」頁面。

   ![升級頁面範例](images/project-upgrade-toolchain.png)

   如需升級處理程序的概觀，請閱讀該頁面上的說明。此工具鏈會包含新的管線，而這個管線包含與專案管線相同的階段及工作。此外，此工具鏈將包含 {{site.data.keyword.contdelivery_short}} 中所執行 Eclipse Orion {{site.data.keyword.webide}} 的指標。

   在此範例中，因為專案使用 github.com 上的公用儲存庫，所以工具鏈將會連接至相同的 GitHub 儲存庫。如果您的專案使用在 JazzHub 上管理的 Git 儲存庫，則該儲存庫的內容將會複製到 {{site.data.keyword.gitrepos}}（這是 {{site.data.keyword.contdelivery_short}} 的一部分）中的新儲存庫。如需各種儲存庫處理方式的完整詳細資料，請參閱下表。

|專案儲存庫 |專案類型	|工具鏈儲存庫 |
|:----------|:------------------------------|:------------------|
|github.com 		|專用或公用 		|具有「{{site.data.keyword.Bluemix_notm}} 公用」的相同 github.com 儲存庫。	|
|hub.jazz.net/git		|專用或公用 		|{{site.data.keyword.gitrepos}} 中具有「{{site.data.keyword.Bluemix_notm}} 公用」的新儲存庫。	|
{: caption="表 1. 對映至工具鏈儲存庫的專案儲存庫" caption-side="top"}

2. 若要自訂工具鏈，您可以配置一些設定：

   - 若要變更工具鏈的名稱，請編輯**名稱**欄位。

      ![名稱欄位](images/name-change.png)

   - 若要變更在其中建立工具鏈的 {{site.data.keyword.Bluemix_notm}} 組織，請從帳戶功能表中選取組織：

      ![Bluemix 組織選擇器](images/bluemix-organization-chooser.png)

   因為工具鏈是在組織層次進行管理，所以請一定要選取已經有或可新增需要存取此工具鏈之專案成員的組織。

3. 如果您已在專案中使用「追蹤及計劃」，則可以將「追蹤及計劃」資料傳送至 GitHub Issues。

   ![「追蹤及計劃」選項](images/upgrade-tutorial-track-and-plan.png)

   - 指出是否要移轉「追蹤及計劃」資料。
   - 預設會移轉所有「追蹤及計劃」資料。如果您偏好只移轉屬於特定查詢一部分的工作項目，請指定該查詢。
   - 選取您要對映至 GitHub Issues 中標籤的任何工作項目屬性。

4. 按一下**建立**。即會建立新的工具鏈，並顯示其「概觀」頁面。

   ![已升級工具鏈的概觀](images/new-toolchain-page.png)

   - 若要存取 GitHub 儲存庫或相關聯的問題追蹤器，請按一下 **GitHub** 或 **Issues**。
   - 若要存取管線，請按一下 **Delivery Pipeline**。
   - 若要存取包含已移出至工作區之儲存庫內容的 {{site.data.keyword.webide}}，請按一下 **Eclipse Orion {{site.data.keyword.webide}}**。

   如果您在升級期間回到專案，則橫幅訊息可能會指出正在升級，特別是升級程序包含將原始碼匯入至新儲存庫時，或將「追蹤及計劃」工作項目匯入為問題時。

   ![將升級至工具鏈之專案的相關訊息](images/project-being-upgraded-banner.png)

## 重新造訪專案
{: #revisit_projects}

您已經準備好使用新的工具鏈。您的專案現在會標示為「已升級」，並且會在「概觀」頁面上顯示確認訊息。

![具有「已升級」標籤之專案卡片的影像](images/card-upgraded-project.png)

![已升級的專案](images/banner-upgraded.png)

您可以從「我的專案」頁面的功能表中選取**已升級的專案**，來查看哪些專案已完成升級：

![「已升級的專案」功能表項目的影像](images/menu-upgraded-projects.png)

如果您需要回復升級，請刪除工具鏈。您可以從工具鏈「概觀」頁面的**其他動作**功能表中刪除工具鏈：

![「其他動作」功能表中「刪除」動作的影像](images/upgrade-tutorial-delete-toolchain.png)

當您回到專案時，會再次顯示升級訊息，而您可以在準備好時重新升級。

## 後續步驟
{: #upgrade_next_steps}

1. 重新整理瀏覽器，並檢查專案「概觀」頁面上您的專案「已升級至此工具鏈」的訊息，確認升級已完成：

   ![橫幅中指出專案已升級的訊息](images/banner-upgraded.png)

   **附註：**如果訊息指出「立即升級」，則升級失敗。按一下**立即升級**鏈結，再試一次。

   ![橫幅中指出專案已準備好升級的訊息](images/banner-ready-to-upgrade.png)

2. 將工具鏈的存取權授與團隊成員。
    - 每一個團隊成員都必須具有有效的 {{site.data.keyword.Bluemix_notm}} 帳戶。沒有帳戶的團隊成員必須進行[註冊 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/registration){:new_window}。
    - 從工具鏈「管理」頁面中，將工具鏈存取權授與組織成員。如需工具鏈存取控制的相關資訊，請參閱[管理存取權 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){:new_window}。
    - 如果使用者不是工具鏈所屬組織的成員，請從「管理組織」頁面中將他們新增至組織。
      如需管理組織的相關資訊，請參閱[管理組織及空間 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](/docs/admin/orgs_spaces.html#orgsspacesusers){:new_window}。

3. 使用工具鏈中的工具，而不是 {{site.data.keyword.jazzhub_short}} 專案中的工具。例如，若要從瀏覽器編輯程式碼，請使用工具鏈中的 Web IDE。

4. 如果您使用的是 {{site.data.keyword.gitrepos}}，請使用個人存取記號或 SSH 金鑰進行鑑別。如需 SSH 金鑰的相關資訊，請參閱[建立個人存取記號或 SSH 金鑰來進行鑑別](/docs/services/ContinuousDelivery/git_working.html#git_authentication)。若要從外部 Git 用戶端透過 https 進行鑑別，請遵循下列步驟：
    1. 移至 {{site.data.keyword.gitrepos}} 使用者設定的[存取記號頁面 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://git.ng.bluemix.net/profile/personal_access_tokens){:new_window}。
    2. 建立使用 **api** 作為範圍的個人存取記號。
    3. 移至[帳戶頁面 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://git.ng.bluemix.net/profile/account){:new_window}，並針對 {{site.data.keyword.gitrepos}} 尋找您的使用者名稱。您的使用者名稱會列在「變更使用者名稱」區段中，並顯示為任何您建立的個人儲存庫的 URL 的第一個部分。
    4. 若要從外部 Git 用戶端透過 https 向 {{site.data.keyword.gitrepos}} 進行鑑別，請使用您的使用者名稱及個人存取記號。
    5. 如果您要重複使用 JazzHub Git 儲存庫的本端儲存庫，請將儲存庫指向 {{site.data.keyword.gitrepos}} 中的新儲存庫。從終端機的 Shell 中，切換至在其中複製 JazzHub Git 儲存庫的目錄。輸入 `git remote set-url` 指令：`git remote set-url origin https://git.ng.bluemix.net/<userid>/<name-of-new-repo>`

        **提示：**若要檢查哪些遠端 URL 設為哪些遠端名稱，請使用 `git remote -v` 指令。預設遠端名稱是 `origin`。如果您有更進階的安裝，則指令的形式如下：`git remote set-url <remote-name-that-uses-jazzhub-repo> https://git.ng.bluemix.net/<userid>/<name-of-new-repo>`

5. 若已設定工具鏈，並且開始使用工具鏈，請考慮採取所有這些步驟或其中任何步驟，以確保沒有人使用您的專案：
    - 新增專案名稱的字尾，指出不得使用它。您可以在專案名稱尾端新增 `_DO_NOT_USE`。
    - 更新專案的說明以提及不再使用它，並新增工具鏈的指標。
    - 從專案中移除成員。
    - 當您不再需要此專案時，請將它刪除。

6. 選用項目：若要探索您專案的開發成熟度、團隊的作法，以及程式碼庫的品質，請將 IBM Cloud {{site.data.keyword.DRA_short}} 新增至工具鏈。{{site.data.keyword.DRA_short}} 會將開發人員、團隊及部署分析人員套用至 DevOps 專案。如需相關資訊，請參閱[開始使用 {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html)。


## 疑難排解
{: #upgrade_troubleshoot}

如果您有任何疑問或問題，請移至[支援討論區](https://developer.ibm.com/answers/questions/ask/?smartspace=devops-services)。在討論區貼文中，併入 {{site.data.keyword.jazzhub_short}} 專案及 {{site.data.keyword.contdelivery_short}} 工具鏈的 URL，並將貼文標上 `devops-services` 標籤。
