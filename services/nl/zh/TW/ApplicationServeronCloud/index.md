---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 開始使用 IBM WebSphere Application Server for Bluemix
{: #getting_started}

*前次更新：2016 年 4 月 8 日*

{{site.data.keyword.IBM}}WebSphere Application Server for {{site.data.keyword.Bluemix}} 服務可協助您在 Bluemix 所管理雲端環境中的預先配置 WebSphere Application Server Liberty、Network Deployment 或典型實例上快速設定。
{: shortdesc}

## WebSphere Application Server for Bluemix 概觀
{: #overview}

WebSphere Application Server for Bluemix 提供消費者預先配置的典型 WebSphere 及 Liberty 設定檔伺服器。它在具有來賓作業系統之 root 存取權的虛擬機器訪客上進行管理。當您建立服務時，請選擇 *Liberty*、*ND* 或*典型 WebSphere*。

您會有熟悉的 WebSphere 管理經驗，以及具有基礎作業系統的完整存取權。您可以重複使用現有 Script，並進行需要的少量系統調整，以便搭配您自己或協力廠商的架構來使用。提供的「管理中心」及「管理主控台」，可用來管理 WebSphere Application Server Liberty、ND 或典型服務（就像內部部署 WebSphere 配置一樣）。

**附註**：WebSphere Application Server for Bluemix Network Deployment 方案現在具有更多功能。此方案包含具有兩個以上虛擬機器的 WebSphere Application Server Network Deployment Cell 環境。第一個虛擬機器包含部署管理程式及 IBM HTTP Server，而其餘虛擬機器包含聯合至部署管理程式的自訂節點（節點代理程式）。使用現有 wsadmin Script 來建立 WebSphere 配置，或使用「WebSphere 管理主控台」來手動配置環境。這些新的功能容許使用者設定叢集環境以獲得高可用性、失效接手及可擴充性。叢集作業是任何中介軟體企業應用程式的重要部分，而且用戶端現在可以選擇對拓蹼進行叢集處理，以負載平衡兩個以上「實例」的要求。

WebSphere Application Server for Bluemix Liberty Core 方案也具有更多功能。此方案包括如何使用 Liberty Collective，而這是一組 Liberty 設定檔（伺服器）的管理網域，並且包含兩個以上的虛擬機器。第一個虛擬機器包含 Collective Controller Liberty 伺服器（即 Liberty Collective 的控制點）。除了 Liberty Collective 之外，此虛擬機器也會包含 IBM HTTP Server，其容許從 Web 瀏覽器存取應用程式。其餘虛擬機器是群體成員所在的群體主機（Liberty 設定檔伺服器）。在 Liberty 控制器伺服器上也會啟用「Liberty 管理中心」特性。

下圖顯示 WebSphere Application Server for Bluemix Network Deployment Cell 及 Liberty Collective 環境的架構。

![圖 1. Network Deployment Cell 及 Liberty Collective 的架構](images/CellCollectiveDiagram.gif)

## 作業環境
{: #operational_environment}

IBM WebSphere Application Server for Bluemix 服務會在共用環境中傳回訪客（虛擬機器），讓消費者部署應用程式。VPN 會保護公用服務抵禦通用埠掃描及其他自發網路型攻擊。不過，請一定要注意，您用來存取服務實例的服務 VPN 可能會在多個 Bluemix 組織與使用者之間共用。虛擬機器也會提供計算、記憶體及 I/O 資源，這些來自 IaaS 資源的共用儲存區。如果您要在專用環境中執行應用程式，請與 IBM 業務代表聯絡，他們可為您介紹我們的專用 IBM WebSphere Application Server for Bluemix 供應項目。

由於在共用環境中，計算、記憶體及 I/O 資源是由虛擬機器執行，因此服務配置可能會不同。透過 IBM WebSphere Application Server for Bluemix 服務儀表板及入口網站，可檢視每一個特定服務實例的配置。

**附註**：IBM WebSphere Application Server for Bluemix 現在為應用程式佔用大量記憶體的用戶端提供了一個選項，以套用更大型的虛擬機器來合理調整其環境的大小。用戶端可以選取具有特定資源大小、且最多包含 32 GB RAM 虛擬機器的已佈建 WebSphere Application Server 元件或單一系統。

## 定價策略
{: #pricing_strategy}

IBM WebSphere Application Server for Bluemix 提供虛擬機器實例。藉由這些實例，用戶端可使用簡單入口網站，以一致且可重複的方式建立並管理企業 WebSphere Application Server 部署，並極其靈活地調整其應用程式。使用者可在管理雲端環境中的預先配置 WebSphere Application Server Liberty、ND 或典型虛擬機器上開始進行。使用者可將現有 WebSphere Application Server 應用程式移轉到 Bluemix，並完全控制基礎作業系統及中介軟體。

提供的 IBM WebSphere Application Server for Bluemix 適用下列收費標準：

*  *實例-小時*：「實例」定義為存取 IBM WebSphere Application Server for Bluemix 服務的特定配置。在計費期間，針對所部署「服務」的每一個「實例」執行的每一個完整小時或局部小時向用戶端收費。每一個「實例小時」為按月計費，如果當月僅部分時候使用實例，則會按比例計算使用率。

例如，如果您使用 ND 方案，則一個「實例」等於包含 2 GB RAM 及 12 GB HD 的 1vCPU。因此，如果選擇為您的 Cell 配置 1 個「控制」節點及 8 個「自訂」節點，您將需要為 9 個節點（實例）付費。

**附註**：最低收費設定為每個「自訂」節點或 Liberty 主機 0.25 個實例小時。在上面的範例中，配置 1 個「控制」節點及 1 個「自訂」節點長達 15 分鐘即等於最低收費（0.25 * 實例數）。

# 相關鏈結
## 一般
* [WASdev](https://developer.ibm.com/wasdev/){: new_window}
* [WebSphere Application Server 文件](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/as_ditamaps/was855_welcome_ndmp.html){: new_window}
* [WebSphere Application Server 典型第 9 版測試版文件](http://www.ibm.com/support/knowledgecenter/SSEQTP_9.0.0/as_ditamaps/was900_welcome_base.html){: new_window}
