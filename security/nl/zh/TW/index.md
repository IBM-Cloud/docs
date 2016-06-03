---

 

copyright:

  years: 2014, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.Bluemix_notm}} 安全
{: #security}
*前次更新：2016 年 5 月 9 日*

{{site.data.keyword.Bluemix}} 平台以安全工程作法進行設計，具有跨網路及基礎架構的分層安全控制。{{site.data.keyword.Bluemix_notm}} 提供一組安全服務，可讓應用程式開發人員用來保護其行動式及 Web 應用程式。這些元素結合在一起，讓 {{site.data.keyword.Bluemix_notm}} 成為具有清楚的安全應用程式開發選擇的平台。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} 堅守由 IBM 在系統、網路及安全工程方面的最佳作法所驅動的安全原則，進而確保安全無虞。這些原則包括原始碼掃描、動態掃描、威脅建模以及滲透測試等作法。{{site.data.keyword.Bluemix_notm}} 遵循 IBM Product Security Incident Response Team (PSIRT) 處理程序，來進行資安事件管理。如需詳細資料，請參閱 [IBM Security Vulnerability Management (PSIRT)](http://www-03.ibm.com/security/secure-engineering/process.html){: new_window} 網站。

「{{site.data.keyword.Bluemix_notm}} 公用」及「Bluemix 專用」使用 IBM SoftLayer 的「基礎架構即服務 (IaaS)」雲端服務，並充分運用其安全架構。SoftLayer IaaS 為您的應用程式及資料提供層層重疊的多個保護層級。若為「{{site.data.keyword.Bluemix_notm}} 本端」，您藉由在公司防火牆後、自己的資料中心內管理「{{site.data.keyword.Bluemix_notm}} 本端」，而掌控實體安全並提供基礎架構。此外，{{site.data.keyword.Bluemix_notm}} 也在「平台即服務」層新增不同種類（平台、資料及應用程式）的安全功能。

## {{site.data.keyword.Bluemix_notm}} 平台的安全
{: #platform-security}

{{site.data.keyword.Bluemix_notm}} 為核心平台提供了功能安全、基礎架構安全、作業安全及實體安全（透過 IBM SoftLayer）。 不過，「{{site.data.keyword.Bluemix_notm}} 本端」獨特之處在於，客戶會提供基礎架構及資料中心，並掌控實體安全。

SoftLayer 的 {{site.data.keyword.Bluemix_notm}} 環境符合最嚴格的 IBM 資訊技術 (IT) 安全標準，這些標準已達到或超越業界標準。這些標準包括下列項目：網路、資料加密及存取控制
 * 應用程式 ACL、許可權及滲透測試
 * 識別、鑑別及授權
 * 資訊及資料保護
 * 服務完整性和可用性
 * 漏洞及修正程式管理
 * 拒絕服務及系統攻擊偵測
 * 資安事件回應

![Bluemix 平台安全概觀](images/platform_sec.svg)

*圖 1. {{site.data.keyword.Bluemix_notm}} 平台安全概觀*

運用「{{site.data.keyword.Bluemix_notm}} 本端」，您可以管理受公司防火牆保護以及在資料中心內的 {{site.data.keyword.Bluemix_notm}}。因此，您要負責特定的安全層面。下圖詳述客戶掌控哪些部分的安全，而哪些部分的安全則由 IBM 所管理及維護。

![Bluemix 本端平台安全概觀](images/security_local_platform.svg)

*圖 2.「{{site.data.keyword.Bluemix_notm}} 本端」平台安全概觀*

IBM 透過「轉遞」來安裝、遠端監視及管理資料中心中的「{{site.data.keyword.Bluemix_notm}} 本端」，而「轉遞」是「{{site.data.keyword.Bluemix_notm}} 本端」內含的一種交付功能。「轉遞」會使用每一個「{{site.data.keyword.Bluemix_notm}} 本端」實例特有的憑證安全地進行連接。如需「{{site.data.keyword.Bluemix_notm}} 本端」及「轉遞」的相關資訊，請參閱 [Bluemix 本端](../local/index.html)。

### 功能安全

{{site.data.keyword.Bluemix_notm}} 提供各種功能安全方面的功能，包括使用者鑑別、存取授權、重要作業審核，以及資料保護。

<dl>
<dt>鑑別</dt>
<dd>應用程式開發人員利用 IBM Web 身分向 {{site.data.keyword.Bluemix_notm}} 進行鑑別。若為「{{site.data.keyword.Bluemix_notm}} 專用」及「Bluemix 本端」，預設支援透過 LDAP 進行鑑別。在要求時，可以改為針對 {{site.data.keyword.Bluemix_notm}} 設定透過 IBM Web 身分進行鑑別。
</dd>

<dt>授權</dt>
<dd>{{site.data.keyword.Bluemix_notm}} 使用 Cloud Foundry 機制來確保每一個應用程式開發人員都只能存取其所建立的應用程式及服務實例。對 {{site.data.keyword.Bluemix_notm}} 服務的授權是根據 OAuth。外部使用者在存取所有「{{site.data.keyword.Bluemix_notm}} 平台」內部端點時會受到限制。</dd>

<dt>審核</dt>
<dd>對應用程式開發人員的所有鑑別嘗試，不論成功或失敗，都會建立審核日誌。對於管理 {{site.data.keyword.Bluemix_notm}} 應用程式執行所在儲存器的 Linux 系統，其特許存取也會建立審核日誌。</dd>

<dt>資料保護</dt>
<dd> 所有 {{site.data.keyword.Bluemix_notm}} 資料流量都會通過 IBM WebSphere® DataPower® SOA Appliance，它們提供反向 Proxy、SSL 終止及負載平衡功能。以下是允許使用的 HTTP 方法：
 * DELETE
 * GET
 * HEAD
 * OPTIONS
 * POST
 * PUT
 * TRACE

HTTP 閒置逾時為 2 分鐘。

下列標頭由 DataPower 移入：
<dl>
<dt>$wsis</dt>
<dd>如果用戶端連線為安全的連線 (HTTPS)，請設為 true；否則請設為 false。</dd>
<dt>$wssc</dt>
<dd>設為下列其中一個用戶端連線方法：https、http、ws 或 wss。</dd>
<dt>$wssn</dt>
<dd>設為用戶端傳送的主機名稱。</dd>
<dt>$wssp</dt>
<dd>設為用戶端連接的伺服器埠。</dd>
<dt>x-client-ip</dt>
<dd>設為用戶端 IP 位址。</dd>
<dt>x-forwarded-proto</dt>
<dd>設為下列其中一個用戶端連線方法：https、http、ws 或 wss。</dd>
</dl>
</dd>

<dt>安全開發作法</dt>
<dd> 若為「{{site.data.keyword.Bluemix_notm}} 公用」及「Bluemix 專用」，會利用 IBM Security AppScan® Dynamic Analyzer，在各種 {{site.data.keyword.Bluemix_notm}} 元件上定期執行安全漏洞掃描。會執行威脅建模及滲透測試，以偵測並解決所有類型之 {{site.data.keyword.Bluemix_notm}} 部署的任何潛在漏洞。此外，應用程式開發人員可以使用 AppScan Dynamic Analyzer 服務來保護在 {{site.data.keyword.Bluemix_notm}} 上部署的 Web 應用程式。</dd>
</dl>

### 基礎架構安全

{{site.data.keyword.Bluemix_notm}} 以 Cloud Foundry 為建置基礎，為執行應用程式提供了強固的基礎。在架構內，提供了多個元件用於安全保護及隔離。此外，也實作了變更管理與備份及回復程序，以確保完整性及可用性。

<dl>
<dt>環境隔離</dt>
<dd> 對於「{{site.data.keyword.Bluemix_notm}} 公用」，開發及正式作業環境會彼此隔離，以提高應用程式的穩定性及安全。</dd>

<dt>防火牆</dt>
<dd> 實施了防火牆，以限制對 {{site.data.keyword.Bluemix_notm}} 網路的存取。對於「{{site.data.keyword.Bluemix_notm}} 本端」，貴公司的防火牆會隔離您的 {{site.data.keyword.Bluemix_notm}} 實例與您網路的其餘部分。</dd>

<dt>侵入防禦</dt>
<dd>「{{site.data.keyword.Bluemix_notm}} 公用」及「Bluemix 專用」能促成侵入防禦，以便發現威脅，進而解決這些威脅。防火牆上已啟用侵入防禦原則。</dd>

<dt>安全應用程式儲存器管理</dt>
<dd>每一個 {{site.data.keyword.Bluemix_notm}} 應用程式都會在自己的儲存器中隔離和執行，而儲存器對於處理器、記憶體及磁碟具有特定的資源限制。</dd>

<dt>強化作業系統安全</dt>
<dd>IBM 管理者會利用 IBM Endpoint Manager 等工具，定期執行網路及作業系統的強化作業。</dd>
</dl>

### 作業安全

{{site.data.keyword.Bluemix_notm}} 提供了強固的作業安全環境，以及下列控制措施。

<dl>
<dt>漏洞掃描</dt>
<dd>{{site.data.keyword.Bluemix_notm}} 會使用 Tenable Network Security 漏洞掃描工具 Nessus，來偵測網路及主機配置中發生的任何問題，以便能解決這些問題。</dd>

<dt>自動化修正程式管理</dt>
<dd>{{site.data.keyword.Bluemix_notm}} 管理者確保依適當的頻率套用作業系統的修正程式。利用 IBM Endpoint Manager 即可啟用自動化修正程式。</dd>

<dt>審核日誌合併及分析</dt>
<dd>{{site.data.keyword.Bluemix_notm}} 使用 IBMSecurity QRadar® 工具來合併 Linux 日誌，以監視 Linux 系統上的特許存取。{{site.data.keyword.Bluemix_notm}} 也會使用 IBM QRadar 安全資訊及事件管理 (SIEM)，來監視應用程式開發人員的成功和不成功的登入嘗試。</dd>

<dt>使用者存取管理</dt>
<dd>在 {{site.data.keyword.Bluemix_notm}} 內，會遵循「權責區分」準則，指派精細的存取權給使用者，並確保根據最低專用權原則，使用者僅具備執行其工作所需的存取權。在「{{site.data.keyword.Bluemix_notm}} 專用」及「Bluemix 本端」環境內，已指派的管理者可以利用「管理主控台」來管理 {{site.data.keyword.Bluemix_notm}} 使用者在其組織中的角色及許可權。如需詳細資料，請參閱[管理 {{site.data.keyword.Bluemix_notm}} 本端及專用](../admin/index.html#mng)。
</dd>
</dl>

### 實體安全

「{{site.data.keyword.Bluemix_notm}} 公用」及「Bluemix 專用」依賴 SoftLayer 的「網中網」(network-within-a-network) 拓蹼來確保實體網路安全。這個網中網架構可確保系統只能由獲得授權的人員進行完全存取。若為「{{site.data.keyword.Bluemix_notm}} 本端」，您掌控了本端實例的實體安全。您的資料中心受到貴公司防火牆的安全保護。

在 SoftLayer 網中網，公用網路層會處理受管理網站或線上資源的公用資料流量。私密網路層容許透過不同的獨立式第三方營運商，經由 SSL、PPTP 或 IPSec VPN 閘道進行真正的頻外管理。資料中心到資料中心的網路層，在位於不同 SoftLayer 設施的伺服器之間，提供了免費的安全連線功能。

每個 SoftLayer 資料中心都受到符合 SSAE 16 及業界公認要求的控制措施的全面保護，無一例外。如需相關資訊，請參閱 SoftLayer Security Compliance 頁面。

## 資料安全
{: #data-security}

使用 {{site.data.keyword.Bluemix_notm}}，{{site.data.keyword.Bluemix_notm}} 會與您共同努力來保護您的資料不受未獲授權的存取。

與執行中應用程式相關聯的資料，可能處於下列三種狀態之一：data-in-transit、data-at-rest 及 data-in-use。

<dl>
<dt>Data-in-transit</dt>
<dd>在網路上的節點之間傳送的資料。</dd>

<dt>Data-at-rest</dt>
<dd>儲存的資料。</dd>

<dt>Data-in-use</dt>
<dd>目前未儲存，且在某一端點上接受操作的資料。</dd>
</dl>

當您在規劃資料安全時，需要考量每一種類型的資料。

{{site.data.keyword.Bluemix_notm}} 平台會透過網路，利用 SSL 來保護一般使用者的應用程式存取安全，藉以保護 data-in-transit 的安全，直到資料在 {{site.data.keyword.Bluemix_notm}} 內部網路的界限達到 IBM DataPower Gateway 為止。IBM DataPower Gateway 作為反向 Proxy，並提供 SSL 終止。

當您在開發應用程式時，必須負責保護 data-in-use 與 data-at-rest 的安全。您可以充分運用 {{site.data.keyword.Bluemix_notm}}「型錄」中可用的數個資料相關服務，來協助這些重要事項。

## {{site.data.keyword.Bluemix_notm}} 應用程式的安全
{: #application-security}

身為應用程式開發人員，您必須為 {{site.data.keyword.Bluemix_notm}} 上執行的應用程式啟用安全配置，包括應用程式資料保護。

您可以使用數個 {{site.data.keyword.Bluemix_notm}} 服務所提供的安全功能來保護應用程式。IBM 生產的所有 {{site.data.keyword.Bluemix_notm}} 服務都遵循 IBM 安全工程開發作法。

**附註：**這裡所述的一些服務可能不適用於「Bluemix 專用」或「Bluemix 本端」實例。

### SSO 服務

IBM Single Sign On for {{site.data.keyword.Bluemix_notm}} 是以原則為基礎的鑑別服務，為 Node.js 或 Liberty for Java™ 應用程式提供了易於內嵌的單一登入功能。若要讓應用程式開發人員將單一登入功能內嵌至應用程式，管理者需建立服務實例並新增身分來源。

Single Sign On 服務支援數個儲存使用者認證的身分來源：

<dl>
<dt>SAML 企業</dt>
<dd>透過交換 SAML 記號而完成鑑別的使用者登錄。</dd>

<dt>雲端目錄</dt>
<dd>「IBM 雲端」中所管理的使用者登錄。</dd>

<dt>社交身分來源</dt>
<dd> 由 Google、Facebook 及 LinkedIn 所維護的使用者登錄。</dd>
</dl>

如需相關資訊，請參閱[開始使用 Single Sign On](../services/SingleSignOn/index.html)。

### Application Security on Cloud

此服務提供行動式及 Web 應用程式的安全分析，並可讓您掃描原始碼是否有安全漏洞。如需相關資訊，請參閱[開始使用 Application Security on Cloud](../services/ApplicationSecurityonCloud/index.html)。

### 用於應用程式安全測試的 IBM UrbanCode 外掛程式

IBM Application Security Testing for {{site.data.keyword.Bluemix_notm}} 外掛程式可讓您針對 {{site.data.keyword.Bluemix_notm}} 上管理的 Web 或 Android 應用程式執行安全掃描。此外掛程式由 IBM UrbanCode™ Deploy Community 在 IBM Bluemix DevOps Services 平台上開發及支援。

如需相關資訊，請造訪 [IBM Application Security Testing for Bluemix](https://developer.ibm.com/urbancode/plugindoc/ibmucd/ibm-application-security-testing-bluemix/1-0/){: new_window}。

### dashDB

dashDB 服務使用內嵌式 LDAP 伺服器進行使用者鑑別。應用程式與資料庫之間的連線受到 SSL 憑證保護。此服務使用 DB2® 原生加密功能自動加密您的已部署資料庫及資料庫備份。每隔 90 天會自動執行一次主要金鑰輪替。

如需相關資訊，請參閱[開始使用 dashDB](../services/dashDB/index.html)。

### Cloud Integration

Cloud Integration 服務可讓您整合雲端與內部部署資料。您可以新增服務，以與 DB2、Oracle 及 SAP 之類的後端資料庫互動。接下來，您可以移動資料或建立 REST API，讓 {{site.data.keyword.Bluemix_notm}} 應用程式存取及使用。此服務能促成與內部部署安全連接器的安全通訊，並將後端記錄系統公開為 REST API，以便應用程式使用。

如需相關資訊，請參閱[開始使用 Cloud Integration](../services/CloudIntegration/index.html)。

### Secure Gateway

Secure Gateway 服務可讓您將 {{site.data.keyword.Bluemix_notm}} 應用程式安全地連接至遠端位置（內部部署或雲端）。它提供安全連線功能，並在您的 {{site.data.keyword.Bluemix_notm}} 組織與您要連接的遠端位置之間建立通道。您可以利用 {{site.data.keyword.Bluemix_notm}} 使用者介面或 API 套件，來配置及建立安全閘道。

如需相關資訊，請參閱[開始使用 Secure Gateway](../services/SecureGateway/secure_gateway.html)。

### SQL Database

SQL Database 服務為您的應用程式增加了完整佈建的關聯式資料庫。此服務使用 IBM Directory Server LDAP 進行鑑別，並使用 IBM InfoSphere® Guardium® Data Activity Monitor 來保護應用程式存取的資料庫。應用程式與資料庫之間的連線受到 DigiCert 簽署的 SSL 憑證保護。

在含有此服務的某些方案中，您可以使用 {{site.data.keyword.Bluemix_notm}} 中的 SQL 資料庫主控台來取得包含下列資訊的報告：

 * 應用程式所存取的資料庫中可能存在的機密資料。
 * 在指定期間內存取資料庫的應用程式使用者。
 * 存取資料庫中的機密資料的應用程式使用者。

若要利用 SQL 來遮罩資料，應用程式可以呼叫與資料庫一起部署的遮罩使用者定義函數 (UDF)。例如，您可以遮罩要用來在其他地方測試的資料。UDF 會實作來自 IBM Infosphere Optim™ 的資料遮罩演算法。

此服務的高階方案也包括資料加密。如需此服務的相關資訊，請參閱[開始使用 SQL Database](../services/SQLDB/index.html)。

### 安全資訊及事件管理

您可以使用安全資訊及事件管理 (SIEM) 工具來分析應用程式日誌中的安全警示。其中一種這類工具是 IBM Security QRadar&reg; SIEM，其提供雲端環境中的安全智慧。如需相關資訊，請參閱 [IBM QRadar Security Intelligence Platform](http://www-01.ibm.com/support/knowledgecenter/SS42VS/welcome?lang=en){: new_window}。

## {{site.data.keyword.Bluemix_notm}} 安全部署
{: #security-deployment}

{{site.data.keyword.Bluemix_notm}} 安全部署架構包括適用於應用程式使用者及開發人員的不同資訊流程，以確保安全存取。

![Bluemix 安全部署架構](images/sec_deployment.svg)

*圖 3. Bluemix 安全部署架構*

針對 {{site.data.keyword.Bluemix_notm}} *應用程式使用者*，**應用程式使用者流程**如下所示：
 1. 透過防火牆，並實施侵入防禦及網路安全。
 2. 透過 IBM DataPower Gateway，並具有反向 Proxy 及 SSL 終止 Proxy。
 3. 透過網路路由器。
 4. 在 Droplet Execution Agent (DEA) 中呼叫應用程式執行時期。

{{site.data.keyword.Bluemix_notm}} *開發人員* 遵循兩個主要流程：一個適用於登入，一個適用於開發及部署。
 * **開發人員登入流程**包括下列項目：
    * 若為登入「{{site.data.keyword.Bluemix_notm}} 公用」的開發人員，流程如下所示：
      1. 透過 IBM Single Sign On 服務。
      2. 透過 IBM Web 身分。
    * 若為登入「{{site.data.keyword.Bluemix_notm}} 專用」或「Bluemix 本端」的開發人員，流程會透過企業 LDAP。
 * **開發及部署流程**如下所示：
    1. 透過防火牆，並實施侵入防禦及網路安全。這僅適用於「{{site.data.keyword.Bluemix_notm}} 專用」。
    2. 透過 IBM DataPower Gateway，並具有反向 Proxy 及 SSL 終止 Proxy。
    3. 透過網路路由器。
    4. 透過利用 Cloud Foundry 雲端控制器所進行的授權，以確保僅能存取開發人員所建立的應用程式及服務實例。

針對「{{site.data.keyword.Bluemix_notm}} 專用」及「{{site.data.keyword.Bluemix_notm}} 本端」*管理者*，**管理者流程**如下所示：
 1. 透過防火牆，並實施侵入防禦及網路安全。
 2. 透過 IBM DataPower Gateway，並具有反向 Proxy 及 SSL 終止 Proxy。
 3. 透過網路路由器。
 4. 到達 {{site.data.keyword.Bluemix_notm}} 使用者介面中的「管理」頁面。

除了這些路徑中所述的使用者之外，經過授權的 IBM 安全作業團隊也會執行各種作業安全作業，例如下列作業：
 * 漏洞掃描。若為「{{site.data.keyword.Bluemix_notm}} 本端」，您掌控了防火牆內的實體安全以及任何掃描。
 * 使用者存取管理。
 * 利用 IBM Endpoint Manager 定期套用修正程式，來強化作業系統。
 * 風險管理與侵入防禦。
 * 使用 QRadar 進行安全監視。
 * 可在「管理」頁面上取得安全報告。

## 安全規範
{: #compliance}

{{site.data.keyword.Bluemix}} 提供了一個您可以信任的安全雲端平台。{{site.data.keyword.Bluemix_notm}} 規範來自於根據業界最佳安全標準（包括 ISO 27001 和 ISO 27002）建置的平台和服務。
{:shortdesc}

![歐盟 (EU) 資料保護示範條款](images/icon_eumc.png) **歐盟 (EU) 示範條款**是一種協議，用於保護從歐盟 (EU) 或歐洲經濟區 (EEA) 傳輸到第三方國家的個人資料。「歐盟 (EU) 示範條款」是由位於 EU 或 EEA 的用戶（資料匯出方）與位於第三方國家的 IBM 資料處理方（資料匯入方）之間簽訂的。[IBM SaaS 歐盟 (EU) 示範條款](http://www-01.ibm.com/common/ssi/cgi-bin/ssialias?subtype=ST&infotype=SA&htmlfid=KUJ12408USEN&attachment=KUJ12408USEN.PDF){: new_window}包含資料匯出方和資料匯入方的權利和責任，以及資料主體的權利。「IBM SaaS 歐盟示範條款」可確保個人資料在第三方國家處理時仍能受到像在 EU 或 EEA 中一樣的保護。

![金融行業資訊系統](images/FISC.gif) 對於日本的銀行和相關金融機構，電腦系統必須具有適當的安全程序，這些程序應根據「金融行業資訊系統中心 (FISC)」安全準則。**FISC** 安全準則由「日本金融廳 (FSA)」、「日本央行 (BOJ)」和 FISC 貫徹實施。

在 [IBM Bluemix 風險意見調查結果](https://www.ibm.com/cloud-computing/jp/ja/bluemix_fisc.html){: new_window}上，可以找到 FISC 安全準則的 {{site.data.keyword.Bluemix_notm}} 自我評量文件（日語）。 

![ISO 27001/2](images/icon_iso27k1.png) {{site.data.keyword.Bluemix_notm}} 已通過**國際標準化組織 (ISO) 27001 和 27002 標準**的認證，這兩個標準定義了資訊安全管理程序的最佳做法。ISO 27001 標準根據不同組織的需求規定了應如何建立、實施和記錄「資訊安全管理系統 (ISMS)」，以及應如何實施安全性控制。ISO 27002 標準對 ISO 27001 中的每種安全控制進行了詳細的說明。ISO 27000 系列標準中包含了一個確定風險規模和評估資產價值的處理程序，旨在保護書面、口頭和電子資訊的機密性、完整性和可用性。

{{site.data.keyword.Bluemix_notm}} 經第三方安全公司審核，符合 ISO 27001 的所有需求：[Bluemix ISO 27001:2013 Certificate of Registration](ftp://public.dhe.ibm.com/cloud/bluemix/compliance/Bluemix_ISO27K1_WWCert_2016.pdf){: new_window}。

![SSAE16 SOC1/2/3](images/icon_aicpa.png) **服務組織控制 (SOC)** 報告定義了如何對服務組織評估與安全性、可用性、處理完整性、機密性和隱私性相關的主要內部控制做法。這些報告是使用「美國註冊會計師協會 (AICPA) 手冊」產生的，包含下列各項目： 
  * 組織監督
  * 供應商管理方案
  * 內部公司治理和風險管理程序
  * 法規監督

{{site.data.keyword.Bluemix_notm}} 使用「IBM SoftLayer 基礎架構即服務 (IaaS)」雲端服務，並充分利用其安全架構。如需相關資訊，請聯絡 [{{site.data.keyword.Bluemix_notm}} 銷售](mailto:bmxcert1@us.ibm.com){:new_window}團隊。

### 平台及服務規範
下表顯示 {{site.data.keyword.Bluemix_notm}} 中的各項服務符合的每一個標準。

|{{site.data.keyword.Bluemix_notm}} 元件		|FISC		|ISO 27001	|SOC 2 類型 1		|
|:----------------------|:---------:|:---------:|:---------:|
|{{site.data.keyword.Bluemix_notm}} 平台		|Y			|Y	|Y	|
|{{site.data.keyword.APIM}}			|Y	|Y |			|
|{{site.data.keyword.autoscaling}}			|Y	|Y |			|
|{{site.data.keyword.bigicloudst}}			|Y |Y |Y |
|{{site.data.keyword.cloudant}}				|Y |Y |Y	|
|{{site.data.keyword.dashdbshort}}			|Y	|Y	|Y	|
|{{site.data.keyword.datacshort}}			|Y	|Y	|			|
|{{site.data.keyword.jazzhub_short}}					|Y	|Y	|			|
|{{site.data.keyword.containerlong}}			|Y		|Y	|			|
|{{site.data.keyword.mql}}				|Y	|Y	|	 		|
|{{site.data.keyword.SecureGateway}}			|Y	|Y |	 		|
|{{site.data.keyword.sescashort}}     |Y |Y | |

*表 1. 平台及服務規範*


# 相關鏈結
{: #rellinks}

## 相關鏈結
{: #general}

* [SoftLayer Security Compliance](http://www.softlayer.com/security)
* [開始使用 Single Sign On](../services/SingleSignOn/index.html)
