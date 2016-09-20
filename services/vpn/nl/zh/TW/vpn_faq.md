---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.vpn_short}} 常見問題 (FAQ)
{: #vpn_faq}
*前次更新：2016 年 3 月 17 日*

下列是一些常見問題。
{:shortdesc}

1. IBM Lab 有哪些合格的協力廠商供應商裝置與 IBM VPN 服務具有交互作業能力？

	IBM Lab 測試出下列 VPN 閘道裝置與 IBM VPN 服務具有交互作業能力：

	* Cisco Adaptive Security Appliance (ASA) 軟體 8.2(1) 版。[請參閱配置範例](vpn_onpremises.html#cisco) 
	* Brocade Vyatta 5415 vRouter 6.7 R7。[請參閱配置範例](vpn_onpremises.html#vyatta){: new_window}
	* Linux StrongSwan U5.1.2/K3.13.0-55-generic。[請參閱配置範例](vpn_onpremises.html#strongswan){: new_window}
	* Linux StrongSwan U5.2.2/K3.13.0-55-generic。[請參閱配置範例](vpn_onpremises.html#strongswan){: new_window}

	此外，任何其他供應商符合 IPSec 標準的 VPN 閘道裝置應該可以與 IBM VPN 服務搭配運作。

2. 多快可以偵測到對等節點故障？
 
	會在配置的保留作用中逾時值偵測到故障的對等節點。預設值是 60 秒。

3. 每個 VPN 服務可以建立多少個 VPN 閘道和連線？
 
	在 Bluemix 空間中，一個 VPN 服務可以建立一個 VPN 閘道應用裝置。您可以為每個 VPN 閘道定義最多 16 個不同目的地的連線。 

4. 何時應該使用 IBM VPN 服務與 Bluemix Secure Gateway 服務？

	這兩種服務都用來在 Bluemix 資源與內部部署資料中心之間提供安全連線功能。 

	當您需要確保任兩個端點之間的連線功能時，請使用 IBM VPN 服務。VPN 服務可在內部部署網路與 IBM Bluemix 雲端環境之間建構第 3 層 IPSec 安全連線。IBM VPN 服務僅可用於安全地存取 IBM 儲存器（Docker 儲存器）。 

	如果您要在 Bluemix 中的特定應用程式端點與內部部署資料中心內的其他端點之間建立安全連線，請使用 Bluemix Secure Gateway 服務。 

5. 我是否可以使用 IBM VPN 服務，在 IBM Bluemix 雲端環境中使用其專用 IP 位址來存取我的儲存器和虛擬伺服器？
 
	目前，IBM VPN 服務僅可用於存取 Bluemix 儲存器。

6. 我是否可以定義「Bluemix 組織」層次的 IBM VPN 服務？

	目前，IBM VPN 服務僅可用於「Bluemix 空間」層次。如果您的「Bluemix 組織」具有多個「空間」，則可以為每一個空間定義個別的 VPN 服務。

7. 如何連接 IBM VPN 服務與 SoftLayer Gateway Appliance Service (GaaS)？

	您可以建置 IPSec 通道，以建立 IBM VPN 服務與 SoftLayer GaaS 之間的安全通訊。[請參閱配置範例。](vpn_onpremises.html#gaas){: new_window}
