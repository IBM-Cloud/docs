{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

#{{site.data.keyword.Bluemix_notm}} 專用
{: #dedicated}

*前次更新：2016 年 1 月 18 日*

{{site.data.keyword.Bluemix}} 是一種以雲端為基礎的開放標準平台，用於建置、執行及管理應用程式。使用「{{site.data.keyword.Bluemix_notm}} 專用」，即可在您自己的專用 SoftLayer 環境中，使用強大而簡潔的 {{site.data.keyword.Bluemix_notm}}，而這個環境同時安全地連接至「{{site.data.keyword.Bluemix_notm}} 公用」環境和您自己的網路。
{:shortdesc}

「{{site.data.keyword.Bluemix_notm}} 專用」包含一份專用型錄，它會顯示只供您使用的專用服務。它也包含來自「{{site.data.keyword.Bluemix_notm}} 公用」，用來形成聯合組織且可供您使用的其他服務。

「{{site.data.keyword.Bluemix_notm}} 專用」以 SoftLayer 為建置基礎，因此您可以使用最高效能的雲端基礎架構。每一個資料中心都有 24 小時全年無休的安全防護及嚴格控管。您和 IBM 會透過 VPN 通道及專用 VLAN，來存取您的 {{site.data.keyword.Bluemix_notm}} 專用實例。

![{{site.data.keyword.Bluemix_notm}} 專用](images/detaileddedicated.png "{{site.data.keyword.Bluemix_notm}} 專用")

*圖 1. 詳細的「{{site.data.keyword.Bluemix_notm}} 專用」圖*

就基礎架構、作業及實體安全而言，「{{site.data.keyword.Bluemix_notm}} 專用」環境的安全標準與公用 {{site.data.keyword.Bluemix_notm}} 相同。不過，開發人員對專用 {{site.data.keyword.Bluemix_notm}} 的存取會受到您的 LDAP 原則所控制，而 {{site.data.keyword.Bluemix_notm}} 團隊可以在設定環境時配置這些 LDAP 原則。在專用環境內，您可以管理使用者角色及許可權。如需詳細資料，請參閱[管理使用者及許可權](../admin/index.html#oc_useradmin)。

「{{site.data.keyword.Bluemix_notm}} 專用」包含所有內含的 {{site.data.keyword.Bluemix_notm}} 執行時期，以及 128 GB 的應用程式記憶體。

此外，預設還會有一組內含的服務，以及您可以為專用實例選擇的選用性服務。

| **類型**        | **名稱**            | **說明** |      
|-----------------|-------------------|-------------------|
| 內含 | {{site.data.keyword.autoscaling}} | 根據原則，動態增加或減少應用程式的運算能力。使用此服務，即可在「{{site.data.keyword.Bluemix_notm}} 專用」環境中無限制地使用。 |
| 內含 | {{site.data.keyword.datacshort}} | 此服務提供記憶體內的資料網格，它支援應用程式的分散式快取情境。包含 50 GB 的記憶體內快取。 |
| 選用 | {{site.data.keyword.mql}} | {{site.data.keyword.mqlfull}} for {{site.data.keyword.Bluemix_notm}} 是一種雲端型傳訊服務，可為 {{site.data.keyword.Bluemix_notm}} 應用程式提供靈活且易於使用的傳訊功能。{{site.data.keyword.mql}} 提供管理簡易的傳訊解決方案。您可以使用 {{site.data.keyword.mql}} 讓應用程式更具回應力且可擴充，也可以使用簡單而強大的 API，在應用程式之間共用及卸載工作。 |
| 選用 | {{site.data.keyword.dashdbshort}} | 使用 dashDB 來儲存關聯式資料，包括地理空間資料之類的特殊類型。然後，使用 SQL 或進階內建分析（例如預測分析及資料採礦、使用 R 的分析和地理空間分析）分析該資料。 |
|選用 | {{site.data.keyword.APIM}} | 使用 {{site.data.keyword.APIMfull}} 服務來組合、管理及社交化 API。您也可以使用 Proxy URL 或組合來自 HTTP 資料來源中的資料，以利用資源匯入 API。使用 {{site.data.keyword.APIM}} 服務的好處是您可以管理 API 的使用方式。 |
|選用 | {{site.data.keyword.SecureGateway}} | {{site.data.keyword.SecureGateway}} 服務使您能夠以安全的方式將 {{site.data.keyword.Bluemix_notm}} 應用程式連接至內部部署或雲端中的遠端位置。  |

*表 1. 專用服務*


##設定 {{site.data.keyword.Bluemix_notm}} 專用
{: #setupdedicated}

「{{site.data.keyword.Bluemix_notm}} 專用」的設計，是為了提供「{{site.data.keyword.Bluemix_notm}} 公用」供應項目的專用版本。您可以使用 {{site.data.keyword.Bluemix_notm}} 服務及執行時期，來支援 IBM 管理之 SoftLayer 帳戶中的運算需求。

IBM 讓您能使用受到密碼保護的登入方式來存取「{{site.data.keyword.Bluemix_notm}} 專用」。您可以存取服務、執行時期及關聯的資源，也可以部署和移除 {{site.data.keyword.Bluemix_notm}} 應用程式。IBM 利用多個 SoftLayer 位置來交付「{{site.data.keyword.Bluemix_notm}} 專用」，讓您可以在接近您的位置取得專用版本。

若要設定您的 {{site.data.keyword.Bluemix_notm}} 專用版本，請執行下列動作：

<ol>
<li>首先聯絡 IBM 指定的客戶代表或<a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">聯絡 {{site.data.keyword.Bluemix_notm}}</a>。</li>
<li>請和 IBM 確認您的「{{site.data.keyword.Bluemix_notm}} 專用」實例費用。
每月的經常性費用是根據您要使用的專用服務，再加上所有 {{site.data.keyword.Bluemix_notm}} 公用服務的訂閱。您會收到關於任何超出訂閱合約之使用項目的發票。</li>
<li>識別設定「{{site.data.keyword.Bluemix_notm}} 專用」實例的每一個階段的截止時間。如需每一個階段和所涉及作業的相關資訊，請參閱 <a href="index.html#rolesresponsibilities" target="_blank">{{site.data.keyword.Bluemix_notm}} 專用角色及責任</a>。</li>
<li>為您的專用實例選取 <a href="http://www.softlayer.com/data-centers" target="_blank">SoftLayer 資料中心位置</a>。然後，建立您的專用平台及帳戶。對於您的帳戶，請指定組織中負責維持專用實例運作所需角色的人員。如需您可指派之角色的相關資訊，請參閱 <a href="index.html#rolesresponsibilities" target="_blank">{{site.data.keyword.Bluemix_notm}} 專用角色及責任</a>。</li>
<li>定義並建立貴公司網路與「{{site.data.keyword.Bluemix_notm}} 專用」實例之間的網路連線功能。
	<ol type="a">
	<li>IBM 針對專用實例安裝監視及安全基礎架構。</li>
	<li>IBM 會安裝您選取的單一承租戶專用服務。</li>
	<li>針對 IP 位址或防火牆之類的事物提供網路配置及端點，並提供 LDAP 的存取權，以整合至 {{site.data.keyword.Bluemix_notm}}。</li>
	</ol>
</li>
<li>識別環境的管理團隊，並指派其角色。
	<ol type="a">
	<li>IBM 會根據您提供的資訊，配置網路存取權及 LDAP。管理存取權會授與給您指定的聯絡人。您也必須指定聯絡人來負責支援及計費。</li>
	<li>IBM 會在您的專用環境中設定聯合型錄，以顯示您的專用服務。聯合型錄包含來自「{{site.data.keyword.Bluemix_notm}} 公用」，用來形成聯合組織且可供您使用的其他服務。您可以選擇根據資料隱私及安全準則來決定符合商業需求的公用服務。</li>
	<li>您會驗證網路和防火牆配置，以及 LDAP 端點和存取權。</li>
	</ol>
</li>
</ol>

對您的環境進行起始部署和配置的過程應類似於下列清單。如需每個作業負責人員的詳細資料，請參閱[角色及責任](../dedicated/index.html#rolesresponsibilities)。

<ol>
<li>您選取要使用哪個資料中心來管理專用實例。如需資料中心選項的相關資訊，請參閱 <a href="http://www.softlayer.com/data-centers" target="_blank">SoftLayer 資料中心位置</a>。</li>
<li>您為部署指定網域名稱，以及要使用的 ID。設定 {{site.data.keyword.Bluemix_notm}} 實例時，您會得到三個網域。請挑選 <code>*mycompany*.*region*.bluemix.net</code> 和 <code>*mycompany*.*region*.mybluemix.net</code> 的字首。然後，選擇第三個網域的完整名稱。<br />
<p>您可以根據自己的需要選擇任意數量的自訂網域。不過，您應負責取得自訂網域的憑證。如需建立自訂網域的相關資訊，請參閱<a href="../manageapps/updapps.html#domain">建立及使用自訂網域</a>。</p></li>
<li>您識別使用哪個公用帳戶的擁有者，在「{{site.data.keyword.Bluemix_notm}} 公用」中代表您的公司。IBM 會使用此帳戶來追蹤聯合服務的使用情形。</li>
<li>您選取資料中心的安全連線類型。可選取的類型包括 SoftLayer VPN、SoftLayer Direct Link 及 AT&T Net Bond。</li>
<li>您決定是否將從公用網際網路存取您的專用環境。</li>
<li>您選取將使用的鑑別類型。可選取的類型包括 IBM ID 或 Active Directory。如需使用及登錄 IBM ID 的相關資訊，請參閱<a href="https://www.ibm.com/account/profile/us?page=regfaqhelp#4">說明及常見問題</a>頁面。</li>
<li>您識別環境的管理團隊，並指派其角色。如需您必須指派哪些角色的相關資訊，請參閱 <a href="index.html#rolesresponsibilities" target="_blank">{{site.data.keyword.Bluemix_notm}} 專用角色及責任</a>。</li>
<li>IBM 部署核心平台，其中包含彈性執行時期、主控台、管理特性和監視。</li>
<li>IBM 配置您對環境的管理存取權。</li>
<li>您可以開始使用您的專用實例來回應警示，該實例由 IBM 作業團隊進行監視。</li>
</ol>

在設定 {{site.data.keyword.Bluemix_notm}} 實例之後，您可以使用「管理」頁面來監視和管理 {{site.data.keyword.Bluemix_notm}} 實例。如需相關資訊，請參閱[管理 {{site.data.keyword.Bluemix_notm}} 本端和專用](../administer/index.html#mng)。如需升級和維護的相關資訊，請參閱[維護專用實例](index.html#maintaindedicated)。

##角色及責任
{: #rolesresponsibilities}

如果您設定「{{site.data.keyword.Bluemix_notm}} 專用」帳戶，請針對啟動及執行實例所需的角色，識別組織中的人員。

###角色

下列清單顯示您可指派的客戶角色及責任：

<dl>
<dt>**採購聯絡人**</dt>
<dd>與 IBM 業務代表一起建立您的「{{site.data.keyword.Bluemix_notm}} 專用」環境，包括識別您組織中處理專案任何層面的正確人員。指派給此角色的人員將擔當專案管理的角色，負責對型樣選取、商業安排以及客戶資源存取安排進行監視。採購聯絡人是設定專用實例和追蹤部署過程的整體聯絡人。</dd>
<dt>**法規遵循管理者**</dt>
<dd>與 IBM 業務代表一起選取符合您安全需求的拓蹼及部署選項。指派給這個角色的人員會與 IBM 規範顧問一起確定哪些部署模式能達到規範目標。</dd>
<dt>**網路專家**</dt>
<dd>與 IBM 業務代表一起訂定 {{site.data.keyword.Bluemix_notm}} 部署的網路計劃。指派給這個角色的人員會檢查 IBM 所需的必要網路規格，並與 IBM 一起訂定實作計劃。安裝及驗證階段結束時，指派給這個角色的人員會進行核准，確認網路配置符合組織標準。</dd>
<dt>**DevOps 聯絡人**</dt>
<dd>與 IBM 業務代表一起計劃並套用 {{site.data.keyword.Bluemix_notm}} 平台、服務及執行時期所需的維護更新作業。指派給這個角色的人員也會與 IBM 業務代表一起配置您的「{{site.data.keyword.Bluemix_notm}} 專用」實例。</dd>
</dl>

您的客戶代表會與您的專用代言人及其他合作的 IBM 專家一起合作，確保您一律擁有所需的支援。您的「專用代言人」是 {{site.data.keyword.Bluemix_notm}} 開發支援團隊內完成下列作業的單一聯絡點：

<ul>
<li>啟用「{{site.data.keyword.Bluemix_notm}} 專用」環境的快速採用。</li>
<li>提供有價值的教育訓練及啟用資料，以改善自給自足。</li>
<li>建立您與所使用的 {{site.data.keyword.Bluemix_notm}} 開發、支援及服務之間的長期關係。</li>
</ul>

與您一起處理 {{site.data.keyword.Bluemix_notm}} 實例的 {{site.data.keyword.Bluemix_notm}} 支援及作業團隊可能會存取本端環境，但只會因為下列原因而這麼做。

<ul>
<li>回應警示，並執行作業維護</li>
<li>嘗試重新產生對支援問題單所報告的問題</li>
</ul>

###責任

透過設定您的環境來進行持續維護，必須完成各種作業。下表概述在初始、進度及完成階段完成作業的必要作業及擁有者。

初始階段用來建立「{{site.data.keyword.Bluemix_notm}} 專用」環境。此階段的主要目標包括下列各項：

- 審查合約，並建立里程碑日期來進行遞送。
- 建立 {{site.data.keyword.Bluemix_notm}} 平台，並提供執行時期及服務的存取權。
- 定義並建立貴公司網路與 {{site.data.keyword.Bluemix_notm}} 作業之間的網路連線功能。
- 識別並指派管理團隊的角色。

*表 1. 初始階段作業*

| **作業** | **作業詳細資料** | **負責單位** |
|----------|------------------|-----------------------|
|設定規範標準 | 識別環境所需的政府、產業及專屬組織標準。 | 客戶 |
|建立安全及規範整合計劃 | 建立安全及整合計劃，以包括達成安全規範所需的成本、排程及資源。 | IBM |
|規範計劃核准 | 核准規範計劃。 | 客戶 |
|建立環境的大小 |  	根據考慮高可用性及災難回復目標的預先定義選項來建立環境大小，以及支援使用平台所建立的應用程式所需的起始 DEA 及服務佈建。您與 IBM 一起定義所需的資料庫、客戶聯合型錄中提供的服務等等（舉例來說）。 | IBM 及客戶共同責任 |
|選取架構 | 根據考慮高可用性及災難回復需求的預先定義選項來選取架構。 | IBM |
|定義災難回復目標 | 定義環境的災難回復需求。 | 客戶 |
|建立災難回復計劃 | 查閱並定義災難回復計劃。IBM 會建立災難回復模型，並向您查閱提供意見並核准計劃的位置。 | IBM 及客戶共同責任 |
|建立備份及回復計劃 | 建立備份及回復計劃，以定義在現場及異地配送備份的頻率及需求。IBM 會備份光纖元件、IBM 服務中心、服務 meta 資料（包括使用者角色）等等。您可以備份任何所負責的應用程式特有資料。 | IBM 及客戶共同責任 |
|識別進行事件偵測及問題判斷的工具 | 識別用於在 {{site.data.keyword.Bluemix_notm}} 平台層次進行事件偵測及問題判斷的 IBM 及協力廠商工具。 | IBM |
|定義提升計劃 | 定義提升計劃來分類並解決從監視元件偵測到的事件。 | IBM |
|簽署基礎架構、平台及支援合約 | 簽署訂閱合約（包括環境的財務條款）。簽署網路及安全監視合約。簽署支援訂閱。 | 客戶 |
|採購環境 | 採購運算資源、網路及儲存體（包括核心及「服務 VLAN」用來管理 {{site.data.keyword.Bluemix_notm}}、裸機服務用來管理 Data Power，以及 SoftLayer Firewall）。提供容許 VPN 通道的基礎架構。 | 客戶 |
|安裝光纖、應用程式，以及監視和管理元件 | 安裝、配置及驗證光纖元件（例如 BOSH Director、「雲端控制器」、「性能管理程式」、傳訊、路由器、DEA 及「服務提供者」），以及提升及問題偵測計劃中所定義的監視元件。 | IBM |
|安裝並配置安全元件 | 安裝並配置連結至監視及提升計劃的安全元件（包括 IBM QRadar、認證儲存庫、侵入防禦系統、IBM BigFix 及「IBM Security 特許身分管理」）。 | IBM |
|安裝並配置自訂元件 |  	安裝並配置位在 {{site.data.keyword.Bluemix_notm}} 產品及服務範圍外部的自訂元件。 | 客戶 |
|建立起始網路配置 | 建立起始網路配置（包括防火牆、DataPower、Fortigate 及 DNS）。 | IBM |
|連接 {{site.data.keyword.Bluemix_notm}} 管線 | 連接 {{site.data.keyword.Bluemix_notm}} 持續整合及持續交付管線與 IBM 儲存庫。 | IBM |
|自訂外部解決方案元件 | 自訂災難回復實務範例的負載平衡器。 | 客戶 |
|安裝 VPN 解決方案 | 安裝雙向 VPN 解決方案。 | IBM |
|配置登入伺服器 | 配置要與公司 LDAP 搭配使用的登入伺服器。 | IBM |
|追蹤安全、規範及審核控制的狀態  | 追蹤狀態，直到所有工具及處理程序都準備好可達到所識別的規範為止。 | 客戶 |
|檢查實體基礎架構 | 檢查可管理威脅解決方案元件的實體場所，並檢查安全控制以保護資料中心。 | 客戶 |
|檢查監視軟體 | 檢查監視及管理元件（如提升及問題判斷計劃中所定義）。 | 客戶 |
|檢查 OS | 檢查以確保作業系統映像檔符合規範標準。IBM 提供 OS 映像檔的存取權。 | IBM 及客戶共同責任 |

接下來是進度階段。進度階段說明您與 IBM Cloud 之間的進行中協同關係。此階段的主要目標包括下列各項：

- 檢查容量，並進行必要調整。
- 檢查維護及平台增進功能。
- 協調進行問題解決及主要原因分析的活動。

*表 2. 進度階段作業*

| **作業** | **作業詳細資料** | **負責單位** |
|----------|------------------|-----------------------|
|檢閱每週容量報告 | 檢閱每週容量報告，並視需要採取更正動作。 | 客戶 |
|建立按月預測 | 收集資訊，並建立容量及耗用量的按月預測。 | IBM 及客戶共同責任 |
|檢閱容量預測 | 檢閱容量預測，因為它們與可能影響容量的外部事件有關，以及預期有新的應用程式部署。與 IBM 一起據此檢閱預測及計劃。 | IBM 及客戶共同責任 |
|檢閱預測 | 檢閱容量預測，因為它與可能影響容量的外部事件有關。 | 客戶 |
|調整容量 |  隨著需求的變更來新增或移除容量。 | IBM |
|發佈即將到來的更新項目及維護 | 建立進行必要 IBM 元件維護的文件。 | IBM |
|執行維護 | 與 IBM 一起排定 30 天時間範圍內的必要維護。您可以提供 30 天時間範圍內無法進行的日期，而 IBM 會據此排定維護。 | IBM 及客戶共同責任 |
|處理佈建失敗 | 修正部署至「型錄」之客戶建立服務的佈建失敗（發生時）。 | IBM |
|執行網路及 IP 掃描 | 執行每日及每月網路和 IP 掃描。 | IBM 及客戶共同責任 |
|提供審核日誌的存取權 | 提供所有安全及管理審核日誌的存取權。   | IBM 及客戶共同責任 |
|進行測試 | 進行定期「重要作業控制」測試及協力廠商滲透測試。 | IBM 及客戶共同責任 |
|狀態報告、審核協調及規範會議  | 完成狀態報告、外部審核協調，以及規範審查狀態會議的呈現。 | IBM |
|聘雇及商業需求驗證 | 完成可存取客戶環境之 IBM 業務代表的每季聘雇驗證及持續商業需求驗證。 | IBM |
|解決安全漏洞 | 解決平台中所報告的安全漏洞。 | IBM |

最終階段「完成」代表您與 IBM {{site.data.keyword.Bluemix_notm}} 之間的關係結束。此階段的主要作業包括下列各項：

* 結束財務合約
* 移除所有網路連線
* 回收基礎架構

*表 3. 完成階段作業*

| **作業** | **作業詳細資料** | **負責單位** |
|----------|------------------|-----------------------|
|結束財務合約 | 討論並同意結束財務合約。 | IBM 及客戶共同責任 |
|解除任務環境 | 關閉環境的存取權及認證。 | IBM 及客戶共同責任 |
|移除客戶網路連線 | 移除 IBM 與客戶環境之間的網路連線。 | IBM 及客戶共同責任 |
|回收基礎架構 | 根據 SoftLayer 定義的處理程序，回收您的環境。 | IBM |

##維護專用實例
{: #maintaindedicated}

當 IBM 認為適用於「{{site.data.keyword.Bluemix_notm}} 專用」平台、執行時期及服務時，IBM 即會維護並安裝更新項目及修正程式。

**重要事項**：IBM 保留視需要岔斷服務以套用緊急維護的權利。IBM 可能會變更排定的維護時間，但是一旦有這類變更以及任何緊急維護資訊時，就會通知您。

「{{site.data.keyword.Bluemix_notm}} 專用」需要下列類型的維護：
<dl>
<dt>**標準維護時間範圍**</dt>
<dd>這些服務使用預先定義的標準維護時間範圍，這樣可能導致服務無法使用。IBM 不需要客戶核准即可執行維護，但是會嘗試將對服務的影響降到最低。<br />
<br />
IBM 會透過電子郵件、電話或其他方法，來傳送針對每一個維護時間範圍所規劃之變更的廣播訊息。<br />
<br />
**重要事項**：在維護期間，部分服務可能無法使用。</dd>

<dt>**每月變更時間範圍**</dt>
<dd>每月維護時間範圍是根據 21 天的時間範圍內，您與 IBM 之間的協調來套用。您可以將 21 天的時間範圍內，可能不適合的特定日期或時間提供給 IBM。IBM 在排定更新時會嘗試避開那些時間。根據要求，IBM 會與您溝通排定的維護時間範圍。每月變更時間範圍預期不會影響執行中的「Bluemix 專用」環境。<br />
<br />
**附註：**如果您未要求在特定時間進行更新，則在時間範圍結束時會自動套用維護。<br />
<br />
移至**管理 > 系統資訊**，以檢視擱置更新、設定無法使用的日期，以及核准更新。如需通知及排定擱置更新的相關資訊，請參閱<a href="../admin/index.html#oc_system">檢視系統資訊</a>。</dd>

<dt>**其他**</dt>
<dd>IBM 打算將可能會影響您服務（特別是會影響「{{site.data.keyword.Bluemix_notm}} 專用」環境、執行時期及服務的可用性）的所有維護，限制在標準及每月更新。其他變更時間範圍可能會以例外情形使用，以便管理環境。IBM 會盡量降低在這類變更時間範圍對您所造成的影響，並會提前通知您。</dd>
</dl>

若要設定專用實例的維護，請與 IBM 指定的客戶業務代表一起找出進行標準維護的協議時間範圍。

如果在維護更新作業之後發生報告過的問題，則您與 IBM 業務代表都同意最好是容許 IBM 回復更新。根據合約，IBM 會回復更新，以將環境還原至前一個狀態。

## 災難回復
{: #dr}

「{{site.data.keyword.Bluemix_short}} 公用」提供持續可用的平台以進行創新。多個失敗安全測量可確保您的組織、空間及應用程式一律可用。將應用程式部署至多個地理區域會啟用持續可用性，以免於非計劃性地同時遺失多個硬體或軟體元件，或遺失整個資料中心，因此，在某個地理位置發生自然災難時，將會使用替代地理位置中的已配送「{{site.data.keyword.Bluemix_notm}} 公用」應用程式實例。
{: shortdesc}

透過應用程式的持續可用性、固有的平台高可用性以及失敗時還原實例的能力，可以進行「{{site.data.keyword.Bluemix_short}} 專用」的災難回復。您負責透過部署至多個地區來啟用應用程式的持續可用性。高可用性是透過 Cloud Foundry 中所含的技術及其他元件建置於平台層次。而且，如果您之後需要還原實例，則可以與 IBM 一起確保已適當地備份資料。

### 啟用「{{site.data.keyword.Bluemix_notm}} 專用」的持續可用性
{: #enabling}

「{{site.data.keyword.Bluemix_notm}} 公用」預設會部署至多個地理位置。不過，您必須執行下列動作，才能啟用廣域配送的「{{site.data.keyword.Bluemix_notm}} 專用」實例：

* 確定您的開發人員將應用程式部署至多個地區（透過手動或自動化處理程序）。地區應該彼此相隔 200 公里以上，確保自然災難不會影響這兩個地理位置。
* 配置廣域負載平衡器（例如 Akamai 或 Dyn），使其指向至少兩個不同地區中的應用程式。

**附註**：並非所有 {{site.data.keyword.Bluemix_notm}} 服務都支援地區配送。當您建構應用程式時，如果要達到地理配送，則也必須確保該應用程式所使用的服務具有資料同步處理這個重要特性。

#### 將「{{site.data.keyword.Bluemix_notm}} 專用」應用程式部署至多個地理位置
{: #deploying}

若要部署至第二個位置或多個位置，您必須遵循與用來啟用主要地理位置類似的處理程序：

1. 啟用新的專用環境來管理您應用程式的其他實例。若要建立新的環境，請聯絡 IBM 銷售團隊來起始處理程序。如需設定專用實例的相關資訊，請參閱[設定 {{site.data.keyword.Bluemix_notm}} 專用](../dedicated/index.html#setupdedicated)。您必須分別登入才能存取每一個環境。所管理環境的每一個實體位置都應該與原始位置距離最少 200 公里，以確保可用性。
2. 取得將管理新的已部署應用程式的唯一網域名稱。例如，如果您的原始網域是 *mycompany.east.bluemix.net*，則可以建立具有新網域（例如 *mycompany.west.bluemix.net*）的新的本端環境，並部署至新網域。
3. 每次部署原始應用程式時，也都會部署至新位置。如需部署的相關資訊，請參閱[上傳應用程式](../starters/upload_app.html)。


#### 啟用「{{site.data.keyword.Bluemix_notm}} 專用」的廣域負載平衡器
{: #glb}

廣域負載平衡器不僅可確保持續可用性，也是災難回復的必要項目，而且它還有數個其他優點：

* 預設會將使用者遞送至最近的 {{site.data.keyword.Bluemix_notm}} 地區
* 根據效能進行遞送
* 選擇性地將某個百分比的資料流量導向新的應用程式版本
* 根據地區性能檢查，提供網站失效接手
* 根據應用程式性能檢查，提供網站失效接手
* 在端點之間使用加權遞送

您可以選擇廣域負載平衡器（例如 Akamai 或 Dyn）。如需使用 Akamai 作為廣域負載平衡器的相關資訊，請參閱 [Global traffic management](https://www.akamai.com/us/en/solutions/products/web-performance/global-traffic-management.jsp){: new_window}。如需使用 Dyn 作為廣域負載平衡器的相關資訊，請參閱 [4 Reasons Businesses Are Taking Global Load Balancing to the Cloud](http://dyn.com/blog/4-reasons-businesses-are-taking-global-load-balancing-to-the-cloud/){: new_window}。

### 高可用性
{: #ha}

除了啟用持續可用性之外，{{site.data.keyword.Bluemix_notm}} 也可透過使用建置至 Cloud Foundry、Docker 及其他元件的技術，來提供跨平台的高可用性。

這些技術包括下列各項：

<dl>
<dt>Cloud Foundry 中的可擴充性</dt>
<dd>Cloud Foundry <a href="https://docs.cloudfoundry.org/concepts/architecture/execution-agent.html" target="_blank">Droplet Execution Agent (DEA)</a> 會對其內部執行的應用程式執行性能檢查。如果應用程式或 DEA 本身發生問題，則會將應用程式的其他實例部署至替代 DEA，以處理問題。如需相關資訊，請參閱 <a href="https://docs.cloudfoundry.org/concepts/high-availability.html" target="_blank">Configuring CF for High Availability with Redundancy</a>。
</dd>
<dt>SoftLayer 備援</dt>
<dd>如果在專用環境中使用 SoftLayer，則每一個雲端儲存體叢集中的資料都會寫入多次，而且儲存體叢集已配置自動修復功能，以防磁碟機故障。如果虛擬機器發生問題，SoftLayer 會嘗試在另一個主機上重新啟動虛擬機器。</dd>
<dt>meta 資料備份</dt>
<dd>使用 SoftLayer EVault Backup，將 meta 資料備份至最少距離 200 公里的位置。</dd>
</dl>

##還原專用實例
{: #restorededicated}

「{{site.data.keyword.Bluemix_notm}} 專用」設定、meta 資料及配置會定期備份，以為環境中發生的任何非計劃性的運作中斷作好準備。您負責備份的資料包括應用程式資料、雲端資料庫服務資料及物件儲存庫。

在資料備份過程（包括系統 meta 資料及配置），IBM 會完成下列作業：

<ul>
<li>加密所有備份副本並管理加密金鑰</li>
<li>監視及管理備份活動</li>
<li>提供已加密的備份檔</li>
<li>還原所要求的資料</li>
<li>管理備份與修正管理作業之間的排程衝突</li>
</ul>

因為保護專用資料十分重要，所以 IBM 需要您的協同作業來處理備份檔管理，讓檔案不會移至資料中心外部。特別的是，IBM 會要求您完成下列作業：

<ul>
<li>將已加密備份資料的副本移到異地，就如同您針對所管理的任何其他備份資料所採取的程序一樣。</li>
<li>在需要進行還原時，將備份檔提供給 IBM 操作員。</li>
</ul>

# 相關鏈結
## 一般
* [探索：{{site.data.keyword.Bluemix_notm}} 專用](http://www.ibm.com/cloud-computing/bluemix/hybrid/dedicated/)
* [管理 {{site.data.keyword.Bluemix_notm}} 本端及 {{site.data.keyword.Bluemix_notm}} 專用](../admin/index.html#mng)
* [與支援中心聯絡](../troubleshoot/getting_customer_support.html#bluemix_support)
