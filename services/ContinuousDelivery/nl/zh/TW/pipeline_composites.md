---

copyright:
  years: 2017
lastupdated: "2017-4-5"
---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be surrounded by 3 dashes.
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 使用複合管線（實驗性）
{: #deliverypipeline_create_composite}

使用 {{site.data.keyword.deliverypipeline}} 的複合管線特性，您可以管理相關軟體應用程式的可重複持續整合及持續交付處理程序。
{:shortdesc}

您可以建立複合管線來管理工具鏈中的應用程式。如果您的工具鏈包含 {{site.data.keyword.deliverypipeline}} 所部署的應用程式，則會在從工具鏈中新增或移除交付管線時動態更新工具鏈。您也可以將應用程式從外部來源新增至複合管線。

## 建立複合管線
{: #compositepipeline_create_for_toolchain}

1. 從 Bluemix 標誌附近的功能表，按一下**服務 > DevOps**

1. 從左導覽中，按一下**管線**。

2. 按一下**進一步瞭解**，然後按一下**啟用**，以啟用複合管線特性。會針對每一位使用者啟用複合管線，因此，只有接受實驗性特性的組織成員才會看到您建立的複合管線。

2. 按一下**建立** > **複合管線**。

3. 鍵入複合管線的名稱。您也可以修改管線說明。

4. 從**工具鏈**清單中，選取工具鏈。

    1. 若要建立空的工具鏈及複合管線，請選取**新建**。

    2. 若要建立其中一個工具鏈的複合管線，請選取其名稱。

5. 如果您建立空的工具鏈，請選取**新增預設環境**。您可以使用這些預設邏輯環境，透過複合管線來控制處理程序執行。

6. 按一下**建立**。

您所配置的階段會自動對映至組織中的適當空間，並建立複合管線的部署方案。

如果您已建立包含交付管線之工具鏈的複合管線，則會將工具鏈中所有管線的應用程式新增至複合管線。您在交付管線中所配置的階段會自動對映至組織中的適當空間，並顯示其狀態。
若要檢視應用程式中每一個工作的狀態，請展開應用程式。

也會建立複合管線的部署方案。根據預設值，空間中所有應用程式的工作會平行執行，但您可以變更方案中應用程式的部署順序。

如果您已建立新工具鏈的複合管線，則會建立一個部署方案，供您自訂。

![展開每一個應用程式，以檢視其管線中的每一個工作](images/composite_view.png "展開每一個應用程式")

## 修改部署方案
{: #compositepipeline_modify_dp}

根據預設值，會建立複合管線的部署方案。此部署方案會擷取工具鏈之任何 Delivery Pipeline 中各階段的所有資訊。您可以檢視及修改每一個階段的部署方案。

在您要修改其部署方案的階段中，按一下功能表，然後按一下**部署方案**。

![開啟部署方案](images/open_deployment_plan.png "開啟部署方案")

即會顯示環境的部署作業清單。

![包含三個個別管線之複合管線的預設部署方案](images/composite_deploy_plan.png)

如需修改部署方案的相關資訊，請參閱[自訂複合管線的部署方案](/docs/services/ContinuousDelivery/pipeline_deployment_plan.html)。

## 修改個別管線
{: #compositepipeline_add_job}

您可以修改複合管線中的個別管線。

1. 展開應用程式。

2. 從階段的功能表中，按一下**配置**。

3. 在階段中新增、修改或刪除工作。如需詳細指示，請參閱[將工作新增至階段](pipeline_build_deploy.html#deliverypipeline_add_job)。

## 執行複合管線中的工作
{: #compositepipeline_run_jobs}

在您展開應用程式以顯示其工作之後，即可在階段中手動執行其所有工作。在應用程式的空間中，按一下**部署至 *階段*** 圖示。

![在單一應用程式中執行階段](images/composite_run_stage.png)

若要執行空間之所有應用程式中的所有工作，請按一下複合管線之空間中的**部署至 *空間*** 圖示。

![在所有應用程式中執行階段](images/composite_run_space.png)

根據複合藍圖的部署方案來執行工作。

## 檢視日誌
{: #compositepipeline_view_logs}

若要檢視工作的日誌，請展開包含工作的應用程式，然後按一下工作。

## 使用 IBM Bluemix DevOps Connect 以與 IBM UrbanCode Deploy 整合
{: #compositepipeline_devops_connect}

IBM Bluemix DevOps Connect 會協調內部部署 IBM&reg; UrbanCode&reg; Deploy 安裝與 {{site.data.keyword.contdelivery_short}} 之間的通訊。在安裝 DevOps Connect 之後，您可以建立用來管理具有複合管線之 IBM UrbanCode Deploy 應用程式的整合。

**必要條件**

   * 若要登錄 DevOps Connect，您必須具有 IBM ID。

   * 確定主機系統上為 [Java&trade; Runtime Environment 第 8 版更新 121 或更新版本 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://java.com/en/download/){:new_window}，而且系統 PATH 變數設為其位置。

   * 您需要來自 IBM UrbanCode Deploy 的管理授權記號。

若要使用 DevOps Connect 以與 IBM UrbanCode Deploy 整合，請遵循下列步驟：

1. 安裝 DevOps Connect，並使用它來整合組織與 IBM UrbanCode Deploy。

  1. 在複合管線中，按一下**新增應用程式**。從**管理者**清單中，選取 **IBM UrbanCode Deploy**。

  1. 顯示整合步驟。如果您看到應用程式清單，請先依**應用程式**按一下資訊圖示 (![「資訊」圖示](/images/info.png))，然後按一下**配置此組織的 IBM UrbanCode Deploy**。

  1. 在「配置 UrbanCode Deploy 整合」視窗中，按一下**下載**來下載 DevOps Connect。請將 JAR 檔放在可存取 IBM UrbanCode Deploy 的電腦上。

  1. 從視窗中，複製 DevOps Connect 安裝 Script。Script 包含可啟動 DevOps Connect 的指令，以及識別 {{site.data.keyword.contdelivery_short}} 服務所需的認證。

  1. 在已放入 DevOps Connect 的電腦上，開啟指令 Shell，並在其中貼入所複製的 Script。

  1. 執行 Script。DevOps Connect 會顯示啟動訊息。

1. 登錄 DevOps Connect。

  1.  在已放入 DevOps Connect 的電腦上，使用 Web 瀏覽器來開啟 DevOps Connect 儀表板。預設 URL 是 `https://localhost:8443`。若要變更 URL，並瞭解其他啟動選項，請參閱 [DevOps Connect 文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/urbancode/plugindoc/urbancode-sync/ibm-urbancode-sync-utility/1-2/){:new_window}。


1. 在「登入 IBM」頁面上，輸入 IBM ID 及密碼，然後按一下**登入**。每次啟動 DevOps Connect 時，您都會登入。

1. 運用 DevOps Connect，使用 IBM UrbanCode Deploy for DevOps Connect 外掛程式來建立組織與 IBM UrbanCode Deploy 之間的整合。

    1. 在「整合」頁面上，按一下**新增**。

    1. 在**名稱**欄位中，鍵入整合的名稱。

    1. 從**整合類型**清單中，選取 **IBM UrbanCode Deploy for DevOps Connect**。

    1. 在**伺服器 URI** 欄位中，鍵入 IBM UrbanCode Deploy 伺服器的公用 URL；例如，`https://my_UCD.example.com:8443`。

    1. 在**鑑別記號**欄位中，鍵入或貼上 IBM UrbanCode Deploy 所產生的鑑別記號。

    1. 在**管理使用者電子郵件**欄位中，鍵入電子郵件位址。

    1. 若要確認整合成功，請按一下**執行整合**。DevOps Connect 會連接至**伺服器 URI** 欄位中所指定的 IBM UrbanCode Deploy 實例。DevOps Connect 是透過**鑑別記號**欄位中所貼入的記號進行授權。

    1. 按一下**儲存**。

如果您的整合成功，則可以將 IBM UrbanCode Deploy 應用程式新增至複合管線。如需相關資訊，請參閱[從 IBM UrbanCode Deploy 新增應用程式](/docs/services/ContinuousDelivery/pipeline_composites.html#compositepipeline_add_apps)。


## 從 IBM UrbanCode Deploy 新增應用程式
{: #compositepipeline_add_apps}

如果您是使用 DevOps Connect 而與 IBM UrbanCode Deploy 整合之組織的成員，則可以將可在 IBM UrbanCode Deploy 中存取的應用程式新增至複合管線。如需安裝指示，請參閱[使用 IBM Bluemix DevOps Connect 以與 IBM UrbanCode Deploy 整合](/docs/services/ContinuousDelivery/pipeline_composites.html#compositepipeline_devops_connect)。

若您是連接至 IBM UrbanCode Deploy 之組織的成員，則可以將 UrbanCode Deploy 應用程式新增至複合管線、選取要包含在部署方案中的應用程式處理程序，以及自訂應用程式的部署。

1. 從複合管線中，按一下**新增應用程式**。

2. 從**管理者**清單中，選取 **IBM UrbanCode Deploy**。如果您最近整合過 {{site.data.keyword.contdelivery_short}} 與 IBM UrbanCode Deploy，則可能需要重新整理瀏覽器，才能看到伺服器。

3. 選取要新增的應用程式，然後按一下**繼續**。即會顯示可供 IBM UrbanCode Deploy 應用程式使用的所有應用程式處理程序。要執行所選取處理程序的項目即會新增至部署方案。

4. 選取要用於應用程式的應用程式處理程序。使用搜尋及過濾選項來找出處理程序。

5. 按一下**儲存**。每一個您選取的 IBM UrbanCode Deploy 應用程式都會顯示為複合管線中的應用程式。

6. 將 IBM UrbanCode Deploy 應用程式的環境對映至複合管線的邏輯環境：

    1. 從邏輯環境名稱附近的功能表中，選取**管理邏輯環境**。

    ![選取「管理邏輯環境」](images/composite_logical_env.png)

    2. 針對複合管線中的每一個應用程式，選取您在 IBM UrbanCode Deploy 中已定義的環境。您選取的應用程式處理程序只會在該應用程式的環境中執行。

    3. 按一下**儲存**。

    4. 針對您使用的每一個邏輯環境，重複這些步驟。
