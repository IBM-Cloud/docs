---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Deployment Risk（測試版）
{: #gettingstarted}

{{site.data.keyword.DRA_short}} 針對部署（尤其是風險）提供豐富的相關資訊。您可以利用它，透過原則和閘道將 Delivery Pipeline 中的品質保護作業自動化。
{:shortdesc}

從工具鏈開啟 {{site.data.keyword.DRA_short}} 之後，按一下 **Deployment Risk**。您可以從這裡取得暫置和正式作業環境中的應用程式概觀，並往下探查，以瞭解程式碼涵蓋面、測試效能和安全報告。儀表板會自動移入管線的 {{site.data.keyword.DRA_short}} 測試中的最新資訊。

## 關於 Deployment Risk
{: #about}

Deployment Risk 可讓您透過原則和閘道，在工具鏈中強制執行品質標準。原則包含規則集；閘道可強制執行原則。例如，您可以建立「單元測試和測試涵蓋面」原則，要求建置需符合單元測試和測試涵蓋面標準。然後，將參照該原則的閘道新增至持續交付程序。不符合原則的建置會在該閘道被阻擋下來。 

Deployment Risk 會與 {{site.data.keyword.deliverypipeline}}（隸屬於 {{site.data.keyword.contdelivery_full}}）和 Jenkins 專案搭配運作。使用其中任一項的方法大致都相同。  

如果是使用 {{site.data.keyword.deliverypipeline}}，請遵循下列步驟：

1. [建立原則和規則](#policies_and_rules)，以供 {{site.data.keyword.DRA_short}} 管理。
2. [準備管線的階段](#integrate_pipeline)，以與 {{site.data.keyword.DRA_short}} 整合。

3. 在管線中[建立或編輯測試工作](#configure_pipeline_jobs)，以將結果上傳至 {{site.data.keyword.DRA_short}}。
4. [新增閘道](#configure_pipeline_gates)至管線，以根據那些結果和您的原則來制定升級決策。
5. 執行管線並[檢視結果](#view_results)。

如果是使用 Jenkins，請遵循下列步驟：

1. [建立原則和規則](#policies_and_rules)，以供 {{site.data.keyword.DRA_short}} 管理。
2. [安裝並配置 Jenkins 外掛程式](#integrate_jenkins)。
3. [依照外掛程式指示的說明來建立測試工作和閘道](#integrate_jenkins)。測試會將結果上傳至 {{site.data.keyword.DRA_short}} 以進行分析，而閘道會使用那些結果來制定升級決策。
4. 執行專案並[檢視結果](#view_results)。 

無論您如何建置及部署程式碼，結果皆相同：符合標準的建置將會通過 Deployment Risk 閘道，而不符合標準的建置就會被阻擋下來。 

## 必要條件
{: #prerequisites}

除了[開始使用 {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html) 中所說明的內容，Deployment Risk 還需要一些配置。

若要使用 Deployment Risk，您需要以下兩項：

* {{site.data.keyword.deliverypipeline}} 實例或 Jenkins 專案
* 您要用來評估專案的測試

## 建立原則和規則
{: #policies_and_rules}

原則是在交付管線中用來控制閘道的規則集。如果您的程式碼不符合或超出特定閘道制定的原則，則會中止部署，以防止釋出有風險的變更。

您可以在 {{site.data.keyword.DRA_short}} 中定義原則。原則會建立在包含 {{site.data.keyword.DRA_short}} 的 {{site.data.keyword.Bluemix_notm}} 組織 (org) 中。相同組織中的任何應用程式都可以使用此原則。 

### 建立原則
{: #create_policies}

若要建立原則，請執行下列動作：

1. 從左導覽中，按一下**設定**。

2. 按一下**原則**。

3. 按一下**建立原則**，然後鍵入新原則的名稱和說明。

4. 按**下一步**。

4. 至少將一個規則新增至原則：
  1. 按一下**新增規則至原則**。
  2. 選取規則類型。
  3. 輸入規則的詳細資料及條件。
  4. 按一下**儲存**。

5. 完成將規則新增至原則時，請按一下**完成**。

### 建立規則
{: #creating_rules}

規則可定義原則用來判斷成功或失敗的準則。您可以建立「單元測試和測試涵蓋面」原則，其中包含的單元測試規則需要 80% 單元測試成功，而測試涵蓋面規則需要 100% 程式碼涵蓋面。如果您新增的閘道在管線中參照此規則，該閘道會阻擋未同時滿足這兩項規則的任何建置繼續進行。 

如果無論如何都必須成功，您可以將測試標示為重要。若要建立規則，請選取原則，然後按一下**新增規則至原則**。 

#### 建立功能驗證測試規則
{: #criteria_fvt}

1. 鍵入說明，並選取格式。

2. 指定必須通過才能宣告成功的測試案例的百分比。

3. 定義任何重要測試案例。

4. 若要監視測試案例回歸，請選取**監視測試案例回歸**勾選框。

5. 按一下**儲存**。


#### 建立單元測試規則
{: #criteria_ut}

1. 鍵入說明，並選取格式。

2. 指定必須通過才能宣告成功的測試案例的百分比。

3. 定義任何重要測試案例。

4. 若要監視測試案例回歸，請選取**監視測試案例回歸**勾選框。

5. 按一下**儲存**。


#### 建立程式碼涵蓋面規則
{: #criteria_codecoverage}

1. 鍵入說明，並選取格式。

2. 指定需要宣告成功的程式碼涵蓋面的百分比。

3. 若要監視程式碼涵蓋面回歸，請選取**監視測試案例回歸**勾選框。

4. 按一下**儲存**。

#### 建立靜態安全掃描規則
{: #criteria_static}

您可以將 {{site.data.keyword.DRA_short}} 與 IBM Application Security on Cloud 整合，以執行 static-code 和 dynamic-app 掃描。如需 Application Security on Cloud 的相關資訊，請參閱[正式文件](/docs/services/ApplicationSecurityonCloud/index.html)。

1. 鍵入說明。

2. 指定規則可容許的高嚴重性、中嚴重性和低嚴重性問題數上限。 

3. 按一下**儲存**。

#### 建立動態安全掃描規則
{: #criteria_dynamic}

您可以將 {{site.data.keyword.DRA_short}} 與 {{site.data.keyword.appseccloudfull}} 整合，以執行 dynamic-app 掃描。如需 Application Security on Cloud 的相關資訊，請參閱[正式文件](/docs/services/ApplicationSecurityonCloud/index.html)。

1. 鍵入說明。

2. 指定規則可容許的高嚴重性、中嚴重性和低嚴重性問題數上限。 

3. 按一下**儲存**。

## 配置 {{site.data.keyword.deliverypipeline}} 
{: #configuration}

將 {{site.data.keyword.DRA_short}} 新增至工具鏈並定義它所監視的原則之後，請將它與 {{site.data.keyword.deliverypipeline}} 整合。如需管線的相關資訊，請參閱[正式文件](/docs/services/ContinuousDelivery/pipeline_working.html)。

### 準備管線階段
{: #integrate_pipeline}

若要讓 Deployment Risk 分析您的專案，您必須在管線中定義暫置和正式作業階段。您可以使用文字環境內容來定義階段（可在**環境內容**下各階段的配置功能表 ![「管線階段配置」圖示](images/pipeline-stage-configuration-icon.png) 中找到文字環境內容）。

1. 在暫置階段，將 `LOGICAL_ENV_NAME` 內容設為 `STAGING`。 

2. 在正式作業階段，將 `LOGICAL_ENV_NAME` 內容設為 `PRODUCTION`。 

您也可以將下列內容新增至建置或部署應用程式的階段：

* `LOGICAL_APP_NAME`，可定義儀表板上的應用程式名稱。
* `BUILD_PREFIX`，可定義附加在階段的建置前面的文字。此文字也會顯示在儀表板上。 

### 新增測試工作
{: #configure_pipeline_jobs}

您可以使用以下兩種測試工作，將 {{site.data.keyword.DRA_short}} 整合至您的管線中：將結果上傳至 {{site.data.keyword.DRA_short}} 以進行分析的工作，以及對該分析採取行動的閘道。 

首先，將「進階測試者」工作新增至管線，以執行測試並上傳結果。 

**附註：**如果您要更新測試工作，以將結果上傳至 {{site.data.keyword.DRA_short}}，請先將其配置儲存在方便取得的地方，再繼續進行。然後，開啟其工作配置功能表，並跳到步驟 3。 

1. 在要新增上傳結果工作的階段，按一下**階段配置**圖示 ![「管線階段配置」圖示](images/pipeline-stage-configuration-icon.png)。按一下**配置階段**。
2. 建立測試工作，並鍵入其名稱。 
3. 針對工作類型，選取**進階測試者**。
4. 完成**測試指令**和**工作目錄**欄位，與一般管線測試工作相同。 
5. 完成其餘欄位，以上傳特定測試類型的測試結果。 

 1. 選擇度量值類型，需符合您要使用的 {{site.data.keyword.DRA_short}} 原則中定義的內容。
 2. 鍵入結果檔案位置。此位置相對於工作目錄。 

6. 如果您要上傳相同工作中第二個測試類型的結果，請完成前面加上*其他* 字首的欄位。
7. 按一下**儲存**，以回到管線。

**度量值類型**及**結果檔案位置**欄位的值必須符合正確的格式：

<table><thead>
<tr>
<th>度量值類型</th>
<th>支援的格式</th>
</tr>
</thead><tbody>
<tr>
<td>功能驗證測試</td>
<td>Mocha、xUnit</td>
</tr>
<tr>
<td>單元測試</td>
<td>Mocha、xUnit、Karma/Mocha</td>
</tr>
<tr>
<td>程式碼涵蓋面</td>
<td>Istanbul、Blanket.js</td>
</tr>
</tbody></table>

圖 1 顯示一個測試工作，其配置成執行單元測試、上傳 Mocha 格式的結果，以及上傳 Istanbul 格式的程式碼涵蓋面結果。

![DevOps Insights 上傳工作](images/insights_upload_job.png)
*圖 1. 將結果上傳至 DevOps Insights*

### 定義閘道
{: #configure_pipeline_gates}

{{site.data.keyword.DRA_short}} 閘道會檢查測試結果是否符合所定義的原則。如果不符合原則，依預設，{{site.data.keyword.DRA_short}} 閘道會失敗。您也可以配置閘道來擔任諮詢角色，以允許管線即使失敗後仍可繼續進行。

在暫置部署工作之後，Deployment Risk 儀表板需要有閘道存在。如果您想要使用此儀表板，請確定在部署至暫置環境之後，且部署至正式作業環境之前，有閘道存在。

通常在管線中，閘道會放在建置升級前面。這些位置很適合用來根據原則檢查建置品質，以確保可以安心從某個環境升級至另一個環境。不過，您可以在管線中任何想要檢查特定準則的位置放置閘道。在您部署至暫置環境之前設置的閘道仍會強制執行原則，但不會出現在 Deployment Risk 儀表板上。

1. 在階段上，依序按一下**階段配置**圖示 ![「管線階段配置」圖示](images/pipeline-stage-configuration-icon.png) 及**配置階段**。
2. 按一下**新增工作**。針對工作類型，選取**測試**。
3. 針對測試者類型，選取 **{{site.data.keyword.DRA_short}} 閘道**。
4. 指定環境名稱。請確定此值符合[環境內容](#toolchain_pipeline_props)中所定義的值。
5. 輸入要在此閘道檢查的原則名稱。

 此名稱必須完全符合您定義的其中一個原則名稱。您只能指定在與工具鏈相同的 {{site.data.keyword.Bluemix_notm}} 組織中所定義的原則。

6. 選用項目：若要在諮詢模式中製作閘道功能，請清除**此工作失敗時停止執行這個階段**勾選框。在諮詢模式中，{{site.data.keyword.DRA_short}} 會在閘道上完成相同的原則分析，並產生報告，但是，失敗時不會停止管線。
7. 按一下**儲存**，以回到管線。
8. 重複這些步驟，以設定所有 {{site.data.keyword.DRA_short}} 原則的閘道。

![Deployment Risk Mocha 工作](images/insights_gate_job.png)
*圖 2. DevOps Insights 閘道*

配置管線之後，請開始使用 {{site.data.keyword.DRA_short}}。如需指示，請參閱[執行 Delivery Pipeline](/docs/services/DevOpsInsights/pipeline_decision_reports.html#toolchain_reports)。

## 配置 Jenkins 專案
{: #integrate_jenkins}

將 {{site.data.keyword.DRA_full}} 新增至開放式工具鏈並定義它所監視的原則之後，可將它與您的 Jenkins 專案整合。 

適用於 Jenkins 的 IBM Cloud DevOps 外掛程式會將 Jenkins 專案與工具鏈整合。*工具鏈* 是一組支援開發、部署及操作作業的工具整合。工具鏈的群體力量大於其個別工具整合的總和。開放式工具鏈是 {{site.data.keyword.contdelivery_full}} 服務的一部分。若要進一步瞭解 {{site.data.keyword.contdelivery_short}} 服務，請參閱[其文件](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html)。

安裝 IBM Cloud DevOps 外掛程式之後，您可以將測試結果發佈至 {{site.data.keyword.DRA_short}}、新增自動化品質閘道，以及追蹤您的部署風險。您也可以將工作通知傳送給工具鏈中的其他工具，例如 Slack 和 PagerDuty。為了協助您追蹤部署，工具鏈可以將部署訊息新增至 Git 確定及其相關 Git 或 JIRA 問題。您也可以在工具鏈的「連線」頁面上檢視您的部署。 

外掛程式提供後建置動作和 CLI 來支援整合。{{site.data.keyword.DRA_short}} 會聚集並分析單元測試、功能測試、程式碼涵蓋面工具、靜態安全程式碼掃描及動態安全程式碼掃描的結果，以在部署程序中判斷您的程式碼是否符合閘道的預先定義原則。如果您的程式碼不符合或超出原則，則會中止部署，以防止釋出有風險的變更。您可以使用 {{site.data.keyword.DRA_short}} 當作持續交付環境的安全網、實作與改善一段時間品質標準的方式，以及協助您瞭解專案性能的資料視覺化工具。

### 必要條件
{: #jenkins_prerequisites}

您必須能夠存取執行 Jenkins 專案的伺服器。

### 建立工具鏈
{: #jenkins_create}

您必須先建立工具鏈，才能將 {{site.data.keyword.DRA_short}} 與 Jenkins 專案整合。 

1. 若要建立工具鏈，請移至[「建立工具鏈」頁面](https://console.ng.bluemix.net/devops/create)，然後遵循該頁面上的指示。 

2. 建立工具鏈之後，將 {{site.data.keyword.DRA_short}} 新增至此工具鏈。如需相關指示，請參閱 [{{site.data.keyword.DRA_short}} 文件](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html)。 

### 安裝外掛程式
{: #jenkins_install}

首先，從 {{site.data.keyword.DRA_short}} 下載外掛程式。  

1. 從工具鏈的「概觀」頁面中，按一下 **DevOps Insights**。
2. 按一下**設定**，然後按一下 **Jenkins 外掛程式設定**。
3. 遵循頁面上的指示下載外掛程式。

然後，在 Jenkins 伺服器上安裝外掛程式。

1. 按一下**管理 Jenkins &gt; 管理外掛程式**，然後按一下**進階**標籤。
2. 按一下**選擇檔案**，然後選取 IBM Cloud DevOps 外掛程式安裝檔。 
3. 按一下**上傳**。
4. 重新啟動 Jenkins，並驗證已安裝外掛程式。

### 配置 Deployment Risk 儀表板的 Jenkins 工作
{: #jenkins_configure}

安裝外掛程式之後，您可以將 {{site.data.keyword.DRA_short}} 整合至 Jenkins 專案中。 

遵循下列步驟，將 Deployment Risk 的閘道和儀表板用於您的專案。

1. 開啟您擁有之任何工作（例如建置、測試或部署）的配置。

2. 針對對應類型，新增後建置動作：

   * 若為建置工作，請使用**將建置資訊發佈至 IBM Cloud DevOps**。
   
   * 若為測試工作，請使用**將測試結果發佈至 IBM Cloud DevOps**。
   
   * 若為部署工作，請使用**將部署資訊發佈至 IBM Cloud DevOps**。
   
3. 完成必要欄位。必要欄位會因工作類型而有所不同。 

   * 從**認證**清單中，選取您的 {{site.data.keyword.Bluemix_notm}} ID 和密碼。如果 ID 和密碼未儲存在 Jenkins 中，請按一下**新增**，予以新增並儲存。按一下**測試連線**，以測試您與 {{site.data.keyword.Bluemix_notm}} 的連線。
   
   * 在**建置工作名稱**欄位中，指定與 Jenkins 中完全相同的建置工作名稱。如果建置隨著測試工作發生，請讓此欄位保留為空欄位。如果建置工作是在 Jenkins 外部發生，請選取**建置在 Jenkins 外部完成**勾選框，然後指定建置號碼和建置 URL。
   
   * 針對環境，如果測試是在建置階段執行，則只選取建置環境。如果測試是在部署階段執行，則選取部署環境，並指定環境名稱。可支援的值有兩個：`STAGING` 和 `PRODUCTION`。
   
   * 針對**結果檔案位置**欄位，請指定結果檔案的位置。如果測試未產生結果檔案，請讓此欄位保留為空欄位。外掛程式會上傳以現行測試工作狀態為基礎的預設結果檔案。

   下列影像顯示配置範例：
   
   ![上傳建置資訊](images/Upload-Build-Info.png "將建置資訊發佈至 DRA")
   *發佈建置資訊*
   
   ![上傳測試結果](images/Upload-Test-Result.png "將測試結果發佈至 DRA")
   *發佈測試結果*
   
   ![上傳部署資訊](images/Upload-Deployment-Info.png "將部署資訊發佈至 DRA")
   *發佈部署資訊*

4. 如果您要使用 {{site.data.keyword.DRA_short}} 原則閘道來控制下游部署工作，請新增後建置動作 **IBM Cloud DevOps 閘道**。選擇原則，並指定測試結果的範圍。為容許原則閘道防止下游部署，請選取**根據原則規則使建置失敗**勾選框。下列影像顯示配置範例：

    ![DevOps Insights 閘道](images/DRA-Gate.png "DevOps Insights 閘道")

5. 執行您的 Jenkins 建置工作。

6. 移至 [IBM Bluemix DevOps](https://console.ng.bluemix.net/devops)、選取您的工具鏈，然後按一下 **DevOps Insights**，以檢視 Deployment Risk 儀表板。

在暫置部署工作之後，Deployment Risk 儀表板需要有閘道存在。如果您想要使用此儀表板，請確定在部署至暫置環境之後，且部署至正式作業環境之前，有閘道存在。
    
### 配置通知
{: #jenkins_notifications}

您可以遵循 [Bluemix 文件](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins)中的指示，配置 Jenkins 工作，以將通知傳送至 Slack 或 PagerDuty 之類的工具。

此範例示範如何配置工作配置的 `ICD_WEBHOOK_URL`：
![設定 ICD_WEBHOOK_URL 參數](images/Set-Parameterized-Webhook.png "設定參數化 WebHook")

此範例示範如何配置工作通知的後建置動作：
![WebHook 通知的後建置動作](images/PostBuild-WebHookNotification.png "在後建置動作中配置 WebHook 通知")

## 檢視結果
{: #view_results}

管線執行之後，{{site.data.keyword.DRA_short}} 會開始收集並分析其測試結果，以建立基準線。收集每個後續執行的資料，並將其與先前的結果進行比較。決策閘道使用此資料來判斷何時停止部署。 

您可以從 Deployment Risk 儀表板查看部署和閘道評估資料。若要開啟儀表板，請開啟 {{site.data.keyword.DRA_short}}，然後從側邊功能表中按一下 **Deployment Risk**。

如果您是使用 {{site.data.keyword.contdelivery_short}} 管線，則可從管線本身檢視個別閘道執行報告。若要從管線檢視閘道的決策報告，請完成下列步驟：

1. 在包含要檢查之閘道的階段上，按一下 **View logs and history**。

2. 從包含閘道的工作中，按一下閘道的名稱。

3. 在日誌視圖中，尋找 `Check {{site.data.keyword.DRA_short}} report here` 訊息，然後按一下鏈結來開啟報告。






