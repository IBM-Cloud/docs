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
前次更新：2016 年 9 月 20 日
{: .last-updated}

如果您具有「{{site.data.keyword.Bluemix}} 本端」或「{{site.data.keyword.Bluemix_notm}} 專用」的管理者存取權，請移至**管理**頁面來管理資源、監視配額用量、管理使用者許可權、排定升級通知，以及檢視安全報告和日誌等。您可以透過建立空間並設定[使用者角色和許可權](index.html#oc_useradmin)來管理組織；請參閱[管理組織](../admin/orgs_spaces.html)。
{:shortdesc}

*表 1. 用於管理 {{site.data.keyword.Bluemix_notm}} 本端或專用實例的管理作業*

| 我能執行哪些操作？ | 詳細資料 |    
|----------------|---------|
|監視系統用量 | 按一下**管理 &gt; 用量**。檢視系統資訊、監視 CPU 使用率，以及計劃用量，以便做出對貴公司最好的決策。請參閱[檢視使用資訊](index.html#oc_resource)。|
|管理型錄 | 按一下**管理 &gt; 型錄管理**，以管理您的使用者及組織可以看見哪些服務。請參閱[管理型錄](index.html#oc_catalog)。|
|管理組織 | 按一下**管理 &gt; 組織管理**，以建立組織、監視組織配額，以及快速做出基於需求的決策。請參閱[管理組織](index.html#oc_organizations)。|
|建立空間和指派使用者角色 | 按一下**{{site.data.keyword.avatar}}**圖示 ![虛擬人像](../support/images/account_support.svg)，然後選取**管理組織**，以在組織內建立空間。新增使用者並將組織和空間角色指派給使用者。請參閱[管理組織](../admin/orgs_spaces.html)。 |
|對管理使用者許可權進行管理 | 按一下**管理 &gt; 使用者管理**，以新增使用者、移除使用者以及調整使用者許可權。請參閱[管理使用者及許可權](index.html#oc_useradmin)。 |
|檢視報告和日誌 | 按一下**管理 &gt; 報告和日誌**，以檢視您實例的安全報告及審核日誌。請參閱[檢視報告](index.html#oc_report)。 |
|檢視系統資訊 | 按一下**管理 &gt; 系統資訊**，以檢視系統資訊，例如擱置維護更新、實例的名稱和版本、地區、API URL、CLI URL、LDAP 配置詳細資料、群組和使用者對映、統計資料以及共用網域。請參閱[檢視系統資訊](index.html#oc_system)。 |
|擴充通知以及設定事件訂閱 | 按一下**管理 &gt; 系統資訊 &gt; *數字* 個擱置**。您可以使用 Webhook 與您選擇的 Web 服務整合，以設定更新或偶發事件的事件通知訂閱。請參閱[通知及事件訂閱](index.html#oc_eventsubscription)。 |



## 通知及事件訂閱
{: #oc_eventsubscription}

透過檢查「狀態」頁面，您隨時都可以知道環境的狀態。偶發事件及已排定的干擾性維護更新事件在發生時會報告在「狀態」頁面上。{{site.data.keyword.Bluemix_notm}} 也會針對已排定或擱置中的維護更新等事件，將通知傳送至「管理」頁面的「通知」區域。

### 通知

您可以檢視有關本端或專用環境的通知，以監視環境的狀態。如需不同通知類型以及各個通知類型張貼位置的相關資訊，請檢閱下表。

*表 2. 事件類型及通知方法*

| **事件類型** | **通知方法** |       
|-----------------|-------------------|
| 維護更新 | 您可以在「管理」頁面的「通知」區域中，收到有關即將進行之維護更新的警示。移至**管理**頁面，然後選取**通知**圖示 ![通知](images/icon_announcement.svg)。若要查看擱置及完成通知的完整清單及歷程，請按一下**管理 &gt; 系統資訊** &gt; *數字* **個擱置**。|
|  | 您也會在「狀態」頁面上收到有關已排定之干擾性維護更新事件的警示。按一下**{{site.data.keyword.avatar}}**圖示 ![虛擬人像](../support/images/account_support.svg)，然後選取**狀態**。|
|  | 若要擴充通知功能，您可以設定訂閱來傳送電子郵件給您選擇的收件者。或者，您可以將訂閱設定為使用 Webhook，將「管理」頁面的通知與您選擇的 Web 服務整合。|
| 重要偶發事件 | 您可以在「狀態」頁面上收到有關重要偶發事件的警示。按一下**{{site.data.keyword.avatar}}**圖示 ![虛擬人像](../support/images/account_support.svg)，然後選取**狀態**。若要擴充通知功能，您可以設定事件訂閱來傳送電子郵件給您選擇的收件者。或者，您可以將訂閱設定為使用 Webhook，將「管理」頁面的通知與您選擇的 Web 服務整合。  |  
| {{site.data.keyword.Bluemix_notm}} 狀態 | 您可以隨時在「狀態」頁面上檢視平台、服務及 {{site.data.keyword.Bluemix_notm}} 實例的最新狀態。按一下**{{site.data.keyword.avatar}}**圖示 ![虛擬人像](../support/images/account_support.svg)，然後選取**狀態**。  |

### 設定事件訂閱

您可以使用事件訂閱，來擴充傳送至「管理」頁面及「狀態」頁面的通知功能。使用事件訂閱來設定自訂電子郵件，或是使用 Webhook 來整合您選擇的工具。 
 * 如果您選取電子郵件選項，則會將通知傳送至您指定的電子郵件位址。您可以選取偶發事件或維護更新的通知。即會傳送起始電子郵件通知。接著，如果已變更偶發事件或維護更新，則每次變更時都會傳送另一個變更通知。  
 * 如果選取 Webhook 選項，您的通知會直接遞送至您選擇的目的地，例如電話號碼（透過 SMS 訊息）。您可以自訂通知類型（特別是維護更新或重要偶發事件警示），以及各通知內文中包含的資訊。

**附註**：只有具備「超級使用者」許可權的使用者 (`ops.admin`) 才能設定事件訂閱。

您可以使用下列其中一種方式來存取**事件訂閱**頁面：

* 針對維護更新通知，請移至**系統資訊 &gt; *數字* 個擱置 &gt; 訂閱**。
* 針對偶發事件通知，請按一下**{{site.data.keyword.avatar}}**圖示 ![虛擬人像](../support/images/account_support.svg) &gt; **狀態**，然後按一下**訂閱**圖示 ![訂閱](images/icon_subscribe.svg)。

**附註**：您可以使用所述兩種方法中的任一項，來存取這兩種類型通知的事件訂閱頁面。

若要從**事件訂閱**頁面建立電子郵件或 Webhook 訂閱，請完成下列步驟：

1. 按一下**新增訂閱**。
2. 填寫事件訂閱表單。如需表單上各欄位、有效負載區段使用值，以及電子郵件範本訊息內文的相關資訊，請檢閱下列各表。
3. 完成表單後，您可以選擇下列選項：

  * 按一下**儲存**，可將訂閱儲存至您的事件訂閱清單。
  * 按一下**儲存並測試**，可儲存並測試通知。
  * 按一下**儲存並關閉**，可將訂閱儲存至您的事件訂閱清單，並回到上一頁。

*表 3. 電子郵件訂閱的事件訂閱表單欄位*

| **欄位** | **說明** |
|-----------------|-------------------|
| 已啟用 | 選取此選項以啟用電子郵件通知。清除此選項以停用電子郵件通知。依預設會啟用訂閱。 |
| 類型 | 選取**電子郵件**。 |
| 事件 | 選擇訂閱**維護**或**偶發事件**事件的通知。 |
| 合併通知 | 選取此選項，以將所有地區的偶發事件通知合併成單一通知。此選項僅適用於偶發事件。 |
| 主旨 | 輸入電子郵件的主旨行。這是必要欄位。  |
| 內文 | 輸入要在電子郵件中傳送的訊息內文。您可以使用 IBM 有效負載值，將相關資訊移入電子郵件通知。請參閱[有效負載區段值](index.html#payload)表格來識別您可以使用的值。使用基本 HTML 標籤可建構您的電子郵件。這是必要欄位。 |
| 收件者 | 使用以逗點區隔的清單來輸入電子郵件通知接收者的電子郵件位址。展開「副本」或「密件副本」選項，可將電子郵件副本傳送給其他人。這是必要欄位。 |
| 說明 | 新增您要建立之訂閱的唯一說明。 |


*表 4. Webhook 訂閱的事件訂閱表單欄位*

| **欄位** | **說明** |
|-----------------|-------------------|
| 已啟用 | 選取此選項以啟用通知。清除此選項以停用通知。依預設會啟用訂閱。 |
| 類型 | 選取 **Webhook** |
| 方法 | 選取 **GET** 或 **POST**。 |
| 事件 | 選擇訂閱**維護**或**偶發事件**事件的通知。 |
| 合併通知 | 選取此選項，以將所有地區的偶發事件通知合併成單一通知。此選項僅適用於偶發事件。 |
| URL | 輸入要連接至 Web 服務的 URL。 |
| 說明 | 新增您要建立之訂閱的唯一說明。 |
| 使用者名稱 | 輸入您 Web 服務的使用者名稱。如果您不想使用個人認證，則可以設定一個正常運作的 ID，以專門與 {{site.data.keyword.Bluemix_notm}} 搭配使用。 |
| 密碼 | 輸入您 Web 服務的密碼。 |
| 有效負載 | 如果您已選取 POST 方法，請輸入您所使用之 Web 服務特有的內容（與用於 IBM 通知的有效負載值成對）。請參閱[有效負載區段值](index.html#payload)表格來識別您可以使用的值。如果您未在此區段中輸入資訊，則會收到沒有任何其他資訊的通知。 |

*表 5. 有效負載區段值*
{: #payload}

| **IBM 值** | **說明** | **事件類型** |
|----------------|----------------|------------------------|
| {{content.title}} | 訊息標題 |  維護更新及偶發事件 |
| {{content.message}} | 訊息說明 |   維護更新及偶發事件 |
| {{region}} | 受影響的地區 | 維護更新及偶發事件 |
| {{content.severity}} | 嚴重性評分 | 偶發事件 |
| {{content.category}} | 受影響的服務 | 偶發事件 |
| {{content.subCategoryName}} | 受影響的元件 | 偶發事件 |
| {{status}} | 更新的狀態 | 維護更新 |
| {{content.scheduleWindow.start}} | 排定的更新開始日期 | 維護更新 |
| {{content.disruption}} | 受影響的元件 | 維護更新 |
| {{type}} | 更新或偶發事件 | 維護更新及偶發事件 |
| {{content.scheduleWindow.end}} | 排定的更新結束時間 | 維護更新 |

儲存事件訂閱時，您會透過所設定的方法來接收通知。通知仍然會張貼到下列位置：  
 * 在偶發事件的「狀態」頁面上 
 * 在已排定干擾性維護更新事件的「狀態」頁面上
 * 在維護更新之「管理」頁面的「通知」區域中

您可以選取任何已儲存的事件訂閱、檢視最近的活動，或是依需要進行編輯。按一下可展開任何最近的活動項目，以檢視其歷程詳細資料。

## 維護更新
{: #oc_schedulemaintenance}

如果您有超級使用者許可權 (`ops.admin`)，則可以檢視已排定及擱置中的維護更新，方法是按一下**管理 &gt; 系統資訊 &gt; *數字* 個擱置**，以存取**系統更新**頁面。您環境的所有使用者都可以檢視已排定的干擾性維護更新事件，方法是按一下**{{site.data.keyword.avatar}}**圖示 ![虛擬人像](../support/images/account_support.svg)，然後選取**狀態**。

**附註**：請參閱下節來[設定預先核准的維護時間範圍](index.html#preapprovedmaintenance)，以開始進行。必須設定這些時間範圍，IBM 才能為您環境排定維護。

<dl>
<dt>非干擾性更新</dt>
<dd>非干擾性更新不會影響您的環境、執行中應用程式，或使用者對您應用程式的存取。此更新類型不需要逐案核准，將會在您從「系統更新」頁面設定的預先核准可用維護時間範圍內套用。</dd>
<dt>干擾性更新</dt>
<dd>干擾性更新可能會影響您的環境、執行中應用程式，或使用者對您應用程式的存取。您必須在分配的 21 天維護時間範圍內排定及核准所有這些維護更新。您可以選取所建議的部署日期和時間、任何預先核准時間範圍的選項，也可以開啟行事曆來選取三個特定日期和時間，供 IBM 在排定更新時進行選擇。</dd>
</dl>


### 設定預先核准的維護時間範圍
{: #preapprovedmaintenance}

開始排定及核准更新之前，必須設定預先核准的維護時間範圍。非干擾性更新會排定在預先核准的時間範圍內。

您必須設定一週內最少 12 小時可用，或每週至少兩天。例如，您可以設定在不同的兩天各 6 小時的時間範圍，也可以設定在不同的三天各 4 小時的時間範圍。為確保時間範圍提供足夠的時間來套用更新，每個時間範圍的持續時間必須最少為 4 小時。

**附註**：只有具備「超級使用者」許可權的使用者 (`ops.admin`) 才能排定及核准維護更新。

1. 移至**管理 &gt; 系統資訊 &gt; *數字* 個擱置 &gt; 管理可用性**。
2. 展開**管理可進行更新的時間範圍**區段。
3. 按一下**新增** ![新增](images/add-new.png)。
4. 設定第一個可用的時間範圍，方法是選取時間範圍的頻率、持續時間及開始時間。
5. 選用項目：如果您要將循環可用性時間範圍設定為排定部署的偏好時間，請選取**標示為偏好**。偏好的時間範圍會有指定的優先順序（在可能時）。
6. 按一下**提交**。
7. 重複此處理程序，直到您符合每週時間範圍的最低需求。

### 設定無法使用的維護時間範圍

設定預先核准的可用維護時間範圍之後，即可選擇設定您的環境無法進行更新的特定日期和時間。例如，您可能會選擇在高資料流量的週末或假日時不套用任何維護，以確保使用者可以使用您的應用程式。

1. 移至**管理 &gt; 系統資訊 &gt; *數字* 個擱置 &gt; 管理可用性**。
2. 展開**管理無法進行更新的時間範圍**區段。
3. 按一下**新增** ![新增](images/add-new.png)。
4. 設定無法使用的時間範圍，方法是選取時間範圍的頻率、持續時間及開始時間。
5. 按一下**提交**。

### 排定及核准更新
{: #scheduleandapprove}

設定預先核准的維護時間範圍之後，將會在那些時間自動排定非干擾性更新。您不需要明確核准這些類型的更新。不過，您可以檢視每一個維護更新的詳細資料，包括所更新的內容、更新所需時間，以及排定更新的時間。

若要檢視非干擾性更新的詳細資料，請完成下列步驟：

1. 移至**管理 &gt; 系統資訊 &gt; *數字* 個擱置**。
2. 識別將**需要客戶排程**設為**否**的任何列。
3. 選取該更新的列，以檢視詳細資料。

干擾性更新可能會影響您的環境、執行中應用程式，或使用者對您應用程式的存取。您必須在分配的 21 天維護時間範圍內排定及核准所有這些維護更新。您可以選取所建議的部署日期和時間、任何預先核准時間範圍的選項，也可以開啟行事曆來選取三個特定日期和時間，供 IBM 在排定更新時進行選擇。

對於確實需要您核准的干擾性更新，請完成下列步驟：

1. 移至**管理 &gt; 系統資訊 &gt; *數字* 個擱置**。
2. 識別將**需要客戶排程**設為**是**的任何列。
3. 選取該更新的列，以檢閱更新的詳細資料，包括更新說明、建議進行更新的日期和時間、受影響的元件，以及更新的持續時間。
4. 選取**排定及核准**。
5. 從下列選項中進行選擇：**建議日期**、**替代日期**或**任何預先核准的時間範圍**。如果您選取**替代日期**，則可以開啟行事曆來選取三個選項，供 IBM 進行選擇。
6. 選用項目：從行事曆中所選取替代日期的清單中，選取您要設為進行部署的偏好日期的日期。針對排定部署的部署人員，每一個選取的日期都會註記為偏好。IBM 會嘗試在偏好的更新時間範圍期間排定維護。
7. 完成後，請選取**提交**。

根據您的選擇，更新會排定在您接受的建議日期期間、您預先核准的其中一個時間範圍期間，或是您選取的其中一個特定日期和時間進行部署。IBM 排定部署更新的日期後，您就會看到排定的日期反映在**系統更新**頁面的更新詳細資料中。唯有在排定開始日期和時間之前仍有一天（24 個小時）的情況下，您才能重新排定已計劃的部署。重新排定部署之後，就無法再次重新排定。


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

如需設定預先核准的維護時間範圍以及設定無法進行維護的特定日期的相關資訊，請參閱[維護更新](admin/index.html#oc_schedulemaintenance)。

### 一般系統資訊

在「一般資訊」區段中，您可以檢視下列資訊：

- 關於 {{site.data.keyword.Bluemix_notm}} 建置的基本資訊。
- API 資訊，包括版本、URL、地區，以及 CLI 文件的鏈結。
- 關於系統及服務的共用網域資訊。
- 關於應用程式、使用者及組織總數的統計資料。

### LDAP 配置詳細資料

在「LDAP 配置詳細資料」區段中，您可以選取 LDAP 伺服器，然後檢視使用者和群組對映的相關資訊。如果您是使用 {{site.data.keyword.IBM}} WebID，它會顯示在本區段中。

## 檢視用量和報告
{: #oc_resource}

您可以針對本端或專用實例和 {{site.data.keyword.Bluemix_notm}} 帳戶，檢視不同類型的使用資訊。您也可以下載及檢視 {{site.data.keyword.Bluemix_notm}} 實例的安全報告和日誌。

- 資源資訊，包括磁碟空間、CPU 使用率、網路用量及平均回應時間。請參閱[資源用量](index.html#resourceusage)。
- 每個組織的帳戶用量，包括含用量的運行環境應用程式數目、運行環境 GB-小時總數，以及含用量的服務實例數目。請參閱[帳戶用量](index.html#accountusage)。
- 組織記憶體配額用量、根據已用記憶體配額總計配置的應用程式記憶體，以及特定組織的每個應用程式的 GB-小時用量視圖。您也可以在「組織管理」頁面的**配額監視**區段中，檢視所有組織的配額用量。請參閱[組織管理](../admin/index.html#orgusage)。


### 資源用量
{: #resourceusage}

若要檢視資源用量資訊，請按一下**管理 &gt; 資源用量**。

在**資源用量**區段中，您可以檢視下列資訊：

- 資源用量資訊，例如可以保留的記憶體和磁碟空間數量與其實際可用量，以及實際保留的記憶體和磁碟空間數量與其實際使用量。您也可以查看跨所有 Droplet Execution Agent (DEA) 的平均 CPU 使用率的相關資訊。若要查看 DEA 的記憶體、磁碟或 CPU 用量，請按一下**明細**。
您可以查看記憶體及磁碟的**保留**和**實體**數量的摘要。
<dl>
	<dt><strong>實體</strong></dt>
	<dd>針對您的環境所購買的記憶體或磁碟空間數量。</dd>
	<dt><strong>保留</strong></dt>
	<dd>環境中的所有已部署及執行中應用程式可保留的記憶體或磁碟空間總數量。因為應用程式很少使用它們保留的所有記憶體，所以實體值通常會小於保留值。</dd>
	</dl>

	除了圖形表示法之外，您還可以查看您的環境所使用的記憶體及磁碟空間百分比。您也可以查看與可用數量相比較之實際用量的保留及實體數量（以 GB 為單位）。
若要查看實體及保留記憶體用量的其他詳細資訊，請按一下**歷程**。您可以指定時間範圍，以每週或每月的形式進行檢視。**歷程記憶體用量**視圖顯示所選擇一段時間內的記憶體用量圖形。  

	<dl>
	<dt><strong>保留限制</strong></dt>
	<dd>「保留限制」顯示為水平點虛線，是環境中執行的所有應用程式可共同保留的記憶體總數。</dd>
	<dt><strong>保留</strong></dt>
	<dd>「保留」區域顯示環境中執行的所有應用程式目前共同保留的記憶體。
	<p>若要查看哪些組織在特定時間點保留大部分記憶體，請移至點與該時間點相關聯的「保留」區域上方。然後，您可以按一下所顯示圓餅圖中的某個組織，以查看該組織的相關資訊。</p></dd>
	<dt><strong>實體限制</strong></dt>
	<dd>「實體限制」顯示為水平點虛線，可顯示針對您的環境所購買的實體記憶體數量。</dd>
	<dt><strong>實體</strong></dt>
	<dd>「實體」區域顯示實際使用的記憶體數量。</dd>
	</dl>
- 過去六小時或一天進出頻寬的網路用量資訊。顯示的資料是根據公開及私密網路的輸入及輸出資料流量的總和。
- {{site.data.keyword.Bluemix_notm}} 在過去十分鐘、一小時及一天的平均回應時間。
- {{site.data.keyword.Bluemix_notm}} 在過去十分鐘、一小時及一天的每秒平均交易數。

### 帳戶用量
{: #accountusage}

您可以檢視專用或本端環境的帳戶的每月用量。您可以使用這項資料，來識別根據其用量對特定組織收取多少費用。**使用者**許可權指派為**讀取**權的所有管理主控台使用者，都可以檢視帳戶用量資料。此外，組織帳單管理員還可以檢視其組織的帳戶用量資料，即使帳單管理員未獲指派管理主控台的**使用者**許可權也是一樣。身為管理主控台管理者（超級使用者許可權），您可以指派組織的帳單管理員角色，方法是按一下**{{site.data.keyword.avatar}}**圖示 ![虛擬人像](../support/images/account_support.svg) &gt; **管理組織**。

若要檢視帳戶用量資料，請完成下列步驟：

<ol>
<li>按一下<strong>{{site.data.keyword.avatar}}</strong>圖示 ![虛擬人像](../support/images/account_support.svg) &gt; <strong>帳戶</strong> &gt; <strong>用量詳細資料</strong>。</li>
<li>選取您要查看資料的組織。</li>
<li>您可以查看下列種類的用量詳細資料：
<ul>
<li>含用量的運行環境應用程式</li>
<li>運行環境應用程式用量總計（以 GB-小時為單位）</li>
<li>含用量的服務實例</li>
</ul>
</li>
<li>選用項目：使用<strong>您的雲端活動</strong>功能表選取您選擇的月份，以檢視特定月份的資料。</li>
<li>選用項目：按一下<strong>匯出資料</strong>，然後選取 <strong>CSV</strong> 或 <strong>JSON</strong>，以將您的選取月份資料匯出為 <code>CSV</code> 或 <code>JSON</code> 檔案。</li>
</ol>

您也可以針對從「{{site.data.keyword.Bluemix_notm}} 公用」聯合的運行環境、應用程式及服務，檢視帳戶層次的每月用量及相關聯的費用。您可以使用這項資料，來識別根據其用量對特定組織收取多少費用。

<ol>
<li>按一下<strong>{{site.data.keyword.avatar}}</strong>圖示 ![虛擬人像](../support/images/account_support.svg) &gt; <strong>帳戶</strong> &gt; <strong>用量詳細資料</strong>。</li>
<li>按一下<strong>公用</strong>。</li>
<li>選取您要查看資料的組織，或選取<strong>所有組織</strong>，一次檢視所有組織的資料。</li>
<li>您可以查看下列種類的用量詳細資料：
<ul>
<li>含用量的運行環境應用程式</li>
<li>運行環境應用程式用量總計（以 GB-小時為單位）</li>
<li>含用量的服務實例</li>
<li>所有聯合運行環境、服務及應用程式的費用摘要</li>
</ul>
</li>
<li>選用項目：從長條圖中選取您選擇的月份，以檢視特定月份的資料。預設會顯示現行月份的資料。</li>
<li>選用項目：按一下<strong>匯出資料</strong>，然後選取 <strong>CSV</strong> 或 <strong>JSON</strong>，以將您的選取月份資料匯出為 <code>CSV</code> 或 <code>JSON</code> 檔案。</li>
</ol>


### 組織用量
{: #orgusage}

若要檢視每個組織的用量，請按一下**管理 &gt; 組織管理**，然後從**組織清單**中選取組織。在所選取組織的**管理組織**頁面上，您可以檢視下列使用資訊：

- 目前使用中的服務數目。
- 目前使用中的路徑數目。
- 記憶體配額圖，顯示已使用的配額量以及目前未使用的配額量。
- 應用程式配置圖，顯示已用記憶體配額中所含的應用程式。
- 計量應用程式用量圖，顯示每個已部署應用程式的已用 GB-小時的三個月報告。您可以選取**清單視圖**，以查看所有應用程式的資料（包括，每個應用程式的記憶體配置，以及過去三個月的計量 GB-小時用量）。

如需檢視每個組織之用量、調整配額方案以及管理組織的相關資訊，請參閱[管理組織](../admin/index.html#oc_organizations)。

### 報告
{: #oc_report}

您可以檢視 {{site.data.keyword.Bluemix_notm}} 實例的安全報告及日誌（例如 DataPower&trade;、防火牆及登入審核）。若要檢視報告及日誌，請按一下**管理 &gt; 報告及日誌**。

從下列選項中選取：

- 您可以從欄位中選取開始及結束日期，以過濾顯示的報告及日誌。
- 您可以從導覽窗格中展開及檢視各種報告。
- 您可以在報告及日誌的集合中進行搜尋。搜尋適用於報告名稱，也適用於報告及日誌內包含的文字內容。您也可以選擇依**管理事件**、**DataPower 報告**、**防火牆**及**登入審核**來過濾您的搜尋。
- 顯示報告或日誌時，可以按一下 ![下載](images/icon_download.png) 圖示來下載報告。

下表顯示針對「{{site.data.keyword.Bluemix_notm}} 本端」及「{{site.data.keyword.Bluemix_notm}} 專用」所產生的安全報告清單。大部分的報告都是每日產生。不過，加密及金鑰管理事件報告是每月產生。所有報告都會在管理主控台中保留 90 天，供您進行擷取。在這 90 天之後，{{site.data.keyword.Bluemix_notm}} 的每個要求都可以離線使用報告 9 個月。總共可擷取報告長達 1 年。

*表 6. 安全報告清單*

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

您可以使用 {{site.data.keyword.Bluemix_notm}}「狀態」頁面來監視 {{site.data.keyword.Bluemix_notm}} 實例的狀態。按一下**{{site.data.keyword.avatar}}**圖示 ![虛擬人像](../support/images/account_support.svg)，然後選取**狀態**。

「狀態」頁面是尋找通知和公告的一個中心位置，從中可瞭解影響 {{site.data.keyword.Bluemix_notm}} 平台以及 {{site.data.keyword.Bluemix_notm}} 中主要服務的重要事件。您可以訂閱 RSS 資訊來源以取得通知，這樣就不必查看是否有通知。如需「狀態」頁面和設定 RSS 資訊來源的相關資訊，請參閱[檢視 {{site.data.keyword.Bluemix_notm}}](../support/index.html#viewing-bluemix-status)。

### 管理主控台狀態

起始部署 {{site.data.keyword.Bluemix_notm}} 環境之後，就會自動完成用來管理您環境之元件的驗證檢查。在執行驗證檢查之後，您可以移至「管理主控台驗證檢查」頁面來檢查元件的狀態。若要存取該頁面，請前往 <code>https://console.&lt;subdomain&gt;.bluemix.net/check</code>，其中 `&lt;subdomain>` 是本端或專用實例的名稱。

您隨時都可以執行驗證。您必須登入，才能選取執行驗證的選項。如果您在新增使用者、編輯組織或管理服務時失敗，請執行此檢查來識別是否有任何元件失敗或斷線。您可以使用檢查所取得的資訊來開啟支援問題單，以便能快速解決問題。

## 管理型錄
{: #oc_catalog}

您可以管理使用者可在 {{site.data.keyword.Bluemix_notm}}「型錄」中看到哪些 {{site.data.keyword.Bluemix_notm}} 服務及入門範本。按一下**管理 &gt; 型錄管理**。

選取服務或入門範本磚，以編輯服務或入門範本方案可見性。若要編輯可見性，請從下列選項中選取：

- 若要顯示隱藏的服務或入門範本，讓您的使用者能在「型錄」中看到它，請選取**啟用所有方案**。
- 若要隱藏服務或入門範本，讓您的使用者在 {{site.data.keyword.Bluemix_notm}}「型錄」中看不到它，請選取**停用所有方案**。
- 若要控制個別方案的可見性，請選取方案名稱，然後使用下拉功能表，選取**針對所有組織啟用**、**針對所有組織停用**或**針對特定組織啟用方案**。

<!-- staging only start -->

您也可以根據開發人員在建立應用程式時的相容性，管理要供選擇之可用建置套件的優先順序。

1. 移至**管理 &gt; 型錄管理**
2. 移至**運算**區段。
3. 選取**建置套件優先順序**。
4. 選取您要在清單中設定較高或較低優先順序的建置套件選項。
5. 選取此選項之後，使用箭頭在清單中移動選項。

<!-- staging only end -->

### 登錄服務分配管理系統
{: #servicebrokerui}

如果您的服務要顯示在 {{site.data.keyword.Bluemix_notm}} 型錄中，則必須實作及登錄[服務分配管理系統](http://docs.cloudfoundry.org/services/api.html){: new_window}。登錄分配管理系統之後，您可以選擇可在本端或專用實例中存取服務的組織。

使用服務分配管理系統的方法會根據所管理的服務數目，或者是否已向 {{site.data.keyword.Bluemix_notm}} 進行登錄而有所不同。

- 如果您的服務分配管理系統管理一個服務，則可以在實作[服務分配管理系統 API](http://docs.cloudfoundry.org/services/api.html){: new_window} 之後透過使用者介面進行登錄。請參閱[登錄可管理一個服務的服務分配管理系統](index.html#registerbrokerui)。
- 如果您的服務分配管理系統管理多個服務，請搭配使用 cf CLI 與 [{{site.data.keyword.Bluemix_notm}} 管理 CLI](../cli/plugins/bluemix_admin/index.html) 外掛程式（`ba` 次指令），或使用 [自訂服務 API](index.html#servicebrokerapi)。
- 如果您已經登錄服務分配管理系統，而且要進行更新或予以刪除，請搭配使用 cf CLI 與 [{{site.data.keyword.Bluemix_notm}} 管理 CLI](../cli/plugins/bluemix_admin/index.html) 外掛程式（`ba` 次指令），或使用[自訂服務 API](index.html#servicebrokerapi)。

#### 登錄可管理一個服務的服務分配管理系統
{: #registerbrokerui}

請檢閱下列資訊並完成這些步驟，以登錄服務分配管理系統：

**開始之前**：<a href="http://docs.cloudfoundry.org/services/api.html" target="_blank">實作 Cloud Foundry 服務分配管理系統 API</a>，以啟用服務與 {{site.data.keyword.Bluemix_notm}} 之間的通訊。「服務分配管理系統 API」是 {{site.data.keyword.Bluemix_notm}} 所耗用的一組 REST 端點。

實作服務分配管理系統時，在 <code>GET /v2/catalog</code> 的 JSON 回應中，您必須提供服務及服務方案的定義（包括您要顯示的服務資訊）。例如，請檢閱 Catalog (GET) 回應的下列範例 JSON：

```
{
"services":[
   {
      "bindable":true,
      "description":"Cool Service is an analytics and data warehousing solution.",
      "id":"cool-service-id",
      "name":"coolservice",
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
               "description":"Cool Service is built to let you connect easily and to all of your services and applications. You can start analyzing your data immediately with familiar tools."
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
```
{: codeblock}

下列各表可以協助您填寫 JSON 檔案。

*表. JSON 欄位*

| **JSON 欄位** | **說明** |
|-----------------|-----------------|
|bindable   | 布林值，指出服務實例是否可以連結至應用程式。  |
|description | 服務的說明，在您使用 cf marketplace 指令或移至 {{site.data.keyword.Bluemix_notm}} 使用者介面之型錄中的服務圖示上方時顯示。您可以新增一個句子或一個詞組來作為說明。 |
|name | cf 指令行介面中所顯示服務的名稱。此名稱在 {{site.data.keyword.Bluemix_notm}} 中必須是唯一的、必須使用小寫字母，而且不得包含空格。在您向 {{site.data.keyword.Bluemix_notm}} 登錄服務之後，即無法變更服務的名稱。 |
|id  | 服務的 ID。此 ID 在 {{site.data.keyword.Bluemix_notm}} 中必須是唯一的，而且必須是 GUID（廣域唯一 ID）。在您向 {{site.data.keyword.Bluemix_notm}} 登錄服務之後，即無法變更服務的 ID。 |
|metadata | {{site.data.keyword.Bluemix_notm}} 型錄及定價單中顯示的服務方案 meta 資料。metadata 欄位是選用欄位。您可以指定 meta 資料的其他欄位。如需相關資訊，請參閱下列 [meta 資料欄位](index.html#metadatafields)表格。 |
|plans | 服務方案定義的陣列。如需相關資訊，請參閱下列[方案欄位](index.html#planfields)表格。 |

*表. meta 資料欄位*
{: #metadatafields}

| **meta 資料值** | **說明** |
|---------------------|-----------------|
|displayName          | {{site.data.keyword.Bluemix_notm}} 使用者介面中所顯示方案的名稱。此名稱會顯示在型錄的服務詳細資料頁面上以及定價單上。只會將方案名稱的第一個字母大寫。請不要使用 "Default" 作為預設方案名稱；請改用 "Standard"。 |
|providerDisplayName | 服務提供者的名稱 |
|longDescription | 服務的詳細說明。請考慮至少使用兩個句子來作為詳細說明。 |
|plans                | 服務方案定義的陣列。plans 欄位的每一個陣列項目都會包含下列欄位：name、description、free、id 及 metadata。如需相關資訊，請參閱下列[方案欄位](index.html#planfields)表格。 |
|bullets | 針對服務所顯示的字串陣列。除了詳細說明之外，您還可以使用項目符號來提供資訊。bullets 欄位必須包含至少兩個 bullet 元素。每一個 bullet 都會包括 title 及 description 欄位。 |
|imageUrl | 大型 PNG 影像（50 x 50 像素）的 URL。 |
|smallImageUrl | 小型 PNG 影像（24 x 24 像素）的 URL。 |
|mediumImageUrl | 中型 PNG 影像（32 x 32 像素）的 URL。 |
|featuredImageUrl | 精選影像（64 x 64 像素）的 URL。 |
|documentationUrl | 服務相關文件的 URL。 |
|termsUrl | 包含合約條款的 PDF 檔案的 URL。 |
|media（選用） | 要顯示在 {{site.data.keyword.Bluemix_notm}} 使用者介面中介紹服務的視訊及畫面擷取的元素陣列。media 元素可以包含下列欄位：type（image、youtube、video）、thumbnailUrl（media 元素之預覽影像的 URL）、url（畫面擷取或 YouTube 視訊的 URL）、source（未在 YouTube 上管理的視訊來源。HTML5 必須支援視訊來源的 "type"。video 包括 "type" 及 "url"）及 caption（media 元素的標題。標題有助於協助殘障人士瞭解您的 media 元素。）。 |
|serviceKeysSupported | 布林值，指出是否支援服務金鑰 API。服務金鑰 API 是用於允許在 {{site.data.keyword.Bluemix_notm}} 外部使用服務。預設值為 false。 |
|plan_updateable | 布林值，指出服務是否支援方案變更。預設值為 false。 |
|embeddableDashboard（選用） | 指出如何在 {{site.data.keyword.Bluemix_notm}} 使用者介面中顯示服務儀表板的欄位。如果您未指定此欄位，則會內嵌儀表板，但將最小寬度限制為 960 px，而且儀表板在 iframe 周圍有其他水平填補。您可以使用 true、false、drilldown 或 launch。您可以針對此值使用下列欄位：true、false、drilldown 及 launch。  |
|notCreatable（選用） | 布林值，指出是否可以從 {{site.data.keyword.Bluemix_notm}} 使用者介面以及從 cf 指令行介面建立服務實例。值 true 表示無法從 {{site.data.keyword.Bluemix_notm}} 使用者介面或 cf 指令行介面建立服務實例。預設值為 false。 |
|notCreatableMessage（選用） | 無法建立服務實例時，會在 {{site.data.keyword.Bluemix_notm}} 使用者介面中顯示的訊息。如果您未指定此欄位，將會顯示下列預設訊息：若要在它可用時收到通知，請確認您的電子郵件位址，或輸入不同的電子郵件位址。 |
|notCreatableRobotMessage（選用） | {{site.data.keyword.Bluemix_notm}} 使用者介面內服務詳細資料頁面的語音泡泡中所顯示的訊息。此訊息是用來指出服務可能發生問題，或是有導致它無法使用的其他原因。您可以指定可說明原因的訊息。如果您未指定此欄位，將會顯示下列預設訊息：此服務目前無法使用。 |
|apiReferenceUrl（選用） | 「型錄」內服務詳細資料頁面的「API 參考資料」區域中的 iframe URL。如果未用於「型錄」中的服務詳細資料頁面，您可以在 {{site.data.keyword.Bluemix_notm}} REST API Doc 微服務中登錄服務時，輸入指派給服務的 REST API Doc 的數值。這將會在服務儀表板中顯示 REST API Doc。 |
|sdkDownloadUrl（選用） | 按一下「下載 SDK」按鈕時所開啟網頁的 URL。「下載 SDK」按鈕位在「儀表板」中應用程式概觀頁面的服務磚上。會在新的瀏覽器分頁中開啟網頁。 |
|serviceMonitorApi    | 傳回報告服務性能的 JSON 資料的 API URL（如下列範例所示）。您的服務 meta 資料中必須要有 serviceMonitorApi 或 serviceMonitorApp。如需範例，請參閱下列程式碼範例。 |
|serviceMonitorApp    | 可以部署至 {{site.data.keyword.Bluemix_notm}} 並連結至服務以提供服務狀態特定輸出的應用程式 URL。應用程式必須傳回與 serviceMonitorApi 相同的 JSON 資料格式。您的服務 meta 資料中必須要有 serviceMonitorApi 或 serviceMonitorApp。如需範例，請參閱下列程式碼範例。 |

```
{
    "service": "servicename",
    "version": 1,
    "health": [
        {
            "plan": "starter",
            "status": 0,
            "serviceinput": "count(*) from healthcheck",
            "serviceoutput": "10…or error 1234 database not running",
            "responsetime": 4
        },
        {
            "plan": "enterprise",
            "status": 1,
            "serviceinput": "count(*)fromhealthcheck",
            "serviceoutput": "10…orerror1234databasenotrunning",
            "responsetime": 4
        }
    ]
}
```
{: pre}

下列範例顯示 GET /v2/catalog 的 JSON 回應如何對映至 {{site.data.keyword.Bluemix_notm}} 型錄中的服務詳細資料頁面：

![型錄中的服務詳細資料。](images/metadata.png "「Bluemix 型錄」服務詳細資料視圖")

*表. 方案欄位*
{: #planfields}

| **方案值** | **說明** |
|---------------------|-----------------|
|name       | cf 指令行介面中所使用服務方案的名稱。例如，方案名稱顯示在 cf marketplace 指令輸出中。方案名稱必須是小寫字母、不得包含空格，而且在服務內必須是唯一的。  |
|description       | 服務方案的說明。在 {{site.data.keyword.Bluemix_notm}} 型錄的服務詳細資料頁面上選取方案之後，會顯示此說明。 |
|free      | 布林值，指出服務方案是否免費。預設值為 true。 |
|id       | 服務方案的 ID。ID 在 {: new_window} 內必須是唯一的，而且必須是 GUID。  |
|metadata（選用）    | {{site.data.keyword.Bluemix_notm}} 型錄及定價單中顯示的服務方案 meta 資料。metadata 欄位是選用欄位。您可以在 metadata 欄位內指定下列欄位：displayName、type（subscription、reservable、planDetails）、bullets、costs（unitId、unit、partNumber）及 paidOnly。如需相關資訊，請參閱下列[方案 meta 資料欄位](index.html#planmetadata)表格。 |

*表. 方案 meta 資料欄位*
{: #planmetadata}

| **方案 meta 資料值** | **說明** |
|------------------------|-----------------|
|displayName             | {{site.data.keyword.Bluemix_notm}} 使用者介面中所顯示方案的名稱。此名稱會顯示在型錄的服務詳細資料頁面上以及定價單上。   |
|type                    | 方案的類型。您可以將下列值用於此欄位：subscription（訂閱方案。預設值為 false）、reservable（可保留方案。只有在方案是訂閱方案（即 plan.metadata.subscription 的值為 true）時，才使用此值。預設值為 false。）、planDetails（可與方案搭配使用的資源的詳細數量及說明。只有在方案是可保留方案（即 plan.metadata.reserveable 的值為 true）時，才使用此值。） |
|bullets                 | 可與方案搭配使用的資源的說明。說明會顯示在型錄的服務詳細資料頁面以及定價單的**特性**直欄中。 |
|costs                   | 在型錄的服務詳細資料頁面以及定價單的「價格」直欄中顯示的服務的成本資訊。每一個陣列項目都會包含下列欄位：unitId（單元的 ID。使用複數形式，並將所有字母都大寫。對於免費方案，此欄位是選用項目。）、unit（用於計算服務費用的度量。在 {{site.data.keyword.Bluemix_notm}} 使用者介面中，使用此欄位的值來代表費用度量。） 及 partNumber（計費系統所使用的 `part_number` ID。對於免費方案，此欄位是選用項目。）。   |
|paidOnly（選用）     | 布林值，指出此服務方案是否僅適用於 {{site.data.keyword.Bluemix_notm}} 付費帳戶。值 **true** 表示服務方案僅適用於付費帳戶，因此不能新增至試用帳戶。值 **false** 表示服務方案可以新增至付費帳戶及試用帳戶。預設值為 **false**。	  |

下列範例顯示 GET /v2/catalog 的 JSON 回應如何對映至 {{site.data.keyword.Bluemix_notm}} 型錄中的服務詳細資料頁面。具體而言，是前一個表格中所說明的方案 meta 資料欄位如何對映至使用者介面：

![型錄中的方案 meta 資料詳細資料。](images/plan_metadata.png "「Bluemix 型錄」方案 meta 資料值視圖")


<ol>
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

您現在可以在 {{site.data.keyword.Bluemix_notm}}「型錄」的「自訂服務」種類中看到您的服務。請移至**管理 &gt; 型錄管理**，然後選取型錄中的磚。您可以啟用不同的方案，並且隨時編輯您組織的方案可見性。


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

1. 移至**{{site.data.keyword.avatar}}**圖示 ![「虛擬人像」圖示](../admin/images/account_support.svg) &gt; **管理組織**頁面。
2. 選取您要新增空間的組織。
3. 按一下**建立空間**。
4. 輸入空間名稱。
5. 按一下**建立**。


### 配額監視

您可以展開**配額監視**區段，以檢視下列資訊：

- 環境記憶體用量詳述完整系統環境的記憶體用量。此圖表顯示下列資訊： 
<ul>
<li>使用中實體記憶體及實體記憶體限制</li>
<li>保留記憶體配額及保留記憶體限制</li>
<li>組織的記憶體配額總計</li>
</ul>
圖表中顯示下列類型的記憶體用量。

	<dl>
	<dt><strong>實體用量</strong></dt>
	<dd>您環境所使用的實體記憶體。</dd>
	<dt><strong>實體限制</strong></dt>
	<dd>可供您環境使用的實體記憶體總計。</dd>
	<dt><strong>保留配額</strong></dt>
	<dd>在所有組織中，保留給所有已部署應用程式的記憶體總和。保留配額總和可能會超出環境的實體記憶體限制。例如，如果您的實體記憶體限制為 16 GB，則針對共五個不同的應用程式各保留 4 GB 的記憶體。保留的配額就會超出實體記憶體限制。不過，在許多情況下，應用程式可能不會使用個別保留給每一個應用程式的配額總計。此外，所有應用程式也可能不會同時使用其保留記憶體配額總計。</dd>
	<dt><strong>保留限制</strong></dt>
	<dd>可在環境的所有應用程式中保留的記憶體總數。</dd>
	<dt><strong>配額總計</strong></dt>
	<dd>所有組織中的記憶體配額總計。</dd>
	</dl>
	**附註**：每隔 4 小時會自動重新整理資料。如果您要先重新整理頁面上的資料，再自動更新資料，請按一下**重新計算**。

- 組織記憶體用量。本區段詳述組織層次的記憶體用量。您可以檢視記憶體配額總計、保留的配額，以及每一個組織所使用的實體記憶體。圖表會提供依每個組織的最高保留記憶體列出的資訊，並且預設會先列出保留最大量記憶體的組織。您可以依**最高記憶體用量**及**超額記憶體配置**來排序。

	<dl>
	<dt><strong>最高記憶體用量</strong></dt>
	<dd>使用此選項，可識別已保留最大量記憶體的組織。依最高記憶體用量排序，可識別已保留最大量記憶體的組織。清單是依保留配額進行排序。</dd>
	<dt><strong>超額記憶體配置</strong></dt>
	<dd>使用此選項，可識別記憶體配額總計大於所需配額的組織。依超額記憶體用量排序，可識別哪些組織針對已配置給組織的配額，使用最少量的記憶體。</dd>
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
- 若要檢視組織的配額方案及用量，請按一下清單中的組織名稱。在所選取組織的**管理組織**頁面上，您可以檢視下列使用資訊：

  - 目前使用中的服務數目。
  - 目前使用中的路徑數目。
  - 記憶體配額圖，顯示已使用的配額量以及目前未使用的配額量。
  - 應用程式配置圖，顯示已用記憶體配額中所含的應用程式。
  - 計量應用程式用量圖，顯示每個已部署應用程式的已用 GB-小時的三個月報告。您可以選取**清單視圖**，以查看所有應用程式的資料（包括，每個應用程式的記憶體配置，以及過去三個月的計量 GB-小時用量）。

- 若要編輯組織名稱，以及新增或移除管理員，請按一下清單中的組織名稱，並遵循畫面上的提示。

## 管理使用者及許可權
{: #oc_useradmin}

您可以新增單一使用者或使用者群組。通常會透過「輕量型目錄存取通訊協定 (LDAP)」，從您公司的使用者登錄，將使用者新增至 {{site.data.keyword.Bluemix_notm}} 實例。您也可以檢視使用者許可權。如果您已獲指派**超級使用者**許可權，則也可以設定及管理其他使用者的許可權。按一下**管理 &gt; 使用者管理**。

「使用者管理」頁面會顯示本端或專用實例的所有使用者。每一位使用者的許可權會以圖示顯示在表格中。許可權可以是下列各項：無、**超級使用者**、**基本存取**、**型錄**、**報告**及**使用者**。**超級使用者**及**基本存取**許可權可以設為**開啟**或**關閉**，其餘的許可權則是以特定存取類型來啟用或停用，包括該許可權的**讀取**或**寫入**存取權，以圖示表示。如需每一種類型的說明以及圖示的說明，請參閱[許可權](#permissions)。

### 處理使用者

依據您對使用者許可權的**讀取**或**寫入**存取權，您可以個別或依群組搜尋現有使用者、移除使用者，以及新增使用者。如果您有**超級使用者**許可權，則表示您有完整存取權可以在該環境中完成管理使用者的任何作業。請檢閱下列使用者管理作業，以及完成每一個作業所需的存取層次：

* 尋找使用者。如果您有**讀取**或**寫入**存取權，並且知道完整或局部使用者名稱，則可以使用**搜尋**欄位在表格中尋找使用者。您也可以依組織及許可權來過濾使用者清單。若要過濾使用者清單，請完成下列步驟：
  <ol>
  <li>按一下<strong>過濾</strong>。</li>
  <li> 根據您要使用的過濾依據，按一下<strong>組織</strong>或<strong>許可權</strong>。
<dl>
	<dt><strong>組織</strong></dt>
	<dd>若要依組織來過濾使用者，請開始在<strong>組織</strong>欄位中鍵入組織名稱，並從清單中選取組織。然後選取指派給組織內使用者的一個以上角色。</dd>
	<dt><strong>許可權</strong></dt>
	<dd>若要依許可權來過濾使用者，請先選取一個以上的使用者類型。例如，您可能要查看所有「超級使用者」。對於<strong>超級使用者</strong>或<strong>基本存取</strong>以外的許可權，您也可以選取存取權類型（例如<strong>讀取</strong>或<strong>寫入</strong>）。</dd>
	</dl></li>
  <li>按一下<strong>套用</strong>。</li>
   </ol>

   「使用者管理」視窗會顯示您設定的過濾器，以及指定的過濾器所產生的使用者。您接著可以在已過濾的表格中搜尋使用者。您也可以從清單中移除過濾選項，來修改所指定過濾器的清單。

* 新增單一使用者。如果您有**超級使用者**許可權，或具有**寫入**存取權的**使用者**許可權，則可以新增使用者。

  1. 若要從 LDAP 目錄新增單一使用者，請按一下**新增使用者**。
  2. 在**搜尋**欄位中，鍵入使用者的電子郵件位址，然後從移入的清單中選取使用者。
  3. 接下來，從**組織**欄位中，輸入組織名稱並從移入的清單中選取組織，以選擇您要新增使用者的組織。
  4. 若要將使用者新增至選取的組織，請按一下**新增使用者**。

  **附註**：新增作業成功時，使用者即會新增至表格中，以供您檢視及搜尋。新增使用者時，他們不具有任何指派權限。

* 從 LDAP 目錄新增一組使用者。如果您有**超級使用者**許可權，或具有**寫入**存取權的**使用者**許可權，則可以新增使用者。

  1. 按一下**新增使用者群組**。
  2. 在**搜尋**欄位中，鍵入要搜尋的群組名稱，然後從移入的清單中選取群組名稱。
  3. 接下來，從**組織**欄位中，輸入組織名稱並從移入的清單中選取組織，以選擇您要新增使用者群組的組織。
  4. 若要將使用者群組新增至選取的組織，請按一下**新增使用者**。
  

  **附註**：超過 50 位使用者的群組會透過背景批次工作來新增。新增作業成功完成時，使用者或群組即會新增至表格中，以供您檢視及搜尋。新增使用者時，他們不具有任何指派權限。

* 匯入試算表，來新增一組使用者，該試算表包含使用者 ID、使用者電子郵件位址，以及您計劃要新增使用者的組織。如果您有**超級使用者**許可權，或具有**寫入**存取權的**使用者**許可權，則可以新增使用者。

**附註**：輸入符合使用者登錄中所使用值的使用者 ID。

  1. 按一下**匯入使用者**。
  2. 按一下**下載範本 (.CSV)**，以下載具有您可填寫之必要直欄的試算表，或者您可以使用包含下列必要直欄標頭的試算表來建立您自己的試算表：**使用者 ID**、**電子郵件**和**組織**。範本中還包含兩個選用性直欄：**名字**和**姓氏**。
  3. 填寫必要直欄的使用者值。如果您沒有使用 LDAP 目錄，請為您所匯入的使用者使用必要和選用的直欄標頭。
  4. 儲存檔案，然後按一下**上傳檔案**。

  **附註**：只要您有所有必要直欄，試算表內的直欄可以是任意順序。如果匯入成功，您會收到確認訊息，指出已新增所有使用者。如果部分使用者的匯入成功，但無法匯入某些使用者，請檢閱錯誤訊息，以對無法新增的使用者採取動作。

* 移除使用者。如果您有**超級使用者**許可權，或具有**寫入**存取權的**使用者**許可權，則可以將使用者從該環境中永久移除。

    1. 找出使用者，然後按一下 ![刪除](images/icon_trash.svg) 圖示。
    2. 按一下**移除**。

* 若要編輯使用者所屬的許可權和組織，您必須要有**超級使用者**許可權。若要編輯使用者的許可權，請找出使用者，然後按一下使用者名稱。從**編輯使用者**頁面中，您可以啟用或停用許可權：

    * 從清單中選取**開啟**，以啟用**超級使用者**或**基本存取**許可權。
    * 從清單中選取**讀取**，讓使用者擁有該許可權的**讀取**（唯讀）存取權，或選取**寫入**，讓使用者擁有該許可權的**寫入**（編輯、新增及移除）存取權。
    * 選取**關閉**以停用任何許可權。

    **附註**：將**超級使用者**許可權設為**開啟**時，會將所有其他許可權都設為具有**寫入**存取權。

* 若要在特定組織中新增或移除使用者，您必須要有**超級使用者**許可權，或具有**寫入**存取權的**使用者**許可權。

    1. 若要將使用者新增至組織，請從表格中選取使用者名稱，以存取**編輯使用者**頁面。然後，使用搜尋欄位來找出組織，並從清單中選取組織，然後按一下**儲存**。
    2. 若要從組織移除使用者，請從表格中選取使用者名稱，以存取**編輯使用者**頁面。然後，針對您要移除使用者的組織，按一下 ![移除](images/icon_remove.svg)，然後按一下**儲存**。

### 許可權
{: #permissions}

使用者可獲指派下列許可權，這些許可權具有可讓使用者在管理主控台內完成特定作業的特定存取層次（讀取或寫入）。

*表 7. 許可權*

| **使用者許可權** | **說明** |       
|-----------------|-------------------|
| 超級使用者 | **超級使用者**許可權設為**開啟**的使用者，可以編輯其他使用者的許可權。如果這個許可權設為開啟，即會自動啟用對所有其他許可權的完整存取權。除了此表格中針對各項許可權所描述的作業之外，它們還可以設定事件訂閱來直接取得維護或偶發事件的警示、排定維護、對主控台元件執行驗證檢查，以及為該環境建立組織和空間。此許可權相當於管理主控台的管理者 (admin) 角色。  |
| 基本存取 | **基本存取**許可權設為**開啟**的使用者，可以看到 {{site.data.keyword.Bluemix_notm}} 使用者介面中的「管理」頁面選項。啟用該許可權的使用者，可以存取[系統資訊](#oc_system)和[資源用量](#oc_resource)磚。如果沒有此許可權，使用者就無法查看或存取「管理」功能表選項。此許可權相當於管理主控台的管理者 (admin) 角色。此許可權相當於管理主控台的先前使用登入許可權。 |
| 型錄 | 具有**型錄**許可權的使用者，可獲指派對本端或專用實例中之可用服務進行**讀取**或**寫入**（修改）的存取權。讀取存取權可讓使用者存取「型錄管理」磚來檢視可用的服務。寫入存取權可讓使用者存取[型錄管理](#oc_catalog)磚來檢視服務、編輯服務的可見性、登錄自訂服務，以及控制建置套件優先順序清單。 |  
| 報告 | 具有**報告**許可權的使用者，可獲指派對安全報告進行**讀取**或**寫入**（修改）的存取權。讀取存取權可讓使用者存取「報告和日誌」磚來下載報告。寫入存取權可讓使用者檢視[報告和日誌](#oc_report)磚，也可以使用 CLI 來上傳新的報告，以及建立新的種類，以供使用者存取。 |
| 使用者 | 具有**使用者**許可權的使用者，可獲指派**讀取**（檢視）使用者清單或是**寫入**（新增或移除）使用者的存取權。此許可權不容許您設定其他使用者的許可權。寫入存取權可讓使用者新增使用者至環境中、從環境刪除使用者，以及將現有的使用者新增至環境中已存在的組織。此外，**寫入**存取權還可讓使用者新增組織、刪除組織，以及編輯組織中的使用者。 |


## 使用 Admin REST API 管理使用者
{: #usingadminapi}

您可以使用 `Admin` REST API 來新增及移除 {{site.data.keyword.Bluemix_notm}} 實例的使用者。`Admin` REST API 端點及 JSON 回應是基於實驗性所提供，以從指令行啟用基本作業。此資訊中範例內的端點及 URL，可能會在通知之後很快就變更或停止使用。

下列工具是利用下面範例的必要條件。您也可以選擇使用其他工具。
* cURL，用來以指令方式輸入 REST API 要求。cURL 是一種免費公用程式，您可以用來透過指令行介面，將 HTTP 要求傳送給伺服器，以及接收伺服器回應。您可以從 [cURL 下載網站](http://curl.haxx.se/download.html){: new_window}下載 cURL。
* Python，用來使用 Python 細緻列印 JSON 工具。這個選用性的工具會以 JSON 文字為輸入，並提供易讀的輸出。您可以從 [Python 下載網站](https://www.python.org/downloads){: new_window}下載 Python。

### 登入管理主控台

您必須登入「管理主控台」，才能執行任何 `Admin` API 要求。如果您有**超級使用者**許可權，或具有**寫入**存取權的**使用者**許可權，則可以新增或移除使用者。您必須具有**超級使用者**許可權，才能編輯其他使用者的許可權。

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
<dd class="pd">傳送「接受」標頭。</dd>

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

新增使用者時，您必須指定組織。您可以使用 `Admin` REST API 來列出所有組織。您必須擁有具**讀取**存取權的**使用者**許可權，才能列出組織。若要列出所有組織，請執行下列指令：

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/organizations | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">將先前使用 <samp class="ph codeph">-c</samp> 選項儲存在檔案中的使用者 ID 及密碼，以 Cookie 方式傳遞給 HTTP 伺服器。</dd>

</dl>

針對每一個組織，結果會包含下列資訊：
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

您可以利用 `Admin` REST API 列出已登錄使用者，以判斷使用者是否已新增至您的 {{site.data.keyword.Bluemix_notm}} 環境。您必須擁有具**讀取**存取權的**使用者**許可權，才能列出已登錄使用者。若要列出所有使用者，請執行下列指令：

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">將先前使用 <samp class="ph codeph">-c</samp> 選項儲存在檔案中的使用者 ID 及密碼，以 Cookie 方式傳遞給 HTTP 伺服器。</dd>
</dl>

針對每一位已登錄使用者，結果會包含下列資訊：
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

您可以使用 `Admin` REST API，將使用者新增至 {{site.data.keyword.Bluemix_notm}} 實例。您必須擁有具**寫入**存取權的**使用者**許可權才能新增使用者，或管理主控台的**超級使用者**許可權 (ops.admin)。此外，Admin 還可以容許沒有一般管理主控台 `user` 或 `superuser` 許可權的組織成員，只將新的使用者新增至其組織。請使用下列 API 指令，讓組織管理者具有此特定功能：

```
PUT console.<subdomain>.bluemix.net/codi/env_config/allow_managers?flag=<TRUE or FALSE>
```
{: screen}

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
<li>執行下列指令，以將 JSON 檔案內容公佈到使用者的端點：<br/><br/>
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

您可以使用 `Admin` REST API，從 {{site.data.keyword.Bluemix_notm}} 實例移除使用者。您必須擁有具**寫入**存取權的**使用者**許可權，才能移除使用者。

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

| **名稱** | **說明** |
|-----------------|-------------------|
| name | 服務分配管理系統的名稱。 |
| auth_username | 用於與服務分配管理系統連接的使用者名稱。 |
| auth_password | 用於與服務分配管理系統連接的密碼。 |
| broker_url | 用於連接服務分配管理系統的 URL。 |
| owningOrganization | 將服務列入白名單時要使用的起始組織。 |

*表 8. 欄位*

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
  "entity": {"name": "Service broker's name",
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

| **名稱** | **說明** |
|-----------------|-------------------|
| name | 服務分配管理系統的名稱。此名稱是建立服務時使用的名稱，無法變更。 |
| auth_username | 用於與服務分配管理系統連接的使用者名稱。 |
| auth_password | 用於與服務分配管理系統連接的密碼。 |
| broker_url | 用於連接服務分配管理系統的 URL。 |
| owningOrganization | 將服務列入白名單時要使用的起始組織。 |

*表 9. 欄位*

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
  "entity": {"name": "Service Broker's name",
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

| **名稱** | **說明** |
|-----------------|-------------------|
| name | 服務分配管理系統的名稱。此名稱是建立服務時使用的名稱，無法變更。 |

*表 10. 參數*

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

**附註**：如果您先前已安裝 {{site.data.keyword.Bluemix_notm}} 管理外掛程式，則可能需要解除安裝外掛程式、刪除儲存庫，然後重新安裝以取得最新更新。

完成下列步驟以新增儲存庫並安裝外掛程式：

<ol>
<li>若要新增 {{site.data.keyword.Bluemix_notm}} 管理外掛程式儲存庫，請執行下列指令：<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://console.&lt;subdomain&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">您的 {{site.data.keyword.Bluemix_notm}} 實例 URL 的子網域。</dd>
</dl>
</li>
<li>若要安裝 {{site.data.keyword.Bluemix_notm}} 管理 CLI 外掛程式，請執行下列指令：<br/><br/>
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
