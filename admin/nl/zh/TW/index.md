{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

#管理 {{site.data.keyword.Bluemix_notm}}
{: #administer}
*前次更新：2015 年 11 月 18 日*

按一下**帳戶及支援** &gt; **管理組織**，以管理您的組織、空間及已指派的使用者。如果您是「{{site.data.keyword.Bluemix_notm}} 本端」或「{{site.data.keyword.Bluemix_notm}} 專用」使用者，請參閱[管理 {{site.data.keyword.Bluemix_notm}} 本端及 {{site.data.keyword.Bluemix_notm}} 專用](index.html#mng)，以取得管理本端或專用實例的相關資訊。
{:shortdesc}

##管理帳戶
{: #mngacct}

在 {{site.data.keyword.Bluemix}} 中，您可以從使用者介面中的儀表板來管理組織及空間（包括使用者存取）。您也可以監視使用情形及計費。{:shortdesc}

###組織及空間
{: #orgsandspaces}

身為組織管理員或帳戶擁有者，您可以使用「管理組織」頁面來檢視及管理組織或空間的設定（包括使用者存取）。若要開啟「管理組織」頁面，請移至功能表上的*帳戶及支援* &gt; **管理組織**。

####組織

組織是依下列項目所定義：

<dl>
<dt>Users</dt>
<dd>組織及空間中具有基本許可權的角色。您必須先被指派給組織，才能獲授與組織內空間的其他許可權。如需詳細資訊，請參閱[使用者及角色](index.html#userroles)。</dd>
<dt>網域</dt>
<dd>提供網際網路上配置給組織的路徑。
路徑具有一個子網域及一個網域。子網域一般是應用程式名稱。網域可能是系統網域，或您針對應用程式所登錄的自訂網域。<br/>
<p>**附註**：如果您新增自訂網域，則必須配置 DNS 伺服器來解析自訂網域，以指向 {{site.data.keyword.Bluemix_notm}} 系統網域。使用此方式，{{site.data.keyword.Bluemix_notm}} 接收到您自訂網域的要求時，可以將它適當地遞送至您的應用程式。</p></dd>
<dt>配額</dt>
<dd>代表組織的資源限制，包括可配置供組織使用的服務數目及記憶體數量。建立組織時，會指派配額。組織空間中的任何應用程式或服務都會對配額使用情形有所貢獻。使用隨收隨付制或訂閱方案，您可以在組織需要變更時，調整
Cloud Foundry 應用程式及儲存器的配額。
</dd>
</dl>

在 {{site.data.keyword.Bluemix_notm}} 中，您可以使用組織來啟用使用者之間的協同作業，以及使用下列方式促進專案資源的邏輯分組：

<ul>
<li>您可以將組織中的一組空間、應用程式、服務、網域、路徑及使用者群組在一起。</li>
<li>您可以根據每位使用者管理空間及組織的存取權。</li>
</ul>

建立組織時，組織名稱在 {{site.data.keyword.Bluemix_notm}} 內必須是唯一的。
在您建立組織之後，會將*組織管理員*許可權自動指派給您，以讓您編輯組織名稱、刪除組織，以及在組織中建立空間。

刪除組織時，會刪除組織內的所有空間、應用程式及服務。

{{site.data.keyword.Bluemix_notm}} 透過在組織及組織空間內指派使用者，以啟用專案的協同作業。您可以使用「**使用者**」標籤來顯示及管理組織的使用者。您也可以按一下**使用者**標籤上的**邀請新的使用者**鏈結來邀請使用者加入您的組織。下列許可權可以指派給組織中的使用者：

<ul>
<li>組織使用者</li>
<li>組織管理員</li>
<li>組織計費管理員</li>
<li>組織審核員</li>
</ul>

####空間

在組織內，您可以使用空間來群組一組應用程式、服務及使用者。

將使用者新增至組織之後，即可將組織內空間的許可權授與他們。與組織類似，空間也會有一組可以指派給使用者的許可權：

<ul>
<li>空間管理員</li>
<li>空間開發人員</li>
<li>空間審核員</li>
</ul>

**附註**：使用者必須至少獲指派空間中的一個許可權。

空間的**網域**標籤是指派給空間的唯讀網域清單。
空間一律可以使用系統網域，也可能會將自訂網域配置給空間。已在空間中建立的應用程式，可能會使用任何針對空間所列出的網域。

###使用者及角色
{: #userroles}

帳戶擁有者會對組織及空間執行所有作業。

####使用者類型

您可以是帳戶的成員或合作者。

<dl>
<dt>成員</dt>
<dd>如果您建立 {{site.data.keyword.Bluemix_notm}} 帳戶，或者受邀使用此帳戶，然後透過邀請進行註冊（這是第一個 {{site.data.keyword.Bluemix_notm}} 經驗），則您是帳戶的成員。</dd>
<dt>合作者</dt>
<dd>如果您先前搭配使用 {{site.data.keyword.Bluemix_notm}} 與不同的帳戶，但之後邀請您使用此帳戶，而您接受邀請，則您是 {{site.data.keyword.Bluemix_notm}} 帳戶的合作者。</dd>
</dl>

####使用者角色

使用者可以獲指派下列許可權，以取得組織或空間中的不同使用者角色：

<dl>
<dt>組織管理員</dt>
<dd>組織管理員具有下列許可權：<ul>
<li>在組織內建立或刪除空間。</li>
<li>如果您也是組織的成員或帳戶擁有者，則會邀請使用者加入組織。</li>
<li>管理已在組織中的現有使用者。</li>
<li>管理組織的網域。</li>
</ul>
<p>**附註**：如果您具有合作者使用者類型，並且先前搭配使用 {{site.data.keyword.Bluemix_notm}} 與不同的帳戶，則無法邀請使用者加入組織，即使您已獲指派組織管理員角色。您必須具有成員使用者類型才能邀請使用者。如需如何暫時解決此問題的相關資訊，請參閱<a href="../troubleshoot/accessing.html#tr_adduser">無法將使用者新增至組織</a>。</p>
</dd>
<dt>計費管理員</dt>
<dd>計費管理員具有許可權可檢視組織的執行時期及服務使用資訊。</dd>
<dt>組織審核員</dt>
<dd>組織審核員具有許可權可檢視空間中的應用程式及服務內容。</dd>
<dt>空間管理員</dt>
<dd>空間管理員具有下列許可權：
<ul>
<li>將使用者新增至空間，以及管理使用者。</li>
<li>啟用空間的特性</li>
</ul>
</dd>
<dt>空間開發人員</dt>
<dd>空間開發人員具有下列許可權：<ul>
<li>建立、刪除及管理空間內的應用程式和服務。</li>
<li>具有空間內日誌的存取權</li>
</ul>
</dd>
<dt>空間審核員</dt>
<dd>空間審核員具有空間的所有資訊（例如應用程式及服務、設定、報告和日誌的相關資訊）的唯讀存取權。</dd>
</dl>

###管理組織
{: #orgmng}

身為組織管理員或帳戶擁有者，您可以管理您的組織。
管理作業包括建立組織、將組織重新命名、建立空間、邀請使用者至空間，以及刪除現有的組織。


<ul>
<li>建立組織<p>只有具有付費帳戶的使用者可以建立組織。
使用付費帳戶，您可以採取下列步驟來建立組織：
</p>
<ol>
<li>移至 {{site.data.keyword.Bluemix_notm}}「儀表板」，按一下右上方的圖示，然後選取**管理組織**。</li>
<li>按一下**建立組織**，然後遵循提示以建立您的組織。</li>
</ol>
</li>
<li>將組織重新命名<p>採取下列步驟以將您的組織重新命名：</p>
<ol>
<li>移至 {{site.data.keyword.Bluemix_notm}}「儀表板」，按一下右上方的圖示，然後選取**管理組織**。</li>
<li>選取您要重新命名的組織。</li>
<li>在**組織**欄位中鍵入新名稱，然後按一下**儲存**。</li>
</ol>
</li>
<li>列出成員<p>採取下列步驟可列出您組織或空間的成員：</p>
<ol>
<li>移至 {{site.data.keyword.Bluemix_notm}}「儀表板」，按一下右上方的圖示，然後選取**管理組織**。您可以在**使用者**標籤中看到組織的成員及其角色。</li>
<li>按一下組織中的空間名稱，以查看此空間的成員及其角色。</li>
</ol>
</li>
<li>建立空間<p>您可以在組織中建立空間；例如，建立 *dev* 空間作為開發環境、*test*
空間作為測試環境，以及 *production* 空間作為正式作業環境。
然後，您可以將應用程式與空間相關聯。採取下列步驟以建立空間：</p>
<ol>
<li>移至 {{site.data.keyword.Bluemix_notm}}「儀表板」，按一下右上方的圖示，然後選取**管理組織**。</li>
<li>在您的組織名稱底下按一下**建立空間**，然後遵循提示以建立空間。</li>
</ol>
</li>
<li>邀請使用者至空間<p>您可以邀請使用者到您的組織來擔任合作者。
您也可以將您組織的使用者新增到不同空間。
使用者只能存取他們已加入的空間。
採取下列步驟以新增使用者至空間：</p>
<ol>
<li>移至 {{site.data.keyword.Bluemix_notm}}「儀表板」，按一下右上方的圖示，然後選取**管理組織**。然後，在您的組織中按一下**新增使用者**，並遵循提示以新增使用者至您的組織。</li>
<li>新增使用者至空間。從左導覽窗格選取空間、按一下**新增使用者**，並遵循提示以新增使用者至您的組織。
</li>
</ol>
</li>
<li>刪除現有的組織<p>請與 {{site.data.keyword.Bluemix_notm}} 登錄及 ID 支援聯絡，以刪除您的組織。</p>
<p>**附註**：刪除作業無法回復。您會遺失與組織相關聯的所有應用程式和服務。
</p>
</li>
</ul>

## 管理 {{site.data.keyword.Bluemix_notm}} 本端及 {{site.data.keyword.Bluemix_notm}} 專用
{: #mng}

使用「管理主控台」來管理資源、監視使用情形、管理使用者許可權，以及檢視您「{{site.data.keyword.Bluemix}} 本端」或「Bluemix 專用」環境中的安全報告、日誌、狀態及升級通知。{:shortdesc}

### 存取管理主控台
{: #oc_access}

您可以輸入下列 URL 來存取「管理主控台」：

`https://opsconsole.&lt;subdomain&gt;.bluemix.net/`。

<dl>
<dt><strong>&lt;subdomain&gt;</strong></dt>
<dd>此值為本端或專用實例的名稱。{{site.data.keyword.Bluemix}} 實例的子網域名稱是在上線期間指派的。</dd>
</dl>

### 檢視系統資訊
{: #oc_system}

使用「管理主控台」，可監視您的系統資訊。

若要檢視系統資訊，請按一下**管理 &gt; 系統資訊**。

您可以展開並檢視有關擱置更新、一般系統資訊及 LDAP 配置詳細資料的各個區段。

* 在「更新」區段中，您可以檢視所有需要您採取動作的擱置更新。您也可以使用行事曆鏈結將排定的更新匯入至行事曆應用程式，來輕鬆地追蹤您的更新。

<ol>
<li>若要針對特定更新採取動作，請完成下列步驟：<ol type="a">
<li>按一下 <strong><em>Number</em> 個更新擱置</strong>，以檢視所有擱置更新。</li>
<li>選取更新，以採取動作或檢視更新的詳細資料，其中包括更新時間範圍、排定日期或服務中斷狀態。</li>
<li>按一下<strong>設定無法使用的日期</strong>，以設定更新時間範圍中不方便套用更新的特定日期。如果您已設定無法使用的日期，IBM 會根據您的選擇來核准及排定更新。在核准及排定更新時，您會收到通知。</li>
<li>如果您沒有任何無法使用的日期，請按一下<strong>核准</strong>來核准更新。如果您核准，則會在排定的更新時間範圍期間套用更新。IBM 會在更新部署開始及結束時傳送通知。</li>
</ol>
</li>
<li>若要將排定的更新匯入至您選擇的行事曆應用程式，請完成下列步驟：
<ol type="a">
<li>開啟行事曆應用程式。</li>
<li>將應用程式「系統資訊」頁面上所列的**行事曆 URL** 貼入，以匯入更新行事曆。或者，按一下「行事曆 URL」以下載行事曆檔案，然後利用 `.ics` 檔案將它匯入至行事曆應用程式。</li>
<li>輸入認證。</li>
<li>檢視您的已排定更新。</li>
</ol>
</li>
</ol>

* 在「一般資訊」區段中，您可以檢視下列資訊：
    * 關於 {{site.data.keyword.Bluemix_notm}} 建置的基本資訊。
    * API 資訊，包括版本、URL、地區，以及 CLI 文件的鏈結。
    * 關於系統及服務的共用網域資訊。
    * 關於應用程式、使用者及組織總數的統計資料。
* 在「LDAP 配置詳細資料」區段中，您可以選取 LDAP 伺服器，然後檢視使用者和群組對映的相關資訊。如果您是使用 {{site.data.keyword.IBM}} WebID，它會顯示在「LDAP 配置詳細資料」區段中。

### 檢視使用資訊
{: #oc_resource}

使用「管理主控台」，可監視資源及網路使用情形。

若要檢視資源資訊，請按一下**管理 &gt; 使用情形**。

在「資源監視」區段中，您可以檢視下列資訊：

* 資源使用資訊，例如已使用多少 GB 的記憶體及多少 GB 的磁碟空間。您可以檢視跨所有 Droplet Execution Agent (DEA) 的平均 CPU 使用率。按一下 **CPU** 磚，您可以查看每一個 DEA 的 CPU 使用率。第一個列出的是具有最高使用率的 DEA，而且每一個 DEA 都依其工作及 IP 位址來識別。CPU 使用率分為三個種類，包括系統處理程序中所花費的 CPU 量、使用者處理程序中所花費的 CPU 量，以及等待處理程序中所花費的 CPU 量。
* 過去一天、一週或一個月之進出頻寬的網路使用資訊。顯示的資料是根據公開及私密網路的輸入及輸出資料流量的總和。
* {{site.data.keyword.Bluemix_notm}} 在過去十分鐘、一小時及一天的平均回應時間。
* {{site.data.keyword.Bluemix_notm}} 在過去十分鐘、一小時及一天的每秒平均交易數。

### 檢視報告
{: #oc_report}

您可以檢視 {{site.data.keyword.Bluemix_notm}} 實例的安全報告及日誌（例如 DataPower&trade;、防火牆及登入審核）。

若要檢視報告及日誌，請按一下**管理 &gt; 報告及日誌**。

從下列選項中選取：

* 您可以從欄位中選取開始及結束日期，以過濾顯示的報告及日誌。
* 您可以從左導覽窗格中展開及檢視各種報告。
* 您可以在報告及日誌的集合中進行搜尋。搜尋適用於報告名稱，也適用於報告及日誌內包含的文字內容。您也可以選擇依**管理事件**、**DataPower 報告**、**防火牆**及**登入審核**來過濾您的搜尋。
* 顯示報告或日誌時，您可以按一下報告右上角的 ![下載](images/icon_download.png) 圖示予以下載。

### 檢視狀態
{: #oc_status}

您可以透過「管理主控台」，來監視 {{site.data.keyword.Bluemix_notm}} 實例的狀態。您也可以訂閱 RSS 資訊來源以取得通知，這樣就不必查看是否有通知。

若要檢視 {{site.data.keyword.Bluemix_notm}} 實例的狀態，請完成下列步驟：

1. 在「管理主控台」的右上角，按一下**設定檔設定**圖示。

2. 然後，按一下**狀態**。

即會顯示「系統狀態」頁面。左窗格會顯示跨地區的執行時期和服務以及 {{site.data.keyword.Bluemix_notm}} 實例的狀態。右窗格則顯示通知。

3. 如果您已針對 RSS 資訊來源配置瀏覽器，則可以訂閱通知的 RSS 資訊來源。在通知清單左上角的**更新**右側，找出 ![RSS](images/icon_RSS.png) 圖示，然後選取下列其中一個動作：

* 將 ![RSS](images/icon_RSS.png) 圖示拖曳到您的 RSS 閱讀器。
* 在 RSS 圖示上按一下滑鼠右鍵、選取**複製鏈結位址**，然後將 URL 貼入您的 RSS 閱讀器。

4. 過濾要顯示的通知。按一下通知清單右上角的**過濾**。然後，鍵入您預期會在通知中找到的單字，例如 "maintenance"，以搜尋通知清單並縮小範圍。或者，您可以按一下以選取要依**類型**、**地區**、**種類**、**開始日期**或**結束日期**顯示的通知。

### 管理型錄
{: #oc_catalog}

您可以管理使用者可在 {{site.data.keyword.Bluemix_notm}} 的「型錄」中看到哪些 {{site.data.keyword.Bluemix_notm}} 服務及入門範本。

若要使用「管理主控台」來管理「型錄」，請按一下**管理 &gt; 型錄管理**。

選取服務或入門範本磚，以編輯服務或入門範本方案可見性。若要編輯可見性，請從下列選項中選取：
* 若要顯示隱藏的服務或入門範本，讓您的使用者能在「型錄」中看到它，請選取**啟用所有方案**。
* 若要隱藏服務或入門範本，讓您的使用者在 {{site.data.keyword.Bluemix_notm}} 的「型錄」中看不到它，請選取**停用所有方案**。
* 若要控制個別方案的可見性，請選取方案名稱，然後使用下拉功能表，選取**針對所有組織啟用**、**針對所有組織停用**或**針對特定組織啟用方案**。

### 管理組織
{: #oc_organizations}

您可以透過建立及刪除組織、將管理員新增至組織，以及監視配額用量，來管理您的組織。

若要使用「管理主控台」來管理您的組織，請按一下**管理 &gt; 組織管理**。

您可以展開及檢視各個區段。您也可以檢閱及管理組織的配額方案。

* 若要建立新的組織並新增管理員，請按一下<strong>建立組織</strong>。請輸入組織的名稱，然後輸入您要新增為管理員的人員名稱或電子郵件。您可以輸入並選取多個名稱，來新增多位管理員。按一下<strong>建立組織</strong>，以儲存變更並建立組織。
* 在「配額監視」區段中，您可以展開區段並檢視下列資訊：
    * 環境記憶體用量。此區段詳述完整系統環境的記憶體用量。圖表提供的資訊包括已使用的系統記憶體、系統記憶體總計、已使用的配額，以及已配置的配額總計。下列術語清單定義圖表中顯示的記憶體用量的類型。
	<dl>
	<dt><strong>已使用的系統記憶體</strong></dt>
	<dd>您環境所使用的實體記憶體。</dd>
	<dt><strong>系統記憶體總計</strong></dt>
	<dd>可供您環境使用的實體記憶體總計。</dd>
	<dt><strong>已部署的配額</strong></dt>
	<dd>在所有組織中，配置給所有已部署應用程式的記憶體總和。已部署的配額總和可超出您環境的實體系統記憶體總計。例如，如果您的系統記憶體總計為 16 GB，而且您已對每一個組織（總共有五個不同的組織）各配置 4 GB 的記憶體，則配額總計超出了已針對所有組織配置給您的系統記憶體總計。不過，在許多情況下，組織可能不會使用到個別配置給每個組織的配額總計。此外，所有組織也可能不會同時間用到其配置的記憶體配額總計。</dd>
	<dt><strong>配額總計</strong></dt>
	<dd>在所有組織中的已配置記憶體總計。</dd>
	</dl>
	* 組織記憶體用量。本區段詳述組織層次的記憶體用量。您可以檢視配額額度總計，以及針對每一個組織所部署的配額。圖表會提供依每個組織的最高記憶體用量列出的資訊，依預設，使用最大量記憶體的組織會最先列出。您可以依**最高記憶體用量**及**超額記憶體配置**來排序。
	<dl>
	<dt><strong>最高記憶體用量</strong></dt>
	<dd>使用此選項，可識別使用最大量記憶體的組織。依最高記憶體用量排序，可識別使用最大量記憶體的組織。清單是依已部署的配額來排序。</dd>
	<dt><strong>超額記憶體配置</strong></dt>
	<dd>使用此選項，可識別哪些組織的配額方案大於所需配額。	依超額記憶體用量排序，可識別哪些組織針對已配置給組織的配額，使用最少量的記憶體。</dd>
	</dl>
* 若要變更組織的配額方案，請按一下圖表中您要在「組織記憶體用量」區段中編輯之組織的長條，或從「組織清單」區段中選取組織的名稱。在「編輯組織」頁面上，您可以變更配額方案、變更組織名稱，以及新增或移除管理員。如果您選取的配額方案不足以提供組織的現行用量，則會收到一則訊息。若要儲存您在「編輯組織」頁面上所做的任何變更，請按一下**儲存**。
* 在「組織清單」區段中，您可以檢視 {{site.data.keyword.Bluemix_notm}} 環境中的所有組織。
	* 若要刪除組織，請在「動作」直欄中按一下 ![刪除](images/icon_trash.png)。
	* 若要檢視及編輯組織的配額方案，請按一下清單中組織的名稱。
	* 若要編輯組織名稱，以及新增或移除管理員，請按一下清單中組織的名稱。

### 管理使用者及許可權
{: #oc_useradmin}
您可以透過 LDAP 將使用者從公司的使用者登錄新增至 {{site.data.keyword.Bluemix_notm}} 實例。您可以新增單一使用者或使用者群組，並且檢視使用者許可權。如果您已獲指派 `admin` 許可權，則同時可以設定及管理其他使用者的許可權。

若要使用「管理主控台」來管理使用者，請按一下**管理 &gt; 使用者管理**。

「使用者管理」頁面會顯示本端或專用實例的所有使用者。顯示每一位使用者的許可權。許可權可以為下列項目：None、`Admin`、`Catalog`、`Login`、`Reports`
及 `Users`。可以啟用許可權，或是可以授與使用者該許可權的
`view` 或 `write` 能力，如圖示所代表。
如需每一種類型的說明以及圖示的說明，請參閱[許可權](#permissions)。

從下列選項中選擇：
* 找出使用者。您可以利用位於頂端的**搜尋**欄位，在表格中找出使用者。
* 新增使用者。如果您具有 `admin` 許可權，或具有 `write` 能力的 `users` 許可權，則可以新增使用者。若要新增使用者或使用者群組，請按一下**新增一位使用者**或**新增使用者群組**。在**搜尋**欄位中，鍵入要搜尋的使用者名稱或群組名稱，然後從**組織**清單中，選取要將使用者或使用者群組新增到哪個組織。找到要新增的使用者或群組時，請按一下使用者名稱，然後按一下**新增使用者**或**新增多位使用者**來進行新增。超過 50
位使用者的群組會透過背景批次工作來新增。新增作業成功完成時，使用者或群組即會新增至表格中，以供您檢視及搜尋。新增使用者時，他們不具有任何指派權限。
* 編輯許可權及組織。如果您具有 `admin` 許可權，即可編輯其他使用者的許可權及組織。若要編輯許可權，請找出使用者，然後按一下使用者名稱。若要啟用或停用許可權，請在開啟的視窗中，從下列選項進行選取：
	* 從清單中選取**開啟**，以啟用許可權。
	* 從清單中選取**讀取**，以容許使用者具有該許可權的 `view`（唯讀）能力，或選取**寫入**，以容許使用者具有該許可權的 `write`（編輯、新增及移除）能力。
	* 選取**關閉**以停用許可權。若要編輯組織，請從下列選項中選取：
	* 利用搜尋欄位以找出組織、按一下以從選項中進行選取，然後按一下**新增**，以將使用者新增至組織。
	* 按一下 ![移除，以減號代表](images/icon_remove.png) 圖示，以移除組織中的使用者。完成時，請按一下**儲存**。
* 移除使用者。如果您具有 `admin` 許可權，或具有 `write` 能力的 `users` 許可權，則可以移除使用者。若要移除使用者，請找出使用者、按一下 ![刪除](images/icon_trash.png) 圖示，然後再按一下**移除**。

#### 許可權
{: #permissions}

使用者可獲指派下列許可權：

| **使用者許可權** | **說明** |
|-----------------|-------------------|
| Admin | 具有 `admin` 許可權的使用者，可編輯其他使用者的許可權。 |
| Catalog | 具有 `catalog` 許可權的使用者，可獲指派對本端或專用實例中可用服務進行 `view` 或 `write`（修改）的能力。 |
| Login | 具有 `login` 許可權的使用者，可登入「管理主控台」。如果沒有此許可權，使用者即無法登入。 |
| Reports | 具有 `reports` 許可權的使用者，可獲指派對安全報告進行 `view` 或 `write`（修改）的能力。 |
| Users | 具有 `users` 許可權的使用者，可獲指派對使用者清單進行 `view`，或對使用者進行 `write`（新增或移除）的能力。此許可權不容許您設定其他使用者的許可權。|

*表 1. 許可權*

可以啟用許可權，或是可以授與使用者該許可權的
`view` 或 `write` 能力，如下列圖示所代表：


* 許可權旁的 ![已啟用，以勾號代表](images/icon_enabled.png) 圖示表示已啟用。
* ![檢視，以眼睛代表](images/icon_read.png) 圖示表示使用者具有該許可權的 `view`（唯讀）能力。
* ![寫入，以鉛筆代表](images/icon_write.png) 圖示表示使用者具有該許可權的 `write`（編輯、新增或移除）能力。

### 使用 Admin REST API 管理使用者
{: #usingadminapi}

您可以使用 `Admin` REST API 來新增及移除 {{site.data.keyword.Bluemix_notm}} 實例的使用者。`Admin` REST API 端點及 JSON 回應是基於實驗性所提供，以從指令行啟用基本作業。此資訊中範例內的端點及 URL，可能會在通知之後很快就變更或停止使用。

下列工具是利用下面範例的必備項目。您也可以選擇使用其他工具。
* cURL，用來以指令方式輸入 REST API 要求。cURL 是一種免費公用程式，您可以用來透過指令行介面，將 HTTP 要求傳送給伺服器，以及接收伺服器回應。您可以從 [cURL 下載網站](http://curl.haxx.se/download.html){: new_window}下載 cURL。
* Python，用來使用 Python pretty-print JSON 工具。這個選用性的工具會以 JSON 文字為輸入，並提供易讀的輸出。您可以從 [Python 下載網站](https://www.python.org/downloads){: new_window}下載 Python。

#### 登入管理主控台

您必須登入「管理主控台」，才能執行任何 `Admin` API 要求。如果您具有 `admin` 許可權，或具有 `write` 能力的 `users` 許可權，則可以新增或移除使用者。您必須具有 `admin` 許可權，才能編輯其他使用者的許可權。

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

下列範例顯示此指令的輸出：```
{
    "message": "Logged in",
    "name": {
        "familyName": "*last_name*",
        "givenName": "*first_name*"
    }
}
```
{: screen}

#### 列出組織
{: #listingorg}

新增使用者時，您必須指定組織。您可以使用 `Admin` REST API 來列出所有組織。您必須有具有 `read` 能力的 `users` 許可權，才能列出組織。若要列出所有組織，請執行下列指令：

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/organizations | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">將先前使用 <samp class="ph codeph">-c</samp> 選項儲存在檔案中的使用者 ID 及密碼，以 Cookie 方式傳遞給 HTTP 伺服器。</dd>

</dl>

針對每一個組織，結果會包括下列資訊：
* `"guid"`，組織的 GUID
* `"name"`，組織的名稱

下列範例顯示此指令的輸出：```
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

#### 列出使用者
{: #listingusr}

您可以利用 `Admin` REST API 列出已登錄使用者，以判斷使用者是否已新增至您的 {{site.data.keyword.Bluemix_notm}} 環境。您必須有具有 `read` 能力的
`users` 許可權，才能列出已登錄使用者。若要列出所有使用者，請執行下列指令：

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

#### 新增使用者

您可以使用 `Admin` REST API，將使用者新增至 {{site.data.keyword.Bluemix_notm}} 實例。您必須有具有 `write` 能力的
`users` 許可權，才能新增使用者。

您可以新增一位使用者或一份使用者清單。您可以將使用者新增至單一組織或多個組織。-->若要新增使用者，您必須提供下列資訊：

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
<code>
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
</code><br/><br/>
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
 &lt; HTTP/1.1 201 Created
 &lt; x-powered-by: Express
 &lt; vary: X-HTTP-Method-Override
 &lt; content-type: application/json
 &lt; date: Wed, 22 Apr 2015 19:32:54 GMT
 &lt; connection: close
 &lt; transfer-encoding: chunked
 &lt; X-Time_Check: Proxy Time: 5612 msec
 ```
{: screen}

#### 移除使用者

您可以使用 `Admin` REST API，從 {{site.data.keyword.Bluemix_notm}} 實例中移除使用者。您必須有具有 `write` 能力的
`users` 許可權，才能移除使用者。

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
 &gt; DELETE /codi/v1/users?user_id=exampleuser@domain.com HTTP/1.1
 &gt; User-Agent: curl/7.37.1
 &gt; Host: localhost:3000
 &gt; Accept: */*
 &gt; Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 &gt; 
 &lt; HTTP/1.1 201 Created
 &lt; x-powered-by: Express
 &lt; content-type: application/json
 &lt; date: Wed, 22 Apr 2015 21:01:09 GMT
 &lt; connection: close
 &lt; transfer-encoding: chunked
 &lt; X-Time_Check: Proxy Time: 1922 msec
 &lt; 
 ```
{: screen}

### 使用 cf CLI 管理使用者
{: #usingadmincli}

您可以利用 Cloud Foundry 指令行介面與「{{site.data.keyword.Bluemix_notm}} 管理 CLI」外掛程式搭配，來管理 {{site.data.keyword.Bluemix_notm}} 環境的使用者。例如，您可以從 LDAP 登錄新增使用者。

在開始之前，請先安裝 cf 指令行介面。{{site.data.keyword.Bluemix_notm}} 管理
CLI 外掛程式需要 cf 6.11.2 版或更新版本。[下載 Cloud Foundry 指令行介面](https://github.com/cloudfoundry/cli/releases){: new_window}

**限制：**Cygwin 不支援 Cloud Foundry 指令行介面。請在非 Cygwin 指令行視窗的指令行視窗中使用 Cloud Foundry 指令行介面。

#### 新增 {{site.data.keyword.Bluemix_notm}} 管理 CLI 外掛程式

安裝 cf 指令行介面之後，您可以新增 {{site.data.keyword.Bluemix_notm}} 管理
CLI 外掛程式。

完成下列步驟以新增儲存庫並安裝外掛程式：

<ol>
<li>若要新增 {{site.data.keyword.Bluemix_notm}} 管理外掛程式儲存庫，請執行下列指令：<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://opsconsole.&lt;subdomain&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">您的 {{site.data.keyword.Bluemix_notm}} 實例 URL 的子網域。</dd>
</dl>
</li>
<li>若要安裝「{{site.data.keyword.Bluemix_notm}} 管理 CLI」外掛程式，請執行下列指令：<br/><br/>
<code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

#### 使用 {{site.data.keyword.Bluemix_notm}} 管理 CLI 外掛程式

您可以使用 {{site.data.keyword.Bluemix_notm}} 管理 CLI 外掛程式來新增或移除使用者、指派或取消指派組織的使用者，以及執行其他管理作業。若要查看指令清單，請執行下列指令：


`cf plugins`
{: codeblock}

如需指令的其他說明，請使用 `--help` 選項。

#### 連接及登入 {{site.data.keyword.Bluemix_notm}}

您必須先連接並登入（如果尚未完成的話），才能使用管理 CLI 外掛程式來管理使用者。

<ol>
<li>若要連接至 {{site.data.keyword.Bluemix_notm}}> API 端點，請執行下列指令：<br/><br/>
<code>
cf api https://api.&lt;subdomain&gt;.bluemix.net
</code>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">您的 {{site.data.keyword.Bluemix_notm}} 實例 URL 的子網域。</dd>
</dl>
<p>您可以查看「管理主控台」的「資源及資訊」頁面，以取得正確的 URL。URL 顯示在「API 資訊」區段的 **API URL** 欄位中。</p>
</li>
<li>使用下列指令來登入 {{site.data.keyword.Bluemix_notm}}：<br/><br/>
<code>
cf login
</code>
</li>
</ol>

#### 新增使用者

您可以從 LDAP 登錄，將使用者新增至您的 {{site.data.keyword.Bluemix_notm}} 環境。請輸入下列指令：

`cf bluemix-admin-add-user <user_name> <organization>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">LDAP 登錄中的使用者名稱。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要新增使用者之 {{site.data.keyword.Bluemix_notm}} 組織的名稱或 GUID。</dd>
</dl>

**提示：**您也可以使用 **baau** 作為較長的 **bluemix-admin-add-user** 指令名稱的別名。

#### 移除使用者

您可以輸入下列指令，從您的 {{site.data.keyword.Bluemix_notm}} 環境中移除使用者：

`cf bluemix-admin-remove-user <user_name>`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中的使用者名稱。</dd>

</dl>

**提示：**您也可以使用 **baru** 作為較長的 **bluemix-admin-remove-user** 指令名稱的別名。

#### 新增及刪除組織

您可以新增及刪除組織。

* 若要新增組織，請輸入下列指令：

`cf Bluemix-admin-create-organization <organization> <manager>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要新增之 {{site.data.keyword.Bluemix_notm}} 組織的名稱或 GUID。</dd>
<dt class="pt dlterm">&lt;manager&gt;</dt>
<dd class="pd">組織管理員的使用者名稱。</dd>
</dl>

**提示：**您也可以使用 **baco** 作為較長的 **bluemix-admin-create-organization** 指令名稱的別名。

* 若要刪除組織，請輸入下列指令：

`cf Bluemix-admin-delete-organization <organization>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要刪除之 {{site.data.keyword.Bluemix_notm}} 組織的名稱或 GUID。</dd>
</dl>

**提示：**您也可以使用 **bado** 作為較長的 **bluemix-admin-create-organization** 指令名稱的別名。

#### 將使用者指派至組織

您可以將 {{site.data.keyword.Bluemix_notm}} 環境中的使用者指派給特定組織。請輸入下列指令：

`cf bluemix-admin-set-org <user_name> <organization> [<role>]`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中的使用者名稱。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要指派使用者之 {{site.data.keyword.Bluemix_notm}} 組織的名稱或 GUID。</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">請參閱[角色](#roles)，以取得 {{site.data.keyword.Bluemix_notm}} 使用者的角色及說明。</dd>
</dl>

**提示：**您也可以使用 **baso** 作為較長的 **bluemix-admin-set-org** 指令名稱的別名。

#### 從組織取消指派使用者

您可以從特定組織取消指派 {{site.data.keyword.Bluemix_notm}} 環境中的使用者。請輸入下列指令：

`cf bluemix-admin-unset-org <user_name> <organization> [<role>]`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中的使用者名稱。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要指派使用者之 {{site.data.keyword.Bluemix_notm}} 組織的名稱或 GUID。</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">請參閱[角色](#roles)，以取得 {{site.data.keyword.Bluemix_notm}} 使用者的角色及說明。</dd>
</dl>

**提示：**您也可以使用 **bauo** 作為較長的 **bluemix-admin-unset-org** 指令名稱的別名。

#### 角色

<dl class="parml">
<dt class="pt dlterm">OrgManager</dt>
<dd class="pd">組織管理員。組織管理員具有執行下列動作的權限：<ul>
<li>在組織內建立或刪除空間。</li>
<li>邀請使用者加入組織及管理使用者。</li>
<li>管理組織的網域。</li>
</ul>
</dd>
<dt class="pt dlterm">BillingManager</dt>
<dd class="pd">計費管理員。計費管理員可以檢視組織的執行時期及服務用量資訊。</dd>
<dt class="pt dlterm">OrgAuditor</dt>
<dd class="pd">組織審核員。組織審核員可以檢視空間中的應用程式及服務內容。</dd>
</dl>

#### 設定組織的配額

您可以設定特定組織的使用配額。

`cf bluemix-admin-set-quota <organization> <plan>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要設定配額之 {{site.data.keyword.Bluemix_notm}} 組織的名稱或 GUID。</dd>
<dt class="pt dlterm">&lt;plan&gt;</dt>
<dd class="pd">組織的配額方案。</dd>
</dl>

**提示：**您也可以使用 **basq** 作為較長的 **bluemix-admin-set-quota** 指令名稱的別名。

#### 新增、刪除及擷取報告

您可以新增、刪除及擷取安全報告。
* 若要新增報告，請輸入下列指令：

`cf bluemix-admin-add-report <category> <date> <PDF|TXT|LOG> <RTF>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">報告的種類。如果名稱中有空格，請使用引號括住該名稱。</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">報告日期，格式為 <samp class="ph codeph">YYYYMMDD</samp>。</dd>
<dt class="pt dlterm">&lt;PDF|TXT|LOG&gt;</dt>
<dd class="pd">要上傳之報告 PDF、文字檔或日誌檔的路徑。</dd>
<dt class="pt dlterm">&lt;RTF&gt;</dt>
<dd class="pd">用來包含 PDF 之「Rich Text 格式 (RTF)」版本的選項。只有在您包含報告 PDF 的路徑時，此選項才適用。RTF 版本用於編製索引及進行搜尋。</dd>
</dl>

**提示：**您也可以使用 **baar** 作為較長的 **bluemix-admin-add-report** 指令名稱的別名。

* 若要刪除報告，請輸入下列指令：

`cf bluemix-admin-delete-report <category> <date> <name>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">報告的種類。如果名稱中有空格，請使用引號括住該名稱。</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">報告日期，格式為 <samp class="ph codeph">YYYYMMDD</samp>。</dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">報告的名稱。</dd>
</dl>

**提示：**您也可以使用 **badr** 作為較長的 **bluemix-admin-delete-report** 指令名稱的別名。

* 若要擷取報告，請輸入下列指令：

`cf bluemix-admin-retrieve-report <category> <date> <name>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">報告的種類。如果名稱中有空格，請使用引號括住該名稱。</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">報告日期，格式為 <samp class="ph codeph">YYYYMMDD</samp>。</dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">報告的名稱。</dd>
</dl>

**提示：**您也可以使用 **barr** 作為較長的 **bluemix-admin-retrieve-report** 指令名稱的別名。

#### 啟用及停用所有組織的服務

您可以針對所有組織啟用或停用讓服務顯示在 {{site.data.keyword.Bluemix_notm}} 的「型錄」中。

* 若要讓所有組織可在 {{site.data.keyword.Bluemix_notm}} 的「型錄」中看見服務，請輸入下列指令：

`cf bluemix-admin-enable-service-plan <plan_identifier>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">您要啟用之服務的名稱或 GUID。如果輸入非唯一的服務名稱，系統會提示您可從中選擇的服務方案。</dd>
</dl>

**提示：**您也可以使用 **baesp** 作為較長的 **bluemix-admin-enable-service-plan** 指令名稱的別名。

* 若要讓所有組織在 {{site.data.keyword.Bluemix_notm}} 的「型錄」中看不見服務，請輸入下列指令：

`cf bluemix-admin-disable-service-plan <plan_identifier>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">您要停用之服務的名稱或 GUID。如果輸入非唯一的服務名稱，系統會提示您可從中選擇的服務方案。</dd>
</dl>

**提示：**您也可以使用 **badsp** 作為較長的 **bluemix-admin-disable-service-plan** 指令名稱的別名。

#### 新增、移除及編輯組織的服務可見性

您可以從組織清單中新增或移除可在 {{site.data.keyword.Bluemix_notm}} 的「型錄」中看見特定服務的組織。您也可以編輯及取代特定組織可在 {{site.data.keyword.Bluemix_notm}}
的「型錄」中看到的服務清單。

* 若要容許組織檢視 {{site.data.keyword.Bluemix_notm}} 的「型錄」中的特定服務，請輸入下列指令：

`cf bluemix-admin-add-service-plan-visibility <plan_identifier> <organization>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">您要新增可見性之服務的名稱或 GUID。如果輸入非唯一的服務名稱，系統會提示您可從中選擇的服務方案。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要新增至服務的可見性清單的 {{site.data.keyword.Bluemix_notm}} 組織的名稱或 GUID。</dd>
</dl>

**提示：**您也可以使用 **baaspv** 作為較長的 **bluemix-admin-add-service-plan-visibility** 指令名稱的別名。

* 若要針對組織移除 {{site.data.keyword.Bluemix_notm}} 的「型錄」中的服務可見性，請輸入下列指令：

`cf bluemix-admin-remove-service-plan-visibility <plan_identifier> <organization>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">您要移除可見性之服務的名稱或 GUID。如果輸入非唯一的服務名稱，系統會提示您可從中選擇的服務方案。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要從服務的可見性清單中移除之 {{site.data.keyword.Bluemix_notm}} 組織的名稱或 GUID。</dd>
</dl>

**提示：**您也可以使用 **barspv** 作為較長的 **bluemix-admin-remove-service-plan-visibility** 指令名稱的別名。

* 若要取代一個組織或多個組織的所有現有可見服務，請使用下列指令：

`cf bluemix-admin-edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>`
{: codeblock}

**附註：**此指令會將所指定組織的現有可見服務取代為您在指令中指定的服務。

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">您要使其可見之服務的名稱或 GUID。如果輸入非唯一的服務名稱，系統會提示您可從中選擇的服務方案。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要新增可見性之 {{site.data.keyword.Bluemix_notm}} 組織的名稱或 GUID。您可以針對多個組織啟用服務的可見性，方法為在指令中輸入其他組織名稱或 GUID。</dd>
</dl>

**提示：**您也可以使用 **baespv** 作為較長的 **bluemix-admin-edit-service-plan-visibility** 指令名稱的別名。
