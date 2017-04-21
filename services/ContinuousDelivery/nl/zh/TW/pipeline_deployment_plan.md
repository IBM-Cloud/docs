---

copyright:
  years: 2017
lastupdated: "2017-3-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 自訂複合管線的部署方案
{: #tasks_overview}

在複合管線的部署方案中，作業代表與軟體部署相關聯的某個有意義的業務活動。作業定義於部署方案中。

{:shortdesc}

大部分作業都會有起點、結束點，以及可測量的持續時間。作業可以是下列其中一種類型：

<ul>
<li>手動作業可以代表任何與軟體部署相關聯的活動（例如，讓伺服器離線，或更新資料庫）。</li>
<li>UrbanCode Deploy 作業代表 IBM&reg; UrbanCode&reg; Deploy 應用程式。您可以搭配執行 IBM UrbanCode Deploy 應用程式與 IBM UrbanCode Deploy 類型的作業。</li>
<li>Continuous Delivery Pipeline 作業代表 {{site.data.keyword.deliverypipeline}} 實例，其為 {{site.data.keyword.contdelivery_full}} 的一部分。您可以使用此作業類型來管理 {{site.data.keyword.deliverypipeline}} 實例。</li>
<li>延遲作業代表在特定時間發生的重大事件。</li>
<li>標頭作業是組織元素。例如，您可以使用標頭作業來識別作業群組。</li>
</ul>

<!-- You can add tasks to deployment plans by creating tasks or you can import tasks from CSV files that are created by IBM UrbanCode Release or another application. You can also copy tasks from other deployment plans. See [Importing tasks](/docs/services/UCCR/UCCR_deployPlan.html#plan_importTasks) for information about the format of the CSV file. -->

## 建立作業
{: #tasks_create}

當您建立作業時，請選取您要新增該作業的部署方案。預設會在部署方案結束時插入新的作業。建立作業之後，即可進行移動，或將它複製並貼入另一個部署方案。您也可以建立與其他[作業](/docs/services/ContinuousDelivery/pipeline_deployment_plan.html#tasks_dependencies)的相依關係。

儲存作業之後，即會顯示作業的動作圖示。您可以在部署期間使用動作圖示來變更作業的狀態。所有作業都會有**跳過**動作圖示。其他圖示（例如**啟動**）在有適用的環境定義時即會顯示。

![](../UCCR/images/deploy-plan-intro.png "一般部署方案")

*圖 1. 具有作業及動作圖示的簡單部署方案*

部署方案中的每一個作業都會包含在個別的列中。下表說明針對每一個作業所顯示的資訊。

### 表格 1. 作業內容

| 內容  | 說明  |
| ------------------ | ------------------ |
| 名稱               |作業名稱       |
| 類型               |作業類型：手動、Continuous Delivery Pipeline、延遲、電子郵件、標頭/附註、UrbanCode Deploy|             
| 狀態             |作業狀態：未啟動、完成、失敗、跳過、不適用 |
| 擁有者              |獲指派作業的人員                                                        |
| 開始時間  |根據排定開始時間的開始時間或預期開始時間，或其他作業的預估持續時間        |
| 結束時間               |解決作業的時間        |
| 持續時間               |從作業開始到作業解決的時間長度（以分鐘為單位）        |
| 相依關係               |為作業必要條件且相依於作業的作業數目        |

---
將作業新增至部署方案之後，您可以透過以下數種方式來進行管理：

   * 若要移動作業，請將它拖曳至新的位置。

   * 若要複製作業或群組，請按一下作業、按一下**複製**圖示 <img class="inline" src="../UCCR/images/copy-group.png"  alt="複製圖示">、將游標放在您要插入所複製作業的位置，然後按一下**貼上**圖示 <img class="inline" src="../UCCR/images/paste-group.png"  alt="貼上圖示">。

   * 若要從部署方案中剪下作業或群組，請按一下該作業，然後按一下**剪下** <img class="inline" src="../UCCR/images/cut-group.png"  alt="剪下圖示">。

   * 若要刪除作業，請按一下它，然後按一下**刪除** <img class="inline" src="../UCCR/images/trash-group.png"  alt="刪除圖示">。即會從部署方案中移除作業。

<!-- ## Creating UrbanCode Deploy tasks
{: #tasks_UDTasks}

UrbanCode Deploy tasks manage UrbanCode Deploy applications. When you run an UrbanCode Deploy task, the associated UrbanCode Deploy application runs by using the process, version, and environment specified by the task. You can set the version and environment at design time or wait and select them at run time.

During deployments, UrbanCode Deploy tasks start automatically when they become eligible to run.   

**Important** Applications become available after {{site.data.keyword.uccr_short}} is integrated with UrbanCode Deploy. The applications that are available to a deployment plan depend on the team that is assigned to the plan. The applications that are managed by the team in UrbanCode Deploy are also available in {{site.data.keyword.uccr_short}}.

Complete the following tasks to create an UrbanCode Deploy task.

1. On the Deployment Plan Details page, click **Create Task**. If you want to insert a task at a specific position in the plan, select a task before using the **Create Task**. The new task is inserted above the selected task.

1. On the Create Task dialog box, in the **Type** list, select **UrbanCode Deploy**.

1. In the **Name** field, enter a name for the task.

3. In the **Duration (minutes)** field, enter the number of minutes that you expect the task to run until it is completed. The estimated duration is used to calculate expected deployment times.

3. In the **Tags** list, attach a tag to the task. You can select multiple tags. To create a tag, type the tag name in list's text field.

3. In the **Application Name** list, select an application.

3. In the **Process** list, select an application process. Processes that belong to the selected UrbanCode Deploy application are available.

3. In the **Environment** list, select an application environment. Environments that belong to the selected UrbanCode Deploy application are available.  To postpone selecting an environment until you are ready to run the deployment, select **Use Version Tab**.

3. In the **Version** list, select an application version. Versions refer to IBM UrbanCode Deploy application snapshots. Versions that belong to the selected application are available.  To postpone selecting a version, select **Use Version Tab**. If the application process does not require a version, select **No Version**. You might select this last option if you are running a configuration-type process that does not require components.

3. In the **Assigned groups and users** list, assign the task to a user or group. The assigned user runs the task during deployment.

3. In the **Owner** list, select the task owner. The default owner is the user who created the task. The **Owner** list is displayed after the task is assigned to a user or group.    

5. Click **Save**. The task is inserted into the deployment plan.

After the task is created, the plan's **Version** tab is updated with information about the application assigned to the task. If you selected **Use Version Tab** for the application environment and version, use the Version tab to set those options before running the deployment. -->

## 建立手動作業
{: #tasks_manual}

一般而言，手動作業代表某個活動，而此活動與具有起點、結束點及可測量持續時間的軟體版本相關聯。

若要建立手動作業，請遵循下列步驟：

1. 在「部署方案詳細資料」頁面上，按一下**建立作業**。若要在方案的特定位置插入作業，請在按一下**建立作業**之前選取作業。新的作業會插在所選取作業的上方。

1. 在「建立作業」視窗中，從**類型**清單中選取**手動**。

1. 在**名稱**欄位中，鍵入作業的名稱。

3. 在**持續時間（分鐘）**欄位中，鍵入您預期作業執行直到完成為止的分鐘數。預估持續時間是用來計算預期的部署時間。

3. 在**標籤**清單中，將標籤附加至作業。您可以選取多個標籤。若要建立標籤，請在清單的文字欄位中鍵入標籤名稱。

3. 在**已指派的群組及使用者**清單中，將作業指派給使用者或群組。指派的使用者會在部署期間執行作業。

3. 從**擁有者**清單中，選取作業擁有者。預設擁有者即建立作業的使用者。將作業指派給使用者或群組之後，會顯示**擁有者**清單。    

5. 按一下**儲存**。即會將作業插入部署方案。

## 建立延遲作業
{: #tasks_delayed}

延遲類型作業代表部署期間的里程碑或重大事件。使用延遲作業，您可以確保重要作業在預期時間開始。一般而言，延遲作業是其他重要作業的必要條件。

延遲作業會在可執行時立刻開始，並在使用者指定的時間完成。已啟動延遲類型作業的狀態為「進行中」，直到達到其計劃時間，則狀態會變更為「完成」。延遲作業完成時，與它相依的作業就會開始執行。

若要建立延遲作業，請遵循下列步驟：

1. 在「部署方案詳細資料」頁面上，按一下**建立作業**。如果您要在方案的特定位置插入作業，請在按一下**建立作業**之前選取作業。新的作業會插在所選取作業的上方。

1. 在「建立作業」視窗中，從**類型**清單中選取**延遲**。

1. 在**名稱**欄位中，鍵入作業的名稱。

3. 在**時間**欄位中，輸入或選取作業將完成的時間。

3. 在**時區**清單中，選取**時間**欄位中所輸入值的時區。    

5. 按一下**儲存**。即會將作業插入部署方案。

## 建立標頭作業
{: #tasks_header}

標頭作業代表您可新增至部署方案的組織元素。如果您建立作業群組，則可以識別具有標頭作業的群組。標頭作業可以有相依關係，就像任何其他作業一樣。

<!-- When you import a deployment plan from IBM UrbanCode Release, segment tasks are bracketed by note-type Start Segment and End Segment tasks. Segment dependencies are represented by dependencies to End Segment tasks. -->

若要建立標頭作業，請遵循下列步驟：

1. 在「部署方案詳細資料」頁面上，按一下**建立作業**。如果您要在方案的特定位置插入作業，請在按一下**建立作業**之前選取作業。新的作業會插在所選取作業的上方。

1. 在「建立作業」視窗中，從**類型**清單中，選取**標頭**。

1. 在**名稱**欄位中，鍵入作業的名稱。名稱可能代表作業群組名稱。

3. 在**說明**欄位中，鍵入或貼上說明。您可以輸入附註、備忘或其他指示。

5. 按一下**儲存**。即會將作業插入部署方案。

## 建立 Delivery Pipeline 作業
{: #tasks_pipelineCD}

在 {{site.data.keyword.contdelivery_short}} 服務中，{{site.data.keyword.deliverypipeline}} 會自動進行 DevOps 工作流程。您可以使用管線作業來管理 {{site.data.keyword.deliverypipeline}} 實例。

若要建立 Delivery Pipeline 作業，請遵循下列步驟：

1. 在「部署方案詳細資料」頁面上，按一下**建立作業**。如果您要在方案的特定位置插入作業，請在按一下**建立作業**之前選取作業。新的作業會插在所選取作業的上方。

1. 在「建立作業」視窗中，從**類型**清單中，選取 **Continuous Delivery Pipeline**。

1. 在**名稱**欄位中，鍵入作業的名稱。名稱可能代表作業群組名稱。

3. 在**說明**欄位中，鍵入或貼上說明。您可以輸入附註、備忘或其他指示。

3. 在**管線 ID** 欄位中，鍵入或貼上管線 ID。

3. 在**階段名稱**欄位中，鍵入或貼上階段名稱。

5. 按一下**儲存**。即會將作業插入部署方案。

## 管理作業群組
{: #tasks_groups}

您可以將兩個以上的作業合併至一個作業群組。當您建立群組時，會定義群組的執行型樣（即循序或平行）。您可以依任意順序執行平行型樣群組中的作業，也可以同時執行作業，除非相依關係存在。循序群組中的作業會依清單順序進行，並且從第一個或最前面的作業開始。

您可以將群組內嵌在其他群組內。您可以將循序型樣群組內嵌在平行型樣群組內，反之亦然。不過，您無法將循序型樣群組內嵌在另一個循序群組內，也無法將平行型樣群組內嵌在另一個平行群組內。  

若要建立作業群組，請遵循下列步驟：

1. 在「部署方案詳細資料」頁面上，選取兩個以上的作業。

1. 根據您要建立之群組的類型，請完成下列其中一個步驟：

  <ul>
  <li>若要建立平行群組，請按一下**平行**圖示 <img class="inline" src="../UCCR/images/para-icon.png"  alt="平行群組圖示">。如果您無法建立含有所選取作業的平行群組，則此圖示會停用。例如，如果所有選取的作業都已在平行群組中，則您可能無法建立平行群組。
  </li>
  <li>若要建立循序群組，請按一下**循序**圖示 <img class="inline" src="../UCCR/images/seq-icon.png"  alt="循序群組圖示">。
  </li>
  </ul>

即會形成群組，並將群組選取列新增至部署方案。如果您選取不連續的作業，則作業會形成從最先選取的作業開始的連續清單。

下圖顯示平行群組。群組選取列會識別群組類型：平行 <img class="inline" src="../UCCR/images/para-select.png"  alt="平行群組選取"> 或循序 <img class="inline" src="../UCCR/images/seq-select.png"  alt="循序群組選取">。

(![](../UCCR/images/group-select.png "一般部署方案"))

*圖 2. 平行群組*

若要移動群組，請按一下**群組選取列**，或按一下群組中的任何位置，並將它拖曳至新位置。

若要複製群組，請選取群組、按一下**複製**圖示 <img class="inline" src="../UCCR/images/copy-group.png"  alt="複製圖示">、將游標放在您要插入所複製群組的位置，然後按一下**貼上** <img class="inline" src="../UCCR/images/paste-group.png"  alt="貼上圖示">。

若要剪下群組，請選取群組，然後按一下**剪下**圖示 <img class="inline" src="../UCCR/images/cut-group.png"  alt="剪下圖示">。

若要將群組取消群組，請選取群組，然後按一下群組選取列上的**取消群組**圖示 <img class="inline" src="../UCCR/images/ungroup-icon.png"  alt="取消群組圖示">。

若要刪除群組中的作業，請選取群組，然後按一下**刪除**圖示 <img class="inline" src="../UCCR/images/trash-group.png"  alt="刪除圖示">。即會從部署方案中移除作業。

## 管理作業標籤
{: #tasks_tags}

標籤會組織您可新增至作業的元素。您可以依標籤過濾部署方案。例如，在部署至正式作業環境期間，您可以停用包括 `DEV_only` 標籤的作業，此標籤指出作業僅適用於開發環境。

若要將標籤新增至作業，請遵循下列步驟：

1. 在「部署方案詳細資料」頁面上，選取作業或作業群組，然後按一下**管理標籤** <img class="inline" src="../UCCR/images/task-tag.png"  alt="管理標籤">。您可以選取多個作業及群組。

1. 在「管理所選取作業的標籤」視窗中，從**共用標籤**清單中選取標籤。您可以在清單的文字框中鍵入名稱，以建立標籤。

1. 按一下**儲存**。

標籤即會顯示在「部署方案詳細資料」頁面的作業列中。在下圖中，「部署 WAR」作業有兩個標籤：`Deployment` 及 `Critical`。

部署方案所使用的標籤會顯示在「部署方案詳細資料」頁面的**版本**標籤上。若要呈現不適用於部署的作業，請清除作業的標籤。無法啟動狀態為「不適用」的作業。  

![](../UCCR/images/task-tag-labels.png "一般部署方案")

*圖 3. 作業標籤*

## 建立作業相依關係
{: #tasks_dependencies}

您可以讓作業成為其他作業的必要條件。如果作業是必要條件，則除非解決必要作業，否則相依作業即使有資格啟動還是會無法啟動。

作業可以有多個相依作業及多個必要作業。您可以定義作業與部署方案中任何其他作業的相依關係。不過，無法建立循環相依關係。例如，您無法讓作業相依於本身與第一個作業相依的作業。

透過控制作業相依關係，您可以確定事件依其預期順序發生。

若要讓作業成為其他作業的必要條件，請完成下列步驟：

1. 在「部署方案詳細資料」頁面上，選取作業或作業群組，然後按一下**管理必要條件** <img class="inline" src="../UCCR/images/task-depend.png"  alt="作業必要條件">。您可以選取多個作業及群組。

1. 在「管理所選取作業的必要條件」視窗中，從**所選取作業的必要作業**清單中選取必要作業。

1. 按一下**儲存**。

作業相依關係即會顯示在「部署方案詳細資料」頁面的「相依關係」直欄中。上移鍵指出作業必要條件，下移鍵則指出作業相依關係。

在下圖中，第一個作業沒有任何必要條件，並且有兩個相依作業。第二個作業有一個必要作業，但沒有相依作業。

(![](../UCCR/images/plan-w-depend.png "一般部署方案"))

*圖 4. 作業相依關係*

若要檢閱或修改相依關係，請選取作業，然後按一下**管理必要條件** <img class="inline" src="../UCCR/images/task-depend.png"  alt="作業必要條件">。
