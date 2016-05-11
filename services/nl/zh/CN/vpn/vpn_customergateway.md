---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 在数据中心或 SoftLayer 服务器配置网关
{: #vpn_yourdatacenter}
*上次更新时间：2016 年 3 月 17 日*

您的数据中心或 SoftLayer 服务器需要 IPSec VPN 网关，才能与 {{site.data.keyword.vpn_short}} 服务安全相连。您的数据中心或 SoftLayer 服务器需要以下 VPN 网关配置：

* 仅当 VPN 网关位于 NAT 后面时，才在 VPN 网关启用网络地址转换 (NAT) 遍历。 
* 使用配置 IBM VPN 服务时使用的相同预共享密钥。
* 将以下子网添加为远程子网：
	* 如果在 IBM Bluemix 空间创建了单个容器，请添加 172.31.0.0/16。
	* 如果在 IBM Bluemix 空间创建了容器组，请添加 172.30.0.0/16。
	* 如果在 IBM Bluemix 空间创建了单个容器和容器组，请添加 172.31.0.0/16 和 172.30.0.0/16。
* 确保 IBM VPN 网关与您的 VPN 网关使用相同的加密、认证和 PFS 组设置。
