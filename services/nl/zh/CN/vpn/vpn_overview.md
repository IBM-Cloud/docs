---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 关于 {{site.data.keyword.vpn_short}}
{: #vpn_overview}  
*上次更新时间：2016 年 3 月 17 日*

{{site.data.keyword.vpn_full}} (VPN) 服务在公司数据中心与 IBM Bluemix&reg; 云环境中的资源之间提供安全通信信道。该连接建立在因特网之上。
{:shortdesc}

{{site.data.keyword.vpn_short}} 服务提供以下功能：  
##安全性 
IBM VPN 服务使用业界标准的因特网协议安全性 (IPSec) 协议组，对公司数据中心与 IBM Bluemix 云环境之间的 IP 通信进行认证和加密。IPSec 提供网络级别的同级认证、数据完整性和数据机密性（加密）。

IBM VPN 服务支持以下 IPSec 协议和转换：

* 认证算法：
	* HMAC-SHA1-96，共享密钥的长度为 160 位（缺省值）  
* 加密算法：
	* 3DES-CBC，共享密钥的长度为 192 位
	* AES-CBC，共享密钥的长度为 128 位（缺省值）、192 位和 256 位
* 认证和加密协议：
	* 支持使用认证头 (AH) 和封装安全性有效负载 (ESP) 协议。AH 仅用于认证。ESP 可用于提供认证和加密。
* IKEv1 Diffie-Hellman (DH) 密钥交换分为 2 组（缺省值）、5 组和 14 组

IBM VPN 服务支持 IPSec 隧道方式。在此方式下，IPSec 可保护整个原始 IP 包。IPSec 对包进行加密、将其封装到新的 IP 包内并将新包转发到 IPSec 同级。 

IBM VPN 服务使用 Diffie-Hellman 密钥交换和预共享密钥，可以确保两个同级之间的关联安全。只要任一方未提供预共享密钥，认证都会失败。 
 
IBM VPN 服务与以下 IETF RFC 兼容：

* 用于 IKEv1 的 RFC 2407、2408 和 2409
* 用于 IPv4 安全性的 RFC 4301   
* 用于 IPv4 认证头的 RFC 4302  
* 用于 IPv4 封装安全性有效负载 (ESP) 的 RFC 4303  
* 用于认证的 RFC 2104 HMAC 和 RFC 2404 HMAC-SHA-1-96  
* 用于加密的 RFC 2451 3DES-CBC、RFC 3602 AES128-CBC、AES192-CBC 和 AES256-CBC
##简易性
使用简单且直观的图形界面即可创建 IBM VPN 服务。您可以指定网关 IP 地址和数据中心子网。您可以使用缺省 IPSec 和 IKE 策略，也可以根据需要定制策略。  
##管理
使用图形界面、[命令行界面](../../cli/plugins/vpn/index.html)或 [API](https://new-console.ng.bluemix.net/apidocs/101) 可管理 IBM VPN 服务。

