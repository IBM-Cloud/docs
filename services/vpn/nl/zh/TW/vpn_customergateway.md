---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 在資料中心或 SoftLayer 伺服器配置閘道
{: #vpn_yourdatacenter}
*前次更新：2016 年 3 月 17 日*

您的資料中心或 SoftLayer 伺服器需要有 IPSec VPN 閘道，才能構成與 {{site.data.keyword.vpn_short}} 服務的安全連線。您的資料中心或 SoftLayer 伺服器需要下列 VPN 閘道配置：

* 只有在 VPN 閘道受網址轉換 (NAT) 保護時，才能在 VPN 閘道啟用 NAT 遍訪。 
* 使用在配置 IBM VPN 服務時所使用的相同預先共用金鑰。
* 將下列子網路新增為遠端子網路：
	* 如果您已在 IBM Bluemix 空間建立單一儲存器，請新增 172.31.0.0/16。
	* 如果您已在 IBM Bluemix 空間建立儲存器群組，請新增 172.30.0.0/16。
	* 如果您已在 IBM Bluemix 空間建立單一儲存器和儲存器群組，請新增 172.31.0.0/16 和 172.30.0.0/16。
* 確保 IBM VPN 閘道和您的 VPN 閘道使用相同的加密、鑑別和 PFS 群組設定。
