---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 關於 {{site.data.keyword.vpn_short}}
{: #vpn_overview}  
*前次更新：2016 年 3 月 17 日*

{{site.data.keyword.vpn_full}} (VPN) 服務在公司資料中心與 IBM Bluemix&reg; 雲端環境中的資源之間提供安全的通訊通道。該連線是建立在網際網路上。
{:shortdesc}

{{site.data.keyword.vpn_short}} 服務提供下列特性：  
##安全 
IBM VPN 服務使用業界標準網際網路通訊協定安全 (IPSec) 通訊協定套組，對公司資料中心與 IBM Bluemix 雲端環境之間的 IP 通訊進行鑑別和加密。IPSec 提供網路層次對等節點鑑別、資料完整性和資料機密性（加密）。

IBM VPN 服務支援下列 IPSec 通訊協定和轉換：

* 鑑別演算法：
	* HMAC-SHA1-96；共用金鑰的長度是 160 位元（預設值）  
* 加密演算法：
	* 3DES-CBC；共用金鑰的長度是 192 位元
	* AES-CBC；共用金鑰的長度是 128 位元（預設值）、192 位元和 256 位元
* 鑑別和加密通訊協定：
	* 支援「鑑別標頭 (AH)」和「封裝安全有效負載 (ESP)」通訊協定。AH 僅適用於鑑別。ESP 可用於提供鑑別和加密。
* IKEv1 Diffie-Hellman (DH) 金鑰交換群組 2（預設值）、5 和 14

IBM VPN 服務支援 IPSec 通道模式。在此模式下，IPSec 可保護整個原始 IP 封包。IPSec 可加密封包、將其封裝到新的 IP 封包內，並將新的封包轉遞到 IPSec 對等節點。 

IBM VPN 服務使用 Diffie-Hellman 金鑰交換和預先共用金鑰，以保護兩個對等節點之間的關聯安全。只要任一方未提供預先共用金鑰，鑑別就會失敗。 
 
IBM VPN 服務符合下列 IETF RFC 標準：

* 適用於 IKEv1 的 RFC 2407、2408 和 2409
* 適用於 IPv4 安全的 RFC 4301   
* 適用於 IPv4 鑑別標頭的 RFC 4302  
* 適用於 IPv4 封裝安全有效負載 (ESP) 的 RFC 4303  
* 適用於鑑別的 RFC 2104 HMAC 和 RFC 2404 HMAC-SHA-1-96  
* 適用於加密的 RFC 2451 3DES-CBC、RFC 3602 AES128-CBC、AES192-CBC 和 AES256-CBC
##簡化
您可以使用簡單且直覺的圖形介面來建立 IBM VPN 服務。您可以指定閘道 IP 位址和資料中心子網路。您可以使用預設 IPSec 和 IKE 原則，也可以根據需要自訂原則。  
##管理
您可以使用圖形介面、[指令行介面](../../cli/plugins/vpn/index.html)或 [API](https://new-console.ng.bluemix.net/apidocs/101) 來管理 IBM VPN 服務。

