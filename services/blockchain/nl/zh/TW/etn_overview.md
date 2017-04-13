---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-09"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 網路態勢
{: #etn_overview}


IBM Blockchain on Bluemix 的「入門範本開發人員」方案及「高安全性商業網路」方案利用 Hyperledger Fabric 0.6 版所提供的特性、「實用拜占庭容錯 (PBFT)」共識通訊協定及 Hyperledger Fabric Client (HFC) SDK for Node.js。兩個方案都包含四個網路節點及一個「憑證管理中心」。「憑證管理中心」控管「成員資格服務」，這項服務透過發行數位憑證來管理身分、網路許可權及機密交易。
{:shortdesc}

下列是兩個方案中可用的區塊鏈功能：

* PBFT 共識通訊協定可管理所有寫入至共用分類帳之交易的順序。儘管有一個「拜占庭」（有缺陷）節點，四個節點的 PBFT 區塊鏈網路也可以達成共識。如需 PBFT 共識測試詳細資料，請參閱[測試共識及可用性](etn_pbft.html)。
* HFC SDK for Node.js 容許用戶端 Node.js 應用程式與區塊鏈網路互動。用戶端應用程式可以透過「成員資格服務」安全地登記使用者、發出交易，以及透過使用 tCert 以加密方式交換資產。如需「成員資格服務」及使用者隱私權的相關資訊，請參閱 [HFC SDK for Node.js](etn_sdk.html) 小節及 Hyperledger Fabric [通訊協定規格](https://github.com/hyperledger/fabric/blob/v0.6/docs/protocol-spec.md)。
* 您可以透過 [Bluemix 監視器儀表板](ibmblockchainmonitor.html)來存取區塊鏈網路環境的詳細資料。  

<br>
## 術語

下列術語以及後續圖表可用來縱觀根據 Hyperledger Fabric 0.6 版的 IBM Blockchain 網路元件：

**成員**：參與區塊鏈網路的身分。有不同類別的成員，包括使用者、對等節點、驗證者及審核者。

**成員資格服務**：與取得及管理成員身分有關的服務。成員資格服務是透過「憑證管理中心」所控管。  

**登錄**：將新的成員身分新增至網路的動作。具有 'registrar'（登記員）專用權的使用者，可以將成員動態新增至網路。成員也會獲指派一些角色及屬性，這些角色及屬性可控制他們對網路的存取權及權限。角色或屬性都不可以動態指派；您必須改為編輯 membersrvc.yaml 檔案。

**登記****：容許新成員存取區塊鏈網路，以完成登錄程序。向登記員（頻外）取得密碼之後，新成員就可以執行登記，或由具有委派權限的中間人員來代表新成員處理。  

**交易者**：透過節點連接到區塊鏈網路的網路參與者，它會從用戶端使用 SDK 或 API 提交交易。

**交易**：交易者要在區塊鏈網路上執行一項功能而提出的要求。交易類型為 deploy、invoke 和 query，它們是透過在網狀架構的 API 合約中提出的鏈碼函數而實作。

**分類帳**：一系列的加密鏈結區塊，包含交易和現行廣域狀態。除了來自先前交易的資料，分類帳也包含目前執行中鏈碼應用程式的資料。

**廣域狀態**：在由交易執行時，鏈碼用來儲存其狀態的索引鍵值資料庫。

**鏈碼**：內嵌的邏輯，會將特定類型的網路交易規則編碼。開發人員撰寫鏈碼應用程式，並將其部署至網路。一般使用者便可以透過與網路對等節點（peer，或節點、node）互動的用戶端應用程式呼叫鏈碼。鏈碼會執行網路交易，這些交易如經驗證，會附加到共用分類帳並修改廣域狀態。

**驗證對等節點**：執行共識通訊協定的網路節點，以便網路能驗證交易並維護分類帳。驗證過的交易會附加到分類帳（以區塊為單位）。如果交易無法達成共識，就會從區塊清除，因此不會寫入分類帳。驗證對等節點 (VP) 具有權限，可以部署、呼叫和查詢鏈碼。

**非驗證對等節點**：發揮 proxy 功能的網路節點，將交易者連接至驗證對等節點。非驗證對等節點 (NVP) 會將呼叫要求轉遞至其連接的驗證對等節點 (VP)。它也管理事件串流伺服器與 REST 服務。


**共識**：維護區塊鏈網路交易（deploy 及 invoke）順序的通訊協定。驗證節點會藉由實作共識通訊協定，一起運作來核准交易。共識可確保節點的仲裁同意共用分類帳上的交易順序。藉由解決對此順序的任何分歧，共識可確保所有節點在相同的區塊鏈分類帳上運作。如需相關資訊和測試案例，請參閱[共識](etn_pbft.html)主題。  

**具有許可權的網路**：區塊鏈網路，在其中每個節點都必須維護網路上的成員身分，且每個節點只能存取其許可權容許的交易。  

<br>
## 網路架構

圖 1 及其後續說明描述 IBM Blockchain 網路架構，以及成員服務、交易、共識及附加至分類帳的資料流程：

![專用網路](images/Architecture_BMX_dedicated.png "IBM Blockchain 網路架構")圖 1.

下列步驟詳述圖 1 的網路流程：

1. 已登錄使用者透過 PKI（成員資格服務）向網路進行登記，並收到長期登記憑證 (eCert) 及一批的交易憑證 (tCert)。
2. 使用者將鏈碼部署至網路。鏈碼（智慧型合約）會針對控管特定類型交易的商業邏輯或規則進行編碼。每一個交易（deploy、invoke 或 query）都需要唯一的 tCert，而且必須利用使用者的私密金鑰進行簽署。使用者會從指派的 tCert 衍生其私密金鑰。
3. 使用者呼叫智慧型合約，這個智慧型合約會觸發合約以自行執行其編碼邏輯。
4. 將交易提交至網路對等節點。對等節點收到交易要求之後，會將要求提交至網路的主要對等節點（圖 1 中的 VP1）。主要對等節點會排序一個區塊的交易，並將此順序播送至其同伴對等節點。
5. 對等節點使用網路共識通訊協定 (PBFT) 來同意所提交交易的順序。這個共同排序交易的程序稱為共識。  
6. 對等節點達成共識之後，會執行交易要求，並將這個區塊附加至共用分類帳。  

<!---Both the developer and high-security networks unlock several features in the Hyperledger fabric which robustly enhance security, confidentiality and privacy.  The only fundamental difference between the two is their operating/hosting environment.  The developer network runs in a shared multi-tenant environment on Softlayer, whereas the high-security network exists as an isolated single-tenant running in a secure services container.  Each network leverages the same capabilities from the fabric, including a PBFT consensus protocol and the enhanced Node.js SDK.~~

~~The High-Security business network runs in an isolated and highly secured environment, distinguishing it from other cloud-hosted offerings. The operating system, fabric, and nodes all exist in a secure services container (SSC), providing your enterprise with the security and impregnability that customers have come to expect from system Z technology.  The SSC delivers performance optimization in - peer to peer communication, availability, scalability, hardware encryption, tamper-proof crypto keys, and securely encrypted VMs.  See the [Secure Services Container](etn_ssc.html) section for more details on the security features provided through the SSC.  Additionally, the high security network unlocks numerous features of the Hyperledger fabric (unavailable in the developer service), which robustly enhance security, confidentiality and privacy.  The configuration is such that you are able to test and affirm these features.~~  
{:shortdesc}

~~The high security plan augments the developer plan by delivering several enhancements that help meet the security requirements and concerns of an enterprise-level participant:~~--->

<!---The environment (LinuxONE on z) consists of a four-peer network implementing PBFT with Membership Services enabled, running in an application container.  The application container protects blockchain software, chaincode, and data running within the system. The blockchain software within the secure boot can be signed, attested, and encrypted; and once installed in the application container, is tamper-resistant.  Root users of the platform and system administrators cannot access or see z secure container contents.  In addition, the LinuxOne on z provides you with FIPS compliance, high Evaluation Assurance Level protection, a highly auditable operating environment, and crypto optimization--->
