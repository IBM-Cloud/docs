---



copyright:

  years: 2015, 2016



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# 管理 {{site.data.keyword.Bluemix_notm}} 本端及 {{site.data.keyword.Bluemix_notm}} 專用
{: #mng}
*前次更新：2016 年 5 月 16 日*

如果您具有「{{site.data.keyword.Bluemix_notm}} 本端」或「{{site.data.keyword.Bluemix_notm}} 專用」的管理者存取權，請移至**管理**頁面來管理資源、監視配額用量、管理使用者許可權、排定升級通知，以及檢視安全報告和日誌等。您可以透過建立空間並設定[使用者角色和許可權](index.html#oc_useradmin)來管理組織；請參閱[管理組織](../admin/orgs_spaces.html)。
{:shortdesc}

*表 1. 用於管理 {{site.data.keyword.Bluemix_notm}} 本端或專用實例的管理作業*

| 我能執行哪些操作？ | 詳細資料 |    
|----------------|---------|
|監視系統使用情形 | 按一下**管理 &gt; 使用情形**。檢視系統資訊、監視 CPU 使用率，以及計劃使用情形，以便做出最佳業務決策。請參閱[檢視使用資訊](index.html#oc_resource)。|
|管理型錄 | 按一下**管理 &gt; 型錄管理**，以管理您的使用者及組織可以看見哪些服務。請參閱[管理型錄](index.html#oc_catalog)。|
|管理組織 | 按一下**管理 &gt; 組織管理**，以建立組織、監視組織配額，以及快速做出基於需求的決策。請參閱[管理組織](index.html#oc_organizations)。|
|建立空間和指派使用者角色 | 按一下**帳戶和支援**圖示 ![帳戶和支援](../support/images/account_support.svg)，然後選取**管理組織**，以在組織內建立空間。新增使用者並將組織和空間角色指派給使用者。請參閱[管理組織](../admin/orgs_spaces.html)。 |
|對管理使用者許可權進行管理 | 按一下**管理 &gt; 使用者管理**，以新增使用者、移除使用者以及調整使用者許可權。請參閱[管理使用者及許可權](index.html#oc_useradmin)。 |
|檢視報告和日誌 | 按一下**管理 &gt; 報告和日誌**，以檢視您實例的安全報告及審核日誌。請參閱[檢視報告](index.html#oc_report)。 |
|檢視系統資訊 | 按一下**管理 &gt; 系統資訊**，以檢視系統資訊，例如擱置更新、實例的名稱和版本、地區、API URL、CLI URL、LDAP 配置詳細資料、群組和使用者對映、統計資料以及共用網域。您也可以在「擱置更新」區段中存取行事曆資訊來源及事件訂閱，以擴充通知。請參閱[檢視系統資訊](index.html#oc_system)。 |
|擴充通知以及設定事件訂閱 | 按一下**管理 &gt; 系統資訊 &gt; *Number* 個擱置的更新**。您可以使用 Webhook 與您選擇的 Web 服務整合，以設定更新或發生事件的事件通知訂閱。請參閱[通知及事件訂閱](index.html#oc_eventsubscription)。 |


## 通知及事件訂閱
{: #oc_eventsubscription}

透過檢查「狀態」頁面，您隨時都可以知道環境的狀態。{{site.data.keyword.Bluemix_notm}} 也會將通知傳送至事件（例如排程維護及升級）的「管理」頁面的「通知」區域。發生事件則報告在「狀態」頁面上。

### 通知

您可以檢視來自 IBM 有關您本端或專用環境的通知，以監視您環境的狀態。如需不同類型通知以及通知張貼位置的相關資訊，請檢閱下表。

*表 2. 事件類型及通知方法*

| **事件類型** | **通知方法** |       
|-----------------|-------------------|
| 維護更新 | 您可以在「管理」頁面的「通知」中收到有關即將到來的維護更新的警示。移至**管理**頁面，然後選取**通知**圖示 ![通知](images/icon_announcement.svg)。若要查看擱置及完成通知的完整清單及歷程，請按一下**管理 &gt; 系統資訊** &gt; *Number* **個更新擱置**。擴充通知功能的方式是設定事件訂閱，以整合「管理」頁面中的維護更新警示與所選擇的 Web 服務，將訊息遞送至服務台電子郵件位址，或將 SMS 訊息遞送至所選擇的電話號碼。 |
| 重要發生事件 | 您可以在「狀態」頁面上收到有關重要發生事件的警示。按一下**帳戶和支援**圖示 ![帳戶和支援](../support/images/account_support.svg)，然後選取**狀態**。擴充通知功能的方式是設定事件訂閱，以整合「狀態」頁面中的發生事件警示與所選擇的 Web 服務，將訊息遞送至服務台電子郵件位址，或將 SMS 訊息遞送至所選擇的電話號碼。 |  
| 狀態 | 您可以檢視平台、服務及 {{site.data.keyword.Bluemix_notm}} 實例的最新狀態。按一下**帳戶和支援**圖示 ![帳戶和支援](../support/images/account_support.svg)，然後選取**狀態**。  |

### 設定事件訂閱

您可以使用實作 Webhook 的事件訂閱，來擴充傳送至「管理」頁面及「狀態」頁面的通知功能。Webhook 會將您的通知直接遞送至您選擇的目的地，例如，服務台電子郵件位址（透過電子郵件）或電話號碼（透過 SMS 訊息）。您可以自訂通知類型（具體而言是維護更新或重要發生事件警示），以及通知中內含的資訊。

若要使用 Webhook 設定特定事件訂閱，請完成下列步驟：

* 對於維護更新通知，移至**系統資訊** &gt; *Number* **個攔置的更新**，然後按一下**訂閱**圖示 ![訂閱](images/icon_subscribe.svg)。
* 對於發生事件警示通知，按一下**帳戶和支援**圖示 ![帳戶和支援](../support/images/account_support.svg) &gt; **狀態**，然後按一下**訂閱**圖示 ![訂閱](images/icon_subscribe.svg)。

**附註**：您可以使用所述的兩種方法的之一，來存取這兩種類型通知的事件訂閱頁面。

1. 按一下**新增訂閱**。

2. 填寫事件訂閱表單。如需表單上的各欄位以及有效負載區段使用值的相關資訊，請檢閱下列各表：

*表 3. 事件訂閱表單欄位*

| **欄位** | **說明** |
|-----------------|-------------------|
| 類型 | 選取  Webhook。 |
| 方法 | 選取 GET 或 POST。 |
| 事件 | 選取要訂閱更新或發生事件的通知。 |
| URL | 輸入要連結至您 Web 服務的 URL。 |
| 說明 | 新增您要建立的事件訂閱的說明。 |
| 使用者名稱 | 輸入您 Web 服務的使用者名稱。如果您不想使用個人認證，則可以設定有效的 ID，以專門與 {{site.data.keyword.Bluemix_notm}} 搭配使用。 |
| 密碼 | 輸入您 Web 服務的密碼。 |
| 有效負載 | 如果您已選取 POST 方法，請輸入 Web 服務特有的內容，以和 IBM 通知所用的值搭配使用。如需可用來移入您通知中的 IBM 值，請參閱下表。如果您未在此區段中輸入資訊，則會收到沒有任何其他資訊的通知。 |

*表 4. 有效負載區段值*

| **IBM 值** | **說明** | **事件類型** |
|----------------|----------------|------------------------|
| {{content.title}} | 訊息標題 |  更新和發生事件  |
| {{status}} | 更新或發生事件的狀態。 | 更新和發生事件 |
| {{type}} | 更新或發生事件 | 更新和發生事件 | 
| {{region}} | 受影響的區域 | 更新和發生事件 |
| {{content.message}} | 訊息說明 |   更新和發生事件  |
| {{content.severity}} | 嚴重性評分 | 發生事件 |
| {{content.category}} | 受影響的服務 | 發生事件 |
| {{content.subCategoryName}} | 受影響的元件 | 發生事件 |
| {{content.scheduleWindow}} | 更新的排定日期 | 更新 |
| {{content.disruption}} | 受影響的元件 | 更新 |

儲存您的事件訂閱時，會透過 Web 服務所設定的方法來接收通知。發生事件的通知仍然會張貼在「狀態」頁面上，維護更新的通知則會張貼在「管理」頁面的「通知」區域中。

您可以選取任何儲存的事件訂閱，以及檢視最近的活動。您可以按一下來展開任何最近的活動項目，以檢視其詳細資料。詳細資料中包括可在有效負載區段中使用的通知的 IBM 值。若要查看這些值，請展開最近的活動項目，展開**事件**，然後展開**物件**。

## 維護更新
{: #oc_schedulemaintenance}

您可以檢視排定及擱置維護更新，方法是移至**管理 &gt; 系統資訊 &gt; *Number* 個更新擱置**來存取**系統更新**頁面。 

**附註**：請參閱下節，以設定預先核准的維護時間範圍來開始進行。必須設定這些時間範圍，IBM 才能排定您環境的維護。

<dl>
<dt>非干擾性更新</dt>
<dd>非干擾性更新不會影響您的環境、執行中應用程式，或使用者對您應用程式的存取。此更新類型不需要逐案核准，將會在從「系統更新」頁面所設定的預先核准可用維護時間範圍套用。</dd>
<dt>干擾性更新</dt>
<dd>干擾性更新可能會影響您的環境、執行中應用程式，或使用者對您應用程式的存取。您必須在分配的 21 天維護時間範圍內排定及核准所有這些維護更新。您可以選取根據預先核准更新時間範圍的建議部署日期和時間，也可以選取兩個其他時間和日期，讓 IBM 在排定更新時進行選擇。</dd>
</dl>


### 設定預先核准的維護時間範圍
{: #preapprovedmaintenance}

開始排定及核准更新之前，必須設定預先核准的維護時間範圍。非干擾性更新會排定在預先核准的時間進行。非干擾性更新不會影響您的環境、執行中應用程式，或使用者對您應用程式的存取。此更新類型不需要逐案核准，將會在從「系統更新」頁面所設定的預先核准可用維護時間範圍套用。

您需要設定一週最少有 24 個可用小時且最少為該週的 3 天。例如，您可以設定三天各 8 小時時間範圍，也可以設定四天各 6 小時時間範圍。若要確保時間範圍提供足夠的時間來套用更新，則每一個時間範圍的持續時間必須最少為 4 小時。

1. 移至**管理 &gt; 系統資訊 &gt; *Number* 個更新擱置 &gt; 管理可用性**。
2. 展開**管理可進行更新的時間範圍**區段。
3. 按一下**新增** ![新增](images/add-new.png)。
4. 設定第一個可用的時間範圍，方法是選取時間範圍的頻率、持續時間及開始時間。
5. 按一下**提交**。
6. 重複此處理程序，直到您已符合每週時間範圍的最低需求。

### 設定無法使用的維護時間範圍

設定預先核准的可用維護時間範圍之後，即可選擇設定您的環境無法進行更新的特定日期和時間。例如，如果您不想要套用任何維護以確保使用者可以使用您的應用程式，則可以選擇高資料流量的週末或假日。

1. 移至**管理 &gt; 系統資訊 &gt; *Number* 個更新擱置 &gt; 管理可用性**。
2. 管理**管理無法進行更新的時間範圍**區段。
3. 按一下**新增** ![新增](images/add-new.png)。
4. 設定無法使用的時間範圍，方法是選取時間範圍的頻率、持續時間及開始時間。
5. 按一下**提交**。

### 排定及核准更新
{: #scheduleandapprove}

設定預先核准的維護時間範圍之後，將會在那些時間自動排定非干擾性更新。您不需要明確核准這些類型的更新。不過，您可以檢視每一個維護更新的詳細資料，包括所更新的內容、更新所需時間，以及排定更新的時間。 

若要檢視非干擾性更新的詳細資料，請完成下列步驟：

1. 移至**管理 &gt; 系統資訊 &gt; *Number* 個更新擱置**。
2. 識別將**需要客戶排程**設為**否**的任何更新列。
3. 選取該更新的列，以檢視詳細資料。

干擾性更新可能會影響您的環境、執行中應用程式，或使用者對您應用程式的存取。您必須在分配的 21 天維護時間範圍內排定及核准所有這些維護更新。您可以選取根據預先核准更新時間範圍的建議部署日期和時間，也可以選取兩個其他時間和日期，讓 IBM 在排定更新時進行選擇。

對於不需要您核准的干擾性更新，請完成下列步驟：

1. 移至**管理 &gt; 系統資訊 &gt; *Number* 個更新擱置**。
2. 識別將**需要客戶排程**設為**是**的任何更新列。
3. 選取該更新的列，以檢閱更新的詳細資料，包括更新說明、建議進行更新的日期和時間、受影響的元件，以及更新的持續時間。
4. 選取**排定及核准**。
5. 從下列選項中進行選擇：**建議日期**、**替代日期**或**所有預先核准的時間範圍**。
6. 選取**提交**。 

根據您的選擇，會在您接受的建議日期期間、其中一個預先核准的時間範圍期間或其中一個替代日期和時間套用更新。IBM 完成您更新的排程日期後，排定日期就會反映在**系統更新**頁面的更新詳細資料中。

### 設定排定更新的行事曆資訊來源

從「系統更新」頁面中，按一下**行事曆**圖示 ![行事曆](images/icon_calendar.svg)，然後下載 `.ics` 檔案，以將排定的更新匯入您選擇的行事曆應用程式中，即可選擇追蹤更新排程：

<ol>
<li>開啟行事曆應用程式。</li>
<li>按一下**行事曆**圖示 ![行事曆](images/icon_calendar.svg) 來下載行事曆檔案，然後使用 `.ics` 檔案將它匯入行事曆應用程式。</li>
<li>輸入認證。</li>
<li>檢視您的已排定更新。</li>
</ol>

您也可以使用事件訂閱來擴充「管理」頁面的通知功能，以與所選擇的 Web 服務整合。若要設定更新或發生事件的事件通知訂閱，請參閱[事件訂閱及通知](index.html#oc_eventsubscription)。

## 檢視系統資訊
{: #oc_system}

若要檢視系統資訊，請按一下**管理 &gt; 系統資訊**。

您可以展開並檢視有關擱置維護更新、一般系統資訊及 LDAP 配置詳細資料的各個區段。

### 擱置系統更新

在「更新」區段中，您可以查看需要您採取動作的擱置更新通知數目。您可能會看到兩種類型的維護更新：

<dl>
<dt>非干擾性更新</dt>
<dd>非干擾性更新不會影響您的環境、執行中應用程式，或使用者對您應用程式的存取。此更新類型不需要逐案核准。這些更新會在從「系統更新」頁面所設定的預先核准可用維護時間範圍套用。</dd>
<dt>干擾性更新</dt>
<dd>干擾性更新可能會影響您的環境、執行中應用程式，或使用者對您應用程式的存取。您可以在分配的 21 天維護時間範圍內排定及核准所有這些維護更新，確保不會在重要營業時間套用更新。您可以選取根據預先核准更新時間範圍的建議部署日期和時間，也可以選取兩個其他時間和日期，讓 IBM 在套用更新時進行選擇。</dd>
</dl>

如需設定預先核准的維護時間範圍、設定無法進行維護的特定日期以及設定行事曆資訊來源的相關資訊，請參閱[維護更新](index.html#oc_schedulemaintenance)。

### 一般系統資訊

在「一般資訊」區段中，您可以檢視下列資訊：

- 關於 {{site.data.keyword.Bluemix_notm}} 建置的基本資訊。
- API 資訊，包括版本、URL、地區，以及 CLI 文件的鏈結。
- 關於系統及服務的共用網域資訊。
- 關於應用程式、使用者及組織總數的統計資料。

### LDAP 配置詳細資料

在「LDAP 配置詳細資料」區段中，您可以選取 LDAP 伺服器，然後檢視使用者和群組對映的相關資訊。如果您是使用 {{site.data.keyword.IBM}} WebID，它會顯示在本區段中。

## 檢視使用情形和報告
{: #oc_resource}

您可以針對本端或專用實例和 {{site.data.keyword.Bluemix_notm}} 帳戶，檢視不同類型的使用資訊。您也可以下載及檢視 {{site.data.keyword.Bluemix_notm}} 實例的安全報告和日誌。

- 資源資訊，包括磁碟空間、CPU 使用率、網路用量及平均回應時間。請參閱[資源用量](index.html#resourceusage)。
- 每個組織的帳戶使用情形，包括含使用情形的執行時期應用程式數目、執行時期 GB-小時總數，以及含使用情形的服務實例數目。請參閱[帳戶使用情形](index.html#accountusage)。
- 組織記憶體配額用量、根據已用記憶體配額總計配置的應用程式記憶體，以及特定組織的每個應用程式的 GB-小時使用情形視圖。您也可以在「組織管理」頁面的「配額監視」區段中，檢視所有組織的配額用量。請參閱[組織管理](../admin/index.html#orgusage)。


### 資源用量
{: #resourceusage}

若要檢視資源使用資訊，請按一下**管理 &gt; 使用情形**。

在「資源監視」區段中，您可以檢視下列資訊：

- 資源使用資訊，例如已使用多少 GB 的記憶體及多少 GB 的磁碟空間。您可以檢視跨所有 Droplet Execution Agent (DEA) 的平均 CPU 使用率。按一下 **CPU** 磚，您可以查看每一個 DEA 的 CPU 使用率。第一個列出的是具有最高使用率的 DEA，而且每一個 DEA 都依其工作及 IP 位址來識別。CPU 使用率分為三個種類，包括系統處理程序中所花費的 CPU 量、使用者處理程序中所花費的 CPU 量，以及等待處理程序中所花費的 CPU 量。
- 過去一天、一週或一個月之進出頻寬的網路使用資訊。顯示的資料是根據公開及私密網路的輸入及輸出資料流量的總和。
- {{site.data.keyword.Bluemix_notm}} 在過去十分鐘、一小時及一天的平均回應時間。
- {{site.data.keyword.Bluemix_notm}} 在過去十分鐘、一小時及一天的每秒平均交易數。

### 帳戶使用情形
{: #accountusage}

您可以檢視專用或本端環境的帳戶的每月使用情形。您可以使用這項資料，來識別根據其用量對特定組織收取的費用。

<ol>
<li>按一下<strong>帳戶和支援</strong>圖示 ![帳戶和支援](../support/images/account_support.svg) &gt; <strong>帳戶</strong> &gt; <strong>使用情形詳細資料</strong>。</li>
<li>選取您要查看資料的組織。</li>
<li>您可以查看下列種類的使用情形詳細資料：
<ul>
<li>含使用情形的執行時期應用程式</li>
<li>執行時期應用程式使用情形總計（以 GB-小時為單位）</li>
<li>含使用情形的服務實例</li>
</ul>
</li>
<li>選用項目：使用<strong>您的雲端活動</strong>功能表選取您選擇的月份，以檢視特定月份的資料。</li>
<li>選用項目：按一下<strong>匯出資料</strong>，然後選取 <strong>CSV</strong> 或 <strong>JSON</strong>，以將您的選取月份資料匯出至 <code>CSV</code> 或 <code>JSON</code> 檔案。</li>
</ol>

您也可以針對從「{{site.data.keyword.Bluemix_notm}} 公用」聯合的執行時期、應用程式及服務，檢視帳戶層次的每月使用情形及關聯的費用。您可以使用這項資料，來識別根據其用量對特定組織收取的費用。

<ol>
<li>按一下<strong>帳戶和支援</strong>圖示 ![帳戶和支援](../support/images/account_support.svg) &gt; <strong>帳戶</strong> &gt; <strong>使用情形詳細資料</strong>。</li>
<li>按一下<strong>公用</strong>。</li>
<li>選取您要查看資料的組織，或選取<strong>所有組織</strong>，一次檢視所有組織的資料。</li>
<li>您可以查看下列種類的使用情形詳細資料：
<ul>
<li>含使用情形的執行時期應用程式</li>
<li>執行時期應用程式使用情形總計（以 GB-小時為單位）</li>
<li>含使用情形的服務實例</li>
<li>所有聯合執行時期、服務及應用程式的費用摘要</li>
</ul>
</li>
<li>選用項目：從長條圖中選取您選擇的月份，以檢視特定月份的資料。預設會顯示現行月份的資料。</li>
<li>選用項目：按一下<strong>匯出資料</strong>，然後選取 <strong>CSV</strong> 或 <strong>JSON</strong>，以將您的選取月份資料匯出至 <code>CSV</code> 或 <code>JSON</code> 檔案。</li>
</ol>


### 組織使用情形
{: #orgusage}

若要檢視每個組織的使用情形，請按一下**管理 &gt; 組織管理**，然後從**組織清單**中選取組織。在所選取組織的**管理組織**頁面上，您可以檢視下列使用資訊：

- 目前使用中的服務數目。
- 目前使用中的路徑數目。
- 記憶體配額圖，顯示已使用的配額量以及目前未使用的配額量。
- 應用程式配置圖，顯示已用記憶體配額中所含的應用程式。
- 計量應用程式使用情形圖，顯示每個已部署應用程式的已用 GB-小時的三個月報告。您可以選取**清單視圖**，以查看所有應用程式的資料（包括，每個應用程式的記憶體配置，以及過去三個月的計量 GB-小時使用情形）。

如需檢視每個組織之使用情形、調整配額方案以及管理組織的相關資訊，請參閱[管理組織](../admin/index.html#oc_organizations)。

### Reports
{: #oc_report}

您可以檢視 {{site.data.keyword.Bluemix_notm}} 實例的安全報告及日誌（例如 DataPower&trade;、防火牆及登入審核）。若要檢視報告及日誌，請按一下**管理 &gt; 報告及日誌**。

從下列選項中選取：

- 您可以從欄位中選取開始及結束日期，以過濾顯示的報告及日誌。
- 您可以從導覽窗格中展開及檢視各種報告。
- 您可以在報告及日誌的集合中進行搜尋。搜尋適用於報告名稱，也適用於報告及日誌內包含的文字內容。您也可以選擇依**管理事件**、**DataPower 報告**、**防火牆**及**登入審核**來過濾您的搜尋。
- 顯示報告或日誌時，可以按一下 ![下載](images/icon_download.png) 圖示來下載報告。

下表顯示針對「{{site.data.keyword.Bluemix_notm}} 本端」及「{{site.data.keyword.Bluemix_notm}} 專用」所產生的安全報告清單。

*表 5. 安全報告清單*

| **種類** | **報告** | **說明** |      
|-----------------|-------------------|---------------------|
| 防火牆 | 防火牆登入 | 與 Vyatta 防火牆裝置的管理者登入有關的事件。 |
| 防火牆 | 防火牆拒絕 | 根據現有的防火牆規則拒絕存取要求時，Vyatta 防火牆裝置所產生的事件。 |
| {{site.data.keyword.Bluemix_notm}} 管理者登入事件 | {{site.data.keyword.Bluemix_notm}} 管理者登入 | 管理者在每個 {{site.data.keyword.Bluemix_notm}} 系統上啟動 SSH 階段作業時，作業系統所產生的事件。 |
| {{site.data.keyword.Bluemix_notm}} 應用程式開發人員登入事件 | {{site.data.keyword.Bluemix_notm}} 應用程式開發人員登入 | {{site.data.keyword.Bluemix_notm}} 平台使用者使用指令行、REST API 或 {{site.data.keyword.Bluemix_notm}} 使用者介面來啟動階段作業時，{{site.data.keyword.Bluemix_notm}} 平台登入元件所產生的事件。 |
| {{site.data.keyword.Bluemix_notm}} 管理者管理事件 | {{site.data.keyword.Bluemix_notm}} 管理者作業系統管理事件 | 管理者在現行工作階段作業內執行動作時，作業系統所產生的事件。 |
| {{site.data.keyword.Bluemix_notm}} 應用程式開發人員管理事件 | {{site.data.keyword.Bluemix_notm}} (Cloud Foundry) 管理事件 | {{site.data.keyword.Bluemix_notm}} 平台使用者使用指令行、REST API 或 {{site.data.keyword.Bluemix_notm}} 使用者介面所執行之作業的相關事件。 |
| {{site.data.keyword.Bluemix_notm}} 管理者資料庫管理事件 | 資料庫管理事件 | 資料庫管理者對 {{site.data.keyword.Bluemix_notm}} 內部資料庫執行之作業的相關事件。 |
| 管理事件 | 使用者管理事件 | 在「管理」頁面上執行之使用者管理動作的相關事件。 |
| 管理事件 | 型錄 | 服務型錄變更的相關事件 |
| 管理事件 | 安全報告管理事件 | 在「管理」頁面上執行之安全報告管理動作的相關事件。 |
| 存取檢閱 | 存取檢閱報告 | 特許存取權的檢閱。 |
| 變更管理 | 軟體變更管理 | 變更管理活動。 |
| 金鑰管理 | 自訂 SSL 憑證管理 | 已上傳及儲存的自訂 SSL 憑證。 |
| 加密 | data-in-transit 加密 | 已配置的 data-in-transit 加密。 |
| 防毒 | 防毒掃描報告 | 現有的防毒軟體。 |
| 軟體修正程式管理 | 修補程式應用程式報告 | 已套用的軟體修正程式。 |
| 資安事件管理 | 資安事件補救報告 | 進行資安事件管理的資安事件證明。 |

## 檢視狀態
{: #oc_status}

您可以檢視 {{site.data.keyword.Bluemix_notm}} 環境和管理主控台的狀態。

### {{site.data.keyword.Bluemix_notm}} 環境狀態

您可以使用 {{site.data.keyword.Bluemix_notm}}「狀態」頁面來監視 {{site.data.keyword.Bluemix_notm}} 實例的狀態。按一下**帳戶和支援**圖示 ![帳戶和支援](../support/images/account_support.svg)，然後選取**狀態**。

「狀態」頁面是尋找通知和公告的一個中心位置，從中可瞭解影響 {{site.data.keyword.Bluemix_notm}} 平台以及 {{site.data.keyword.Bluemix_notm}} 中主要服務的重要事件。您可以訂閱 RSS 資訊來源以取得通知，這樣就不必查看是否有通知。如需「狀態」頁面和設定 RSS 資訊來源的相關資訊，請參閱[檢視 {{site.data.keyword.Bluemix_notm}}](../support/index.html#viewing-bluemix-status)。

### 管理主控台狀態

起始部署 {{site.data.keyword.Bluemix_notm}} 環境之後，就會自動完成用來管理您環境之元件的驗證檢查。在執行驗證檢查之後，您可以移至「管理主控台驗證檢查」頁面來檢查元件的狀態。若要存取該頁面，請前往 <code>https://console.&lt;subdomain&gt;.bluemix.net/check</code>，其中 `&lt;subdomain>` 是本端或專用實例的名稱。

您隨時都可以執行驗證。您必須登入，才能選取執行驗證的選項。如果您在新增使用者、編輯組織或管理服務時失敗，請執行此檢查來識別是否有任何元件失敗或斷線。您可以使用該檢查的資訊來開啟支援問題單，以快速解決問題。

## 管理型錄
{: #oc_catalog}

您可以管理使用者可在 {{site.data.keyword.Bluemix_notm}}「型錄」中看到哪些 {{site.data.keyword.Bluemix_notm}} 服務及入門範本。按一下**管理 &gt; 型錄管理**。

選取服務或入門範本磚，以編輯服務或入門範本方案可見性。若要編輯可見性，請從下列選項中選取：

- 若要顯示隱藏的服務或入門範本，讓您的使用者能在「型錄」中看到它，請選取**啟用所有方案**。
- 若要隱藏服務或入門範本，讓您的使用者在 {{site.data.keyword.Bluemix_notm}}「型錄」中看不到它，請選取**停用所有方案**。
- 若要控制個別方案的可見性，請選取方案名稱，然後使用下拉功能表，選取**針對所有組織啟用**、**針對所有組織停用**或**針對特定組織啟用方案**。

<!-- staging only start -->

### 登錄服務分配管理系統
{: #servicebrokerui}

如果您的服務要顯示在 {{site.data.keyword.Bluemix_notm}} 型錄中，則必須實作及登錄服務分配管理系統。登錄分配管理系統之後，您可以選擇可在本端或專用實例中存取服務的組織。

使用服務分配管理系統的方法會根據下列項目而不同：所管理的服務數目，或者是否已向 {{site.data.keyword.Bluemix_notm}} 進行登錄。

- 如果您的服務分配管理系統管理一個服務，則可以在實作[服務分配管理系統 API](http://docs.cloudfoundry.org/services/api.html){: new_window} 之後透過使用者介面進行登錄。請參閱[登錄可管理一個服務的服務分配管理系統](index.html#registerbrokerui)。
- 如果您的服務分配管理系統管理多個服務，則目前無法在實作「服務分配管理系統 API」之後進行登錄。請改成搭配使用 cf CLI 與 [{{site.data.keyword.Bluemix_notm}} 管理 CLI](../cli/plugins/bluemix_admin/index.html) 外掛程式（`ba` 次指令），或使用[自訂服務 API](index.html#servicebrokerapi)。
- 如果您已經登錄服務分配管理系統，而且要進行更新或予以刪除，請搭配使用 cf CLI 與 [{{site.data.keyword.Bluemix_notm}} 管理 CLI](../cli/plugins/bluemix_admin/index.html) 外掛程式（`ba` 次指令），或使用[自訂服務 API](index.html#servicebrokerapi)。

#### 登錄可管理一個服務的服務分配管理系統
{: #registerbrokerui}

請完成下列步驟，以登錄服務分配管理系統：

<ol>
<li><a href="http://docs.cloudfoundry.org/services/api.html" target="_blank">實作 Cloud Foundry 服務分配管理系統 API</a>，以啟用服務與 {{site.data.keyword.Bluemix_notm}} 之間的通訊。「服務分配管理系統 API」是 {{site.data.keyword.Bluemix_notm}} 所取用的一組 REST 端點。<br />
<br />
<p>實作服務分配管理系統時，在 <code>GET /v2/catalog</code> 的 JSON 回應中，您必須提供服務及服務方案的定義（包括您要顯示的服務資訊）。例如，請檢閱 Catalog (GET) 回應的下列範例 JSON：</p>
<p><pre>
"services": [ 
   {
      "bindable":true,
      "description":"Cool Service is a data warehousing and analytics solution.",
      "id":"cool-service-id",
      "name":"coolservice",
      "tags":[
         "customer_dedicated"
      ],
      "metadata":{
         "displayName":"Cool Service",
         "serviceMonitorApi":"https://myservicesstatus.mybluemix.net/healthcheck/",
         "providerDisplayName":"Cool company",
         "longDescription":"Cool Service is a data warehousing and analytics solution. You can quickly move your data into a next-generation columnar in-memory database and start running complex analytical queries.",
         "bullets":[
            {
               "title":"Fast and Simple",
               "description":"Cool Service uses dynamic in-memory columnar technology and innovations, such as parallel vector processing and actionable compression to rapidly scan and return relevant data."
            },
            {
               "title":"Connectivity",
               "description":"Cool Service is built to let you connect easily and to all of your services and applications. You can start analyzing your data right away with familiar tools."
            }
         ],
         "featuredImageUrl":"http://path/to/icon_64x64.png",
         "imageUrl":"http://path/to/icon_50x50.png",
         "mediumImageUrl":"http://path/to/icon_32x32.png",
         "smallImageUrl":"http://path/to/icon_24x24.png",
         "documentationUrl":"http://path/to/documentation.html",
         "instructionsUrl":"http://path/to/servicesample.md",
         "termsUrl":"http://path/to/terms_of_agreement.pdf",
         "media":[
            {
               "type":"youtube",
               "thumbnailUrl":"http://path/to/thumbnail.png",
               "url":"http://path/to/youtube/video",
               "caption":"Using Cool Service in 60 Seconds"
            },
            {
               "type":"image",
               "thumbnailUrl":"http://path/to/thumbnail.png",
               "url":"http://path/to/image_file.png",
               "caption":"Cool Service connects applications"
            },
            {
               "type":"video",
               "thumbnailUrl":"http://path/to/thumb.png",
               "caption":"Cool Service works with tables",
               "source":[
                  {
                     "type":"video/mp4",
                     "url":"http://path/to/video_file.mp4"
                  },
                  {
                     "type":"video/ogg",
                     "url":"http://path/to/video_file.ogg"
                  }
               ]
            }
         ]
      },
      "plans":[
         {
            "name":"smallplan",
            "description":"Dedicated schema and tablespace per service instance on a shared server. 1GB and 10GB of compressed database storage can hold up to 5GB and 50GB of uncompressed data respectively based on typical compression ratios.",
            "free":false,
            "id":"cool-service-plan-id",
            "metadata":{
               "bullets": [
"1 GB Min per instance. 10 GB Max per instance."
],
               "costs":[
                  {
                     "unitId":"INSTANCES_PER_MONTH",
                     "unit":"MONTHLY",
                     "partNumber":"D15UTLL"
                  }
               ],
               "displayName":"Small"
            }
         }
      ]
   }
]
}
</pre></p>
<p><strong>附註</strong>：當您建立本端或專用環境的服務分配管理系統時，必須在服務定義 JSON 檔案的 "tags" 欄位中指定 `customer_dedicated`。</p>
</li>
<li>實作「服務分配管理系統 API」之後，請移至<strong>管理</strong> &gt; <strong>型錄管理</strong>。</li>
<li>按一下<strong>登錄服務分配管理系統</strong>。</li>
<li>在下列欄位中輸入值，以完成表單：<ul>
<li>服務分配管理系統名稱</li>
<li>服務分配管理系統 URL</li>
<li>服務分配管理系統使用者名稱</li>
<li>服務分配管理系統密碼</li>
</ul>
</li>
<li>按一下<strong>連接</strong>。</li>
<li>檢閱服務的資訊，包括可用方案、圖示及服務說明。<br />
<p><strong>附註</strong>：如果您需要變更服務的型錄資訊，請更新服務分配管理系統，然後填寫表單來重新啟動登錄程序。</p>
</li>
<li>按一下<strong>登錄</strong>。</li>
<li>選擇啟用服務的所有方案或僅特定方案。預設會停用所有方案。</li>
<li>啟用所有組織或特定組織的服務實例。</li>
</ol>

您現在可以在「{{site.data.keyword.Bluemix_notm}} 型錄」的「自訂服務」種類中看到您的服務。請移至**管理 &gt; 型錄管理**，然後選取型錄中的磚。您可以啟用不同的方案，並且隨時編輯您組織的方案可見性。

## 管理組織
{: #oc_organizations}

透過建立及刪除組織、新增或移除組織的管理員以及監視配額用量，做出對貴公司最好的決策，以管理您的組織。

按一下**管理 &gt; 組織管理**。

您可以展開及檢視各個區段。您也可以檢閱及管理組織的配額方案。

### 建立組織

若要建立新的組織並新增管理員，請完成下列步驟：

1. 按一下<strong>建立組織</strong>。
2. 輸入組織的名稱。
3. 輸入您要新增為管理員的人員名稱或電子郵件。您可以輸入並選取多個名稱，來新增多位管理員。
4. 按一下<strong>建立組織</strong>，以儲存變更並建立組織。

### 建立空間

您可以在組織中建立空間；例如，建立 *dev* 空間作為開發環境、*test*
空間作為測試環境，以及 *production* 空間作為正式作業環境。
然後，您可以建立應用程式與空間的關聯。請完成下列步驟，以建立空間：

1. 移至**帳戶和支援**圖示 ![「帳戶和支援」圖示](../admin/images/account_support.svg) &gt; **管理組織**頁面。
2. 選取您要新增空間的組織。
3. 按一下**建立空間**。
4. 輸入空間名稱。
5. 按一下**建立**。

### 配額監視

在「配額監視」區段中，您可以展開區段並檢視下列資訊：

- 環境記憶體用量。此區段詳述完整系統環境的記憶體用量。圖表提供的資訊包括已使用的系統記憶體、系統記憶體總計、已使用的配額，以及已配置的配額總計。下列術語清單定義圖表中顯示的記憶體用量的類型。

	<dl>
	<dt><strong>已使用的系統記憶體</strong></dt>
	<dd>您環境所使用的實體記憶體。</dd>
	<dt><strong>系統記憶體總計</strong></dt>
	<dd>可供您環境使用的實體記憶體總計。</dd>
	<dt><strong>已部署的配額</strong></dt>
	<dd>在所有組織中，配置給所有已部署應用程式的記憶體總和。部署的配額總和
	可能會超過環境的實體系統記憶體總計。例如，如果您的系統記憶體總計為 16 GB，而且您已對每一個組織（總共有五個不同的組織）各配置 4 GB 的記憶體，則配額總計超出了已針對所有組織配置給您的系統記憶體總計。不過，在許多情況下，組織可能不會使用到個別配置給每個組織的配額總計。此外，所有組織也可能不會同時間用到其配置的記憶體配額總計。</dd>
	<dt><strong>配額總計</strong></dt>
	<dd>在所有組織中的已配置記憶體總計。</dd>
	</dl>

- 組織記憶體用量。本區段詳述組織層次的記憶體用量。您可以檢視配額額度總計，以及針對每一個組織所部署的配額。圖表會提供依每個組織的最高記憶體用量列出的資訊，依預設，使用最大量記憶體的組織會最先列出。您可以依**最高記憶體用量**及**超額記憶體配置**來排序。

	<dl>
	<dt><strong>最高記憶體用量</strong></dt>
	<dd>使用此選項，可識別使用最大量記憶體的組織。依最高記憶體用量排序，
	可識別使用最大量記憶體的組織。清單是依已部署的配額來排序。</dd>
	<dt><strong>超額記憶體配置</strong></dt>
	<dd>使用此選項，可識別哪些組織的配額方案大於所需配額。	依超額記憶體用量排序，可識別哪些組織針對已配置給組織的配額，使用最少量的記憶體。</dd>
	</dl>

### 調整配額方案

若要變更組織的配額方案，請完成下列步驟：

<ol>
<li>按一下圖表中您要在「組織記憶體用量」區段中編輯之組織的長條，或從「組織清單」區段中選取組織的名稱。</li>
<li>在「管理組織」頁面上，您可以變更配額方案、變更組織名稱，以及新增或移除管理員。<br />
<p><strong>附註</strong>：如果您選取的配額方案不足以提供組織的現行用量，則會收到一則訊息。</p>
</li>
<li>若要儲存您在「管理組織」頁面上所做的任何變更，請按一下<strong>儲存</strong>。</li>
</ol>

### 從組織清單中管理組織

在「組織清單」區段中，您可以檢視 {{site.data.keyword.Bluemix_notm}} 環境中的所有組織，而且按一下組織名稱即可針對個別組織採取動作。

- 若要刪除組織，請按一下「動作」直欄中的**刪除**圖示 ![刪除](images/icon_trash.svg)。
- 若要檢視組織的配額方案及使用情形，請按一下清單中的組織名稱。在所選取組織的**管理組織**頁面上，您可以檢視下列使用資訊：

  - 目前使用中的服務數目。
  - 目前使用中的路徑數目。
  - 記憶體配額圖，顯示已使用的配額量以及目前未使用的配額量。
  - 應用程式配置圖，顯示已用記憶體配額中所含的應用程式。
  - 計量應用程式使用情形圖，顯示每個已部署應用程式的已用 GB-小時的三個月報告。您可以選取**清單視圖**，以查看所有應用程式的資料（包括，每個應用程式的記憶體配置，以及過去三個月的計量 GB-小時使用情形）。

- 若要編輯組織名稱，以及新增或移除管理員，請按一下清單中的組織名稱，並遵循畫面上的提示。

## 管理使用者及許可權
{: #oc_useradmin}

您可以透過 LDAP 將使用者從公司的使用者登錄新增至 {{site.data.keyword.Bluemix_notm}} 實例。您可以新增單一使用者或使用者群組，並且檢視使用者許可權。如果您已獲指派 `admin` 許可權，則您也能設定及管理其他使用者的許可權。按一下**管理 &gt; 使用者管理**。

「使用者管理」頁面會顯示本端或專用實例的所有使用者。會顯示每一位使用者的許可權。許可權可以為下列項目：None、`Admin`、`Catalog`、`Login`、`Reports`
及 `Users`。可以啟用許可權，或是可以授與使用者該許可權的 `view` 或 `write` 存取權，如圖示所代表。如需每一種類型的說明以及圖示的說明，請參閱[許可權](index.html#permissions)。

### 處理使用者

您可以個別或依群組來搜尋現有使用者、移除使用者，以及新增使用者。從下列選項中選擇：

* 尋找使用者。您可以使用**搜尋**欄位在表格中尋找使用者。

* 新增單一使用者。如果您具有 `admin` 許可權，或具有 `write` 存取權的 `users` 許可權，則可以新增使用者。

  1. 若要從 LDAP 目錄新增單一使用者，請按一下**新增使用者**。
  2. 在**搜尋**欄位中，鍵入使用者的電子郵件位址，然後從移入的清單中選取使用者。
  3. 接下來，從**組織**欄位中，輸入組織名稱並從移入的清單中選取組織，以選擇您要新增使用者的組織。
  4. 若要將使用者新增至選取的組織，請按一下**新增使用者**。

  **附註**：新增作業成功時，使用者即會新增至表格中，以供您檢視及搜尋。新增使用者時，他們不具有任何指派權限。

* 從 LDAP 目錄新增一組使用者。

  1. 按一下**新增使用者群組**。
  2. 在**搜尋**欄位中，鍵入要搜尋的群組名稱，然後從移入的清單中選取群組名稱。
  3. 接下來，從**組織**欄位中，輸入組織名稱並從移入的清單中選取組織，以選擇您要新增使用者群組的組織。
  4. 若要將使用者群組新增至選取的組織，請按一下**新增使用者**。
  **附註**：超過 50 位使用者的群組會透過背景批次工作來新增。新增作業成功完成時，使用者或群組即會新增至表格中，以供您檢視及搜尋。新增使用者時，他們不具有任何指派權限。

* 匯入試算表，來新增一組使用者，該試算表包括使用者 ID、使用者電子郵件位址，以及您計劃要新增使用者的組織。

  1. 按一下**匯入使用者**。
  2. 按一下**下載範本 (.CSV)**，以下載具有您可填寫的必要直欄的試算表，或建立至少具有以下必要直欄標頭的專屬試算表：**使用者 ID**、**電子郵件**、**組織**。
  3. 填寫必要直欄的使用者值。如果您未使用 LDAP 目錄，請使用必要直欄及選用直欄標頭（**名字**和**姓氏**）進行使用者匯入。
  4. 儲存檔案，然後按一下**上傳檔案**。
 

  **附註**：輸入符合使用者登錄中所使用值的使用者 ID。只要您擁有所有必要直欄，試算表內的直欄可以是任意順序。如果匯入成功，您會收到一則確認訊息，指出已新增所有使用者。如果部分使用者的匯入成功，但其他使用者不然，請檢閱錯誤訊息，以對無法新增的使用者採取動作。

* 移除使用者。如果您具有 `admin` 許可權，或具有 `write` 存取權的 `users` 許可權，則可以移除使用者。


    1. 找出使用者，然後按一下 ![刪除](images/icon_trash.svg) 圖示。
    2. 按一下**移除**。

### 許可權
{: #permissions}

使用者可獲指派下列許可權：

*表 6. 許可權*

| **使用者許可權** | **說明** |       
|-----------------|-------------------|
| Admin | 具有 `admin` 許可權的使用者，可編輯其他使用者的許可權。 |
| Catalog | 具有 `catalog` 許可權的使用者，可獲指派對本端或專用實例中可用服務進行 `view` 或 `write`（修改）的存取權。 |  
| Login | 擁有 `login` 許可權的使用者可以查看「管理」頁面。沒有此許可權，使用者無法查看「管理」功能表選項。 |
| Reports | 具有 `reports` 許可權的使用者，可獲指派對安全報告進行 `view` 或 `write`（修改）的存取權。 |
| Users | 具有 `users` 許可權的使用者，可獲指派對使用者清單進行 `view`，或對使用者進行 `write`（新增或移除）的存取權。此許可權不容許您設定其他使用者的許可權。|


可以啟用許可權，或是可以授與使用者該許可權的 `view` 或 `write` 存取權，如下列圖示所代表：

* 許可權旁的 ![已啟用，以勾號代表](images/icon_enabled.svg) 圖示表示已啟用。
* ![檢視，以眼睛代表](images/icon_read.svg) 圖示表示使用者具有該許可權的 `view`（唯讀）存取權。
* ![寫入，以鉛筆代表](images/icon_write.svg) 圖示表示使用者具有該許可權的 `write`（編輯、新增或移除）存取權。

編輯其他使用者的許可權及組織需要您具備 `admin` 許可權。若要編輯許可權，請找出使用者，然後按一下使用者名稱。從**編輯使用者**頁面中，您可以啟用或停用許可權：

* 從清單中選取**開啟**，以啟用許可權。
* 從清單中選取**讀取**，以容許使用者具有該許可權的 `view`（唯讀）存取權，或選取**寫入**，以容許使用者具有該許可權的 `write`（編輯、新增及移除）存取權。
* 選取**關閉**以停用許可權。

若要在組織中新增或移除使用者，請從下列選項中選取：

* 若要將使用者新增至組織，請從表格中選取使用者名稱，來存取**編輯使用者**畫面。然後，使用搜尋欄位來找出組織，並從清單中選取組織，然後按一下**儲存**。
* 若要從組織中移除使用者，請從表格中選取使用者名稱，來存取**編輯使用者**畫面。然後，針對您要移除使用者的組織，按一下 ![移除](images/icon_remove.svg)，然後按一下**儲存**。


## 使用 Admin REST API 管理使用者
{: #usingadminapi}

您可以使用 `Admin` REST API 來新增及移除 {{site.data.keyword.Bluemix_notm}} 實例的使用者。`Admin` REST API 端點及 JSON 回應是基於實驗性所提供，以從指令行啟用基本作業。此資訊中範例內的端點及 URL，可能會在通知之後很快就變更或停止使用。

下列工具是利用下面範例的必要條件。您也可以選擇使用其他工具。
* cURL，用來以指令方式輸入 REST API 要求。cURL 是一種免費公用程式，您可以用來透過指令行介面，將 HTTP 要求傳送給伺服器，以及接收伺服器回應。您可以從 [cURL 下載網站](http://curl.haxx.se/download.html){: new_window}下載 cURL。
* Python，用來使用 Python 細緻列印 JSON 工具。這個選用性的工具會以 JSON 文字為輸入，並提供易讀的輸出。您可以從 [Python 下載網站](https://www.python.org/downloads){: new_window}下載 Python。

### 登入管理主控台

您必須登入「管理主控台」，才能執行任何 `Admin` API 要求。如果您具有 `admin` 許可權，或具有 `write` 存取權的 `users` 許可權，則可以新增或移除使用者。您必須具有 `admin` 許可權，才能編輯其他使用者的許可權。

若要登入「管理主控台」，您可以在 `https://<your_host>.ibm.com/login` 端點上使用基本存取鑑別。伺服器會使用您的階段作業傳回 Cookie。您可以使用該 Cookie 來執行「管理主控台」的所有作業。

**附註：**如果有幾個小時未使用，則階段作業會變成無效。

若要登入「管理主控台」，請執行下列指令：

`curl --user <user_id>:<password> -c ./cookies.txt --header "Accept: application/json" https://<your_host>.ibm.com/login | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">--user <em>user_id</em>:<em>password</em></dt>
<dd class="pd">接受使用者 ID 及密碼，以及傳送「基本授權」標頭。</dd>


<dt class="pt dlterm">-c <em>filename</em></dt>
<dd class="pd">將指定的使用者 ID 及密碼以 Cookie 方式儲存在指定的檔案中。</dd>


<dt class="pt dlterm">--header</dt>
<dd class="pd">傳送 Accept 標頭。</dd>

</dl>

下列範例顯示此指令的輸出：
```
{
    "message": "Logged in",
    "name": {
        "familyName": "*last_name*",
        "givenName": "*first_name*"
    }
}
```
{: screen}

### 列出組織
{: #listingorg}

新增使用者時，您必須指定組織。您可以使用 `Admin` REST API 來列出所有組織。您必須擁有具 `read` 存取權的 `users` 許可權，才能列出組織。若要列出所有組織，請執行下列指令：

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/organizations | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">將先前使用 <samp class="ph codeph">-c</samp> 選項儲存在檔案中的使用者 ID 及密碼，以 Cookie 方式傳遞給 HTTP 伺服器。</dd>

</dl>

針對每一個組織，結果會包括下列資訊：
* `"guid"`，組織的 GUID
* `"name"`，組織的名稱

下列範例顯示此指令的輸出：
```
{
     "resources": [
         {
             "guid": "05af098d-d476-4fb0-8b87-a84350e72af3",
             "name": "org-1"
         },
         {
             "guid": "5129a5a8-37c2-4ee4-a9b2-bebae3531db5",
             "name": "org-2"
         },

		 		 ....

		 ],
		 "total_results": 284
}
```
{: screen}

### 列出使用者
{: #listingusr}

您可以利用 `Admin` REST API 列出已登錄使用者，以判斷使用者是否已新增至您的 {{site.data.keyword.Bluemix_notm}} 環境。您必須擁有具 `read` 存取權的 `users` 許可權，才能列出已登錄使用者。若要列出所有使用者，請執行下列指令：

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">將先前使用 <samp class="ph codeph">-c</samp> 選項儲存在檔案中的使用者 ID 及密碼，以 Cookie 方式傳遞給 HTTP 伺服器。</dd>
</dl>

針對每一位已登錄使用者，結果會包括下列資訊：
* `"first_name"`（名字）及 `"last_name"`（姓）
* `"user_id"`，使用者 ID 及電子郵件位址
* `"guid"`，組織的 GUID。
* 指派給「管理主控台」使用者的 `"permissions"`。

下列範例顯示此指令的輸出：

```
{
    "next_url": "/codi/v1/users?results_per_page=100&amp;page=2",
    "prev_url": "",
    "resources": [
        {
            "active": true,
            "created_at": "2015-04-08T17:38:51.788Z",
            "created_by": "",
            "first_name": "some first name",
            "guid": "5d5268cf-39c0-48d3-96ae-7afe928e5dd7",
            "last_name": "some last name",
            "permissions": [
                {
                    "display": "ops.admin"
},
                {
                    "display": "ops.catalog.write"
},
                {
                    "display": "ops.reports.write"
},
                {
                    "display": "ops.catalog.read"
},
                {
                    "display": "ops.users.write"
},
                {
                    "display": "ops.reports.read"
},
                {
                    "display": "ops.login"
},
                {
                    "display": "ops.users.read"
                }
            ],
            "user_id": "someid@us.ibm.com"
        },
		 		 ...


     }
    ],
    "total_pages": 395,
    "total_results": 39421
}

```
{: screen}

### 新增使用者

您可以使用 `Admin` REST API，將使用者新增至 {{site.data.keyword.Bluemix_notm}} 實例。您必須擁有具 `write` 存取權的 `users` 許可權，才能新增使用者。

您可以新增一位使用者或一份使用者清單。您可以將使用者新增至單一組織或多個組織。若要新增使用者，您必須提供下列資訊：

* 使用者的名字及姓氏。從[列出使用者](index.html#listingusr)中提供 `"first_name"` 及 `"last_name"`。
* 電子郵件位址及使用者 ID：從[列出使用者](index.html#listingusr)中提供電子郵件位址及使用者 ID 的 `"user_id"`。
* `"guid"`。從[列出組織](index.html#listingorg)中提供組織的 GUID。

您可以在 JSON 檔案中提供資訊。

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">將先前使用 <samp class="ph codeph">-c</samp> 選項儲存在檔案中的使用者 ID 及密碼，以 Cookie 方式傳遞給 HTTP 伺服器。</dd>
</dl>

<ol>
<li>建立包含適當 JSON 格式資訊的 JSON 檔案。<p>例如，建立名為 `user.json` 且含有下列內容的檔案：
</p>
<pre>
{
    "members": [
        {
            "emails": [
"some_user_id@domain.com"
],
            "first_name": "Some_first_name",
            "last_name": "Some_last_name",
            "user_id": "some_user_id@domain.com"
        }
    ],
    "organization_roles": [
        {
            "id": "7a891f9c-e4e7-46c7-8b4e-dffaa7eb3bcd"
        }
    ]
}
</pre>
</li>
<li>執行下列指令，以將 JSON 檔案內容公佈到使用者的端點：&lt;br/>&lt;br/>
<code>
curl -v -b ./cookies.txt -X POST -H "Content-Type: application/json" -d @./user.json https://<your_host>.ibm.com/codi/v1/users
</code>
</li>
</ol>

<dl class="parml">

<dt class="pt dlterm">-v </dt>
<dd class="pd">指定詳細輸出。</dd>


<dt class="pt dlterm">-X POST</dt>
<dd class="pd">指定 POST 要求，並置換預設的 GET 要求。</dd>


<dt class="pt dlterm">-H "Content-Type: application/json"</dt>
<dd class="pd">指定 content-type 標頭（在此案例中為 JSON）。</dd>


<dt class="pt dlterm">-d *data*</dt>
<dd class="pd">指定 POST 要求中要傳送給 HTTP 伺服器的資料（在此案例中為 `user.json` 檔案）。</dd>

</dl>



下列範例顯示此指令的輸出：

```
* Connected to localhost (127.0.0.1) port 3000 (#0)
 > POST /codi/v1/users HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 > Content-Type: application/json
 > Content-Length: 333
 >
 * upload completely sent off: 333 out of 333 bytes
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < vary: X-HTTP-Method-Override
 < content-type: application/json
 < date: Wed, 22 Apr 2015 19:32:54 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 5612 msec
 ```
{: screen}

### 移除使用者

您可以使用 `Admin` REST API，從 {{site.data.keyword.Bluemix_notm}} 實例中移除使用者。您必須擁有具 `write` 存取權的 `users` 許可權，才能移除使用者。

若要移除使用者，您必須提供使用者的使用者 ID。請執行下列指令：

`curl -v -b ./cookies.txt -X DELETE https://<your_host>.ibm.com/codi/v1/users?user_id=<some_user_id@domain.com>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-X DELETE</dt>
<dd class="pd">指定 DELETE 要求。</dd>
</dl>

下列範例顯示此指令的輸出：

```
 * connect to ::1 port 3000 failed: Connection refused
 *   Trying 127.0.0.1...
 * Connected to localhost (127.0.0.1) port 3000 (#0)
 > DELETE /codi/v1/users?user_id=exampleuser@domain.com HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 >
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < content-type: application/json
 < date: Wed, 22 Apr 2015 21:01:09 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 1922 msec
 <
 ```
{: screen}


## 自訂服務 API
{: #servicebrokerapi}

有三個 API 可用於登錄或建立新服務、更新服務和刪除服務。

所有 API 都是相對於 <code>https://console.&lt;subdomain&gt;.bluemix.net/</code>。

<dl>
<dt><strong>&lt;subdomain&gt;</strong></dt>
<dd>此值為本端或專用實例的名稱。{{site.data.keyword.Bluemix}} 實例的子網域名稱是在上線期間指派的。</dd>
</dl>

## 登錄新服務

請使用下列 API 和程式碼範例來登錄新服務。

### 路徑
{: #registerroute}

```
POST /codi/v1/serviceBrokers
```
{: screen}

### 要求
{: #registerrequest}

*表 7. 欄位*

| **名稱** | **說明** |
|-----------------|-------------------|
| name | 服務分配管理系統的名稱。 |
| auth_username | 用於與服務分配管理系統連接的使用者名稱。 |
| auth_password | 用於與服務分配管理系統連接的密碼。 |
| broker_url | 用於連接服務分配管理系統的 URL。 |
| owningOrganization | 將服務列入白名單時要使用的起始組織。 |


#### 內文
{: #registerbody}

```
{
  "name" : "Service broker's name",
  "auth_username" : "username",
  "auth_password" : "password",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

#### 標頭
{: #registerheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### 回應
{: #registerresponse}

#### 狀態
{: #registerstatus}

```
201 Created
```
{: screen}

#### 內文
{: #registerbody2}

```
{
  "entity": {
    "name": "Service broker's name",
    "broker_url": "https://provision-broker.comp.bluemix.net/bmx/provisioning/brokers/2063580064-8f23230c-7f36-4ce5-a298-2ab4108f1120",
    "auth_username": "username",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "49f3adcc-ecc2-46fa-83c1-03322f04b3b1",
    "created_at": "2015-12-07T19:51:50Z",
    "updated_at": null,
    "url": "/v2/service_brokers/49f3adcc-ecc2-46fa-83c1-03322f04b3b1"
  }
}
```
{: screen}

## 更新服務

請使用下列 API 和程式碼範例來更新服務。

### 路徑
{: #updateroute}

`PUT /codi/v1/serviceBrokers`
{: screen}

### 要求
{: #updaterequest}

*表 8. 欄位*

| **名稱** | **說明** |
|-----------------|-------------------|
| name | 服務分配管理系統的名稱。此名稱是建立服務時使用的名稱，無法變更。 |
| auth_username | 用於與服務分配管理系統連接的使用者名稱。 |
| auth_password | 用於與服務分配管理系統連接的密碼。 |
| broker_url | 用於連接服務分配管理系統的 URL。 |
| owningOrganization | 將服務列入白名單時要使用的起始組織。 |


#### 內文
{: #updatebody}

```
{
  "name" : "Service Broker's name",
  "auth_username" : "username",
  "auth_password" : "newPassword",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

#### 標頭
{: #updateheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### 回應
{: #updateresponse}

#### 狀態
{: #updatestatus}

```
201 Created
```
{: screen}

#### 內文
{: #updatebody2}

```
{
  "entity": {
    "name": "Service Broker's name",
    "broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-d11bdd84-7556-469f-858d-2098b531f7f2",
    "auth_username": "username",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "2cbdb812-d37f-443b-894a-a96de31e5c38",
    "created_at": "2015-12-07T20:11:08Z",
    "updated_at": "2015-12-07T20:11:19Z",
    "url": "/v2/service_brokers/2cbdb812-d37f-443b-894a-a96de31e5c38"
  }
}
```
{: screen}

## 刪除服務

請使用下列 API 和程式碼範例來刪除服務。

*表 9. 參數*

| **名稱** | **說明** |
|-----------------|-------------------|
| name | 服務分配管理系統的名稱。此名稱是建立服務時使用的名稱，無法變更。 |


### 路徑

```
DELETE /codi/v1/serviceBrokers?name=name of service broker
```
{: screen}

### 要求
{: #deleterequest}

#### 標頭
{: #deleteheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### 回應
{: #deleteresponse}

#### 狀態
{: #deletestatus}

```
204 No Content
```
{: screen}

## 使用 cf CLI 管理使用者
{: #usingadmincli}

您可以利用 Cloud Foundry 指令行介面與 {{site.data.keyword.Bluemix_notm}} 管理 CLI 外掛程式搭配，來管理 {{site.data.keyword.Bluemix_notm}} 環境的使用者。例如，您可以從 LDAP 登錄新增使用者。

在開始之前，請先安裝 cf 指令行介面。{{site.data.keyword.Bluemix_notm}} 管理
CLI 外掛程式需要 cf 6.11.2 版或更新版本。[下載 Cloud Foundry 指令行介面](https://github.com/cloudfoundry/cli/releases){: new_window}

**限制：**Cygwin 不支援 Cloud Foundry 指令行介面。請在非 Cygwin 指令行視窗的指令行視窗中使用 Cloud Foundry 指令行介面。

### 新增 {{site.data.keyword.Bluemix_notm}} 管理 CLI 外掛程式

安裝 cf 指令行介面之後，您可以新增 {{site.data.keyword.Bluemix_notm}} 管理 CLI 外掛程式。

**附註**：如果您先前已安裝 {{site.data.keyword.Bluemix_notm}} 管理外掛程式，則可能需要解除安裝外掛程式，刪除儲存庫，然後重新安裝以取得最新更新。

完成下列步驟以新增儲存庫並安裝外掛程式：

<ol>
<li>若要新增 {{site.data.keyword.Bluemix_notm}} 管理外掛程式儲存庫，請執行下列指令：&lt;br/>&lt;br/>
<code>
cf add-plugin-repo BluemixAdmin https://console.&lt;subdomain&gt;.bluemix.net/cli
</code>&lt;br/>&lt;br/>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">您的 {{site.data.keyword.Bluemix_notm}} 實例 URL 的子網域。</dd>
</dl>
</li>
<li>若要安裝 {{site.data.keyword.Bluemix_notm}} 管理 CLI 外掛程式，請執行下列指令：&lt;br/>&lt;br/>
<code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

若要查看指令清單，請執行下列指令：


`cf plugins`
{: codeblock}

如需指令的其他說明，請使用 `-help` 選項。

如需如何使用 {{site.data.keyword.Bluemix_notm}} 管理 CLI 外掛程式的相關資訊，請參閱 [{{site.data.keyword.Bluemix_notm}} 管理](../cli/plugins/bluemix_admin/index.html)。
