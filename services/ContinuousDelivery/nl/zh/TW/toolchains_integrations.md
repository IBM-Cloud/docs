---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}    

# 配置工具整合
{: #integrations}

您可以在建立開放式工具鏈時配置可支援開發、部署及操作作業的工具整合，也可以新增及配置用來自訂現有工具鏈的工具整合。  
{:shortdesc}

**重要事項**：在「{{site.data.keyword.Bluemix_notm}} 公用」上，工具鏈只適用於美國南部地區。

可用來新增及配置工具鏈的工具整合，會根據是在「{{site.data.keyword.Bluemix_notm}} 公用」還是在「{{site.data.keyword.Bluemix_notm}} 專用」上使用工具鏈而不同。如果您在「{{site.data.keyword.Bluemix_notm}} 專用」上使用工具鏈，則可供您使用的工具整合取決於 {{site.data.keyword.contdelivery_full}} 在特定環境上的設定方式。

|工具整合 |可用於 {{site.data.keyword.Bluemix_notm}} 公用	|可用於 {{site.data.keyword.Bluemix_notm}} 專用（環境相依）|
|:----------|:------------------------------|:------------------|
|{{site.data.keyword.alertnotificationshort}}		|是		|否		|
|Artifactory		|是		|否		|
|可用性監視		|是		|否		|
|雲端事件管理		|是		|否		|
|{{site.data.keyword.deliverypipeline}} 		|是	   	|是  		|
|{{site.data.keyword.DRA_short}} 		|是		|否			|
|Eclipse Orion {{site.data.keyword.webide}}		|是		|是			|
|Git 儲存庫及問題追蹤	|是		|否		|
|GitHub 和 GitHub Issues		|是		|是		|
|專用 {{site.data.keyword.ghe_short}} 及問題			|否		|是		|
|Jenkins		|是		|否		|
|JIRA		|是		|否		|
|Nexus			|是		|否		|
|其他工具			|是		|是		|
|PagerDuty			|是		|是		|
|Sauce Labs		|是		|否		|
|Slack			|是		|是		|
{: caption="Table 1. Tool integrations available for toolchains on {{site.data.keyword.Bluemix_notm}} Public and Dedicated" caption-side="top"}

**提示**：如果您要在「{{site.data.keyword.Bluemix_notm}} 公用」上開始使用原始碼進行開發，請先配置 GitHub 工具整合或「Git 儲存庫及問題追蹤」工具整合，再配置 {{site.data.keyword.deliverypipeline}}。如果您要在「{{site.data.keyword.Bluemix_notm}} 專用」上開始使用程式碼進行開發，請先配置 {{site.data.keyword.ghe_short}} 工具整合或 GitHub 工作整合，再配置 {{site.data.keyword.deliverypipeline}}。


## 配置警示通知（實驗性）
{: #alertnotification}

{{site.data.keyword.alertnotificationfull}} 是一個混合式雲端型解決方案，可用來集中化及簡化通知策略。它與其他雲端型及內部部署應用程式搭配運作。使用安全 RESTful API，即可將警示轉遞給 {{site.data.keyword.alertnotificationshort}}。

配置 {{site.data.keyword.alertnotificationshort}} 以接收有關 DevOps 處理程序期間之問題的通知。

### 必要條件

1. 如果您沒有 {{site.data.keyword.alertnotificationshort}} 帳戶，請註冊一個帳戶：

 a. 開啟 IBM Marketplace 中的 [IBM {{site.data.keyword.alertnotificationshort}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/us-en/marketplace/alert-notification){: new_window} 頁面。

 b. 購買訂閱，或註冊以取得免費 90 天試用。

1. 設定 {{site.data.keyword.alertnotificationshort}} 帳戶之後，請開啟[我的 IBM 儀表板 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://myibm.ibm.com/dashboard/){: new_window}。
1. 按一下 IBM {{site.data.keyword.alertnotificationshort}} 旁的**啟動**。
1. 按一下**管理 API 金鑰**，然後按一下**建立 API 金鑰**。
1. 在**建立 API 金鑰**欄位中，鍵入說明。
1. 按一下**產生**。即會顯示新的 API 金鑰資訊（包括名稱及密碼）。您需要該資訊來進行工具整合配置，因此仍會開啟「新建 API 金鑰」視窗。基於安全目的，您之後無法擷取 API 金鑰密碼。

### 配置警示通知

1. 如果您要在建立工具鏈時配置此工具整合，請按一下「可配置的整合」區段中的 **{{site.data.keyword.alertnotificationshort}}**。
1. 如果您有工具鏈，並且要在其中新增此工具整合，請在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟其「概觀」頁面。或者，在應用程式之「概觀」頁面的「持續交付」卡上，按一下**檢視工具鏈**。然後，按一下**概觀**。  

 a. 按一下**新增工具**。

 b. 在「工具整合」區段中，按一下 **{{site.data.keyword.alertnotificationshort}}**。

1. 鍵入您要使用之 {{site.data.keyword.alertnotificationshort}} API 的 URL。您可以在 {{site.data.keyword.alertnotificationshort}} 服務的「管理 API 金鑰」頁面上找到此 URL；例如，`https://ibmnotifybm.mybluemix.net/api/alerts/v1`。
1. 鍵入 {{site.data.keyword.alertnotificationshort}} 的 API 金鑰名稱。您可以在「新建 API 金鑰」視窗中找到 API 金鑰名稱。
1. 鍵入 {{site.data.keyword.alertnotificationshort}} 針對 API 金鑰所產生的密碼。您可以在「新建 API 金鑰」視窗中找到 API 金鑰密碼。
1. 按一下**建立整合**。
1. 從工具鏈中，按一下 **{{site.data.keyword.alertnotificationshort}}**。

如需相關資訊，請參閱 [IBM {{site.data.keyword.alertnotificationshort}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/devops/method/content/manage/tool_alert_notification/){: new_window}。


## 配置 Artifactory
{: #artifactory}

配置 Artifactory 儲存庫管理員，以將建置構件儲存至 Artifactory 儲存庫：

1. 如果您要在建立工具鏈時配置此工具整合，請按一下「可配置的整合」區段中的 **Artifactory**。
1. 如果您有工具鏈，並且要在其中新增此工具整合，請在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟其「概觀」頁面。或者，在應用程式之「概觀」頁面的「持續交付」卡上，按一下**檢視工具鏈**。然後，按一下**概觀**。  

 a. 按一下**新增工具**。

 b. 在「工具整合」區段中，按一下 **Artifactory**。

1. 鍵入當您按一下 Artifactory 卡時所要開啟的 Artifactory 儲存庫 URL。
1. 選取您要連接的儲存庫類型。
1. 如果您使用的是 Artifactory npm 登錄，請遵循下列步驟：

 a. 鍵入與您的登錄相關聯的電子郵件位址。

 b. 鍵入與您的登錄相關聯的鑑別記號。

 c. 鍵入 Artifactory 版本儲存庫的 URL，這是您在 Artifactory 伺服器上的專用登錄。

 d. 鍵入您用來合併多個公用及專用 npm 登錄的「鏡映」或「公用」登錄 URL。例如，此 URL 可能是 Artifactory 伺服器上可存取專用登錄及 npm 廣域登錄快取的虛擬登錄 URL。

1. 如果您使用的是 Artifactory Maven 儲存庫，請遵循下列步驟：

 a. 鍵入與您的儲存庫相關聯的使用者 ID。

 b. 鍵入與您的儲存庫相關聯的密碼。

 c. 鍵入 Artifactory 版本儲存庫的 URL，這是您在 Artifactory 伺服器上的專用版本儲存庫。

 d. 鍵入 Artifactory Snapshot 儲存庫的 URL，這是您在 Artifactory 伺服器上的專用 Snapshot 儲存庫。

 e. 鍵入您用來合併多個公用及專用 Maven 儲存庫的「鏡映」或「公用」儲存庫 URL。例如，此 URL 可能是 Artifactory 伺服器上可存取專用儲存庫及 Maven 中央儲存庫快取的虛擬儲存庫 URL。

1. 按一下**建立整合**。
1. 按一下您要使用的 Artifactory 儲存庫卡。即會開啟 Artifactory 網站，您可以在其中檢視儲存庫的內容。
1. 選用項目：如果您是在「{{site.data.keyword.Bluemix_notm}} 公用」上使用工具鏈，並且想要透過搭配使用 Artifactory 與 npm 來建置應用程式，請配置管線來新增 npm 建置工作。如需配置建置工作的指示，請參閱[在管線中配置 Artifactory npm 建置工作](#config_artifactory_npm)一節。
1. 選用項目：如果您是在「{{site.data.keyword.Bluemix_notm}} 公用」上使用工具鏈，並且想要透過搭配使用 Artifactory 與 Maven 來建置應用程式，請配置管線來新增 Maven 建置工作。如需配置建置工作的指示，請參閱[在管線中配置 Artifactory Maven 建置工作](#config_artifactory_maven)一節。

### 在管線中配置 Artifactory npm 建置工作
{: #config_artifactory_npm}

您必須具有可使用建置 SCM 儲存庫作為輸入的可運作管線，而且必須為工具鏈配置 Artifactory，然後才能在管線中配置 npm 建置工作。如需配置 Artifactory 的指示，請參閱 [Artifactory](#artifactory) 一節。

配置 {{site.data.keyword.deliverypipeline}} 來新增 npm 建置工作：

1. 建立階段，並設定適當 SCM 儲存庫的輸入。
1. 在此階段上，新增建置工作。
1. 配置建置工作：![npm 建置工作](images/artifactory_npm_job.png)

  a. 針對建置器類型，選取 **NPM 建置**。

  b. 如果您已配置多個 Artifactory 工具整合實例，請輸入您要為其配置 npm 建置工作之 Artifactory 工具整合的名稱。

  c. 針對工具整合類型，選取 **Artifactory**。

  d. 針對建置指令，輸入指令來建置 npm 模組或將它發佈至登錄。此範例顯示用來建置或發佈模組的指令。
     ```
     npm install
     # or
     npm publish --registry "${NPM_RELEASE_URL}"
     ```
  **提示**：您可以在 Artifactory 工具整合的配置設定中，找到用來連接至登錄的 URL 及使用者認證。

  e. 如果您的建置工作發佈至 Artifactory 登錄，而且節點模組版本的格式為 `x.y.z-SNAPSHOT.w`，請選取**增量 Snapshot 模組版本**勾選框。建置工作會自動更新模組版本，然後才將工作發佈至 Artifactory 登錄。工作會從 npm 登錄及本端 `package.json` 檔案中選取最高版本的模組，並使用 semver 來增量模組版本。建置工作不會將變更遞送至 SCM 儲存庫。

1. 按一下**儲存**。只要管線執行，此建置工作就會使用 Artifactory 工具整合中的配置資訊來連接至 npm 登錄。

### 在管線中配置 Artifactory Maven 建置工作
{: #config_artifactory_maven}

您需要有可使用建置 SCM 儲存庫作為輸入的可運作管線，而且必須為工具鏈配置 Artifactory，然後才能在管線中配置 Maven 建置工作。如需配置 Artifactory 的指示，請參閱 [Artifactory](#artifactory) 一節。

配置 {{site.data.keyword.deliverypipeline}} 來新增 Maven 建置工作：

1. 建立階段，並設定適當 SCM 儲存庫的輸入。
1. 在此階段上，新增建置工作。
1. 配置建置工作：![Maven 建置工作](images/artifactory_maven_job.png)

  a. 針對建置器類型，選取 **Maven 建置**。

  b. 如果您已配置多個 Artifactory 工具整合實例，請輸入您要為其配置 Maven 建置工作之 Artifactory 工具整合的名稱。

  c. 針對工具整合類型，選取 **Artifactory**。

  d. 針對建置指令，輸入指令來建置 Maven 模組或將它發佈至 Snapshot 登錄。此範例顯示用來建置模組或將它發佈至 Snapshot 登錄的指令。
     ```
     mvn -B clean package
     # or
     mvn -DaltDeploymentRepository="snapshots::default::${MAVEN_SNAPSHOT_URL}" deploy
     ```
  **提示**：您可以在 Artifactory 工具整合的配置設定中，找到用來連接至登錄的 URL 及使用者認證。

1. 按一下**儲存**。只要管線執行，此建置工作就會使用 Artifactory 工具整合中的配置資訊來連接至 Maven 儲存庫。

若要進一步瞭解，請參閱 [Artifactory ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/devops/method/content/code/tool_artifactory/){: new_window}。


## 新增可用性監視
{: #availabilitymonitoring}

{{site.data.keyword.prf_hublong}} 可在影響使用者之前隔離問題、識別型樣，以及改善效能。您可以從世界各地測試應用程式、與各交付管線整合，以及瞭解如何持續最佳化程式碼。

**附註**：這是預先配置的工具整合，且不需要任何配置參數。您無法重新配置此工具整合。

若要在建置應用程式時測試、監視及改善應用程式的性能，請新增 {{site.data.keyword.prf_hubshort}} 工具整合：

1. 如果您有工具鏈，並且要在其中新增此工具整合，請在 DevOps 儀表板的「工具鏈」頁面上按一下工具鏈，以開啟其「概觀」頁面。或者，在應用程式之「概觀」頁面的「持續交付」卡上，按一下**檢視工具鏈**，然後按一下**概觀**。

 a. 按一下**新增工具**。

 b. 在「工具整合」區段中，按一下 **{{site.data.keyword.prf_hubshort}}**。

1. 按一下**建立整合**。
1. 按一下 **{{site.data.keyword.prf_hubshort}}**，以開啟 {{site.data.keyword.prf_hubshort}} 儀表板、選取應用程式，以及配置監視應用程式。

若要進一步瞭解，請參閱 [{{site.data.keyword.prf_hublong}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/devops/method/content/manage/tool_bluemix_availability_monitoring/){: new_window}。


## 新增雲端事件管理（實驗性）
{: #cloudeventmanagement}

{{site.data.keyword.evtmgt_full}} 提供服務、應用程式及基礎架構所發生問題的合併視圖。您可以設定即時突發事件管理，以更有效率地解決問題。

**附註：**這是預先配置的工具整合，且不需要任何配置參數。您無法重新配置。

若要協助 DevOps 團隊達成可靠的操作性能、服務品質及持續改善目標，請將「雲端事件管理」新增至工具鏈：

1. 在 DevOps 儀表板的「工具鏈」頁面上，按一下要新增「雲端事件管理」的工具鏈。或者，在應用程式之「概觀」頁面的「持續交付」卡上，按一下**檢視工具鏈**，然後按一下**概觀**。

 a. 按一下**新增工具**。

 b. 在「工具整合」區段中，按一下**雲端事件管理**。

1. 按一下**建立整合**。
1. 從工具鏈中，按一下下列任何工具卡：

 * **雲端事件管理**，以開始使用「雲端事件管理」。

 * **{{site.data.keyword.alertnotificationshort}}**，以建立原則來判斷使用者何時收到突發事件通知。

 * **Runbook Automation**，以在「雲端事件管理」中管理 Runbook 型錄。


## 配置 Delivery Pipeline
{: #deliverypipeline}

{{site.data.keyword.deliverypipeline}} 會透過一系列擷取輸入並執行工作（例如建置、測試及部署）的階段，來自動進行專案的持續部署。

配置 {{site.data.keyword.deliverypipeline}} 來自動進行應用程式的持續建置、測試及部署：

1. 如果您要在建立工具鏈時配置此工具整合，請按一下「可配置的整合」區段中的 **{{site.data.keyword.deliverypipeline}}**。根據您使用的範本，可能會有不同的欄位。請檢閱預設欄位值，並在必要時變更那些設定。
1. 如果您有工具鏈，並且要在其中新增此工具整合，請在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟其「概觀」頁面。或者，在應用程式之「概觀」頁面的「持續交付」卡上，按一下**檢視工具鏈**，然後按一下**概觀**。

 a. 按一下**新增工具**。

 b. 在「工具整合」區段中，按一下 **{{site.data.keyword.deliverypipeline}}**。

1. 指定新管線的名稱。
1. 如果您計劃使用管線來部署使用者介面，請選取**在「檢視應用程式」功能表中顯示應用程式**勾選框。管線所建立的所有應用程式都會顯示在工具鏈之「概觀」頁面的**檢視應用程式**清單中。
1. 按一下**建立整合**，以將 {{site.data.keyword.deliverypipeline}} 新增至您的工具鏈。
1. 按一下 **{{site.data.keyword.deliverypipeline}}**，以檢視管線並進行配置。若要瞭解如何配置管線的基本觀念，請參閱[建置及部署管線](/docs/services/ContinuousDelivery/pipeline_build_deploy.html){: new_window}。

  **提示**：如果要在將變更推送至 GitHub、{{site.data.keyword.ghe_short}} 或 Git 儲存庫時觸發管線，您必須先配置工具鏈的 GitHub、{{site.data.keyword.ghe_short}} 或「Git 儲存庫及問題追蹤」，再定義管線的階段。管線階段需要儲存庫的 Git URL。每一個管線階段都只能參照與您工具鏈相關聯的其中一個 GitHub、{{site.data.keyword.ghe_short}} 或 Git 儲存庫。如需配置 GitHub 的指示，請參閱 [GitHub](#github) 一節。如需配置「專用 {{site.data.keyword.ghe_short}}」的指示，請參閱[開始使用 {{site.data.keyword.ghe_long}}](/docs/services/ghededicated/index.html){: new_window}。如需配置「Git 儲存庫及問題追蹤」的指示，請參閱 [Git 儲存庫及問題追蹤](##gitbluemix)一節。    

  **附註：**如果您沒有 GitHub 或 GitHub Enterprise 儲存庫的管理者專用權，或沒有要鏈結之「Git 儲存庫及問題追蹤」儲存庫的「主要」或「擁有者」專用權，則整合會受到限制，因為您無法使用 Webhook。需要有 Webhook，才能在將確定推送至儲存庫時自動觸發管線。如果沒有 Webhook，您必須手動啟動管線。

1. 選用項目：如果您是在「{{site.data.keyword.Bluemix_notm}} 公用」上使用工具鏈，並且想要 Sauce Labs 對您的應用程式執行測試，請配置 {{site.data.keyword.deliverypipeline}} 來新增 Sauce Labs 測試工作。如需配置測試工作的指示，請參閱[在管線中配置 Sauce Labs 測試工作](#config_saucelabs)一節。

### 在管線中配置 Sauce Labs 測試工作
{: #config_saucelabs}

您需要可運作的管線，具中包含階段可建置及部署應用程式，而且您必須為工具鏈配置 Sauce Labs，然後才在管線中配置 Sauce Labs 測試工作。如需配置 Sauce Labs 的指示，請參閱 [Sauce Labs](#saucelabs) 一節。

配置 {{site.data.keyword.deliverypipeline}} 來新增 Sauce Labs 測試工作：

1. 如果您沒有可部署您應用程式之測試版本的階段，請建立一個。
1. 在此階段上，於部署工作之後新增測試工作。將這些工作放在相同的階段中，它們即可存取一組相同的環境內容。
     
  ![測試工作](images/toolchain_test_job.png)

1. 配置階段：

  a. 在**環境內容**標籤上，建立三個內容：CF_APP_NAME、SAUCE_USERNAME 及 SAUCE_ACCESS_KEY。

  b. 輸入 Sauce Labs 使用者名稱和存取金鑰。這麼做可以將那些值外部化，以便用於測試中。

1. 配置部署工作。在**部署 Script** 欄位中，包括下列指令：`export CF_APP_NAME="$CF_APP"`。該指令會將應用程式名稱匯出為環境內容。
1. 配置測試工作。下列影像中的值是範例。**服務實例**、**目標**、**組織**及**空間**欄位會移入您正在使用的 Sauce Labs 使用者名稱、地區、組織及空間。
  
![配置工作](images/toolchain_configure_job.png)

  a. 針對測試器類型，選取 **Sauce Labs**。

  b. 針對服務實例，選取您為工具鏈配置 Sauce Labs 時所使用的 Sauce Labs 使用者名稱。

   **提示**：若要查看您為工具鏈配置 Sauce Labs 時所使用的使用者名稱和存取金鑰，請按一下**配置**。

  c. 在**測試執行指令**欄位中，輸入可安裝測試所需相依關係的指令，然後執行測試。例如，針對 Node.js 應用程式，您可以輸入下列指令：
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```

    d. 如果您要在測試工作日誌中查看測試報告，請選取**啟用測試報告**勾選框，然後將「測試結果檔案型樣」設為 `test/*.xml`。

1. 按一下**儲存**。只要執行管線，就會執行 Sauce Labs 測試。

若要進一步瞭解，請參閱 [Delivery Pipeline ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/devops/method/content/deliver/tool_delivery_pipeline/){: new_window}。


## 新增 DevOps Insights（測試版）
{: #dra}

{{site.data.keyword.DRA_full}} 會收集並分析單元測試、功能測試及程式碼涵蓋面工具的結果，來判定您的程式碼是否符合部署程序中所指定閘門的預先定義準則。如果程式碼不符合或超出準則，則會停止部署，以防止釋出風險。您可以使用 {{site.data.keyword.DRA_short}} 作為持續交付環境的安全網，或作為實作並改善品質標準的方法。

 **附註**：此工具整合僅適用於「{{site.data.keyword.Bluemix_notm}} 公用」。它是預先配置的，且不需要任何配置參數。您無法重新配置此工具整合。

新增「{{site.data.keyword.DRA_short}}」來維護及改善您的程式碼在 {{site.data.keyword.Bluemix_notm}} 中的品質，方法是在釋出風險之前監視部署來識別風險。

1. 如果您有工具鏈，並且要在其中新增此工具整合，請在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟其「概觀」頁面。或者，在應用程式之「概觀」頁面的「持續交付」卡上，按一下**檢視工具鏈**，然後按一下**概觀**。

 a. 按一下**新增工具**。

 b. 在「工具整合」區段中，按一下 **{{site.data.keyword.DRA_short}}**。

1. 按一下**建立整合**。
1. 按一下 **{{site.data.keyword.DRA_short}}**，然後完成開始使用步驟：建立準則，並將準則連接至管線，然後執行管線。

若要進一步瞭解，請參閱 [{{site.data.keyword.DRA_short}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/devops/method/content/learn/tool_devops_insights/){: new_window}。


## 新增 Eclipse Orion Web IDE
{: #webide}

Eclipse Orion {{site.data.keyword.webide}} 是一個整合的 Web 型環境，您可以在其中建立、編輯、執行、除錯以及完成來源控制作業。您可以平順地依序從編輯移至執行、提交、部署。

 **附註**：這是預先配置的工具整合。它不需要任何配置參數，而且您無法重新配置它。

若要完成來源控制作業，請新增 Eclipse Orion {{site.data.keyword.webide}} 工具整合：

1. 如果您有工具鏈，並且要在其中新增此工具整合，請在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟其「概觀」頁面。或者，在應用程式之「概觀」頁面的「持續交付」卡上，按一下**檢視工具鏈**，然後按一下**概觀**。

 a. 按一下**新增工具**。

 b. 在「工具整合」區段中，按一下 **Eclipse Orion Web IDE**。

1. 按一下**建立整合**。
1. 按一下 **Eclipse Orion {{site.data.keyword.webide}}**。您的工作區會預先移入您的 GitHub 或 {{site.data.keyword.ghe_short}} 儲存庫。會強調顯示與現行工具鏈相關聯的儲存庫。

若要進一步瞭解，請參閱[使用 Eclipse Orion {{site.data.keyword.webide}} 編輯程式碼](/docs/services/ContinuousDelivery/web_ide.html){: new_window}以及 [Eclipse Orion {{site.data.keyword.webide}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/devops/method/content/code/tool_eclipse_orion_web_ide/){: new_window}。


## 配置 Git 儲存庫及問題追蹤（實驗性）
{: #gitbluemix}

「Git 儲存庫及問題追蹤」工具整合是根據 GitLab Community Edition，其為 Git 儲存庫的 Web 型管理服務。您可以同時具有儲存庫的本端及遠端副本。若要進一步瞭解，請參閱 [Git 儲存庫及問題追蹤（實驗性）![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://git.ng.bluemix.net/help){:new_window}。

如果您要在建立工具鏈時配置「Git 儲存庫及問題追蹤」，請遵循下列步驟：    

1. 在「可配置的整合」區段中，按一下 **Git 儲存庫及問題追蹤**。
1. 檢閱 Git 儲存庫的預設目標位置。那些儲存庫是從範例儲存庫中複製而來。必要的話，請變更目標儲存庫的名稱。
 

如果您有工具鏈，並要向其新增「Git 儲存庫及問題追蹤」，請遵循下列步驟：    

1. 在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟其「概觀」頁面。或者，在應用程式之「概觀」頁面的「持續交付」卡上，按一下**檢視工具鏈**，然後按一下**概觀**。
1. 按一下**新增工具**。
1. 在「工具整合」區段中，按一下 **Git 儲存庫及問題追蹤**。
1. 選取儲存庫類型：     

  a. 若要建立空的儲存庫，請針對儲存庫類型按一下**新建**，然後鍵入儲存庫名稱。    
  b. 若要分出 Git 儲存庫，以透過合併要求來提出變更，請針對儲存庫類型按一下**分出**。鍵入來源儲存庫的 URL。    
  c. 若要建立 Git 儲存庫的副本，請針對儲存庫類型按一下**複製**。鍵入新的儲存庫名稱，以及來源儲存庫的 URL。     
  d. 如果您有 Git 儲存庫並且想要使用它，請針對儲存庫類型按一下**現有**。鍵入 URL。    

1. 如果您要使用 Issues 進行問題追蹤，請選取**啟用 Issues** 勾選框。
1. 如果您要透過建立確定的標籤和註解以及確定所參照之問題的標籤和註解來追蹤程式碼變更部署，請選取**追蹤程式碼變更部署**勾選框。如需相關資訊，請參閱[使用工具鏈追蹤程式碼的部署位置 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/blogs/bluemix/2017/03/track-code-deployed-toolchains/){:new_window}。
1. 按一下**建立整合**。
1. 按一下您要使用的 Git 儲存庫卡。即會開啟您的專案概觀頁面。    

**附註：**如果您沒有要鏈結之儲存庫的「主要」或「擁有者」專用權，則整合會受到限制，因為您無法使用 Webhook。需要有 Webhook，才能在將確定推送至儲存庫時自動觸發管線。如果沒有 Webhook，您必須手動啟動管線。


## 配置 GitHub 及 Issues
{: #github}

GitHub 是 Git 儲存庫的 Web 型管理服務。您可以同時具有儲存庫的本端和遠端副本，方便進行分工合作。

GitHub Issues 是一項追蹤工具，可將您的工作和方案都保留在一個位置。它與您的開發儲存庫整合，因此您可以專注於重要作業。

配置 GitHub，以在雲端上管理您的原始碼：

1. 如果您要在建立工具鏈時配置此工具整合，請遵循下列步驟：

 a. 在「可配置的整合」區段中，按一下 **GitHub**。如果您在「{{site.data.keyword.Bluemix_notm}} 公用」上建立工具鏈，但並未授權 {{site.data.keyword.Bluemix_notm}} 存取 GitHub，請按一下**授權**來移至 GitHub 網站。如果您沒有作用中的 GitHub 階段作業，則系統會提示您登入。按一下**授權應用程式**，以容許 {{site.data.keyword.Bluemix_notm}} 存取 GitHub 帳戶。如果您有作用中的 GitHub 階段作業，但最近未輸入過密碼，則系統可能會提示您輸入 GitHub 密碼進行確認。

 b. 檢閱 GitHub 儲存庫的預設目標儲存庫位置。那些儲存庫是從範例儲存庫中複製而來。必要的話，請變更目標儲存庫的名稱。
 ![預設目標儲存庫位置](images/toolchain_github_config.png)

1. 如果您有工具鏈，並且要在其中新增此工具整合，請在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟其「概觀」頁面。或者，在應用程式之「概觀」頁面的「持續交付」卡上，按一下**檢視工具鏈**，然後按一下**概觀**。

 a. 按一下**新增工具**。

 b. 在「工具整合」區段中，按一下 **GitHub**。

1. 如果您有 GitHub 儲存庫並且想要使用它，請針對儲存庫類型按一下**現有**，然後鍵入 URL。
1. 如果您要使用新的 GitHub 儲存庫，請鍵入 GitHub 儲存庫的名稱，並鍵入您所複製或分出之儲存庫的 URL，然後選取儲存庫類型：

 a. 若要建立空的儲存庫，請按一下**新建**。

 b. 若要建立 GitHub 儲存庫的副本，請按一下**複製**。

 c. 若要分出 GitHub 儲存庫，以透過取回要求來提出變更，請按一下**分出**。

1. 如果您要使用 GitHub Issues 進行問題追蹤，請選取**啟用 GitHub Issues** 勾選框。
1. 如果您要透過建立確定的標籤和註解以及確定所參照之問題的標籤和註解來追蹤程式碼變更部署，請選取**追蹤程式碼變更部署**勾選框。如需相關資訊，請參閱[使用工具鏈追蹤程式碼的部署位置 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/blogs/bluemix/2017/03/track-code-deployed-toolchains/){:new_window}。
1. 按一下**建立整合**。
1. 按一下您要使用的 GitHub 儲存庫卡。即會開啟 GitHub 網站，您可以在其中檢視儲存庫的內容。

  **提示**：您可以使用 Eclipse Orion {{site.data.keyword.webide}} 中的整合原始碼管理工具來編輯 GitHub 儲存庫，以及從工作區中部署應用程式。

1. 如果您已啟用 GitHub Issues，請按一下 **GitHub Issues** 將它開啟。您可以將此 GitHub Issues 實例用於整個工具鏈，即使工具鏈包含多個 GitHub 儲存庫。    

**附註：**如果您沒有要鏈結之儲存庫的管理者專用權，則整合會受到限制，因為您無法使用 Webhook。需要有 Webhook，才能在將確定推送至儲存庫時自動觸發管線。如果沒有 Webhook，您必須手動啟動管線。

如需相關資訊，請參閱 [GitHub ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} 及 [GitHub Issues ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}。


## 在 Bluemix 專用上配置 GitHub Enterprise 及 Issues
{: #configghe}

 **附註：**這些指示適用於 {{site.data.keyword.ghe_short}} 的「{{site.data.keyword.Bluemix_notm}} 專用」。如果您使用的是專屬受管理版本的 {{site.data.keyword.ghe_short}}，則根據內部程序，有些步驟可能會有所不同。

{{site.data.keyword.ghe_long}} 是 Git 儲存庫的內部部署 Web 型管理服務。「專用 {{site.data.keyword.ghe_short}}」僅供「{{site.data.keyword.Bluemix_notm}} 專用」客戶使用。GitHub Issues 是一項追蹤工具，可將您的工作和方案都保留在一個位置。它與您的開發儲存庫整合，因此您可以專注於重要作業。如需「專用 {{site.data.keyword.ghe_short}}」及 GitHub Issues 的相關資訊，請參閱[開始使用 {{site.data.keyword.ghe_long}}](/docs/services/ghededicated/index.html){: new_window} 及 [GitHub Issues ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}。

您可以將 {{site.data.keyword.ghe_short}} 配置為工具鏈中的工具整合，以在公司的 [{{site.data.keyword.Bluemix_notm}} 專用](/docs/dedicated/index.html#dedicated){: new_window}實例中管理原始碼。

1. 如果您要在建立工具鏈時配置此工具整合，請遵循下列步驟：

 a. 第一次登入「專用 {{site.data.keyword.ghe_short}}」之前，請要求公司的地區管理者使用 LDAP 將您的使用者 ID 從公司的使用者登錄新增至「{{site.data.keyword.Bluemix_notm}} 專用」實例。如需設定 {{site.data.keyword.ghe_short}} 帳戶的相關資訊，請參閱[開始使用 {{site.data.keyword.ghe_long}}](/docs/services/ghededicated/index.html){: new_window}。

 b. 在「可配置的整合」區段中，按一下 **{{site.data.keyword.ghe_short}}**。    

 c. 檢閱新 {{site.data.keyword.ghe_short}} 儲存庫的預設名稱。必要的話，請變更新儲存庫的名稱。下列影像顯示從範例儲存庫複製的儲存庫範例。您可以使用現有儲存庫或新儲存庫。若要使用新的儲存庫，您可以建立空的儲存庫、複製儲存庫，或分出儲存庫。
 ![預設儲存庫位置](images/toolchain_ghe_config.png)

1. 如果您有工具鏈，並且要在其中新增此工具整合，請在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟其「概觀」頁面。或者，在應用程式之「概觀」頁面的「持續交付」卡上，按一下**檢視工具鏈**，然後按一下**概觀**。

 a. 按一下**新增工具**。

 b. 在「工具整合」區段中，按一下 **{{site.data.keyword.ghe_short}}**。

1. 如果您有想要使用的 {{site.data.keyword.ghe_short}} 儲存庫，請鍵入儲存庫的 URL。針對儲存庫類型，請按一下**現有**。
1. 如果您要使用新的 {{site.data.keyword.ghe_short}} 儲存庫，請鍵入儲存庫的名稱，並鍵入您所複製或分出之儲存庫的 URL，然後選取儲存庫類型：

 a. 若要建立空的儲存庫，請按一下**新建**。

 b. 若要建立儲存庫的副本，請按一下**複製**。

 c. 若要分出儲存庫，以透過取回要求來提出變更，請按一下**分出**。

1. 若要使用 GitHub Issues 進行問題追蹤，請選取**啟用 GitHub Issues** 勾選框。
1. 按一下**建立整合**。
1. 按一下您要使用的 {{site.data.keyword.ghe_short}} 儲存庫卡。即會開啟您公司的 {{site.data.keyword.ghe_short}} 儲存庫。

  **提示**：您可以使用 Eclipse Orion {{site.data.keyword.webide}} 中的整合原始碼管理工具來編輯 {{site.data.keyword.ghe_short}} 儲存庫，以及從工作區中部署應用程式。

1. 如果您已啟用 GitHub Issues，請按一下 **GitHub Issues**。您可以將此 GitHub Issues 實例用於整個工具鏈，即使工具鏈包含多個 GitHub 儲存庫。    

**附註：**如果您沒有要鏈結之儲存庫的管理者專用權，則整合會受到限制，因為您無法使用 Webhook。需要有 Webhook，才能在將確定推送至儲存庫時自動觸發管線。如果沒有 Webhook，您必須手動啟動管線。


## 配置 Jenkins
{: #jenkins}

Jenkins 是一種可持續建置及測試軟體的開放程式碼、伺服器型工具，並支援持續整合及持續交付的作法。

**重要事項**：您必須先有 Jenkins 伺服器，才能建立 Jenkins 工具整合。

使用 Jenkins 工具整合，您可以將 Jenkins 工作通知傳送至工具鏈中的其他工具（例如 Slack 及 PagerDuty）。若要在部署時追蹤程式碼，您可以將部署訊息新增至 Git 確定及相關 Git 或 JIRA 問題。您也可以在「工具鏈連線」頁面上檢視部署。您可以將測試結果提供給 {{site.data.keyword.DRA_short}}，並新增自動化品質限制，然後追蹤部署風險。

配置 Jenkins 來自動進行應用程式的持續建置、測試及部署：

1. 如果您要在建立工具鏈時配置此工具整合，請按一下「可配置的整合」區段中的 **Jenkins**。
1. 如果您有工具鏈，並且要在其中新增此工具整合，請在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟其「概觀」頁面。或者，在應用程式之「概觀」頁面的「持續交付」卡上，按一下**檢視工具鏈**。然後，按一下**概觀**。  

 a. 按一下**新增工具**。

 b. 在「工具整合」區段中，按一下 **Jenkins**。

1. 在工具鏈的 Jenkins 卡上，鍵入要針對此工具整合顯示的名稱。
1. 鍵入當您從工具鏈按一下 Jenkins 卡時所要開啟的 Jenkins 伺服器 URL。
1. 複製產生的工具鏈 Webhook。
1. 在 Jenkins 伺服器中，完成下列步驟：

 a. 安裝 [Cloud Foundry CLI ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window}。

 b. 輸入下列其中一個指令，以安裝 IBM Cloud DevOps Cloud Foundry 外掛程式：

  * Mac OS：`cf install-plugin https://icd.ng.bluemix.net/icd_darwin_amd64`

  * Linux 或 Docker：`cf install-plugin https://icd.ng.bluemix.net/icd_linux_amd64`

 c. 安裝及配置 DevOps Insights and Notifications 的 IBM Cloud DevOps Jenkins 外掛程式。如需相關資訊，請參閱[安裝及配置外掛程式](/docs/services/DevOpsInsights/insights_risk.html#integrate_jenkins){: new_window}。

 d. 在您要將通知傳送至工具鏈的每一個工作中，完成下列步驟：

  * 選取**此專案已參數化**勾選框。

  * 新增 `ICD_WEBHOOK_URL` 字串參數。

  * 貼上產生的工具鏈 Webhook。
 ![Webhook URL](images/jenkins_webhook_url.png)

  * 新增「IBM Cloud DevOps - Webhook 通知」的後建置動作，然後選取**工作已完成**勾選框。
 ![後建置動作](images/jenkins_postbuild_action.png)  

 e. 在部署工作中，完成下列步驟：

  * 新增 `ICD_WEBHOOK_URL`、`CF_API`、`CF_ORG`、`CF_SPACE` 及 `CF_APP` 字串參數。這些範例顯示如何新增每一個字串參數。
 ![Webhook URL 字串參數](images/jenkins_set_webhook_url.png)
 ![CFI API 字串參數](images/jenkins_set_cfapi.png)
 ![CFI ORG 字串參數](images/jenkins_set_cforg.png)
 ![CFI SPACE 字串參數](images/jenkins_set_cfspace.png)
 ![CFI APP 字串參數](images/jenkins_set_cfapp.png)

  * 使用 `CF_CREDS_USR` 使用者名稱變數及 `CF_CREDS_PSW` 密碼變數，來配置 Cloud Foundry CLI 的連結。
 ![Cloud Foundry CLI 連結](images/jenkins_config_bindings.png)  

  * 在**建置**欄位中，輸入這些指令來登入及使用 IBM Cloud DevOps Cloud Foundry 外掛程式，以透過 Git 確定可追蹤性將應用程式可部署對映傳送至工具鏈：![建置指令](images/jenkins_build_commands.png)    

  * 在**建置**欄位中，輸入 `cf icd --create-connection $ICD_WEBHOOK_URL $CF_APP` 指令，以將應用程式可部署對映傳送至工具鏈。    

 f. 儲存變更，並回到 Jenkins 工具整合的「配置整合」頁面。

1. 按一下**建立整合**。
1. 從工具鏈中，按一下 **Jenkins** 以檢視 Jenkins 伺服器。  

如需相關資訊，請參閱 [Jenkins ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/devops/method/content/deliver/tool_jenkins/){: new_window}。


## 配置 JIRA
{: #jira}

JIRA 是一個工具，可追蹤與您軟體相關的問題及錯誤。只要 Jenkins 或 {{site.data.keyword.deliverypipeline}} 執行部署，JIRA 工具整合就會更新專案的問題。若要讓 JIRA 工具整合追蹤問題，您必須在確定訊息中使用 JIRA Smart Commit。若要進一步瞭解 JIRA Smart Commit，請參閱[使用 Smart Commits ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://confluence.atlassian.com/fisheye/using-smart-commits-298976812.html){: new_window}。

配置 JIRA，以計劃、追蹤及遞送品質代碼：

1. 如果您要在建立工具鏈時配置此工具整合，請按一下「可配置的整合」區段中的 **JIRA**。
1. 如果您有工具鏈，並且要在其中新增此工具整合，請在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟其「概觀」頁面。或者，在應用程式之「概觀」頁面的「持續交付」卡上，按一下**檢視工具鏈**。然後，按一下**概觀**。  

 a. 按一下**新增工具**。

 b. 在「工具整合」區段中，按一下 **JIRA**。

1. 如果您有 JIRA 專案，並且要與之連接，請針對 JIRA 類型按一下**現有**：

 a. 鍵入 JIRA 專案的 JIRA 專案索引鍵。您可以在 JIRA 專案的 URL 中找到專案索引鍵。

 b. 鍵入 JIRA 實例的基礎 API URL。您可以從 JIRA 實例的標頭中找到 API URL。按一下**管理**圖示，然後按一下**系統**。

 c. 選用項目：鍵入 JIRA 使用者名稱。只有在連接至專用 JIRA 實例，或是連接至公用實例並且想要接收可追蹤性資訊時，才需要使用者名稱。

 d. 選用項目：鍵入 JIRA 密碼。只有在連接至專用 JIRA 實例，或是連接至公用實例並且想要接收可追蹤性資訊時，才需要密碼。

 e. 若要透過建立所參照問題的標籤及註解來追蹤專案的程式碼變更部署，請選取**追蹤程式碼變更部署**勾選框。請確定您使用 JIRA Smart Commit，以參照 GitHub 確定中的 JIRA 問題。如果您未選取此選項，則 JIRA 工具整合會忽略任何確定。

1. 如果您要建立 JIRA 專案，請針對 JIRA 類型按一下**新建**：

 a. 鍵入要用於新專案的 JIRA 專案索引鍵。此索引鍵用作專案 URL 中的唯一 ID。

 b. 鍵入 JIRA 專案的名稱。

 c. 鍵入 JIRA 實例的基礎 API URL。您可以從 JIRA 實例的標頭中找到 API URL。按一下**管理**圖示，然後按一下**系統**。

 d. 鍵入您要用於此專案之 JIRA 專案領導人的使用者名稱。若要將某個人指定為 JIRA 專案領導人，該人員必須具有 JIRA 中的專案領導人許可權。

 e. 鍵入此 JIRA 實例的管理者使用者名稱。

 f. 鍵入此 JIRA 實例的管理者密碼。

 g. 若要透過建立所參照問題的標籤及註解來追蹤專案的程式碼變更部署，請選取**追蹤程式碼變更部署**勾選框。請確定您使用 JIRA Smart Commit，以參照 GitHub 確定中的 JIRA 問題。如果您未選取此選項，則 JIRA 工具整合會忽略任何確定。

1. 按一下**建立整合**。
1. 從工具鏈中，按一下 **JIRA** 以檢視您已連接之 JIRA 專案的儀表板。

若要進一步瞭解，請參閱 [JIRA ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/devops/method/content/code/tool_jira/){: new_window}。


## 配置 Nexus
{: #nexus}

配置「Nexus 儲存庫管理員」，以將建置構件儲存至 Nexus 儲存庫：

1. 如果您要在建立工具鏈時配置此工具整合，請按一下「可配置的整合」區段中的 **Nexus**。
1. 如果您有工具鏈，並且要在其中新增此工具整合，請在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟其「概觀」頁面。或者，在應用程式之「概觀」頁面的「持續交付」卡上，按一下**檢視工具鏈**。然後，按一下**概觀**。  

 a. 按一下**新增工具**。

 b. 在「工具整合」區段中，按一下 **Nexus**。

1. 鍵入此 Nexus 工具整合實例的名稱。
1. 鍵入當您從工具鏈按一下 Nexus 卡時所要開啟的 Nexus 儲存庫 URL。
1. 選取您要連接的儲存庫類型。
1. 如果您已選取 **npm 登錄**，請遵循下列步驟：

 a. 鍵入與您的登錄相關聯的電子郵件位址。

 b. 鍵入與您的登錄相關聯的鑑別記號。

 c. 鍵入 Nexus 版本儲存庫的 URL，這是您在 Nexus 伺服器上的專用登錄。

 d. 鍵入您用來合併多個公用及專用 npm 登錄的「鏡映」或「公用」登錄 URL。例如，此 URL 可能是 Nexus 伺服器上可存取專用登錄及 npm 廣域登錄快取的虛擬登錄 URL。

1. 如果您已選取 **Maven 儲存庫**，請遵循下列步驟：

 a. 鍵入與您的儲存庫相關聯的使用者 ID。

 b. 鍵入與您的儲存庫相關聯的密碼。

 c. 鍵入 Nexus 版本儲存庫的 URL，這是您在 Nexus 伺服器上的專用版本儲存庫。

 d. 鍵入 Nexus Snapshot 儲存庫的 URL，這是您在 Nexus 伺服器上的專用 Snapshot 儲存庫。

 e. 鍵入您用來合併多個公用及專用 Maven 儲存庫的「鏡映」或「公用」儲存庫 URL。例如，此 URL 可能是 Nexus 伺服器上可存取專用儲存庫及 Maven 中央儲存庫快取的虛擬儲存庫 URL。

1. 按一下**建立整合**。
1. 從工具鏈中，按一下您要使用的 Nexus 儲存庫卡。即會開啟 Nexus 網站，您可以在其中檢視儲存庫的內容。
1. 選用項目：如果您是在「{{site.data.keyword.Bluemix_notm}} 公用」上使用工具鏈，並且想要透過搭配使用 Nexus 與 npm 來建置應用程式，請配置管線來新增 npm 建置工作。如需配置建置工作的指示，請參閱[在管線中配置 Nexus npm 建置工作](#config_nexus_npm)一節。
1. 選用項目：如果您是在「{{site.data.keyword.Bluemix_notm}} 公用」上使用工具鏈，並且想要透過搭配使用 Nexus 與 Maven 來建置應用程式，請配置管線來新增 Maven 建置工作。如需配置建置工作的指示，請參閱[在管線中配置 Nexus Maven 建置工作](#config_nexus_maven)一節。

### 在管線中配置 Nexus npm 建置工作
{: #config_nexus_npm}

您需要有可使用建置 SCM 儲存庫作為輸入的可運作管線，而且必須為工具鏈配置 Nexus，然後才能在管線中配置 npm 建置工作。如需配置 Nexus 的指示，請參閱 [Nexus](#nexus) 一節。

配置 {{site.data.keyword.deliverypipeline}} 來新增 npm 建置工作：

1. 建立階段，並設定適當 SCM 儲存庫的輸入。
1. 在此階段上，新增建置工作。
1. 配置建置工作：![npm 建置工作](images/nexus_npm_job.png)

  a. 針對建置器類型，選取 **NPM 建置**。

  b. 如果您已配置多個 Nexus 工具整合實例，請輸入您要配置 npm 建置工作之 Nexus 工具整合的名稱。

  c. 針對工具整合類型，選取 **Nexus**。

  d. 針對建置指令，輸入指令來建置 npm 模組或將它發佈至登錄。此範例顯示用來建置或發佈模組的指令。
     ```
     npm install
     # or
     npm publish --registry "${NPM_RELEASE_URL}"
     ```
  **提示**：您可以在 Nexus 工具整合的配置設定中，找到用來連接至登錄的 URL 及使用者認證。

  e. 如果您的建置工作發佈至 Nexus 登錄，而且節點模組版本的格式為 `x.y.z-SNAPSHOT.w`，請選取**增量 Snapshot 模組版本**勾選框。建置工作會自動更新模組版本，然後才將工作發佈至 Nexus 登錄。建置工作會從 npm 登錄及本端 `package.json` 檔案中選取最高版本的模組，並使用 semver 來增量模組版本。建置工作不會將變更遞送至 SCM 儲存庫。

1. 按一下**儲存**。只要管線執行，此建置工作就會使用 Nexus 工具整合中的配置資訊來連接至 npm 儲存庫。

### 在管線中配置 Nexus Maven 建置工作
{: #config_nexus_maven}

您需要有可使用建置 SCM 儲存庫作為輸入的可運作管線，而且必須為工具鏈配置 Nexus，然後才能在管線中配置 Maven 建置工作。如需配置 Nexus 的指示，請參閱 [Nexus](#nexus) 一節。

配置 {{site.data.keyword.deliverypipeline}} 來新增 Maven 建置工作：

1. 建立階段，並設定適當 SCM 儲存庫的輸入。
1. 在此階段上，新增建置工作。
1. 配置建置工作：![Maven 建置工作](images/nexus_maven_job.png)

  a. 針對建置器類型，選取 **Maven 建置**。

  b. 如果您已配置多個 Nexus 工具整合實例，請輸入您要配置 Maven 建置工作之 Nexus 工具整合的名稱。

  c. 針對工具整合類型，選取 **Nexus**。

  d. 針對建置指令，輸入指令來建置 Maven 模組或將它發佈至 Snapshot 登錄。此範例顯示用來建置或發佈模組的指令。
     ```
     mvn -B clean package
     # or
     mvn -DaltDeploymentRepository="snapshots::default::${MAVEN_SNAPSHOT_URL}" deploy
     ```
  **提示**：您可以在 Nexus 工具整合的配置設定中，找到用來連接至登錄的 URL 及使用者認證。

1. 按一下**儲存**。只要管線執行，此建置工作就會使用 Nexus 工具整合中的配置資訊來連接至 Maven 儲存庫。

如需相關資訊，請參閱 [Nexus ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/devops/method/content/code/tool_nexus/){: new_window}。


## 配置自訂工具（其他工具）
{: #othertool}

如果您的團隊使用未內含在工具鏈整合清單中的工具，您可以整合自訂工具。

配置自訂工具，使其可與工具鏈上的其他工具一起運作，且可供您的團隊使用：

1. 如果您要在建立工具鏈時配置此工具整合，請按一下「可配置的整合」區段中的**其他工具**。
1. 如果您有工具鏈，並且要在其中新增此工具整合，請在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟其「概觀」頁面。或者，在應用程式之「概觀」頁面的「持續交付」卡上，按一下**檢視工具鏈**，然後按一下**概觀**。

 a. 按一下**新增工具**。

 b. 在「工具整合」區段中，按一下**其他工具**。

1. 鍵入工具名稱。
1. 選取與工具最密切關聯的生命週期階段。此選項可決定您的工具會列在「概觀」頁面的哪個種類下。
1. 新增圖示 URL。此圖示將會顯示在工具整合卡上。
1. 新增文件 URL。
1. 指定工具實例名稱。例如：我的團隊工具。
1. 新增工具實例 URL。只要按一下工具整合卡，就會開啟此 URL。
1. 新增工具的說明。
1. （進階）必要的話，新增更多內容。例如，列出您的工具與工具鏈中的其他工具整合時所需的任何資訊或屬性。  
1. 按一下**建立整合**。

若要進一步瞭解，請參閱 [{{site.data.keyword.Bluemix_notm}} 工具鏈的自訂工具整合簡介 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/blogs/bluemix/2016/10/custom-tool-integration-with-bluemix-toolchains/){: new_window}。


## 配置 PagerDuty
{: #pagerduty}

PagerDuty 會將多個監視系統中的資料整合至單一視圖。發生問題時，PagerDuty 可確保當時最有能力修正問題的團隊成員能收到通知。如果團隊成員未回應問題，則可以配置呈報，將它遞送給次要工程師或作業管理員。

配置 PagerDuty 在管線階段失敗時傳送通知，讓您可以更快速地修正問題，並減少關閉時間：

1. 如果您要在建立工具鏈時配置此工具整合，請按一下「可配置的整合」區段中的 **PagerDuty**。
1. 如果您有工具鏈，並且要在其中新增此工具整合，請在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟其「概觀」頁面。或者，在應用程式之「概觀」頁面的「持續交付」卡上，按一下**檢視工具鏈**，然後按一下**概觀**。

 a. 按一下**新增工具**。

 b. 在「工具整合」區段中，按一下 **PagerDuty**。

1. 鍵入 PagerDuty 帳戶的 API 存取金鑰。如果您沒有 PagerDuty 帳戶，請[註冊一個帳戶 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://signup.pagerduty.com/accounts/new){: new_window}。如需尋找金鑰的指示，請參閱[產生 API 金鑰 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://support.pagerduty.com/hc/en-us/articles/202829310-Generating-an-API-Key){: new_window}。
1. 鍵入 PagerDuty 服務的名稱。
1. 鍵入主要 PagerDuty 聯絡人的電子郵件位址。
1. 鍵入主要 PagerDuty 聯絡人的電話號碼。
1. 按一下**建立整合**。
1. 按一下 **PagerDuty** 以移至 pagerduty.com。您可以檢視與 PagerDuty 服務相關聯的事件，而 PagerDuty 服務是您在配置工具鏈的這個工具整合時所指定。

若要進一步瞭解，請參閱 [PagerDuty ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}。


## 配置 Sauce Labs
{: #saucelabs}

Sauce Labs 會執行功能單元測試。在 {{site.data.keyword.deliverypipeline}} 中將 Sauce Labs 測試套組配置為測試工作時，測試套組可以在持續交付處理程序期間對 Web 或行動應用程式執行測試。這些測試可以為專案提供寶貴的流程控制，作為防止部署不當程式碼的閘門。

 **附註**：此工具整合僅適用於「{{site.data.keyword.Bluemix_notm}} 公用」。

配置 Sauce Labs 對多個作業系統和瀏覽器執行自動化功能測試，讓您模擬使用者可能使用網站或應用程式的方式：

1. 如果您要在建立工具鏈時配置此工具整合，請按一下「可配置的整合」區段中的 **Sauce Labs**。
1. 如果您有工具鏈，並且要在其中新增此工具整合，請在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟其「概觀」頁面。或者，在應用程式之「概觀」頁面的「持續交付」卡上，按一下**檢視工具鏈**，然後按一下**概觀**。

 a. 按一下**新增工具**。

 b. 在「工具整合」區段中，按一下 **Sauce Labs**。

1. 鍵入與 Sauce Labs 帳戶相關聯的使用者名稱。您可以[在 Sauce Labs 帳戶頁面頂端的歡迎使用訊息中找到使用者名稱 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://saucelabs.com/account){: new_window}。
1. 鍵入 Sauce Labs 帳戶的存取金鑰。您可以[在 Sauce Labs 帳戶頁面上找到金鑰 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://saucelabs.com/account){: new_window}。
1. 按一下**建立整合**。
1. 按一下 **Sauce Labs** 以移至 saucelabs.com，然後檢視工具鏈的測試活動。

 **提示**：如果您已將 Sauce Labs 測試工作新增至 {{site.data.keyword.deliverypipeline}}，則可以選取服務實例。

若要進一步瞭解，請參閱 [Sauce Labs ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}。


## 配置 Slack
{: #slack}

**重要事項**：團隊的所有人都可以看到張貼到公用 Slack 頻道的通知。請記住，您需要為您張貼的內容負責。

Slack 是一種雲端型、即時傳訊和通知系統。Slack 會提供持續性會談，這個替代方案在進行團隊協同作業時比電子郵件更具互動性。您可以透過專用頻道或與工作直接相關的一組頻道來與團隊進行通訊。您也可以透過頻道或兩位以上人員之間的直接訊息來共用檔案和影像。會保留透過直接訊息和頻道的通訊，讓您可以搜尋它們。

配置 Slack 接收來自工具整合有關工具鏈的通知（例如測試和部署活動）：

1. 如果您要在建立工具鏈時配置此工具整合，請按一下「可配置的整合」區段中的 **Slack**。
1. 如果您有工具鏈，並且要在其中新增此工具整合，請在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟其「概觀」頁面。或者，在應用程式之「概觀」頁面的「持續交付」卡上，按一下**檢視工具鏈**，然後按一下**概觀**。

 a. 按一下**新增工具**。

 b. 在「工具整合」區段中，按一下 **Slack**。

1. 鍵入 Slack Webhook URL，這是由 Slack 產生作為送入 Webhook。您需要 Slack 頻道的 Slack Webhook URL，以接收來自工具整合之工具鏈的通知。如需建立或尋找 Webhook 的指示，請參閱[送入 Webhook ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://api.slack.com/incoming-webhooks){: new_window}。

 **提示**：如果您已使用 API 金鑰，讓 Slack 頻道接收來自工具整合之工具鏈的通知，則必須更新配置以改用 Webhook。

1. 鍵入您要傳送通知的目標 Slack 頻道名稱。此頻道必須已經存在，而且在 Slack 團隊中為作用中。
1. 鍵入 Slack 團隊的 URL 主機名稱，這是團隊 URL 中 `.slack.com` 前面的單字或詞組。例如，如果團隊 URL 是 `https://team.slack.com`，則主機名稱是 `team`。
1. 按一下**建立整合**。

 **提示**：如果無法到達所指定的 Slack 頻道及團隊，則會在 Slack 卡上顯示 `Setup Failed` 錯誤。將游標移至 `Setup Failed` 訊息上方，然後按一下**重新配置**。請確定您是針對 Slack 團隊的 Slack Webhook URL、Slack 頻道及 URL 主機名稱，使用有效的配置參數。視需要更新設定，然後按一下**儲存整合**。

1. 按一下 **Slack**。您可以在已配置的 Slack 頻道中檢視工具鏈的所有活動。

若要進一步瞭解，請參閱 [Slack ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}。
