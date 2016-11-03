---

copyright:
  years: 2015, 2016

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

# 延伸 {{site.data.keyword.deliverypipeline}} 服務
{: #deliverypipeline_extending}
前次更新：2016 年 8 月 29 日
{: .last-updated}

將工作配置成使用支援的服務，即可延伸 {{site.data.keyword.deliverypipeline}} 服務功能。例如，測試工作可以執行靜態程式碼掃描，建置工作則可以將字串進行全球化。
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->

下列作業說明如何使用 Delivery Pipeline 來整合選取的工具。

## 使用管線執行靜態程式碼掃描

{: #deliverypipeline_scan}

要在部署程式碼之前找出其中的安全問題嗎？如果您將 IBM® Static Analyzer for Bluemix™ 當成管線的一部分來使用，則可以針對 Java™ 應用程式的靜態 `.war`、`.ear`、`.jar` 或 `.class` 建置二進位檔來執行自動化檢查。

使用 Static Analyzer 服務的管線通常包括下列階段：

+ 建置原始檔的建置階段
+ 包括下列工作的處理階段：
  + 執行 Static Analyzer 服務的建置工作
  + 執行容器建置的建置工作
+ 部署容器的部署階段


### 建立靜態程式掃描

開始之前，請[檢閱服務的使用條款](http://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-6814-01)。

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. 建立處理階段。

  a. 按一下**新增階段**。

  b. 將階段命名（例如，`Processing`）。

  c. 針對輸入類型，選取**建置構件**。

  d. 針對階段和工作，驗證值並在必要時予以更新。

2. 在處理階段中，新增建置工作來執行程式碼掃描。

  a. 在**工作**標籤上，按一下**新增工作**。

  b. 針對工作類型，選取**測試**。

  c. 針對測試器類型，選取 **IBM Security Static Analyzer**。

  d. 針對組織及空間，驗證值並在必要時予以更新。

  e. 視需要，選取或清除**為我設定服務及空間**勾選框。

    * 如果您要管線檢查服務的 Bluemix 空間，以及將服務連結至容器的應用程式，請選取此勾選框。如果服務或所連結的應用程式不存在，則管線會將服務的免費方案新增至您的空間。建立的已連結應用程式命名為 `pipeline_bridge_app`。然後，管線會使用來自 pipeline_bridge_app 的認證，以存取連結的服務。

    * 如果您已在 Bluemix 空間中配置服務及連結的應用程式，或者要[手動配置這些需求](https://www.ng.bluemix.net/docs/containers/container_group_pipeline_ov.html#container_binding_pipeline)，請清除此勾選框。

  f. 在**等待分析完成的分鐘數**欄位中，鍵入 0 - 59 分鐘的值。預設值為 5 分鐘。在工作結束時，Static Analyzer 儀表板的 URL 是在主控台日誌中。

     如果 Static Analyzer 掃描未在指定的時間之前完成，則工作會失敗。不過，掃描分析會繼續執行，而且您可以在 Static Analyzer 儀表板上進行檢視。Static Analyzer 掃描完成之後，如果您重新執行工作，則不會重新提交掃描要求，而且可以完成管線工作。您也可以配置在掃描結果成功時不封鎖管線。如需指示，請參閱下一步。

  g. 根據此工作失敗或逾時要發生的狀況，選取或清除**此工作失敗時停止執行這個階段**勾選框。漏洞數太高時，工作會失敗。

    * 如果您選取此勾選框，而且工作失敗，則階段中的後續工作以及後續階段不會執行。

    * 如果您清除此勾選框，而且工作失敗，則階段會繼續執行，而不封鎖後續的工作及階段。例如，如果您知道報告包括許多要處理的問題，則可以配置階段繼續執行，因為掃描可能需要很長的時間。在此情況下，您可能不想要工作及階段的其餘部分只因為掃描花費太長的時間而停止。

  h. 按一下**儲存**。

3. 工作完成時，請按一下**檢視日誌及歷程**來檢視結果。如果分析成功或逾時，則會在掃描結果中顯示 URL。如果掃描狀態為擱置中，請等待掃描完成，以查看完整結果。

4. 如果您需要在分析完成之前再次執行處理階段，則可以重新執行。不過，在下列情況下，不會重新提交新的分析，並使用先前的結果：
  * 當您啟動新的分析時，處理階段仍在執行中
  * 已提交掃描來進行建置
  * 尚未執行新的來源建置

5. 若要開始新的分析，請完成下列其中一個步驟：
  * 執行輸入至處理階段的建置階段，然後重新執行處理階段。
  * 開啟掃描結果的 URL，然後按一下**垃圾**圖示。然後，重新執行處理階段。

主控台輸出範例：

**成功掃描**
![範例成功掃描](images/analyzer_success.png)

**擱置掃描**
![範例擱置掃描](images/analyzer_pending.png)

如需使用 Static Analyzer 服務的相關資訊，請參閱 [Static Analyzer 服務文件](https://console.ng.bluemix.net/docs/services/ApplicationSecurityonCloud/index.html)。

<!--

## Globalizing strings by using the pipeline
{: #deliverypipeline_globalize}

You can translate strings automatically into other languages when you use the IBM Globalization Pipeline service with your pipeline. IBM Globalization Pipeline uses machine translation to translate your source files as part of the pipeline's build and deployment process.

You can also update the machine-translated strings within the globalization project. A translator or native speaker of the language can then review the machine-translated strings to ensure that they are of a high quality.

To see an example of a typical pipeline that uses the Globalization Pipeline service, watch this video:

<iframe width="640" height="360" src="https://www.youtube.com/embed/UToj7FIomCg?feature=player_embedded" frameborder="0" allowfullscreen></iframe>

### Creating a globalization stage and job
Before you begin:

1. All English-translatable strings should be included in one or more `filename_en.properties` or `filename_en.json` files that all use the same name. For example: `messages_en.properties`.

2. If your messages are in `.json` files, remove the depth from the structure by removing any subkeys. To remove the subkeys, change instances of `{key: {subkey: value, subkey:value}}` to `{key:value, key:value}`.

To create the globalization stage and job:

1. Create a globalization stage.

  a. Click **ADD STAGE**.

  b. Name the stage; for example, `Globalization`.

  c. For the input type, select **SCM repository**.

2. In the globalization stage, add a job to translate the source files.

  a. On the **JOBS** tab, click **ADD JOB**.

  b. For the job type, select **Build**.

  c. For the builder type, select **IBM Globalization Pipeline**.

  d. For the organization and space, verify the values and update them if needed.

  e. In the **Source file name** field, type the name and extension of the `.properties` or `.json` input file. If you have files in different subdirectories, but they all have the same name, you need to type the file name once only. For example, if you have a `messages_en.properties` file in three directories, type `messages_en.properties` for the source file name, and all files with that name will be translated.

  f. Determine whether to select the **Set up service and space for me** check box.

    * If you want the pipeline to check your Bluemix space for the service and an app that binds the service to the container, select this check box. If the service or bound app does not exist, the pipeline adds the free plan of the service to your space for you. The bound app that is created is named `pipeline_bridge_app`. Then, the pipeline uses the credentials from pipeline_bridge_app to access the bound services.

    * If you configured the service and bound app in your Bluemix space already or if you want to [configure these requirements manually](https://www.ng.bluemix.net/docs/containers/container_group_pipeline_ov.html#container_binding_pipeline), leave this check box cleared.

  g. For the Globalization bundle prefix, enter a prefix for the bundle name, which is structured in this format: `<globalization_bundle_prefix>.path.to.source.file`. The pipeline job creates this Globalization bundle for you in the Globalization Pipeline service.

    **Tip:** Use the DevOps Services project name in the prefix so that the project can be identified easily in the Globalization Pipeline service.

  h. Click **SAVE**.

3. Create another stage to package your app. For the input of the job in this stage, use the IBM Globalization Pipeline job from the previous stage. Do not use the source as the input. The Globalization Pipeline job augments the source files with the machine-translated strings.

4. To ensure that the machine-translated content is included in the packaged app, create another stage to package the app in. For the input to that stage, include the Globalization Pipeline job.

The machine translated files are placed in the same directory as the source `.properties` or `.json` file. To view the files, click **Job > Artifacts**.

After the stage is completed, you can review the translated files from the console output. You can also direct translators to the files so that they can review the machine-translation output and provide revisions to improve quality. The revisions are stored in a Cloudant™ database and take precedence over any future machine translations of the same strings.

For more information about using the Globalization Pipeline service from the Bluemix Dashboard, [see the Globalization Pipeline service documentation](https://www.ng.bluemix.net/docs/services/GlobalizationPipeline/index.html).

-->

## 在管線中建立建置的 Slack 通知
{: #deliverypipeline_slack}

您可以將 IBM Container Service、IBM Security Static Analyzer 及 IBM Globalization 建置結果的相關通知，從 Delivery Pipeline 傳送至 Slack 通道。

開始之前，請建立或複製 Slack WebHook URL：

1. 開啟您團隊的「Slack 整合」頁面：`https://_project_name_.slack.com/services`
2. 在整合清單中，尋找**送入的 WebHook**，然後按一下**新增**。
3. 選取通道，然後按一下**新增送入的 WebHook 整合**。
4. 新增 **WebHook URL**，或複製現有項目。

如需相關資訊，請參閱 [Slack 文件中的送入 WebHook](https://api.slack.com/incoming-webhooks)。

若要建立 Slack 通知，請執行下列動作：

1. 在管線中，開啟階段的配置。
2. 在**環境內容**標籤中，按一下**新增內容**。
3. 選取**文字內容**。
4. 輸入環境內容的名稱及值。重複以建立多個環境內容。

  *表格 1. 用於配置 Slack 通知的環境內容*

  <table>
  <tr>
  <th>名稱</th>
  <th>值</th>
  <th>說明</th>
  <tr/>
  <tr>
    <td><code>SLACK_WEBHOOK_PATH</code></td>
    <td>URL</td>
    <td>必要。設定中針對「Slack 專案」所儲存的 WebHook URL。</td>
  </tr>
  <tr>
    <td><code>SLACK_COLOR</code></td>
    <td>您可以輸入下列其中一個值：
      <ul><li><code>good</code></li>
      <li><code>warning</code></li>
      <li><code>danger</code></li>
      <li>任何十六進位顏色（例如 #439FEO）</li></ul></td>
    <td>選用。沿著 Slack 中訊息端所顯示的邊框顏色。預設顏色如下：綠色代表良好訊息、紅色代表錯誤訊息，而灰色代表參考訊息。</td>
  </tr>
  <tr>
    <td><code>NOTIFY_FILTER</code></td>
    <td>若只要接收一部分的訊息類型，請輸入下列其中一個值：
      <ul>
      <li><code>good</code>：只取得不明、良好及參考訊息。不會傳送錯誤訊息。</li>
      <li><code>bad</code>：取得所有訊息。</li>
      <li><code>info</code>：只取得參考訊息。不會傳送良好、錯誤及不明訊息。</li>
      <li><code>unknown</code>：取得所有訊息。</li></ul>
      範例：如果您設定 <code>NOTIFY_FILTER = bad</code>，則只會在「Slack 通道」中顯示錯誤通知。</td>
    <td>選用。決定哪些類型的訊息要傳送通知。依預設，會傳送良好及錯誤訊息，但不會傳送參考訊息。
      <ul><li><code>good</code>：成功建置結果。</li>
      <li><code>bad</code>：失敗建置結果。</li>
      <li><code>info</code>：建置程序的參考訊息。</li>
      <li><code>unknown</code>：不會將類型指派給不明訊息。</li></ul></td>
   </table>

5. 按一下**儲存**。

6. 重複這些步驟，以針對包括 IBM Container Service、IBM Security Analyzer 及 IBM Globalization 工作的其他階段傳送 Slack 通知。

Slack 中所顯示的建置通知包括 DevOps Services 專案的鏈結，有時會包括專案儀表板的鏈結。為了讓 Slack 使用者開啟這些鏈結，必須在 DevOps Services 中註冊使用者，而且使用者必須是在其中配置管線之專案的成員。

## 在管線中建立建置的 HipChat 通知
{: #deliverypipeline_hipchat}

您可以將 IBM Container Service、IBM Security Static Analyzer 及 IBM Globalization 建置結果的相關通知，從 Delivery Pipeline 傳送至 HipChat 會議室。

開始之前，請建立或複製現有 HipChat 記號：

1. 移至您團隊的「HipChat 帳戶」頁面：`https://_project_name_.hipchat.com/account/api`
2. 建立新的記號，或使用現有記號。

若要建立 HipChat 通知，請執行下列動作：

1. 在管線中，開啟階段的配置。
2. 在**環境內容**標籤中，按一下**新增內容**。
3. 選取**文字內容**。
4. 輸入環境內容的名稱及值。重複以建立多個環境內容。

  *表格 2. 用於配置 HipChat 通知的環境內容*

  <table>
  <tr>
  <th>名稱</th>
  <th>值</th>
  <th>說明</th>
  </tr>
  <tr>
    <td><code>HIP_CHAT_TOKEN</code></td>
    <td>英數字串</td>
    <td>必要。如需建立或複製現有 HipChat 記號的指示，請參閱「開始之前」。</td>
  </tr>
  <tr>
    <td><code>HIP_CHAT_ROOM_NAME</code></td>
    <td>會議室名稱</td>
    <td>必要。</td>
  </tr>
  <tr>
    <td><code>HIP_CHAT_COLOR</code></td>
    <td>輸入下列其中一個值：
      <ul><li><code>yellow</code></li>
      <li><code>red</code></li>
      <li><code>green</code></li>
      <li><code>purple</code></li>
      <li><code>gray</code></li>
      <li><code>random</code></li></ul>
    </td>
    <td>選用項目：指定 HipChat 通知的背景顏色及邊框顏色。如果您設定 <code>HIP_CHAT_COLOR</code>，則不需要在呼叫 Script 時指定顏色。
     <p><code>-l notification_level</code></p> </td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_COLOR</code></td>
    <td>輸入下列其中一個值：
      <ul><li><code>good</code></li>
      <li><code>danger</code></li>
      <li><code>info</code></li></ul>
    此變數適用於 HipChat 和 Slack 通知顏色。如果您指定 <code>NOTIFICATION_COLOR</code>，則不需要指定 <code>HIP_CHAT_COLOR</code> 或 <code>SLACK_COLOR</code>。</td>
    <td>選用項目：指定 HipChat 和 Slack 通知的背景顏色及邊框顏色。如果您設定 <code>NOTIFICATION_COLOR</code>，則不需要在呼叫 Script 時指定顏色。
     <p><code>-l notification_level</code></p> </td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_LEVEL</code></td>
    <td>輸入下列其中一個值：
      <ul><li><code>good</code></li>
      <li><code>info</code></li>
      <li><code>bad</code></li></ul></td>
    <td>選用項目：指定通知層次。如需哪些項目觸發通知的詳細資料，請參閱 <code>NOTIFICATION_FILTER</code>。</td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_FILTER</code></td>
    <td>輸入下列其中一個值：
      <ul><li><code>good</code></li>
      <li><code>info</code></li>
      <li><code>bad</code></li></ul>
    <td>選用項目：指定通知過濾層次。符合下列參數時，會傳送通知：
      <ul><li><code>NOTIFICATION_FILTER = good</code> 及 <code>NOTIFICATION_LEVEL = bad</code>、<code>good</code> 或 <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = info</code> 及 <code>NOTIFICATION_LEVEL = bad</code>、<code>good</code>、<code>info</code> 或 <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = bad</code> 及 <code>NOTIFICATION_LEVEL = bad</code> 或 <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = unknown</code> 及 <code>NOTIFICATION_LEVEL = bad</code>、<code>good</code> 或 <code>unknown</code></li></ul></td>
    </tr>
  </table>

5. 按一下**儲存**。

6. 重複這些步驟，以針對包括 IBM Container Service、IBM Security Static Analyzer 及 IBM Globalization 工作的其他階段傳送 HipChat 通知。

## 在管線中使用 Active Deploy 進行零關閉時間部署
{: #deliverypipeline_activedeploy}

在 Bluemix® DevOps Services Delivery Pipeline 中使用 IBM® Active Deploy 服務，即可自動化持續部署應用程式或容器群組。如需開始使用的相關資訊，請參閱 [Active Deploy 文件](https://new-console.ng.bluemix.net/docs/services/ActiveDeploy/updatingapps.html#adpipeline)。

## 使用管線建置及部署容器映像檔
{: #deliverypipeline_containers}

使用 IBM® Continuous Delivery Pipeline for Bluemix，即可自動化 Bluemix® 的應用程式建置及容器部署。DevOps Services 中的 Delivery Pipeline 服務支援：
  - 建置 Docker 映像檔
  - 將容器中的映像檔部署至 Bluemix

如需開始使用的相關資訊，請參閱 [Delivery Pipeline 及容器概觀](https://new-console.ng.bluemix.net/docs/containers/container_pipeline_ov.html#container_pipeline_ov)。
