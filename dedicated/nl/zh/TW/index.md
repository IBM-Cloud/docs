{:new_window: target="_blank"} 
{:shortdesc: .shortdesc}

#{{site.data.keyword.Bluemix_notm}} 專用
{: #dedicated}

*前次更新：2015 年 11 月 3 日*

{{site.data.keyword.Bluemix}} 是一種以雲端為基礎的開放標準平台，用於建置、執行及管理應用程式。使用「{{site.data.keyword.Bluemix_notm}}
專用」，即可使用強大而簡潔的 {{site.data.keyword.Bluemix_notm}}—在您自己的專用
SoftLayer 環境，且這個環境同時安全地連接至「{{site.data.keyword.Bluemix_notm}} 公用」環境和您自己的網路。{:shortdesc}

「{{site.data.keyword.Bluemix_notm}} 專用」包含一份專用型錄，它會顯示只供您使用的專用服務。它也包含來自「{{site.data.keyword.Bluemix_notm}}
公用」，用來形成聯合組織且可供您使用的其他服務。

「{{site.data.keyword.Bluemix_notm}} 專用」以 SoftLayer 為建置基礎，因此您可以使用最高效能的雲端基礎架構。每一個資料中心都有 24 小時全年無休的安全防護及嚴格控管。您和 IBM
會透過 VPN 通道及專用 VLAN，來存取您的 {{site.data.keyword.Bluemix_notm}} 專用實例。

![{{site.data.keyword.Bluemix_notm}} 專用](images/detaileddedicated.png "{{site.data.keyword.Bluemix_notm}} 專用")

*圖 1. 詳細的「{{site.data.keyword.Bluemix_notm}} 專用」圖*

就基礎架構、作業及實體安全而言，「{{site.data.keyword.Bluemix_notm}} 專用」環境的安全標準與公用 {{site.data.keyword.Bluemix_notm}} 相同。不過，開發人員對專用 {{site.data.keyword.Bluemix_notm}} 的存取會受到您的 LDAP
原則所控制，而 {{site.data.keyword.Bluemix_notm}} 團隊可以在設定環境時配置這些 LDAP 原則。在專用環境內，您可以管理使用者角色及許可權。如需詳細資料，請參閱[管理使用者及許可權](../admin/index.html#oc_useradmin)。

「{{site.data.keyword.Bluemix_notm}} 專用」包含所有內含的 {{site.data.keyword.Bluemix_notm}} 執行時期，以及 128 GB 的應用程式記憶體。

此外，預設還會有一組內含的服務，以及您可以為專用實例選擇的選用性服務。 

| **類型**        | **名稱**            | **說明** |      
|-----------------|-------------------|-------------------|
| 內含 | {{site.data.keyword.autoscaling}} | 根據原則，動態增加或減少應用程式的運算能力。使用此服務，即可在「{{site.data.keyword.Bluemix_notm}} 專用」環境中無限制地使用。 |
| 內含 | {{site.data.keyword.datacshort}} | 此服務提供記憶體內的資料網格，它支援應用程式的分散式快取情境。包含 50 GB 的記憶體內快取。 |
| 內含 | {{site.data.keyword.cloudant}} | IBM 的 NoSQL 資料庫，提供高效能的 JSON 資料層（與 CouchDB 相容）。包含 1.6 TB 及最多每秒 3,000 個 API 要求。 |
| 選用 | {{site.data.keyword.sqldb}} | IBM {{site.data.keyword.sqldbfull}} Database for {{site.data.keyword.Bluemix_notm}} 為您的應用程式增添了完整佈建的關聯式資料庫。{{site.data.keyword.sqldb}} 提供受管理資料庫來處理貴公司嚴苛的 Web 及交易式工作量。 |
| 選用 | {{site.data.keyword.mql}} | IBM {{site.data.keyword.mqlfull}} for {{site.data.keyword.Bluemix_notm}} 是以雲端為基礎的傳訊服務，它為 {{site.data.keyword.Bluemix_notm}} 應用程式提供富有彈性且易於使用的傳訊。{{site.data.keyword.mql}} 提供管理簡易的傳訊解決方案。您可以使用 {{site.data.keyword.mql}} 讓應用程式更具回應力且可擴充，也可以使用簡單而強大的 API，在應用程式之間共用及卸載工作。 |
| 選用 | {{site.data.keyword.dashdbshort}} | 使用 dashDB 來儲存關聯式資料，包括地理空間資料之類的特殊類型。然後，使用 SQL 或進階內建分析（例如預測分析及資料採礦、使用 R 的分析和地理空間分析）分析該資料。 |

*表 1. 專用服務*

##設定 {{site.data.keyword.Bluemix_notm}} 專用
{: #setupdedicated}

「{{site.data.keyword.Bluemix_notm}} 專用」的設計，是為了提供「{{site.data.keyword.Bluemix_notm}} 公用」供應項目的專用版本。您可以使用 {{site.data.keyword.Bluemix_notm}} 服務及執行時期，來支援 IBM 管理之 SoftLayer 帳戶中的運算需求。

IBM 讓您能使用受到密碼保護的登入方式來存取「{{site.data.keyword.Bluemix_notm}} 專用」。您可以存取服務、執行時期及關聯的資源，也可以部署和移除 {{site.data.keyword.Bluemix_notm}} 應用程式。IBM 利用多個 SoftLayer 位置來交付「{{site.data.keyword.Bluemix_notm}} 專用」，讓您可以在接近您的位置取得專用版本。

若要設定您的 {{site.data.keyword.Bluemix_notm}} 專用版本，請執行下列動作：

<ol>
<li>要開始使用，請與您的 IBM 指定客戶業務代表，或與 <a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">{{site.data.keyword.Bluemix_notm}}</a>
聯絡。</li>
<li>每月的經常性費用是基於您要使用的專用服務，外加所有 {{site.data.keyword.Bluemix_notm}} 公用服務的訂閱。您會收到關於任何超出訂閱合約之使用項目的發票。<ol type="a">
	<li>請和 IBM 確認您的「{{site.data.keyword.Bluemix_notm}} 專用」實例費用。	每月的經常性費用是基於您要使用的專用服務，外加所有 {{site.data.keyword.Bluemix_notm}} 公用服務的訂閱。您會收到關於任何超出訂閱合約之使用項目的發票。</li>
	<li>確認設定「{{site.data.keyword.Bluemix_notm}} 專用」實例的每一個階段的截止時間。</li>
	</ol>
	</li>
<li>為您的專用實例選取 <a href="http://www.softlayer.com/data-centers" target="_blank">SoftLayer 資料中心位置</a>。然後，建立您的專用平台及帳戶。對於您的帳戶，請指定組織中負責維持專用實例運作所需角色的人員。<br />
<br />
<dl>
<dt>**採購聯絡人**</dt>
<dd>與 IBM 業務代表一起建立您的「{{site.data.keyword.Bluemix_notm}} 專用」環境，包括識別您組織中處理專案任何層面的正確人員。這個角色會監督模式選擇、商業安排，以及客戶資源存取的安排。採購聯絡人是設定專用實例的整體聯絡人。</dd>
<dt>**法規遵循管理者**</dt>
<dd>與 IBM 業務代表一起選取符合您安全需求的拓蹼及部署選項。這個角色與 IBM 法規遵循顧問一起確定哪些部署模式能達到法規遵循目標及目的。</dd>
<dt>**網路專家**</dt>
<dd>與 IBM 業務代表一起訂定 {{site.data.keyword.Bluemix_notm}} 部署的網路計劃。這個角色會向 IBM 業務代表提供需求，並與業務代表一起訂定實作計劃。安裝及驗證階段結束時，這個角色會進行「簽核」，確認網路配置符合組織標準。</dd>
<dt>**DevOps 聯絡人**</dt>
<dd>與 IBM 業務代表一起計劃並套用 {{site.data.keyword.Bluemix_notm}} 平台、服務及執行時期所需的維護更新作業。這個角色也與 IBM 業務代表一起配置您的「{{site.data.keyword.Bluemix_notm}} 專用」實例。</dd>
</dl>
</li>
<li>定義並建立貴公司網路與「{{site.data.keyword.Bluemix_notm}} 專用」實例之間的網路連線功能。<ol type="a">
	<li>IBM 針對專用實例安裝監視及安全基礎架構。</li>
	<li>IBM 安裝您選取的單一承租戶專用服務。</li>
	<li>針對 IP 位址或防火牆之類的事物提供網路配置及端點，並提供 LDAP 的存取權，以整合至 {{site.data.keyword.Bluemix_notm}}。</li>
	</ol>
</li>
<li>識別環境的管理團隊，並指派角色。<ol type="a">
	<li>IBM 會根據您提供的資訊，配置網路存取權及 LDAP。管理存取權會授與給您指定的聯絡人。您也必須指定聯絡人來負責支援及計費。</li>
	<li>IBM 會在您的專用環境中設定聯合型錄，以顯示您的專用服務及許多公用 {{site.data.keyword.Bluemix_notm}} 服務。</li>
	<li>您會驗證網路和防火牆配置，以及 LDAP 端點和存取權。</li>
	</ol>
</li>
</ol>

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

##還原專用實例
{: #restorededicated}

「{{site.data.keyword.Bluemix_notm}} 專用」設定及配置會定期備份，以為環境中發生的任何意外停電作好準備。

在備份資料過程中，IBM 會完成下列作業：

<ul>
<li>加密所有備份副本並管理加密金鑰</li>
<li>監視及管理備份活動</li>
<li>提供已加密的備份檔</li>
<li>還原所要求的資料</li>
<li>管理備份與修正管理作業之間的排程衝突</li>
</ul>

因為保護專用資料十分重要，所以 IBM 需要您的協同作業來處理備份檔管理，讓檔案不會移至資料中心外部。特別的是，IBM 會要求您完成下列作業：

<ul>
<li>將已加密備份資料的副本移動離站，就像針對所管理的任何其他備份資料進行地一樣。</li>
<li>在需要進行還原時，提供 IBM 操作員的備份檔。</li>
</ul>

# 相關鏈結
## 一般 
* [探索：{{site.data.keyword.Bluemix_notm}} 專用](http://www.ibm.com/cloud-computing/bluemix/hybrid/dedicated/)
