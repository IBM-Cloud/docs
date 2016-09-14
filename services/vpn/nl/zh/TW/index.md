---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 開始使用 {{site.data.keyword.vpn_short}}
{: #vpn}  
*前次更新：2016 年 5 月 9 日*

Bluemix&reg; 的 {{site.data.keyword.vpn_full}} 服務可用來安全地在 IBM Bluemix 雲端環境中存取 IBM Containers（Docker 儲存器）。您可以使用 IBM Bluemix 雲端環境作為公司資料中心的延伸。您也可以使用 IBM VPN 服務與 SoftLayer 伺服器連接。
{:shortdesc}

開始之前，請確定您可以使用 IBM Docker 儲存器。請參閱 [IBM Containers for Bluemix](https://www.ng.bluemix.net/docs/containers/container_index.html)，以取得如何建立和管理 IBM Containers 的詳細資料。  

若要開始使用，請選取 Bluemix 儀表板上的 **Virtual Private Network** 服務實例磚。請完成下列步驟：

1. 選取**建立閘道**以配置 {{site.data.keyword.vpn_short}} 閘道。會建立一個預設閘道。視需要編輯閘道配置，如下列步驟所示。
{: #gateway}  

  1. 選取**編輯**。  
  2. 指定閘道名稱。  
  3. 選取您要用來搭配 VPN 服務的儲存器或儲存器群組。
	**附註：**會預先選取儲存器及儲存器群組專用子網路，以便您可以透過 VPN 連線存取它們。
  4. 選取**儲存**。  

 您可以使用預設的 IKE 及 IPSec 原則，或是配置自訂原則。如果您想要使用預設原則，請跳到步驟 4。

2. 選取 **IKE & IPSec 原則**標籤來配置 IKE 原則。
  1. 選取**新增**。  
  2. 指定下列詳細資料：
	* **名稱**：IKE 原則的名稱
	* **授權演算法**：sha1；無法變更  
	* **加密演算法**：從下拉清單選取。值：aes-128（預設值）、aes-192、aes-256、3des
	* **金鑰生命期限**：IKE 安全關聯的生命期限值（秒）。範圍：60-86400。預設值：86400
	* **PFS**：Diffie-Hellman (DH) 群組 ID。值：Group2、Group5、Group14。預設值：Group2
	* **協議模式**：Main；無法變更
	* **版本**：IKEV1；無法變更
  3. 選取**儲存**。

3. 配置 IPSec 原則：
  1. 選取**新增**。  
  2. 指定下列詳細資料：
  	* **名稱**：IPSec 原則的名稱  
  	* **授權演算法**：sha1；無法變更  
  	* **加密演算法**：從下拉清單選取。值：aes-128（預設值）、aes-192、aes-256、3des
  	* **金鑰生命期限**：安全關聯的生命期限值（秒）。範圍：60-86400。預設值：3600
  	* **PFS**：Diffie-Hellman (DH) 群組 ID。值：Group2、Group5、Group14。預設值：Group2
  	* **轉換通訊協定**：ESP；無法變更
  	* **封裝模式**：Tunnel；無法變更
  3. 選取**儲存**。  

4. 提供詳細資料，以建立資料中心或 SoftLayer 伺服器 VPN 閘道與 IBM VPN 閘道之間的連線。
{: #site}  

  1. 選取**閘道應用裝置**標籤。
  2. 在**網站連線**區段中，選取**建立連線**。
  3. 指定下列網站連線詳細資料：  
  	* **名稱**：連線的名稱  
  	* **說明**：連線的說明（選用）  
  	* **預先共用金鑰字串**：要用於鑑別的預先共用（秘密）金鑰
  	* **管理狀態**：VPN 連線的狀態。從下拉清單選取：UP 或 DOWN。預設值：UP  
  	* **客戶閘道 IP**：VPN 通道的遠端端點 IP 位址  
  	* **客戶子網路**：CIDR 格式的遠端子網路位址。選取加號以新增另一個子網路。
  4. （選用）配置下列**進階設定**參數：  
  	* **IKE 原則**：選取 IKE 原則。  
  	* **保留作用中間隔**：保留作用中間隔（秒）。依配置的間隔傳送保留作用中訊息，以檢查對等節點是否活躍。預設值：15。範圍：5-86399
  	* **對等節點停用時的動作**：偵測到對等節點為停用時所要採取的動作。
    	值： 
  		* hold（預設值）：安全關聯 (SA) 被置於保留 
  		* clear：刪除 SA
  		* disabled：已停用 SA
  		* restart：重新協議 SA
  		* restart-by-peer：重新協議所有對等節點已停用的 SA  
  	* **IPSec 原則**：選取 IPSec 原則。
  	* **保留作用中逾時**：逾時值（秒），在此期間之後會終止階段作業。預設值：120。範圍：6-86400。保留作用中逾時值必須高於保留作用中間隔值。
  5. 選取**儲存**。

  **附註：**正在建立連線時，連線狀態會顯示為 ***建立擱置中***。當您看到此狀態時，請重新整理畫面數次，查看連線作用中狀態。

**重要事項：**如果您使用 Web 應用程式，則必須將 Web 應用程式連結至正在使用的 Docker 儲存器。必須進行此連結作業，資料流量才能透過 IPSec VPN 通道傳遞。

**重要事項：**IBM VPN 服務目前以回應者模式運作。若要起始 VPN 連線，資料封包必須從 IBM VPN 閘道流出，然後流到您的內部部署資料中心或 SoftLayer 伺服器。建立 VPN 連線之後，資料流量可以在 VPN 連線的端點之間以任一方向流動。

 
# 相關鏈結
## 範例 
{: #samples}  
* [內部部署的 strongSwan 閘道配置範例](vpn_onpremises.html#strongswan){: new_window}
* [內部部署的 Vyatta 閘道配置範例](vpn_onpremises.html#vyatta){: new_window}
* [內部部署的 SoftLayer Gateway Appliance Service (GaaS) 配置範例](vpn_onpremises.html#gaas){: new_window}
* [內部部署的 Cisco ASA 配置範例](vpn_onpremises.html#cisco){: new_window}

## API  
{: #api}  
* [IBM VPN RESTful API](https://new-console.ng.bluemix.net/apidocs/101){: new_window}

## 一般  
{: #general}  
* [IBM VPN 指令行介面](../../cli/plugins/vpn/index.html){: new_window}
* [IBM VPN 常見問題 (FAQ)](vpn_faq.html#vpn_faq){: new_window}
* [IBM Bluemix 定價單](https://console.{DomainName}/pricing/){: new_window}
* [IBM Bluemix 必要條件](https://developer.ibm.com/bluemix/support/#prereqs)
